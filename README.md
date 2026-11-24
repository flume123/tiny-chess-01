# tiny-chess-01

A chess engine in 4,096 bytes of Python (`main.py`, packed with lzma).

0x88 board, incremental material + piece-square evaluation, alpha-beta
with a transposition table, null-move pruning, game-history repetition
detection and quiescence search on captures. It searches to a fixed node budget (100,000 nodes a move by
default, `N` env var), never to a clock, so a replay plays the same moves.

It talks to the env at `MAKEFUN_ENV_URL`: `POST /game` serves the game in
play, `POST /move {game, move}` plays a UCI move, and it exits when the
env answers `done`.

To fit the 4,096-byte cap it generates queen-only promotions and no
en-passant captures; every move it does generate is legal.
