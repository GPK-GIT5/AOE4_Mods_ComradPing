# Coop Arabia (2p) — Documentation Mirror

Navigation hub for [`Scenarios/coop_2_arabia/`](../../../Scenarios/coop_2_arabia/).

## TL;DR

2-player co-op scenario on an Arabia-style map. Unlike the 4-player scenarios, the SCAR modules sit **flat** at the scenario root rather than in a `scar/` subfolder.

## Reference documents

| Document | Purpose |
|---|---|
| [arabia-mod-index.md](arabia-mod-index.md) | Full module index, implementation notes, optimization patterns |

## SCAR modules (flat layout at scenario root)

| Module | Purpose |
|---|---|
| `coop_2_arabia.scar` | Scenario entry point |
| `coop_2_arabia_data.scar` | Static data |
| `coop_2_arabia_debug.scar` | Debug commands |
| `coop_2_arabia_difficulty.scar` | Difficulty scaling |
| `coop_2_arabia_diplomacy.scar` / `_diplomacy_ui.scar` | Diplomacy + UI |
| `coop_2_arabia_objectives.scar` | Objectives |
| `coop_2_arabia_relations.scar` | Relationship setup |
| `coop_2_arabia_spawns.scar` | Spawn logic |
| `coop_2_arabia_tribute.scar` / `_tributes.scar` | Tribute system |
| `day_night_cycle.scar` | Day/night cycle controller |

## See also

- [../README.md](../README.md) — Scenarios overview + common module pattern
- [../../gamemodes/MOD-INDEX.md](../../gamemodes/MOD-INDEX.md) — cross-mod index
