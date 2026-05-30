# Coop Japanese (4p) — Documentation Mirror

Navigation hub for [`Scenarios/coop_4_japanese/`](../../../Scenarios/coop_4_japanese/).

## TL;DR

4-player Japan co-op scenario. SCAR logic lives in [`Scenarios/coop_4_japanese/scar/`](../../../Scenarios/coop_4_japanese/scar/). This scenario has the most extensive documentation of any scenario — see the checkpoint/stage references below.

## Active references

| Document | Purpose |
|---|---|
| [japan-guide-api-reference.md](japan-guide-api-reference.md) | Complete API reference (helpers, resolvers, restriction functions) |
| [japan-checkpoint-index.md](japan-checkpoint-index.md) | Stage status snapshots and checksums |
| [japan-checkpoint-summary.md](japan-checkpoint-summary.md) | High-level checkpoint summary |
| [japan-stage4-restriction.md](japan-stage4-restriction.md) | Stage 4 profile audit + restriction points |

## Historical checkpoint snapshots

These files are now archived. The links below remain as redirect stubs and point to the archive location.

| [japan-checkpoint-stage3.md](japan-checkpoint-stage3.md) | Rollback guide + verification steps for Stage 3 |
| [japan-checkpoint-stage3-manifest.md](japan-checkpoint-stage3-manifest.md) | Line-by-line file breakdown for Stage 3 |
| [japan-stage1-summary.md](japan-stage1-summary.md) | Stage 1 work summary |
| [japan-stage2-summary.md](japan-stage2-summary.md) | Stage 2 work summary |
| [japan-archive-refactor-log.md](japan-archive-refactor-log.md) | Refactor history |

Archive hub: [docs/archive/scenarios/japan-development/README.md](../../archive/scenarios/japan-development/README.md)

Checksum and integrity notes are maintained in the markdown checkpoint documents above.

## SCAR module layout — `scar/` subfolder

Common modules (see [../README.md](../README.md) for the shared pattern):
`coop_4_japanese_data.scar`, `_difficulty.scar`, `_disconnect.scar`, `_objectives.scar`, `_spawns.scar`, `_training.scar`, `_debug.scar`, plus `diplomacy/` subfolder.

## See also

- [../README.md](../README.md) — Scenarios overview
- [../../gamemodes/MOD-INDEX.md](../../gamemodes/MOD-INDEX.md) — cross-mod index (Japan section)
- [../../gamemodes/onslaught/onslaught-debug-reference.md](../../gamemodes/onslaught/onslaught-debug-reference.md) — debug system used by this scenario
