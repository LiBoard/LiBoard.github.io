---
title: How it works
parent: Home
---
# {{ page.title }}
{: .no_toc}
## Table of contents
{: .no_toc .text-delta }
- TOC
{:toc}

## The board
The chessboard has a light sensor in each square and continuously checks which
squares are occupied by a piece. Whenever this data changes, it sends it to the
connected PC or phone (the "recipient") as a
[bitboard](https://www.chessprogramming.org/Bitboards) via USB.

## The recipient
Because the sensors cannot determine which piece is on which square,
the recipient has to do it.
In order to do this, it keeps track of three things:
- The last known position ("old position")
- The bitboard corresponding to said position ("old bitboard")
- A set of squares which have been "emptied" at some point
  since the last played move ("lifted pieces")

Whenever new data comes in, the recipient checks if it matches the starting position.
If so, a new game is started, meaning:
- The last known position is set to the starting position.
- The corresponding bitboard is set to 0xFFFF00000000FFFF.
- The set of lifted pieces is emptied.

If new data ("new bitboard") comes in which doesn't match the starting position, the recipient does the following:
- It adds every square that isn't occupied in the new bitboard but was occupied
  in the old bitboard to the lifted pieces.
- It checks if the last known position has a legal move
  which would transform the corresponding bitboard into the received bitboard
  (see [Checking for legal moves](#checking-for-legal-moves)).

### Checking for legal moves
In order to recognize played moves, the recipient needs to determine three things:
- The squares which were occupied in the old bitboard but aren't occupied in the
  new bitboard ("disappearances") and vice versa ("appearances")
- The squares in the lifted pieces set which are occupied in the new bitboard ("temporarily lifted pieces")

Then the recipient checks for the following:
- If there's one square each in disappearances and appearances: Check if there's
  a legal, "normal" (no capture, no castling) move from the disappearance square
  to the appearance square.
- If there's one disappearance, no appearance and there has been at least one
  temporarily lifted piece: Find the first (if any) temporarily lifted piece for which
  there is a legal (not en passant) capture from the disappearance to the
  temporarily lifted piece.
- If there's two disappearances and one appearance: Check if there's a legal en
  passant capture from one of the disappearances to the appearance square.
- If there's two appearances and disappearances each: Check if any of the four
  disappearance-appearance combinations is a legal castling move.

If such a move is found, it is "played", meaning:
- The old position is updated to the position after the move.
- The old bitboard is updated to the new bitboard.
- The lifted pieces are cleared.

If no such move is found, the recipient waits for new board data.

## Technical limitations
Because the sensors can only determine which squares are occupied by a piece, but
cannot determine which pieces they are occupied by, there are a few technical
limitations:
- The starting position of each piece needs to be known. For standard chess,
  this isn't a problem, but it means that in order to support Chess960, the
  "recipient" would need to be told the starting position by the user.
- If a pawn is promoted, the board has no way of determining which piece is used
  to replace the pawn. Currently, it is assumed that every pawn promotes to a
  Queen. There are several paths I see to implement underpromotion:
  - Adding buttons to the board so that the user can select the piece type there.
    This would mean that a 64-bit bitboard is no longer sufficient.
  - Adding an option to specify the piece type in the recipient.
- If pieces that are not going to be captured are lifted temporarily (of if the
  sensor gives a wrong reading for a moment), the recipient might think the user
  played a capture even though the user didn't intend to.

  To illustrate, let's imagine the following position:
  <iframe
    src="https://lichess.org/embed/NthUrXlz#23?theme=auto&bg=auto"
    width=600
    height=397
    frameborder=0></iframe>

  Black wants to play Nh5. However, if the e4 pawn was lifted since g5 was played,
  the recipient will recognize the move Nxe4 as soon as the knight is lifted.
