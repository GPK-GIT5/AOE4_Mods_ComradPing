# API Reference

*Age of Empires IV © Microsoft Corporation. This workspace was created under Microsoft's "Game Content Usage Rules" using assets from Age of Empires IV, and it is not endorsed by or affiliated with Microsoft.*

Primary reference hub for SCAR/API lookups in this repository. This folder is the canonical lookup layer for SCAR functions, signatures, constants, events, Onslaught symbol indexes, and game data cross-references.

---

## Folder structure

```
api_reference/
└── README.md                           ← this file (all reference content is inline)
```

---

## SCAR scripting system

The `api/` subfolder previously contained five Relic/Microsoft engine API catalog files. Those files have been removed to comply with the [Xbox Game Content Usage Rules](https://www.xbox.com/en-US/developers/rules). The coverage areas of the removed files were:

- **Scripting function surface** — The callable Lua API organized into namespaces by target object type: `Squad_*`, `Entity_*`, `SGroup_*`, `EGroup_*`, `Player_*`, `UI_*`, `World_*`, `AI_*`, `Rule_*`, `Misc_*`, `Util_*`, and others. Functions covered creation, destruction, state queries, movement, combat, ability activation, production, resources, diplomacy, and objective/event integration.
- **Typed engine signatures** — Full parameter and return-type annotations across 89 namespaces, sourced from `Essence_ScarFunctions.api`.
- **Command constants** — Enumerated integer constants: `CMD_*` (entity), `SCMD_*` (squad), `PCMD_*` (player), `TASK_*` (AI task types).
- **Game constants and enumerations** — `RT_*` (resource types), `AGE_*` (age tiers), unit stances, diplomatic relationships, win-condition reasons, objective states, and other engine-defined enumerations.
- **Game event system** — The `GE_*` event catalog used with `Rule_AddGlobalEvent()`: entity killed/created/garrisoned, construction complete, upgrade complete, ability triggered, resource change, game state transitions.

---

## Onslaught indexes

Project-owned indexes derived from this repository's Onslaught SCAR source. Safe to redistribute.

### Function index

Auto-generated 2026-04-02. **1,746 total functions** — 1,266 public / 331 private (`_` prefix) / 149 local.

| Module | Functions | Files |
|---|---:|---:|
| conditions | 68 | 4 |
| debug | 678 | 28 |
| gameplay | 291 | 21 |
| helpers | 52 | 3 |
| observerui | 156 | 25 |
| playerui | 216 | 13 |
| rewards | 18 | 4 |
| root | 220 | 8 |
| specials | 29 | 3 |
| startconditions | 18 | 2 |

### Globals index

Auto-generated 2026-04-02. **647 total top-level assignments**.

| Module | Globals |
|---|---:|
| conditions | 69 |
| debug | 45 |
| gameplay | 100 |
| helpers | 135 |
| observerui | 50 |
| playerui | 137 |
| rewards | 4 |
| root | 92 |
| specials | 5 |
| startconditions | 10 |

### Villager/engineer map

Maps villager build capability per civilization. Covers 42 civilization/variant combinations derived from `all-optimized.json` (AoE4World). Each row lists race folder, villager squad file, variant type, civ code, building category counts, and the full `building_*` attrib_name list.

### Excluded sources

The following index files are generated from AoE4 game data or Relic SCAR documentation and are **not** redistributed in the public repository:

| File | Source | Reason |
|---|---|---|
| `campaign-index.md` | Relic campaign SCAR dump | Derived from Relic IP |
| `cardinal-ucs-strings.csv` | `cardinal.ucs` (game localization) | Game IP |
| `construction-menu-map.{csv,lua,md}` | AoE4World JSON + AGS construction menu | Derived third-party data |
| `function-index.{csv,md}` | Relic SCAR dump | Derived from Relic IP |
| `gameplay-index.md` | Relic gameplay SCAR dump | Derived from Relic IP |
| `globals-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `groups-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `imports-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `objectives-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `scar-engine-functions.csv` | Relic `Essence_ScarFunctions.api` | Engine API surface |
| `scar-engine-constants.csv` | Relic `Essence_Constants.api` | Engine API surface |
| `ebp_alias_map.json` | Empty pipeline stub | No content yet |

To regenerate excluded indexes locally: install the official Age of Empires IV Content Editor, export `cardinal.ucs`, SCAR documentation, and blueprint XML, then run the private extraction pipeline against that local data. The pipeline and its output are not part of the public repository.

---

## Dependency & data index

Auto-generated snapshot of SCAR import/dependency structure (2026-02-23).

| Metric | Count |
|---|---:|
| Import statements | 1,283 |
| Unique imported modules | 453 |
| SGroup/EGroup declarations | 3,214 (2,716 SGroups / 498 EGroups) |
| Global variable assignments | 14,158 |

> OBJ_/SOBJ_ constants (835 entries) were removed — those reference Relic campaign source files not in the public repository.

Top 10 most-imported modules (of 453): `MissionOMatic/MissionOMatic.scar` (166 files), `cardinal.scar` (140), `training/campaigntraininggoals.scar` (42), `training/coretraininggoals.scar` (39), `training.scar` (34), `obj_<prefix>.scar` (26), `MissionOMatic/MissionOMatic_utility.scar` (20), `training/coretrainingconditions.scar` (18), `scarutil.scar` (18), `missionomatic/missionomatic_artofwar.scar` (14).

---

## AoE4 World data

Cross-reference guide for parsed AoE4 game data from [AoE4 World](https://data.aoe4world.com/) (data version 0.0.2, updated 2026-02-23). Machine-readable JSON: units, buildings, technologies, civilizations.

### Data folders

| Folder | Files | Purpose |
|---|---:|---|
| `data/units/` | 1,266 | Unit statistics by civilization |
| `data/buildings/` | 861 | Building statistics by civilization |
| `data/technologies/` | 2,207 | Technology/upgrade data by civilization |
| `data/civilizations/` | 23 | Civilization metadata (ID, name, abbreviation, expansion, attribName) |

File naming: `{civ}.json` / `{civ}-unified.json` (base + `variations[]`) / `{civ}-optimized.json` (fast lookup) / `all.json` (aggregated) / `all-unified.json` / `all-optimized.json` / `all-baseids.json` (buildings — base ID cross-reference).

### Field mapping: SCAR ↔ AoE4 JSON

| SCAR Blueprint Field | AoE4 JSON Field | Description | Example |
|---|---|---|---|
| Blueprint Name | `attribName` | Internal game identifier | `"unit_archer_2_abb"` |
| Blueprint ID | `pbgid` | Unique integer variant ID (PBG = PropertyBlueprintGroup) | `199706` |
| Object ID | `id` | Human-readable identifier | `"archer-2"` |
| Base Type | `baseId` | Shared across variants | `"archer"` |
| Display Name | `name` | In-game display name | `"Archer"` |
| Type | `type` | Entity category | `"unit"`, `"building"`, `"technology"` |
| Civilization(s) | `civs[]` | Civilization abbreviations | `["ab", "ch", "en"]` |
| Classes | `classes[]` | Gameplay tags | `["infantry", "ranged", "military"]` |
| Age | `age` | Minimum age requirement (2–4) | `2` |

**Lookup priority:** `pbgid` (exact variant, fastest) → `attribName` (blueprint name string) → `baseId` (class-based substitution) → `id` (human-readable).

### Civilization abbreviations

`ab` Abbasid · `ay` Ayyubids · `by` Byzantines · `ch` Chinese · `de` Delhi Sultanate · `fr` French · `gol` Golden Horde (Mongol HA) · `hr` HRE · `ja` Japanese · `je` Jeanne d'Arc (French HA) · `kt` Order of the Dragon · `hl` House of Lancaster · `mac` Macedonians (Byzantine HA) · `ma` Malians · `mo` Mongols · `ot` Ottomans · `ru` Rus · `sen` Oda Clan (Japanese HA) · `tug` Tughlaq Dynasty (Sultanate HA) · `od` Ottonian Dynasty (HRE HA) · `zx` Zhuge Liang (Chinese HA)

---

## Campaign design notes

Each campaign README contains mission overview, shared patterns, and Onslaught-relevant analysis.

| Campaign | Missions | Era / Mode | Design Patterns |
|---|---:|---|---|
| [Abbasid Dynasty](../design_notes/campaigns/abbasid/README.md) | 9 | Crusades | Dual win conditions, tug-of-war balance, resource-threshold assaults |
| [Angevin Empire](../design_notes/campaigns/angevin/README.md) | 11 | Norman conquest | Progressive objective chains, garrison clearance, multi-vector defense |
| [Art of War Challenges](../design_notes/campaigns/challenges/README.md) | 13 | Tutorial/challenges | Medal benchmarking, wall defense, civ-specific training |
| [Hundred Years' War](../design_notes/campaigns/hundred/README.md) | 8 | French reconquest | Wave defense, hero-survival arc, siege relief duality |
| [Mongol Empire](../design_notes/campaigns/mongol/README.md) | 9 | Cavalry campaigns | Feigned retreat, progressive breach, multi-stage siege arc |
| [Rise of Moscow](../design_notes/campaigns/russia/README.md) | 8 | Russian unification | Tribute delivery, diplomatic restraint victory, forest concealment |
| [Rogue Mode](../design_notes/campaigns/rogue/README.md) | — | Wonder defense | Lane system, combinatorial waves, polynomial difficulty, medal progression |
| [The Normans / Salisbury](../design_notes/campaigns/salisbury/README.md) | 6 | Tutorial arc | Hold-under-outnumbered, withdrawal objectives, economy scaffolding |

---

## Gameplay systems

| System | File | Description |
|---|---|---|
| Gameplay Frameworks | [game_systems/gameplay/README.md](../game_systems/gameplay/README.md) | MissionOMatic, AI modules, Army/Encounter system, Rogue mode, prefab/trigger system |
| Cross-Cutting Systems | [game_systems/systems/README.md](../game_systems/systems/README.md) | Module lifecycle, wave/spawn pipeline, objective methodology, difficulty scaling |
| Onslaught PlayerUI | [game_systems/ui/README.md](../game_systems/ui/README.md) | Custom HUD architecture, two-layer timing, XAML data flow, tracking modules |

---

## Usage workflows

### Quick API lookup

1. Read the [SCAR scripting system](#scar-scripting-system) section above for coverage area context.
2. For Onslaught-specific symbols use the [Function index](#function-index) or [Globals index](#globals-index) tables above.

### Deep symbol lookup (Onslaught-heavy work)

1. Use the module breakdown tables above to narrow the relevant module.
2. Navigate to the [Function index](#function-index) and locate the module section.
3. Cross-reference with the [Globals index](#globals-index) for related global state.

### Blueprint / data lookup

1. Identify the blueprint string or entity type you need.
2. Consult the [field mapping table](#field-mapping-scar--aoe4-json) to locate the correct JSON field.
3. Search `game_data/extracted/aoe4/data/` using the lookup priority: `pbgid` → `attribName` → `baseId`.
4. For per-civ villager build sets see the [Villager/engineer map](#villagerengineer-map) section above.

### Troubleshooting missing/ambiguous references

1. Check the [Excluded sources](#excluded-sources) section — the reference may be from a non-public source.
2. Check the [Dependency & data index](#dependency--data-index) section above for import/dependency context.
3. Cross-check implementation context in [../gamemodes/MOD-INDEX.md](../gamemodes/MOD-INDEX.md) and [../game_systems/README.md](../game_systems/README.md).

---

## Related docs

- [../README.md](../README.md) — top-level docs index
- [../game_systems/README.md](../game_systems/README.md) — system-level references
- [../development_guides/README.md](../development_guides/README.md) — implementation guides
- [../gamemodes/MOD-INDEX.md](../gamemodes/MOD-INDEX.md) — mod/scenario cross-reference hub
- [../scenarios/README.md](../scenarios/README.md) — scenario runtime mirror

## Maintenance notes

- This README is the canonical entry point; keep all section summaries current when reference content changes.
- New reference content should be added directly to this README.
- Regenerated indexes (function, globals) update stats in the [Onslaught indexes](#onslaught-indexes) section.
