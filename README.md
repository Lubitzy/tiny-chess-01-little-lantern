# tiny-chess-01 — little-lantern v2b

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Lubitzy/tiny-chess-01-little-lantern/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Lubitzy/tiny-chess-01-little-lantern/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Built for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01).

A small, deterministic chess engine in 4 KB of Python. Rebuilt on the
simple, proven design of the earlier Little Lantern entry: plain
alpha-beta, capture ordering, and quiescence — no transposition table,
no history, no null-move, no late-move reductions. Castling and
en passant are included.

## How it works

- 0x88 board, copy-make move generation with king-safety legality.
- Negamax with alpha-beta, fixed depth 3, deterministic node budget
  of 24,000 nodes per move (no clock, no randomness). The budget
  covers the main search and quiescence together, so a tactical
  position can never run past the time limit.
- Move ordering by MVV-LVA (captured piece value, highest first).
- Quiescence search: captures only when not in check, all evasions
  when in check, depth limit 8.
- Evaluation: material (100/320/330/500/900) plus a simple
  piece-square score — pawn advance and centre bonus, and a
  centrality bonus for knights and bishops.
- The source is packed into one line with the make.fun kit's
  compress tool (LZMA stream with a small unpacker stub),
  then unpacked and executed at startup (see `main.py`).

## Play

The bot speaks the make.fun environment protocol over HTTP
(`MAKEFUN_ENV_URL`): it polls `/game`, answers with UCI moves
via `/move`, and never resigns early.

## Files

- `main.py` — the whole engine (2,628 bytes, packed).
- `README.md` — this file.
- `LICENSE` — MIT.

Built for the make.fun tiny-chess-01 bounty.
