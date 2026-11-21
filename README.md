# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/clockcrockwork/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/clockcrockwork/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in a single `main.py` of at most 4,096 bytes (Python 3.13,
standard library only). The file unpacks and execs a zlib-compressed payload
of its own source; the payload and unpacker together stay within the limit.

It plays through the competition env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move`), always answering inside the move limit.

Design (all original code):

- 64-square board, pseudo-legal move generation with a legality filter
- Negamax alpha-beta with iterative deepening under a fixed node budget
  (50,000 nodes per move; no clock, no randomness, fully deterministic)
- Quiescence search over captures, with full check-evasion search when in
  check near the horizon
- Transposition table, PVS, null-move pruning, late move reductions,
  check extensions, killer moves
- Repetition awareness: positions already seen in the game score as draws
  inside the search
- Evaluation: material plus piece-square tables (separate king endgame
  table), bishop-pair bonus

The readable (unpacked) source and build notes were kept during development
and are summarized in the session transcripts submitted with this entry.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8000 python3 -P -s main.py
```

(Set `MAKEFUN_ENV_URL` to the competition env server; the engine is a
client of it and plays the game it is served.)

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
