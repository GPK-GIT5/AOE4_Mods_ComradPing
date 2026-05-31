# Master Index — AoE4 SCAR Reference

> Complete navigation hub for all reference documentation: 8 campaign summaries, 3 gameplay system overviews, 6 cross-cutting system indexes, and 5 mechanical CSV indexes.

**→ New users: Start with [INDEX.md](INDEX.md) for organized navigation by workflow and task.**

---

## Quick Links
- [Function Index](../indexes/function-index.md) | [CSV](../indexes/function-index.csv)
- [Objectives Index (mechanical)](../indexes/objectives-index.csv) | [Objectives Index (annotated)](../systems/objectives-index.md)
- [Imports Index](../indexes/imports-index.csv)
- [Groups Index](../indexes/groups-index.csv)
- [Globals Index](../indexes/globals-index.csv)

---

## Campaign Design Notes

Each link goes to the campaign's consolidated README with mission overview, shared patterns, and Onslaught-relevant analysis.

### Abbasid Dynasty (9 missions)
[../../../design_notes/campaigns/abbasid/README.md](../../../design_notes/campaigns/abbasid/README.md) — Crusades era; dual win conditions, tug-of-war balance, resource-threshold assaults

### Angevin Empire (11 missions)
[../../../design_notes/campaigns/angevin/README.md](../../../design_notes/campaigns/angevin/README.md) — Norman conquest; progressive objective chains, garrison clearance, multi-vector defense

### Art of War Challenges (13 missions)
[../../../design_notes/campaigns/challenges/README.md](../../../design_notes/campaigns/challenges/README.md) — Tutorial/challenge missions; medal benchmarking, wall defense, civ-specific training

### Hundred Years' War (8 missions)
[../../../design_notes/campaigns/hundred/README.md](../../../design_notes/campaigns/hundred/README.md) — French reconquest; wave defense, hero-survival arc, siege relief duality

### Mongol Empire (9 missions)
[../../../design_notes/campaigns/mongol/README.md](../../../design_notes/campaigns/mongol/README.md) — Cavalry campaigns; feigned retreat, progressive breach, multi-stage siege arc

### Rise of Moscow (8 missions)
[../../../design_notes/campaigns/russia/README.md](../../../design_notes/campaigns/russia/README.md) — Russian unification; tribute delivery, diplomatic restraint victory, forest concealment

### Rogue Mode
[../../../design_notes/campaigns/rogue/README.md](../../../design_notes/campaigns/rogue/README.md) — Wonder defense; lane system, combinatorial waves, polynomial difficulty, medal progression

### The Normans / Salisbury (6 missions)
[../../../design_notes/campaigns/salisbury/README.md](../../../design_notes/campaigns/salisbury/README.md) — Tutorial arc; hold-under-outnumbered, withdrawal objectives, economy scaffolding

---

## Gameplay Systems
| System | File | Description |
|--------|------|-------------|
| Gameplay Frameworks | [../../../game_systems/gameplay/README.md](../../../game_systems/gameplay/README.md) | MissionOMatic, AI modules, Army/Encounter system, Rogue mode, prefab/trigger system |
| Cross-Cutting Systems | [../../../game_systems/systems/README.md](../../../game_systems/systems/README.md) | Module lifecycle, wave/spawn pipeline, objective methodology, difficulty scaling |
| Onslaught PlayerUI | [../../../game_systems/ui/README.md](../../../game_systems/ui/README.md) | Custom HUD architecture, two-layer timing, XAML data flow, tracking modules |
| Training | [training.md](../gameplay/training.md) | Goal→GoalSequence architecture, civ-specific modules, three input modes (PC/Xbox Controller/Xbox KBM), timer constants |
| UI | [ui.md](../gameplay/ui.md) | Ottoman Vizier/Imperial Council mechanic: Vizier Points tracking, audio notifications, observer/replay mode |
| Win Conditions | [winconditions.md](../gameplay/winconditions.md) | Annihilation, Conquest, Religious, Wonder, Regicide, Elimination, Surrender, Empire Wars; team and FFA support |

---

## System Indexes (6 files)
| Index | File | Cross-cuts |
|-------|------|------------|
| Objectives | [objectives-index.md](../systems/objectives-index.md) | All campaigns |
| Difficulty | [difficulty-index.md](../systems/difficulty-index.md) | All campaigns |
| Spawns | [spawns-index.md](../systems/spawns-index.md) | All campaigns + AI/MissionOMatic |
| AI Patterns | [ai-patterns.md](../systems/ai-patterns.md) | All campaigns + AI gameplay |
| Training | [training-index.md](../systems/training-index.md) | Training + Challenges + Salisbury |
| MissionOMatic | [missionomatic-modules.md](../systems/missionomatic-modules.md) | MissionOMatic + All campaigns |

---

## Phase 1 Mechanical Indexes
| File | Records | Description |
|------|---------|-------------|
| [function-index.csv](../indexes/function-index.csv) | ~9,000 | All function signatures with file, line, and parameter info |
| [objectives-index.csv](../indexes/objectives-index.csv) | ~1,500 | OBJ_/SOBJ_ constants with file and line references |
| [imports-index.csv](../indexes/imports-index.csv) | ~1,300 | import() dependency graph across all SCAR files |
| [groups-index.csv](../indexes/groups-index.csv) | ~3,200 | SGroup/EGroup creation calls with context |
| [globals-index.csv](../indexes/globals-index.csv) | ~14,000 | Global variable assignments across all files |

---

## Additional Reference Files
| File | Description |
|------|-------------|
| [function-index.md](../indexes/function-index.md) | Narrative companion to function-index.csv with usage patterns |
| [api/README.md](../api/README.md) | SCAR scripting system overview (engine catalogs removed — see Xbox Game Content Usage Rules) |
| [data-index.md](data-index.md) | Data file index and descriptions |
| [aoe4world-data-index.md](aoe4world-data-index.md) | AoE4 World parsed game data cross-reference (units, buildings, techs, civs) |
| [blueprints/](../blueprints/) | Per-civilization blueprint references (14 files) |
| [ui/PlayerUI_Architecture.md](../ui/PlayerUI_Architecture.md) | Onslaught PlayerUI HUD architecture, lifecycle, and XamlPresenter bindings |
| [ui/UI_SetPlayerDataContext_FieldDiscovery.md](../ui/UI_SetPlayerDataContext_FieldDiscovery.md) | UI_SetPlayerDataContext field discovery methodology and results |
| [ui/UI_SetPlayerDataContext_QuickReference.md](../ui/UI_SetPlayerDataContext_QuickReference.md) | Quick reference for safe vs. fatal XamlPresenter bindings |
