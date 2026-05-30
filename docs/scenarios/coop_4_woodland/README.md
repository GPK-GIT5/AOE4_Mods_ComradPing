# Coop Woodland (4p) — Documentation Mirror

Navigation hub for [`Scenarios/coop_4_woodland/`](../../../Scenarios/coop_4_woodland/).

## TL;DR

4-player Woodland co-op scenario. SCAR logic lives in [`Scenarios/coop_4_woodland/scar/`](../../../Scenarios/coop_4_woodland/scar/).
This scenario follows the shared 4p coop module pattern and keeps scenario-specific behavior mostly in spawn/objective tuning.

## Recommended read order

1. `coop_4_woodland.scar` (entry script and imports)
2. `scar/coop_4_woodland_data.scar` (state and constants)
3. `scar/coop_4_woodland_objectives.scar` and `scar/coop_4_woodland_spawns.scar`
4. `scar/coop_4_woodland_difficulty.scar` (difficulty modifiers)
5. `scar/diplomacy/` (relations, tribute, and UI flow)

## SCAR module layout — `scar/` subfolder

Common modules (see [../README.md](../README.md) for the shared pattern):
`coop_4_woodland_data.scar`, `_difficulty.scar`, `_disconnect.scar`, `_objectives.scar`, `_spawns.scar`, `_training.scar`, `_debug.scar`, plus `diplomacy/` subfolder.

## Module intent quick map

- `_data.scar`: scenario state, constants, and helper glue.
- `_difficulty.scar`: per-level challenge scaling.
- `_objectives.scar`: objective activation/completion handlers.
- `_spawns.scar`: enemy unit timing and spawn orchestration.
- `diplomacy/`: team diplomacy UI and tribute event handling.

## See also

- [../README.md](../README.md) — Scenarios overview + common module pattern
- [../coop_4_japanese/README.md](../coop_4_japanese/README.md) — most similar scenario with extensive docs
