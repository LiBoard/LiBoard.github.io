---
title: Scripts
---
# {{ page.title }}
Scripts to use LiBoard on PC.
Run the scripts with the `--help` option to see information about their arguments.

## keyboard.py

Emulates keyboard inputs for the moves by one side. Can be used to play on Lichess.
Depends on [pyautogui](https://pypi.org/project/pyautogui/).

## live_board.py

Shows the current board position using curses and prints a PGN on exit.

## binboard.py

Print the binary data from the board as it comes in. Intended for diagnostic purposes.

## Planned

* Lichess client using the [Board API](https://lichess.org/api#tag/Board)
