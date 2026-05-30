# Civ Data Debugger & Extraction Plan

> Staged plan for building a reliable AI-consumable source of truth for AoE4 SCAR modding.
> Covers: civs, units, buildings, abilities, upgrades, weapons, dependencies, inheritance, requirements, progression, costs, roles, comparisons, and inconsistencies.

**Created:** 2026-03-26  
**Status:** Plan  
**Storage convention:** `/data` → raw, parsed, normalized | `/references` → summaries, maps, comparisons, AI outputs

---

## Current State Assessment

### What Exists

| Source | Location | Format | Records | Coverage |
|--------|----------|--------|---------|----------|
| Unit data (all civs, all ages) | `game_data/extracted/aoe4/data/units/all-unified.json` | JSON | ~1,200 variations | id, pbgid, attribName, age, civs, classes, costs, hitpoints, weapons[], armor[], sight, movement, producedBy |
| Building data | `game_data/extracted/aoe4/data/buildings/all-unified.json` | JSON | ~600 variations | Same schema as units + influences[] |
| Technology data | `game_data/extracted/aoe4/data/technologies/all-unified.json` | JSON | ~800 variations | id, age, civs, classes, costs (array), appliesTo[], effects[] (text) |
| Civ metadata | `game_data/extracted/aoe4/data/civilizations/civs-index.json` | JSON | 22 entries | id, name, abbr, slug, attribName, expansion |
| Per-civ JSON files | `game_data/extracted/aoe4/data/units/{civ}/`, `buildings/{civ}/`, `technologies/{civ}/` | JSON | Per-unit/building/tech | Individual file per age variant |
| DLC blueprint inventory | `game_data/extracted/aoe4/data/dlc_bp_inventory.txt` | Pipe-delimited | All DLC civs | attribName ↔ id mapping |
| Engine API docs | `game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api` | Text records | 1,983 functions | Full typed signatures with descriptions |
| Constants/enums | `game_data/extracted/aoe4/scardocs/Essence_Constants.api` | 1-per-line | 975 constants | Names only (no numeric values) |
| Parsed API (JSON) | `game_data/extracted/aoe4/scardocs/parsed_functions.json`, `parsed_constants.json` | JSON | Structured parse | Namespace, params, descriptions |
| SCAR code dump (Relic) | `game_data/extracted/aoe4/scar_dump/scar campaign/`, `scar gameplay/` | .scar | ~90 files | Official campaign + gameplay scripts |
| Blueprint references | `game_data/extracted/blueprints/*.md` | Markdown | 13 civ + 4 special | Unit/entity/upgrade constants per source |
| Function index | `docs/api_reference/indexes/function-index.csv` | CSV | 8,989 rows | Category, File, Function, Params, Line, Visibility |
| Globals index | `docs/api_reference/indexes/globals-index.csv` | CSV | 14,158 rows | Category, File, Variable, Line, Value |
| Onslaught runtime tables | Onslaught SCAR | Lua tables | 22 civs + 6 DLC | AGS_ENTITY_TABLE, CBA_SIEGE_TABLE, AGS_UPGRADE_TABLE, CBA_CIV_BP_SUFFIX, AGS_CIV_PARENT_MAP |
| Runtime audit systems | Onslaught debug/ | SCAR | 25 civs | CivOverview, BlueprintAudit (existence + coverage) |

### Key Gaps

| Gap | Impact | Recoverable From |
|-----|--------|------------------|
| No health-per-age progression | Can't compare unit scaling | Per-civ JSON files (separate files per age exist) |
| No DPS aggregates | No combat power metric | Computable from weapons[].damage × speed |
| Tech effect numerics missing | Can't model upgrade impact | Only text descriptions in effects[]; requires AI parsing or external data |
| No prerequisite chains | Can't build tech tree graph | Not in JSON; partial from `producedBy[]` + age gates; attrib files may have |
| No garrison capacity | Missing building slot data | SCAR runtime: `Entity_GetMaxHoldSquadSlots()` (requires live entity) |
| No influence radius values | Aura effects text-only | JSON influences[] is text; no numeric extraction available |
| No ability data | Missing active abilities | Not in current JSON schema; may exist in attrib files |
| No weapon modifier details | Can't model bonus damage | weapons[].modifiers[] exists but may be sparse |
| DLC civ blueprint refs incomplete | Only 13 base-civ markdown refs exist | Must generate from per-civ JSON + DLC inventory |
| No civ balance metadata | No patch history or balance context | External only (patch notes, community wikis) |

### Runtime SCAR APIs Available for Live Extraction

| API | Data Accessible | Constraint |
|-----|----------------|------------|
| `BP_GetPropertyBagGroupCount(type)` + `BP_GetPropertyBagGroupPathName(type, i)` | Enumerate ALL blueprints (entity, squad, upgrade) | Runtime only; need game running |
| `World_GetPossibleSquadsCount(racePBG)` + `World_GetPossibleSquadsBlueprint(racePBG, i)` | All squad BPs available to a race | Civ-filtered enumeration |
| `BP_GetEntityBPCost(ebp)`, `Player_GetSquadBPCost(player, sbp)` | Costs (base or with player modifiers) | Player-modified costs need live player |
| `BP_GetEntityBPBuildTime(ebp)` | Build time | Base value only |
| `BP_GetEntityBPDefaultSpeed(ebp, modified, player)` | Movement speed | Optional player modifier |
| `EBP_PopulationCost(ebp, player, type)` | Pop cost by cap type | Needs player for modifiers |
| `Entity_GetHealthMax(eid)` | HP (at current age) | Requires live spawned entity |
| `Entity_GetMaxHoldSquadSlots(eid)` | Garrison capacity | Requires live spawned entity |
| `Entity_GetWeaponBlueprint(eid, hardpoint)` | Weapon blueprint per hardpoint | Requires live spawned entity |
| `SBP_Exists(name)`, `EBP_Exists(name)` | Blueprint existence check | Fast validation; no data |
| `Player_HasUpgrade(player, ubp)` | Upgrade completion state | Live state only |
| `BP_GetName(pbg)` | Stable string name for any PBG | Use for table keys, NEVER raw handles |

---

## Stage 1: Source Discovery

**Objective:** Catalog every accessible data source, validate freshness, quantify coverage, identify authoritative sources per data domain.

### Data to Retrieve
- File inventory of `/game_data/extracted/aoe4/data/` with last-modified timestamps and record counts
- Cross-reference civs-index.json (22 civs) against per-civ folder coverage in units/, buildings/, technologies/
- Inventory all Onslaught runtime tables (AGS_ENTITY_TABLE key count per civ, CBA_SIEGE_TABLE key count, AGS_UPGRADE_TABLE key count)
- Map extraction script outputs to their source inputs
- Verify scardocs API version matches current game build

### Why It Matters
Prevents extracting data that already exists in a different location. Establishes which source is authoritative for each data domain (e.g., costs → JSON is authoritative; blueprint validity → runtime EBP_Exists is authoritative).

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| `source-inventory.json` | JSON | `game_data/extracted/aoe4/source-inventory.json` |
| Source authority matrix (which source owns which data domain) | Markdown table | `research/investigations/workspace_history/data-authority-matrix.md` |

### Dependencies
- None (baseline stage)

### Limitations
- Timestamps only prove extraction date, not data freshness relative to game patches
- Runtime tables can't be inventoried without a running game session

### Storage
- `game_data/extracted/aoe4/source-inventory.json` — machine-readable catalog
- `research/investigations/workspace_history/data-authority-matrix.md` — human/AI-readable authority map

---

## Stage 2: Raw Extraction

**Objective:** Pull new data not currently captured. Fill the highest-impact gaps using both offline processing and SCAR runtime extraction.

### Sub-stage 2a: Offline Extraction (PowerShell / JSON Processing)

**Data to retrieve:**
1. **Health-per-age tables** — Parse per-civ unit JSON files (e.g., `game_data/extracted/aoe4/data/units/english/longbowman-2.json`, `-3.json`, `-4.json`) to build `{unit → {age → hp}}` maps
2. **DPS computation** — From all-unified.json weapons[], compute `damage × (1 / (aim + windup + attack + winddown + reload))` per weapon per unit
3. **Cost normalization** — Normalize technology costs from `[{resource, amount}]` array format to `{food, wood, gold, stone, total, time}` dict matching unit/building schema
4. **Weapon modifier extraction** — Parse `weapons[].modifiers[]` fully from all-unified.json to build bonus-damage tables
5. **Production chain mapping** — From `producedBy[]` across units + buildings + technologies, build `{producer → [products]}` reverse map
6. **DLC civ completeness check** — Compare per-civ folder contents between DLC variants and their parents (e.g., lancaster vs english) to detect missing/extra entries
7. **Blueprint suffix → attribName mapping** — Parse DLC inventory + all-unified attribNames to build complete `{civ_suffix → [attribNames]}` catalog

**Script:** New `scripts/extract_civ_data.ps1`

### Sub-stage 2b: Runtime Extraction (SCAR Debug Console)

**Data to retrieve:**
1. **Full BP enumeration** — Use `BP_GetPropertyBagGroupCount` + `BP_GetPropertyBagGroupPathName` for ENTITY, SQUAD, UPGRADE types. Dump all path names to log.
2. **Per-race squad inventory** — Use `World_GetPossibleSquadsCount` + `World_GetPossibleSquadsBlueprint` for each of the 22 race PBGs. This gives the *engine's* view of what each civ can build.
3. **Base costs from BPs** — For each entity/squad BP, call `BP_GetEntityBPCost` / `BP_GetEntityBPBuildTime` to get engine-side base costs (validates JSON data).
4. **Garrison capacity** — Spawn one of each building BP per civ, read `Entity_GetMaxHoldSquadSlots`, destroy. Log to structured output.
5. **Population costs by type** — For each unit BP, read `EBP_PopulationCost(ebp, player, CT_Personnel)`, `CT_Vehicle`, `CT_Medic`.

**Script:** New SCAR debug module `debug/cba_debug_data_extract.scar` with console commands:
- `Debug_ExtractAllBlueprints()` — Full BP path enumeration
- `Debug_ExtractRaceSquads()` — Per-race squad inventory
- `Debug_ExtractBuildingData()` — Garrison + costs for all buildings
- `Debug_ExtractUnitCosts()` — Pop costs + base costs for all units

### Why It Matters
Stage 2a fills computable gaps cheaply (DPS, health progression, cost normalization). Stage 2b provides ground-truth engine data that JSON files may not capture (garrison slots, pop costs by type, runtime-only BPs). Together they close the majority of the gap inventory.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Health-per-age tables | JSON | `game_data/generated/derived/health-by-age.json` |
| DPS tables | JSON | `game_data/generated/derived/dps-by-unit.json` |
| Normalized tech costs | JSON | `game_data/generated/derived/tech-costs-normalized.json` |
| Weapon modifier tables | JSON | `game_data/generated/derived/weapon-modifiers.json` |
| Production chain map | JSON | `game_data/generated/derived/production-chains.json` |
| DLC completeness report | JSON | `game_data/generated/derived/dlc-completeness.json` |
| BP suffix catalog | JSON | `game_data/generated/derived/bp-suffix-catalog.json` |
| Runtime BP enumeration | JSON (from scarlog parse) | `game_data/extracted/aoe4/data/runtime/all-blueprints.json` |
| Per-race squad inventory | JSON | `game_data/extracted/aoe4/data/runtime/race-squads.json` |
| Building garrison data | JSON | `game_data/extracted/aoe4/data/runtime/building-garrison.json` |
| Unit pop-cost data | JSON | `game_data/extracted/aoe4/data/runtime/unit-pop-costs.json` |

### Dependencies
- Stage 1 (source inventory confirms which files to parse)
- Running game session required for Stage 2b

### Limitations
- DPS calculation assumes unmodified base weapon stats (no civ bonuses, veterancy, upgrades applied)
- Garrison extraction requires spawning entities (test map only, not live match)
- `BP_GetEntityBPCost` returns context-free base cost; player-specific modifiers need a live player
- Runtime enumeration includes ALL loaded mod BPs, not just base game — must filter by namespace
- Tech effect numerics remain text-only (Stage 3 will attempt AI parsing)

### Storage
- `game_data/generated/derived/` — computed offline outputs
- `game_data/extracted/aoe4/data/runtime/` — extracted from live game session

---

## Stage 3: Normalization

**Objective:** Unify all data into consistent, cross-referenceable schemas. Resolve naming conflicts, merge static + runtime data, standardize units of measurement.

### Data to Retrieve / Transform
1. **Unified unit record schema:**
   ```json
   {
     "id": "string",
     "attribName": "string",
     "displayName": "string",
     "type": "unit|building|technology",
     "civ": "string",
     "age": 1-4,
     "classes": ["string"],
     "unique": true|false,
     "costs": { "food": 0, "wood": 0, "gold": 0, "stone": 0, "popcap": 0, "time": 0.0 },
     "combat": {
       "hp": 0,
       "hpByAge": { "1": 0, "2": 0, "3": 0, "4": 0 },
       "armor": [{ "type": "string", "value": 0 }],
       "weapons": [{
         "name": "string",
         "type": "melee|ranged",
         "damage": 0,
         "dps": 0.0,
         "speed": 0.0,
         "range": { "min": 0, "max": 0 },
         "modifiers": [{ "target": "string", "value": 0 }]
       }],
       "dpsTotal": 0.0
     },
     "movement": { "speed": 0.0 },
     "sight": { "inner": 0, "outer": 0 },
     "garrison": { "capacity": 0 },
     "population": { "personnel": 0, "vehicle": 0, "medic": 0 },
     "producedBy": ["string"],
     "icon": "string"
   }
   ```

2. **Unified technology record schema:**
   ```json
   {
     "id": "string",
     "attribName": "string",
     "displayName": "string",
     "civ": "string",
     "age": 1-4,
     "classes": ["string"],
     "unique": true|false,
     "costs": { "food": 0, "wood": 0, "gold": 0, "stone": 0, "time": 0.0 },
     "appliesTo": ["string"],
     "effects": ["string"],
     "effectsParsed": [{ "stat": "string", "delta": 0, "type": "flat|percent" }]
   }
   ```

3. **Civ normalization table:**
   ```json
   {
     "id": "string",
     "displayName": "string",
     "attribName": "string",
     "suffix": "string",
     "expansion": "base|sultans-ascend|dynasties-of-the-east|knights-of-cross-and-rose",
     "parent": "string|null",
     "isVariant": true|false,
     "unitCount": 0,
     "buildingCount": 0,
     "techCount": 0,
     "uniqueUnitCount": 0,
     "uniqueTechCount": 0
   }
   ```

4. **Name resolution index** — map between: JSON `id`, `attribName`, `displayName`, SCAR `BP_GetName()` output, and `game_data/extracted/blueprints/*.md` constant names. This is the Rosetta Stone for cross-referencing.

5. **Tech effect parsing (AI-assisted)** — For the ~800 tech records with text-only `effects[]`, attempt structured extraction:
   - Pattern-match common forms: "+N damage", "+N% speed", "+N range", "+N armor"
   - Flag ambiguous entries for manual review
   - Store in `effectsParsed[]` alongside original text

### Why It Matters
Every downstream stage (validation, comparison, AI references) depends on uniform schemas. Without normalization, queries like "compare all Age 3 cavalry across civs" require ad-hoc joins across 3+ data formats.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Normalized units | JSON | `game_data/extracted/aoe4/data/normalized/units.json` |
| Normalized buildings | JSON | `game_data/extracted/aoe4/data/normalized/buildings.json` |
| Normalized technologies | JSON | `game_data/extracted/aoe4/data/normalized/technologies.json` |
| Normalized civs | JSON | `game_data/extracted/aoe4/data/normalized/civs.json` |
| Name resolution index | JSON | `game_data/extracted/aoe4/data/normalized/name-index.json` |
| Tech effect parse results | JSON | `game_data/extracted/aoe4/data/normalized/tech-effects-parsed.json` |
| Parse confidence report | Markdown | `research/investigations/workspace_history/tech-effects-confidence.md` |

### Dependencies
- Stage 2a outputs (health-by-age, DPS, normalized tech costs, weapon modifiers)
- Stage 2b outputs (garrison, pop costs) — optional enrichment; schema has nullable fields

### Limitations
- Tech effect parsing will have ~60-70% confidence on first pass; remainder needs manual review or external data
- JSON `id` ↔ SCAR `attribName` mapping may have edge cases for renamed/aliased blueprints
- DLC variant normalization depends on AGS_CIV_PARENT_MAP accuracy
- No abilities data to normalize (not in source files)

### Storage
- `game_data/extracted/aoe4/data/normalized/` — all normalized outputs

---

## Stage 4: Relationship Mapping

**Objective:** Build queryable graph structures capturing how game objects relate: production chains, tech trees, civ inheritance, unit role classifications, and upgrade dependencies.

### Data to Retrieve / Build
1. **Production graph** — Directed graph: `building → produces → [units, technologies]`
   - Source: normalized units `producedBy[]` (inverted), tech `appliesTo[]`
   - Per-civ variant (some civs have unique production buildings)

2. **Tech dependency tree** — `tech → requires → [age, building, prerequisite_tech]`
   - Age requirement: from `age` field
   - Building requirement: from production chain (which building researches this)
   - Prerequisite tech: inferred from age sequencing + `appliesTo` overlap (same unit line with lower-age tech = probable prereq)
   - **Note:** True prerequisite data is NOT in JSON; this produces a best-effort approximation

3. **Civ inheritance graph** — `variant_civ → parent_civ → shared/overridden entries`
   - Source: AGS_CIV_PARENT_MAP + DLC completeness report
   - Per-table: which entity/siege/upgrade keys are inherited vs. overridden

4. **Unit role classification** — Categorize every unit by tactical role:
   - Source: `classes[]` tags + combat stats
   - Categories: `melee_infantry, ranged_infantry, light_cavalry, heavy_cavalry, siege, naval, religious, economic, hero, support`
   - Assign primary/secondary roles based on class tags + weapon types

5. **Age progression map** — For each unit line (baseId), track stat changes across ages:
   - HP scaling curve, damage scaling curve, armor changes
   - Source: normalized data grouped by baseId

6. **Building → capability matrix** — What each building unlocks:
   - Units producible
   - Technologies researchable
   - Per-civ differences

### Why It Matters
Relationship data enables: "What does this civ lack?" "How does this DLC variant differ from its parent?" "What's the fastest path to Age 3 knights?" — the analytical queries that raw flat data can't answer.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Production graph | JSON (adjacency list) | `game_data/extracted/aoe4/data/graphs/production-graph.json` |
| Tech dependency tree | JSON (tree structure) | `game_data/extracted/aoe4/data/graphs/tech-dependencies.json` |
| Civ inheritance graph | JSON | `game_data/extracted/aoe4/data/graphs/civ-inheritance.json` |
| Unit role classification | JSON | `game_data/extracted/aoe4/data/graphs/unit-roles.json` |
| Age progression map | JSON | `game_data/extracted/aoe4/data/graphs/age-progression.json` |
| Building capability matrix | JSON | `game_data/extracted/aoe4/data/graphs/building-capabilities.json` |

### Dependencies
- Stage 3 normalized data (all 6 files)
- Stage 2a production chain map

### Limitations
- Tech prerequisites are **inferred**, not ground-truth — accuracy ~70-80% for linear upgrade chains, lower for branching trees
- Unit roles derived from class tags may misclassify edge cases (e.g., mounted archers = ranged_infantry or light_cavalry?)
- Building capability matrix doesn't capture conditional unlocks (e.g., dynasty buildings, landmark effects)
- Civ inheritance only covers Onslaught's AGS tables; engine-level inheritance may differ

### Storage
- `game_data/extracted/aoe4/data/graphs/` — all relationship data

---

## Stage 5: Validation

**Objective:** Cross-reference static data against runtime ground truth. Detect stale entries, missing blueprints, schema drift, and data inconsistencies.

### Validation Checks
1. **Blueprint existence (JSON ↔ Runtime):**
   - For every attribName in normalized units/buildings, verify `EBP_Exists()` / `SBP_Exists()` at runtime
   - Flag entries that exist in JSON but not in engine (removed/renamed BPs)
   - Flag entries that exist in engine but not in JSON (new BPs from patches)
   - Compare against Stage 2b full BP enumeration

2. **Cost consistency (JSON ↔ Runtime):**
   - Compare `BP_GetEntityBPCost` runtime output against JSON costs
   - Delta threshold: flag any discrepancy > 5% or > 10 resource units
   - This catches JSON data that's stale relative to balance patches

3. **AGS table ↔ Normalized data cross-check:**
   - For every `(civ, key)` in `AGS_ENTITY_TABLE`, verify the attribName exists in normalized units/buildings
   - For every `(civ, key)` in `CBA_SIEGE_TABLE`, verify against normalized buildings or unit_roles where role=siege
   - For every `(civ, key)` in `AGS_UPGRADE_TABLE`, verify against normalized technologies

4. **CivOverview audit integration:**
   - Run `Debug_CivOverview_DumpStructured(true)` and compare matrix against Stage 4 civ inheritance graph
   - Ensure no regression: current scarlog shows `issues=0` — maintain this

5. **DLC parent coverage validation:**
   - For every key in parent civ's entity table, verify DLC variant either: has own entry, or parent entry is valid for variant
   - Cross-reference against DLC completeness report from Stage 2a

6. **Class tag consistency:**
   - Verify units with `military` class have weapons
   - Verify units with `siege` class are in CBA_SIEGE_TABLE
   - Verify buildings with production classes (`barracks`, `stable`, etc.) appear in production graph

### Why It Matters
Static data drifts with patches. The Onslaught mod relies on hundreds of blueprint strings that must match the engine exactly. Validation catches breaks before they manifest as runtime errors.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Validation report | JSON + Markdown | `game_data/extracted/aoe4/data/validation/validation-report.json`, `research/investigations/workspace_history/validation-report.md` |
| BP existence delta | JSON | `game_data/extracted/aoe4/data/validation/bp-existence-delta.json` |
| Cost drift report | JSON | `game_data/extracted/aoe4/data/validation/cost-drift.json` |
| AGS coverage report | JSON | `game_data/extracted/aoe4/data/validation/ags-coverage.json` |
| Class consistency report | JSON | `game_data/extracted/aoe4/data/validation/class-consistency.json` |

### Dependencies
- Stage 3 normalized data
- Stage 2b runtime data (for existence + cost checks)
- Stage 4 graphs (for cross-reference checks)
- Running game session for runtime validation

### Limitations
- Runtime checks require a game session with all mods loaded
- Cost drift detection can't distinguish intentional mod overrides from data staleness
- Some validation checks are only meaningful for Onslaught's specific table structure

### Storage
- `game_data/extracted/aoe4/data/validation/` — machine-readable reports
- `research/investigations/workspace_history/validation-report.md` — human-readable summary

---

## Stage 6: Comparison

**Objective:** Generate civ-vs-civ, DLC-vs-parent, and cross-category comparison datasets that expose balance relationships, unique strengths, and coverage gaps.

### Comparisons to Build
1. **Civ unit roster comparison:**
   - Matrix: `civ × unit_role → [unit_names]`
   - Highlights: which civs lack a role category, which have unique units per role
   - Source: Stage 4 unit role classification + Stage 3 normalized units

2. **DLC variant delta report:**
   - For each of the 6 DLC variants: what's added, removed, or changed vs parent
   - Entity key overrides, unique units/buildings, missing parent entries
   - Source: Stage 4 civ inheritance + Stage 5 DLC validation

3. **Combat power index per age:**
   - For each civ × age, compute: total available DPS, average unit HP, cost-efficiency (DPS/total_resource_cost)
   - Normalize relative to cross-civ average
   - Source: Stage 3 normalized data + Stage 2a DPS tables

4. **Tech tree breadth comparison:**
   - Civs ranked by: total unique techs, techs per age, coverage of upgrade categories (military, economy, defense)
   - Source: Stage 3 normalized technologies

5. **Building availability matrix:**
   - `civ × standard_building_type → available|disabled|unique_variant`
   - Highlights civs missing standard buildings (e.g., Mongol walls, Japanese arsenals)
   - Source: Stage 3 normalized buildings + entity table disabled entries (value=false)

6. **Cost-curve analysis:**
   - Per civ: average unit cost by age, most/least expensive units relative to cross-civ average
   - Source: Stage 3 normalized units

### Why It Matters
Comparisons are the primary value for mod debugging ("why does this civ feel weaker?"), balance assessment, and generating AI-readable summaries that answer natural-language questions about civ differences.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Unit roster comparison matrix | JSON | `game_data/extracted/aoe4/data/comparisons/unit-roster-matrix.json` |
| DLC delta reports (×6) | JSON | `game_data/extracted/aoe4/data/comparisons/dlc-deltas.json` |
| Combat power index | JSON | `game_data/extracted/aoe4/data/comparisons/combat-power-index.json` |
| Tech breadth comparison | JSON | `game_data/extracted/aoe4/data/comparisons/tech-breadth.json` |
| Building availability matrix | JSON | `game_data/extracted/aoe4/data/comparisons/building-availability.json` |
| Cost-curve analysis | JSON | `game_data/extracted/aoe4/data/comparisons/cost-curves.json` |
| Comparison summary | Markdown | `research/investigations/workspace_history/civ-comparison-summary.md` |

### Dependencies
- Stages 3, 4, 5 (all normalized + relationship + validation data)

### Limitations
- Combat power index is theoretical (no terrain, micro, or composition effects)
- DLC delta accuracy depends on parent mapping completeness
- Cost-curve analysis doesn't account for production time (time cost normalization is approximate)

### Storage
- `game_data/extracted/aoe4/data/comparisons/` — machine-readable comparison data
- `research/investigations/workspace_history/civ-comparison-summary.md` — narrative comparison reference

---

## Stage 7: AI-Ready References

**Objective:** Package all processed data into formats optimized for AI agent consumption: compressed context, natural-language summaries, and structured query-ready indexes.

### Outputs to Generate
1. **Civ profile cards (×22+6):**
   - One markdown file per civ: roster, unique units, strengths/weaknesses, building availability, tech highlights, DLC delta (if variant)
   - Designed for single-file context loading when answering "tell me about X civ" queries
   - Source: all Stage 3-6 outputs

2. **Blueprint Rosetta Stone:**
   - Single JSON file mapping between ALL naming systems: JSON id ↔ attribName ↔ BP_GetName ↔ display name ↔ SCAR constant ↔ civ
   - Every entity, squad, and upgrade BP in one cross-reference
   - Primary aid for: "what's the SCAR name for the English Man-at-Arms?" type queries

3. **Queryable unit database:**
   - Single JSON file: all units with full normalized schema, indexed by attribName
   - Supports programmatic filtering: filter by civ, age, role, cost range, DPS range
   - Size target: <2MB for practical AI context loading

4. **Civ diff summaries (natural language):**
   - For each DLC variant pair: "Lancaster differs from English in: [list]. Lancaster gains: [list]. Lancaster loses: [list]."
   - For each base civ pair frequently compared: E.g., "French vs English: [key differences]"

5. **Dependency quick-reference:**
   - "To get X unit, you need: [building] + [age] + [optional tech]"
   - Per-civ production path reference

6. **Known issues & limitations log:**
   - Aggregated list of all data gaps, confidence levels, and recommended manual verification points
   - Source: Stage 5 validation + Stage 3 parse confidence

### Why It Matters
Raw data is not AI-friendly. A 2MB JSON file is usable but not optimal. Civ profile cards let the agent load one file (~5KB) for targeted questions. The Rosetta Stone eliminates the #1 friction point in SCAR modding: name confusion across systems.

### Outputs
| Output | Format | Location |
|--------|--------|----------|
| Civ profile cards (×28) | Markdown | `references/civs/{civ}.md` |
| Blueprint Rosetta Stone | JSON | `docs/api_reference/indexes/blueprint-rosetta.json` |
| Queryable unit database | JSON | `game_data/extracted/aoe4/data/normalized/units-queryable.json` |
| Civ diff summaries | Markdown | `references/civs/comparisons/` |
| Dependency quick-reference | Markdown | `docs/game_systems/gameplay/production-paths.md` |
| Known issues log | Markdown | `research/investigations/workspace_history/data-known-issues.md` |
| Master data index | Markdown | `research/investigations/workspace_history/CIV_DATA_INDEX.md` |

### Dependencies
- All previous stages (1-6)

### Limitations
- Civ profile cards require periodic regeneration after balance patches
- Natural-language summaries are AI-generated and should be reviewed for accuracy
- Queryable database may exceed practical context window for very large queries (all units × all fields)

### Storage
- `references/civs/` — per-civ AI-ready references
- `docs/api_reference/indexes/blueprint-rosetta.json` — cross-system name mapping
- `research/investigations/workspace_history/CIV_DATA_INDEX.md` — master navigation index for all generated data

---

## Execution Order & Dependency Graph

```
Stage 1: Source Discovery
    ↓
Stage 2a: Offline Extraction ──────┐
Stage 2b: Runtime Extraction ──────┤ (parallel, independent)
    ↓                              ↓
Stage 3: Normalization (merges 2a + 2b)
    ↓
Stage 4: Relationship Mapping
    ↓
Stage 5: Validation (needs runtime for some checks)
    ↓
Stage 6: Comparison
    ↓
Stage 7: AI-Ready References
```

### Parallelism Notes
- **2a and 2b** can run in parallel (offline scripts vs. game session extraction)
- **Stage 3** blocks on 2a; enriched by 2b (nullable fields if 2b unavailable)
- **Stage 5** runtime checks can run alongside Stage 4 if game session is available
- **Stages 6 and 7** are strictly sequential (comparison before summarization)

---

## New Files to Create

### Scripts
| File | Purpose | Stage |
|------|---------|-------|
| `scripts/extract_civ_data.ps1` | Offline JSON processing: HP-by-age, DPS, cost normalization, production chains, DLC completeness | 2a |
| `scripts/normalize_civ_data.ps1` | Schema unification: merge sources into canonical records, name resolution | 3 |
| `scripts/generate_civ_comparisons.ps1` | Build comparison matrices and summaries | 6 |
| `scripts/generate_civ_profiles.ps1` | Generate per-civ markdown profile cards | 7 |

### SCAR Debug Modules
| File | Purpose | Stage |
|------|---------|-------|
| `Gamemodes/Onslaught/assets/scar/debug/cba_debug_data_extract.scar` | Runtime BP enumeration, cost extraction, garrison data | 2b |

### Data Directories (new)
| Directory | Purpose |
|-----------|---------|
| `game_data/generated/derived/` | Computed offline outputs (DPS, HP-by-age, etc.) |
| `game_data/extracted/aoe4/data/runtime/` | Extracted from live game session |
| `game_data/extracted/aoe4/data/normalized/` | Unified schema records |
| `game_data/extracted/aoe4/data/graphs/` | Relationship graph structures |
| `game_data/extracted/aoe4/data/comparisons/` | Cross-civ comparison datasets |
| `game_data/extracted/aoe4/data/validation/` | Validation reports |

### Reference Directories (new)
| Directory | Purpose |
|-----------|---------|
| `references/civs/` | Per-civ AI-ready profile cards |
| `references/civs/comparisons/` | Natural-language civ diff summaries |

---

## Open Questions & Items Requiring AI Interpretation

| Item | Stage | Approach |
|------|-------|----------|
| Tech effect numerics ("+1 range", "+20% damage") | 3 | Regex pattern matching + AI fallback for ambiguous entries |
| True tech prerequisites (not in JSON) | 4 | Infer from age gates + production chain + `appliesTo` overlap; flag confidence |
| Ability data (active abilities not in schema) | 2 | Not extractable from current sources; may require attrib file parsing or external wiki data |
| Conditional building unlocks (dynasty, landmark) | 4 | Document as limitation; partial info from class tags |
| Balance patch drift detection | 5 | Runtime cost comparison flags drift; root cause requires external patch notes |
| Weapon bonus damage targets | 3 | modifiers[] exists but target strings may need mapping to unit classes |
| Civ bonuses (passive effects) | 3 | Only narrative text in civ JSON overview[]; requires AI parsing |

---

## Summary

| Stage | New Outputs | Primary Tool | Runtime Needed |
|-------|-------------|-------------|----------------|
| 1. Source Discovery | 2 files | PowerShell file scan | No |
| 2a. Offline Extraction | 7 JSON files | `extract_civ_data.ps1` | No |
| 2b. Runtime Extraction | 4 JSON files | `cba_debug_data_extract.scar` | Yes |
| 3. Normalization | 7 files | `normalize_civ_data.ps1` | No |
| 4. Relationship Mapping | 6 graph files | PowerShell/manual | No |
| 5. Validation | 5 reports | SCAR runtime + PowerShell | Yes |
| 6. Comparison | 7 files | `generate_civ_comparisons.ps1` | No |
| 7. AI-Ready References | 7+ files (28 civ cards) | `generate_civ_profiles.ps1` | No |
| **Total** | **~45 new artifacts** | | **2 stages need game** |
