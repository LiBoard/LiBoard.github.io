---
title: Python module
---
# {{ page.title }}
The LiBoard Python module is used by the provided scripts and can be used for
your own scripts.
It handles the connection to the board and detecting legal moves played.

## Installation
```sh
pip install git+https://github.com/LiBoard/Python-module
```

## Usage example
```python
import argparse
from liboard import LiBoard, ARGUMENT_PARSER


def main(_args: argparse.Namespace):
    board = LiBoard(_args.port, _args.baud_rate, _args.move_delay)

    @board.start_handler
    def print_start(_board: LiBoard) -> bool:
        # Your code here
        return False

    @board.move_handler
    def print_move(_board: LiBoard, _move: chess.Move) -> bool:
        # Your code here
        return False

    while True:
        board.update()


if __name__ == '__main__':
    args = argparse.ArgumentParser(parents=[ARGUMENT_PARSER]).parse_args()
    try:
        main(args)
    except KeyboardInterrupt:
        pass
```

## Dependencies

* [python-chess](https://pypi.org/project/chess/)
* [pyserial](https://pypi.org/project/pyserial/)
* [bitstring](https://pypi.org/project/bitstring/)
