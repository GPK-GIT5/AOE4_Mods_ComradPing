# Coop Taiga (4p) — Documentation Mirror

Navigation hub for [`Scenarios/coop_4_taiga/`](../../../Scenarios/coop_4_taiga/).

## TL;DR

4-player Taiga co-op scenario. SCAR logic lives in [`Scenarios/coop_4_taiga/scar/`](../../../Scenarios/coop_4_taiga/scar/).
This scenario follows the shared 4p coop module pattern with one Taiga-specific extension module (`roving_army.scar`).

## Recommended read order

1. `coop_4_taiga.scar` (entry script and module imports)
2. `scar/coop_4_taiga_data.scar` (state and data contracts)
3. `scar/coop_4_taiga_objectives.scar` and `scar/coop_4_taiga_spawns.scar`
4. `scar/roving_army.scar` (Taiga-specific behavior)
5. `scar/diplomacy/` (UI + relations + tribute flow)

## SCAR module layout — `scar/` subfolder

Common modules (see [../README.md](../README.md) for the shared pattern):
`coop_4_taiga_data.scar`, `_difficulty.scar`, `_disconnect.scar`, `_objectives.scar`, `_spawns.scar`, `_training.scar`, `_debug.scar`, plus `roving_army.scar` (Taiga-specific) and `diplomacy/` subfolder.

## Module intent quick map

- `_data.scar`: shared scenario state and helper constants.
- `_difficulty.scar`: difficulty gates and scale multipliers.
- `_objectives.scar`: objective lifecycle and progression triggers.
- `_spawns.scar`: enemy wave and placement scheduling.
- `roving_army.scar`: Taiga-specific roaming pressure behavior.
- `diplomacy/`: alliance/tribute UI and relationship handlers.

## See also

- [../README.md](../README.md) — Scenarios overview + common module pattern
- [../coop_4_japanese/README.md](../coop_4_japanese/README.md) — most similar scenario with extensive docs
