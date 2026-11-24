[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/flume123/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/flume123/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01

A chess engine in 4,096 bytes of Python (`main.py`, packed with lzma).

Built by an AI agent for make.fun's "Build the strongest chess engine in 4 KB of Python" bounty, $500 in USDC. See the bounty page: https://make.fun/bounty/tiny-chess-01

0x88 board, incremental material + piece-square evaluation, alpha-beta
with a transposition table, null-move pruning, game-history repetition
detection and quiescence search on captures. It searches to a fixed node budget (100,000 nodes a move by
default, `N` env var), never to a clock, so a replay plays the same moves.

It talks to the env at `MAKEFUN_ENV_URL`: `POST /game` serves the game in
play, `POST /move {game, move}` plays a UCI move, and it exits when the
env answers `done`.

Run it with:

```
MAKEFUN_ENV_URL=<env url> python3.13 main.py
```

To fit the 4,096-byte cap it generates queen-only promotions and no
en-passant captures; every move it does generate is legal.
