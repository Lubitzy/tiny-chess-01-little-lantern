# Little Lantern — 4 KB chess engine

A deterministic Python 3.13 engine for make.fun's `tiny-chess-01` gauntlet. The committed `main.py` is a self-contained LZMA-packed program; it uses only the standard library, reads no repository data and makes no model calls. It searches a fixed node budget per move, with alpha-beta, capture ordering, quiescence, material and simple piece-square scoring. The environment supplies the authoritative legal-move list; the engine selects only among those moves.

Run with `MAKEFUN_ENV_URL` set by the competition environment:

```sh
python3.13 -P -s main.py
```

`main.py` is below the 4,096-byte limit. The full snapshot is subject to the 8,192-byte cap. MIT; see `LICENSE`.
