---
title: Python module
---
# Python module
The LiBoard Python module is used by the provided scripts and can be used for
your own scripts.
It handles the connection to the board and detecting legal moves played.

## Installation
```sh
pip install git+https://github.com/LiBoard/Python-module
```

## Usage example
```python
from liboard import LiBoard


def main():
    board = LiBoard()

    @board.start_handler
    def print_start(_board: LiBoard) -> bool:
        # Your code here

    @board.move_handler
    def print_move(_board: LiBoard, _move: chess.Move) -> bool:
        # Your code here

    while True:
        board.update()


if __name__ == '__main__':
    try:
        main()
    except KeyboardInterrupt:
        pass

```

## Dependencies

* [python-chess](https://pypi.org/project/chess/)
* [pyserial](https://pypi.org/project/pyserial/)
* [bitstring](https://pypi.org/project/bitstring/)
