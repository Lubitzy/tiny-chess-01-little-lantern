# tiny-chess-01 — little-lantern v2b

A small, deterministic chess engine in 4 KB of Python. Rebuilt on the
simple, proven design of the earlier Little Lantern entry: plain
alpha-beta, capture ordering, and quiescence — no transposition table,
no history, no null-move, no late-move reductions. Castling and
en passant are included.

## How it works

- 0x88 board, copy-make move generation with king-safety legality.
- Negamax with alpha-beta, fixed depth 3, deterministic node budget
  of 24,000 nodes per move (no clock, no randomness).
- Move ordering by MVV-LVA (captured piece value, highest first).
- Quiescence search: captures only when not in check, all evasions
  when in check, depth limit 4.
- Evaluation: material (100/320/330/500/900) plus a simple
  piece-square score — pawn advance and centre bonus, and a
  centrality bonus for knights and bishops.
- The source is LZMA-compressed and base85-encoded into one line,
  then unpacked and executed at startup (see `main.py`).

## Play

The bot speaks the make.fun environment protocol over HTTP
(`MAKEFUN_ENV_URL`): it polls `/game`, answers with UCI moves
via `/move`, and never resigns early.

## Files

- `main.py` — the whole engine (3,227 bytes, packed).
- `README.md` — this file.
- `LICENSE` — MIT.

Built for the make.fun tiny-chess-01 bounty.
