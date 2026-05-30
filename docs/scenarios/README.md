# Scenarios — Documentation Mirror

Navigation hub for the [`Scenarios/`](../../Scenarios/) runtime tree.
Scenario folders are AoE4 scenario packages and cannot hold README/metadata files, so all navigation lives here in `docs/`.

## TL;DR

Four co-op scenarios share a common SCAR module pattern. Each scenario folder contains a `.scenario` file plus a SCAR module set; the three 4-player maps additionally have a `scar/` subfolder housing the bulk of their logic.

## Scenarios

| Scenario | Runtime path | Layout | Docs entry |
|---|---|---|---|
| Coop Arabia (2p) | [`Scenarios/coop_2_arabia/`](../../Scenarios/coop_2_arabia/) | Flat (no `scar/` subfolder) | [coop_2_arabia/README.md](coop_2_arabia/README.md) |
| Coop Japanese (4p) | [`Scenarios/coop_4_japanese/`](../../Scenarios/coop_4_japanese/) | Uses `scar/` subfolder | [coop_4_japanese/README.md](coop_4_japanese/README.md) |
| Coop Taiga (4p) | [`Scenarios/coop_4_taiga/`](../../Scenarios/coop_4_taiga/) | Uses `scar/` subfolder | [coop_4_taiga/README.md](coop_4_taiga/README.md) |
| Coop Woodland (4p) | [`Scenarios/coop_4_woodland/`](../../Scenarios/coop_4_woodland/) | Uses `scar/` subfolder | [coop_4_woodland/README.md](coop_4_woodland/README.md) |

## Common SCAR module pattern

Each scenario typically splits its logic into:

| Module suffix | Purpose |
|---|---|
| `_data.scar` | Static data tables (squads, blueprints, intel) |
| `_difficulty.scar` | Difficulty scaling values |
| `_diplomacy.scar` | Team/relationship setup |
| `_objectives.scar` | Objective registration + progression |
| `_spawns.scar` | Wave/spawn logic |
| `_debug.scar` | Debug commands + cheats |
| `_disconnect.scar` | Disconnect/AFK handling (4p only) |
| `_training.scar` | Training hints / tutorial flows |

## See also

- [../gamemodes/README.md](../gamemodes/README.md) — gamemode mirror (Onslaught, AGS)
- [../game_systems/](../game_systems/) — engine/system-level references
- [../archive/scenarios/README.md](../archive/scenarios/README.md) — archived scenario history and checkpoints
