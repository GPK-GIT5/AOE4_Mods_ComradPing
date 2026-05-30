# AoE4 World Data Index

Last Updated: 2026-02-23

> Cross-reference guide for parsed AoE4 game data: units, buildings, technologies, and civilizations in JSON format.

---

## Overview

This directory contains parsed Age of Empires IV game data extracted from the official game files and structured as JSON. The data source is **AoE4 World** (https://data.aoe4world.com/), which provides machine-readable information about all in-game entities.

**Key Features:**
- Complete unit, building, and technology statistics
- Per-civilization variants with unique attributes
- SCAR-compatible field mappings for scripting integration
- Aggregate files for fast cross-civilization lookups
- Blueprint identifiers (pbgid) for direct game engine references

**Use Cases:**
- Campaign/scenario scripting (MissionOMatic blueprint validation)
- AI composition recipes (baseId-based unit substitutions)
- Spawn system configuration (pbgid lookups for exact variants)
- Data-driven objective tracking (attribName mapping from blueprints)

---

## Data Folders

| Folder | Files | Purpose |
|--------|-------|---------|
| [data/units/](../../game_data/extracted/aoe4/data/units/) | 1,266 | Unit statistics by civilization (per-civ JSON + unified + optimized variants) |
| [data/buildings/](../../game_data/extracted/aoe4/data/buildings/) | 861 | Building statistics by civilization (per-civ JSON + unified + optimized variants) |
| [data/technologies/](../../game_data/extracted/aoe4/data/technologies/) | 2,207 | Technology/upgrade data by civilization (per-civ JSON + unified + optimized variants) |
| [data/civilizations/](../../game_data/extracted/aoe4/data/civilizations/) | 23 | Civilization metadata (ID, name, abbreviation, expansion, attribName) |

**File Naming Convention:**
- `{civ}.json` — Full data for a specific civilization (e.g., `abbasid.json`)
- `{civ}-unified.json` — Base entities + civilization variants nested as `variations[]`
- `{civ}-optimized.json` — Minimal data structure for fast lookups
- `all.json` — Aggregated data across all civilizations (largest files: 117K lines for units, 49K for buildings)
- `all-unified.json` — Aggregated unified format with variations
- `all-optimized.json` — Aggregated optimized format
- `all-baseids.json` — (Buildings only) Base ID cross-reference for variant mapping

---

## Field Mapping: SCAR ↔ AoE4 JSON

When working with SCAR scripts, you'll encounter blueprint references (SBP/EBP/UBP strings). Use this mapping to locate the corresponding JSON data:

| SCAR Blueprint Field | AoE4 JSON Field | Description | Example |
|---------------------|-----------------|-------------|---------|
| Blueprint Name | `attribName` | Internal game identifier for the blueprint | `"unit_archer_2_abb"` |
| Blueprint ID | `pbgid` | Unique integer ID for the exact variant (PBG = PropertyBlueprintGroup) | `199706` |
| Object ID | `id` | Human-readable identifier (may include age suffix) | `"archer-2"` |
| Base Type | `baseId` | Base entity type (shared across variants) | `"archer"` |
| Display Name | `name` | In-game display name | `"Archer"` |
| Type | `type` | Entity category | `"unit"`, `"building"`, `"technology"` |
| Civilization(s) | `civs[]` | Civilization abbreviations | `["ab", "ch", "en"]` |
| Classes | `classes[]` | Gameplay tags (targeting, AI behavior, upgrades) | `["infantry", "ranged", "military"]` |
| Age | `age` | Minimum age requirement (2-4) | `2` |

**Lookup Priority:**
1. **Exact Match:** Use `pbgid` when you have a SCAR blueprint ID (fastest, most precise)
2. **Blueprint Name:** Use `attribName` when matching SCAR blueprint strings (e.g., from objectives)
3. **Base Type:** Use `baseId` for class-based substitutions (AI composition, unit variety)
4. **Object ID:** Use `id` for human-readable references (documentation, debugging)

---

## Lookup Recipes by SCAR Area

### Objectives

**Problem:** Campaign objectives reference blueprints as strings (e.g., `"sbp_path_to_unit"`). How do I find the unit stats?

**Solution:**
1. Extract the blueprint string from the objective (e.g., `Obj_Create(..., "sbp.path.to.archer", ...)`)
2. Convert to attribName format: Replace `.` with `_`, strip `sbp`/`ebp` prefix → `unit_archer_2_abb`
3. Search `game_data/extracted/aoe4/data/units/all.json` or `game_data/extracted/aoe4/data/buildings/all.json` for `"attribName": "unit_archer_2_abb"`
4. Cross-check with `game_data/extracted/aoe4/data/civilizations/` to validate civilization compatibility

**Example:**
```scar
-- Objective requires building 3 archery ranges
Obj_Create(OBJ_ARCHERY, "ebp.building.archery_range.abb")
```

**Lookup Steps:**
```bash
# 1. Blueprint string: ebp.building.archery_range.abb
# 2. Convert to attribName: building_unit_ranged_control_abb
# 3. Search buildings/all.json:
"attribName": "building_unit_ranged_control_abb"
# 4. Result: Abbasid Archery Range (pbgid: 199645, baseId: "archery-range")
```

---

### Spawns

**Problem:** Wave spawner needs to spawn units by blueprint ID. How do I map composition arrays to exact variants?

**Solution:**
1. **Direct Spawn:** Use `pbgid` from JSON for exact variant (age/civ-specific)
2. **Dynamic Age:** Use `baseId` + age filter to select age-appropriate variant
3. **Wave Composition:** Mix `attribName` for named blueprints + `baseId` for randomization

**Example:**
```scar
-- Spawn 10 Age 2 Abbasid Archers
UnitEntry_Deploy(player, SBP.unit_archer_2_abb, ...)  -- attribName lookup
-- OR using pbgid:
UnitEntry_DeployByID(player, 199706, ...)  -- Direct pbgid reference
```

**Age-Variant Lookup:**
```json
// Find all archer variants for Abbasid (ab) across ages 2-4
// In abbasid.json, search for baseId: "archer"
{
  "id": "archer-2",
  "baseId": "archer",
  "pbgid": 199706,
  "age": 2,
  "attribName": "unit_archer_2_abb"
},
{
  "id": "archer-3",
  "baseId": "archer",
  "pbgid": 199707,
  "age": 3,
  "attribName": "unit_archer_3_abb"
}
```

**Wave Randomization:**
Use `baseId` for class-based substitutions:
```lua
-- Substitute any light infantry (baseId filter)
local lightInfantry = {"archer", "spearman", "javelin-thrower"}
for _, baseId in ipairs(lightInfantry) do
  -- Look up civilization-specific variant by baseId + civs filter
end
```

---

### AI

**Problem:** AI needs to substitute unit types dynamically (e.g., replace archers with crossbowmen). How do I find equivalent units?

**Solution:**
1. Use `baseId` for direct variant swaps (same unit, different age/civ)
2. Use `classes[]` for role-based substitutions (e.g., all ranged infantry)
3. Cross-reference `displayClasses[]` for similar unit roles

**Example: Unit Class Substitution**
```scar
-- Find all "ranged infantry" units for Chinese civilization
-- Search units/chinese.json for classes containing "ranged_infantry"
```

**Result:**
```json
[
  {
    "id": "archer-2",
    "baseId": "archer",
    "classes": ["ranged_infantry", "infantry", "military"],
    "civs": ["ch"]
  },
  {
    "id": "zhuge-nu-2",
    "baseId": "zhuge-nu",
    "classes": ["ranged_infantry", "infantry", "military"],
    "civs": ["ch"],
    "unique": true
  }
]
```

**Base Type Substitution:**
Use `baseId` for age-independent swaps:
```lua
-- Replace all "archer" units with "crossbowman" units at age 3+
-- Search for baseId: "crossbowman", filter age >= 3
```

---

### MissionOMatic

**Problem:** MissionOMatic modules reference blueprints in config strings. How do I validate they exist for a civilization?

**Solution:**
1. Extract blueprint `attribName` from module configuration
2. Search civilization-specific JSON file (e.g., `game_data/extracted/aoe4/data/units/abbasid.json`)
3. Validate `civs[]` array includes target civilization abbreviation
4. Cross-reference with `game_data/extracted/aoe4/data/civilizations/civs-index.json` for attribName mappings

**Example: TownLife Module Validation**
```lua
-- Module config: "unit_villager_male_abb"
-- 1. Load civilizations/abbasid.json
-- 2. Search for "attribName": "unit_villager_male_abb"
-- 3. Confirm civs contains "ab"
```

**Civilization Abbreviations:**
See [data/civilizations/civs-index.json](../../game_data/extracted/aoe4/data/civilizations/civs-index.json):
```json
{
  "ab": "abbasid_dynasty",
  "ay": "ayyubids",
  "by": "byzantines",
  "ch": "chinese",
  "de": "delhi_sultanate",
  ...
}
```

**Multi-Civilization Validation:**
For shared blueprints (e.g., common units across civs), check `civs[]` array:
```json
{
  "id": "archer",
  "attribName": "unit_archer_2_abb",
  "civs": ["ab", "ay", "by", "ch", "de", "fr", "gol", "hr"]
}
```

---

## Aggregate Files

For performance-critical lookups or cross-civilization analysis, use aggregate files:

| File | Size | Use Case |
|------|------|----------|
| [units/all.json](../../game_data/extracted/aoe4/data/units/all.json) | 117K lines | Full unit data, all civilizations |
| [units/all-unified.json](../../game_data/extracted/aoe4/data/units/all-unified.json) | 124K lines | Base units + `variations[]` nested structure (recommended for most lookups) |
| [buildings/all.json](../../game_data/extracted/aoe4/data/buildings/all.json) | 49K lines | Full building data, all civilizations |
| [buildings/all-baseids.json](../../game_data/extracted/aoe4/data/buildings/all-baseids.json) | Varies | Base ID cross-reference for building variants |
| [technologies/all.json](../../game_data/extracted/aoe4/data/technologies/all.json) | 96K lines | Full technology data, all civilizations |

**Performance Tips:**
- **Single Civilization:** Use per-civ files (e.g., `abbasid.json`) for faster parsing
- **Cross-Civ Comparison:** Use `all-unified.json` to compare base stats + variations
- **Blueprint Lookup:** Use `all.json` with `attribName` search for direct SCAR mapping
- **Base Type Filtering:** Use `all-unified.json` to group by `baseId`

**Unified Format Example:**
```json
{
  "id": "archer",
  "baseId": "archer",
  "name": "Archer",
  "civs": ["ab", "ch", "en", ...],
  "variations": [
    {
      "id": "archer-2",
      "pbgid": 199706,
      "attribName": "unit_archer_2_abb",
      "age": 2,
      "civs": ["ab"]
    },
    {
      "id": "archer-2",
      "pbgid": 123456,
      "attribName": "unit_archer_2_chi",
      "age": 2,
      "civs": ["ch"]
    }
  ]
}
```

---

## Update/Maintenance Checklist

Update this index when:

- [ ] **Game Patch Released** — Re-download data from https://data.aoe4world.com/
- [ ] **New Civilization Added** — Add entry to civilizations/ folder, verify attribName mappings
- [ ] **SCAR Blueprint Changes** — Update field mapping table if blueprint structure changes
- [ ] **New Data File Type** — Add new folder to "Data Folders" section (e.g., `data/abilities/`)
- [ ] **Aggregate File Changes** — Update "Aggregate Files" section if new aggregates are added
- [ ] **Lookup Recipe Gaps** — Add new examples to "Lookup Recipes" if common use cases are missing

**Data Source Updates:**
1. Visit https://data.aoe4world.com/ for latest data version
2. Check `__version__` field in JSON files for current version (currently `0.0.2`)
3. Review `__note__` field for update instructions: _"This file is autogenerated, do not edit it manually."_

**Validation Steps:**
1. Verify all `pbgid` values are unique per civilization
2. Confirm `attribName` values match SCAR blueprint naming conventions
3. Cross-check `baseId` mappings across age variants
4. Test civilization abbreviations against `civs-index.json`

**Related Documentation:**
- [data-index.md](data-index.md) — General data file descriptions
- [blueprints/](blueprints/) — Per-civilization blueprint references (14 files)
- [systems/missionomatic-modules.md](systems/missionomatic-modules.md) — MissionOMatic module configuration patterns

---

**Last Updated:** February 24, 2026  
**Data Version:** 0.0.2  
**Source:** https://data.aoe4world.com/
