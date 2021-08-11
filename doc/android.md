---
title: Android app
---
# {{ page.title }}
There's an [Android app](https://github.com/liboard/android) for LiBoard which
can be used to save OTB games.
Additionally, it can be used as a chess clock.  
It has a dark and a light theme.

## App layout
![Screenshot of the app's main screen](/assets/images/app/main.jpg){: width="200"}

The purple floating button in the lower right corner establishes a connection to
a board that has been connected via USB.

The three tabs do the following:
- Board: Shows the current known board position and whose move it is.
- Moves: Shows the moves which have been played in the current game.
- Clock: [see Chess clock](#chess-clock)

The icons in the app bar allow saving the current game as a pgn file
or sending it as a message.

## Chess clock
![Screenshot of the clock tab](/assets/images/app/clock.jpg){: width="200"}

The chess clock measures each players time down to the millisecond.
It supports time odds.
The button with the gear icon opens a settings screen
where users can select the clock mode and time control.

### Settings
#### Modes
- **Independent**: Allows the clock to be used entirely independent from the board.
- **Synchronized**: A chess clock that automatically switches the active side when a move is played.
- **Stopwatch**: Like synchronized, but simply measures the time
  each player used, without a time limit.
- **Clock move**: The active side is switched by tapping the running clock.
  However, the clock will only switch sides if a legal move has been played on the board.
  The board will also only register played moves when the clock is tapped.

#### Time control types
- **Increment**: Adds a certain number of seconds after each move.
- **Delay**: Waits for a certain number of seconds before the clock starts counting down.

Set the increment to 0 s for sudden death mode.

#### UI framerate
By default, the time shown on the screen is updated 10 times per second.
If this leads to issues, users can lower the refresh rate.
