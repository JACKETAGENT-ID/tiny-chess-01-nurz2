# nurz-chess2 — tiny-chess-01 entry

An original chess engine in one Python file (<= 4,096 bytes packed), built for
the make.fun tiny-chess-01 gauntlet. It plays through the env at
MAKEFUN_ENV_URL (POST /game, /move, /resign) and never calls a model.

Design: 0x88 mailbox board, negamax alpha-beta with iterative deepening
under a fixed node budget (no clock anywhere in the search, so a replay
makes the same moves), PVS with late-move reductions, null-move pruning and
check extensions, quiescence over captures, promotions and check evasions
with delta pruning, a transposition table with mate-distance adjustment,
MVV-LVA ordering with killer moves and a history heuristic. Evaluation is
incremental tapered material plus piece-square tables (midgame/endgame) and
the bishop pair. Repetitions, the hundred-ply rule and dead positions score
0 inside the search, like the house engines.

The readable source is engine.py (kept beside the packed entry, gitignored);
main.py is the packed entry produced by the kit's `makefun compress`.
