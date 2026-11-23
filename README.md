# WallWizard

A two-player, Quoridor-style wall and pawn game that runs entirely in the terminal.

Two players take turns moving their pawn across a 9x9 board while placing walls to slow each other down. The first player to reach the opposite side wins.

## Features

- 9x9 board rendered in the terminal with ANSI colors
- 10 walls per player, placed in four directions (`U`, `R`, `L`, `D`)
- Path validation using depth-first search, so a wall can never fully block a player
- Per-player signup and login, with accounts stored in `users.json`
- Passwords stored as SHA-256 hashes
- Arrow-key driven menus with a typing-effect logo
- Randomly chosen starting player

## Requirements

- Python 3.8 or newer
- [`rich`](https://pypi.org/project/rich/) for colored board output
- [`keyboard`](https://pypi.org/project/keyboard/) for reading menu input

```bash
pip install rich keyboard
```

On Linux and macOS, the `keyboard` library may require root privileges.

## Usage

```bash
python test.py
```

1. Player 1 signs up or logs in.
2. Player 2 signs up or logs in.
3. The game starts with a randomly selected player.

### Menu controls

| Key        | Action                  |
| ---------- | ----------------------- |
| `Up`/`Down`| Move between menu items |
| `E`        | Confirm selection       |

### In-game controls

| Input  | Meaning                                              |
| ------ | ---------------------------------------------------- |
| `M`    | Move your pawn                                       |
| `W`    | Place a wall                                         |
| `U`    | Up (movement or wall direction)                      |
| `R`    | Right                                                |
| `L`    | Left                                                 |
| `D`    | Down                                                 |
| `exit` | Leave the game                                       |

When placing a wall you will be asked for a column, a row, and a direction.

## How the game works

- Player 1 starts near the bottom of the board; Player 2 starts near the top.
- Player 1 wins by reaching the bottom row, Player 2 by reaching the top row.
- Each player has 10 walls.
- A wall cannot fully block the opponent from reaching their goal. The game checks this with a depth-first search before accepting a wall.

## Project structure

```
WALLWIZARD/
├── test.py     # Entire game: menu, accounts, board, movement, wall logic
├── README.md
└── users.json  # Created automatically on first signup
```

> `users.json` is generated at runtime and contains account data. Do not commit it to version control.

## Notes

- The game relies on ANSI escape codes and a real terminal; it may not render correctly in some IDE consoles.
- Clearing the screen uses `cls` on Windows and `clear` elsewhere.
