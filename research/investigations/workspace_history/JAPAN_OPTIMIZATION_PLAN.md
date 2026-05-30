# Japan Co-op Data.SCAR Optimization Plan — 50% Reduction

> **Status**: Planning Phase  
> **Target**: 2789 lines → 1395 lines (50.0% reduction, ~1394 lines to save)  
> **Reference**: Arabia mod optimization (1591 → 795 lines, proven patterns)  
> **Estimated Phase Budget**: 6 implementation phases, 12–15 multi_replace_string_in_file calls

---

## Executive Summary

**Current State:**
- File: `mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_data.scar`
- **Size**: 2,789 lines, ~137 KB
- **Sections**: 1 Stage 1 (constants), 2 Spawn Compositions, 3 landmark restrictions, 4 restriction profiles, 5 DLC resolver, 6 AGS_ENTITY_TABLE (HUGE), 7 CBA_SIEGE_TABLE, 8 CIV maps, 9 Unit_Types, 10 SetupVariables_data, 11 Unit_Path_Data, 12 Difficulty upgrade functions, 13 test functions

**Optimization Approach:**
Apply the same proven patterns from Arabia mod success:
1. **Data-driven generation** for AGS_ENTITY_TABLE (22 civs × 26 entries each = 572+ lines)
2. **Helper function extraction** for duplicate restriction logic
3. **Template + Override** for CBA_SIEGE_TABLE
4. **Auto-generated composition maps** from DLC registration
5. **Compression techniques**: single-line entries, removed blank lines, debug gating
6. **Test function removal** or consolidation

**Expected Savings Breakdown:**
| Phase | Change | Lines Saved | Running Total |
|-------|--------|-------------|---------------|
| 1 | Constants + Spawn_Compositions compaction | 250–300 | 250–300 |
| 2 | AGS_ENTITY_TABLE data-driven generation | **300–400** | 550–700 |
| 3 | Extract restriction profile helpers | 150–200 | 700–900 |
| 4 | CBA_SIEGE_TABLE template generation | 100–150 | 800–1050 |
| 5 | CIV maps auto-generation + SetupVariables | 150–200 | 950–1250 |
| 6 | Test functions + final cleanup | 100–150 | 1050–1400 |
| **Total** | **All phases** | **~1050–1400** | **50.0% target** |

---

## Phase 1: Constants & Spawn_Compositions Compaction (250–300 lines)

### Current State
- Lines 1–252: Constant definitions (BP_SIEGE_*, AGS_BP_*) already well-organized
- Lines 27–1903: Spawn_Compositions table with verbose comments and multi-line entries

### Optimizations

#### 1a. Reduce Spawn_Compositions Comments
- Remove per-spawn "HOW TO EDIT" blocks (90+ lines of guidance text)
- Move to README or wiki documentation instead
- Consolidate section headers from multi-line to single-line format

**Example Before:**
```lua
    -- =========================================================
    -- PHASE 1: VILLAGE DEFENSE (~5–30 min)
    -- =========================================================
    -- Controls: waves_5min_flank, waves_late_extra,
    --           waves_hardest_extra, hard_waves_siege,
    --           hard_waves_infantry
    -- Set in: difficulty.scar → "ATTACK WAVES" section per tier
    -- =========================================================
```

**Example After:**
```lua
    -- PHASE 1: VILLAGE DEFENSE (5–30m) | Controls: waves_5min_flank, waves_late_extra, waves_hardest_extra
```

**Estimated Savings**: 80–120 lines

#### 1b. Compress Spawn_Compositions Entries
- Remove blank lines between flank_early, late_extra_40m, etc.
- Single-line format for simple entries

**Example Before:**
```lua
        flank_early = {
            unit_types_key = "wave_city_5m",
            -- Unit_Types entry: ...
            -- TO EDIT: Search "wave_city_5m" in Unit_Types below
        },

        late_extra_40m = {
```

**Example After:**
```lua
        flank_early = {unit_types_key = "wave_city_5m"},
        late_extra_40m = {
```

**Estimated Savings**: 70–100 lines

#### 1c. Consolidate QUICK_REFERENCE Comments
- Move table to README or reference file
- Keep only a 1-line summary comment per table

**Estimated Savings**: 50–80 lines

**Phase 1 Total Savings**: 200–300 lines ✅

---

## Phase 2: AGS_ENTITY_TABLE Data-Driven Generation (300–400 lines)

### Current State
Lines ~1300–2000: 22 civ entries × 26 blueprint types each = **572+ lines of hand-maintained tables**

**Example:**
```lua
AGS_ENTITY_TABLE = {
    english = {castle = "building_defense_keep_eng", town_center_capital = "...", ...},
    chinese = {castle = "building_defense_keep_chi", town_center_capital = "...", ...},
    ...
}
```

### Problem
- 22 civs share ~80% identical structure
- Only 2–3 overrides per civ (e.g., unique landmarks, dialect-specific buildings)
- Manual maintenance → typo risk, sync issues

### Solution: Template + Override Pattern

#### 2a. Create Shared Blueprint Template
Define base template with all 26 keys, then generate each civ from parent:

```lua
-- Base template shared by all civs (26 keys)
local AGS_TEMPLATE = {
    castle = nil,  -- will be filled by civ-specific override
    town_center_capital = nil,
    town_center = nil,
    market = nil,
    villager = nil,
    -- ... 21 more keys
}

-- Civilization-specific overrides (only keys that differ from default)
-- Most civs will only have castle = civ_code and 2–3 unique entries
local AGS_OVERRIDES = {
    english = {
        castle = "building_defense_keep_eng",
        town_center_capital = "building_town_center_capital_eng",
        -- ... etc (26 entries compressed to single table per civ)
    },
    chinese = {...},
    ...
}

-- Generate AGS_ENTITY_TABLE at runtime
function _GenerateAGSEntityTable()
    for civ, overrides in pairs(AGS_OVERRIDES) do
        AGS_ENTITY_TABLE[civ] = {}
        for key, val in pairs(overrides) do
            AGS_ENTITY_TABLE[civ][key] = val
        end
    end
end
```

#### 2b. Compress Overrides Table
- Use **pattern-based naming** to infer blueprints:
  - `castle` for "english" → `"building_defense_keep_eng"` (auto-append `_eng`)
  - Skip entries that follow the pattern
  - Only list exceptions

**Example Compressed:**
```lua
-- AGS_ENTITY_TABLE overrides (only non-standard entries)
-- All civs follow pattern: key_name → "unit/building_{key}_{civ_code}"
-- Exceptions listed below:
local AGS_OVERRIDES = {
    english = {
        castle = "building_defense_keep_eng",
        crossbow = "unit_crossbowman_3_eng",
        -- auto-inferred: town_center = "building_town_center_eng", etc.
    },
    ...
}
```

**Estimated Savings**: 250–350 lines (by replacing 572-line table with ~100-line override table + 20-line generator)

#### 2c. Validation Helper
Add validator to ensure no keys are missing:

```lua
function Validator_AGSEntityTable()
    print("[DLC] AGS_ENTITY_TABLE validation:")
    for civ, entries in pairs(AGS_ENTITY_TABLE) do
        if type(entries) ~= "table" then
            error("[AGS] Entry for civ '" .. civ .. "' is not a table")
        end
    end
    print("[DLC] All " .. tostring(_CountKeys(AGS_ENTITY_TABLE)) .. " civ entries valid")
end
```

**Phase 2 Total Savings**: 300–400 lines ✅

---

## Phase 3: Extract Restriction Profile Helpers (150–200 lines)

### Current State
Lines ~350–750: 4 restriction profiles (starting, siege_available, engineers_available, workshop_available)

**Problem**: Massive code duplication:
- The `starting` profile body: ~310 lines (7 multi-step restrictions)
- The `siege_available` profile body: ~100 lines (duplicates 80% of starting logic)
- The `engineers_available` profile body: ~80 lines (calls siege_available then adds 20 lines more)

### Solution: Extract Helpers (like Arabia mod)

#### 3a. Extract `_ApplySiegeRestrictions` Helper
All 3 profiles apply siege restrictions; consolidate into helper:

```lua
function _ApplySiegeRestrictions(player, item_state)
    -- Mangonel
    Player_SetSquadProductionAvailability(player.id, AGS_GetSiegeSquad(player.raceName, BP_SIEGE_MANGONEL), item_state)
    -- Mangonel / Field construct (abbasid + mongol family)
    if IsCivFamilyAny(player.id, {"abbasid", "mongol"}) then
        Player_SetEntityProductionAvailability(player.id, AGS_GetSiegeEntity(player.raceName, BP_SIEGE_MANGONEL_BUILDABLE), item_state)
    end
    -- ... 15+ more unit/squad checks
end
```

**Estimated Savings**: 100–130 lines (consolidate 3 copies into 1 function, call with ITEM_LOCKED or ITEM_DEFAULT)

#### 3b. Extract `_ApplyEngineerRestrictions` Helper
Similar to siege, engineer restrictions repeated in 2 profiles:

```lua
function _ApplyEngineerRestrictions(player, item_state)
    -- Siege Engineers upgrade
    if not IsCivFamily(player.id, "sultanate") then
        Player_SetUpgradeAvailability(player.id, BP_GetUpgradeBlueprint("upgrade_siege_engineers"), item_state)
    else
        Player_SetUpgradeAvailability(player.id, BP_GetUpgradeBlueprint("upgrade_siege_engineers_sul"), item_state)
    end
    -- ... 10+ more conditionals
end
```

**Estimated Savings**: 50–70 lines

#### 3c. Refactor Profile Bodies
Profiles now call helpers instead of copy-pasting:

```lua
Restriction_Profile = {
    starting = {
        description = "...",
        apply = function(player)
            -- [1] Walls
            if not IsCivFamily(player.id, "mongol") then
                ... (30 lines)
            end
            -- [7] Siege Restriction: call helper
            if DC.restrict_siege then
                _ApplySiegeRestrictions(player, ITEM_LOCKED)
            end
            -- [8] Engineers
            if DC.restrict_engineers then
                _ApplyEngineerRestrictions(player, ITEM_LOCKED)
            end
            -- ... (50 more lines of specific logic)
        end
    },
    siege_available = {
        description = "...",
        apply = function(player)
            -- Just call helpers with ITEM_DEFAULT
            _ApplySiegeRestrictions(player, ITEM_DEFAULT)
            ... etc
        end
    },
}
```

**Estimated Savings**: 50–100 lines

**Phase 3 Total Savings**: 200–300 lines (conservative estimate: 150–200) ✅

---

## Phase 4: CBA_SIEGE_TABLE Template Generation (100–150 lines)

### Current State
Lines ~1900–2200: CBA_SIEGE_TABLE with 16 civ entries, each with 6–14 keys

**Problem**: Similar to AGS_ENTITY_TABLE, but for siege units:
```lua
CBA_SIEGE_TABLE = {
    english = {
        ram = "unit_ram_3_eng",
        workshop_ram = "unit_workshop_ram_3_eng",
        springald = "unit_springald_3_eng",
        ...
    },
    chinese = {
        -- mostly same keys, different values
    },
    ...
}
```

### Solution: Template + Civ Variants

Use same pattern as Arabia's _BuildSiegeTable():

```lua
-- Siege unit template (common to most civs)
local SIEGE_TEMPLATE = {
    ram = "unit_ram_3_{civ}",
    workshop_ram = "unit_workshop_ram_3_{civ}",
    springald = "unit_springald_3_{civ}",
    mangonel = "unit_mangonel_3_{civ}",
    -- ... 10 more keys
}

-- Siege-specific overrides per civ (only keys that differ from template pattern)
local SIEGE_OVERRIDES = {
    chinese = {
        nest_of_bees = "unit_nest_of_bees_4_chi",
        nestofbees_clocktower_chi = "unit_nest_of_bees_4_clocktower_chi",
        -- ... 6 more overrides specific to Chinese
    },
    french = {
        royal_cannon = "unit_cannon_4_royal_fre",
        royal_culverin = "unit_culverin_4_royal_fre",
        royal_ribauldequin = "unit_ribauldequin_4_royal_fre",
    },
    -- ... 3 more civs with overrides
}

-- Generate CBA_SIEGE_TABLE
function _BuildSiegeTable()
    local civs = {"english", "chinese", "french", "hre", "rus", "abbasid", "mongol", "sultanate", "malian", "ottoman", "japanese", "byzantine", "abbasid_ha_01", "chinese_ha_01", "french_ha_01", "hre_ha_01"}
    for _, civ in ipairs(civs) do
        CBA_SIEGE_TABLE[civ] = {}
        for key, pattern in pairs(SIEGE_TEMPLATE) do
            CBA_SIEGE_TABLE[civ][key] = string.gsub(pattern, "{civ}", civ)
        end
        -- Apply overrides
        if SIEGE_OVERRIDES[civ] then
            for key, val in pairs(SIEGE_OVERRIDES[civ]) do
                CBA_SIEGE_TABLE[civ][key] = val
            end
        end
    end
    print("[SIEGE] CBA_SIEGE_TABLE generated for " .. tostring(#civs) .. " civs")
end
```

**Estimated Savings**: 150–200 lines (compress ~300-line table to ~50-line template + 80-line overrides + 30-line generator)

**Phase 4 Total Savings**: 100–150 lines ✅

---

## Phase 5: CIV Maps Auto-Generation & SetupVariables Compression (150–200 lines)

### Current State
Lines ~2200–2350: Manually-maintained CIV_MELEE_MAP, CIV_RANGED_MAP, REINFORCE_MELEE_MAP, REINFORCE_RANGED_MAP
Lines ~2350–2600: SetupVariables_data() with lots of repetitive SGroup creation

### 5a. Auto-Generate CIV Maps from DLC_CIV_COMPOSITION

**Problem**: Maps are manually kept in sync with DLC registrations.

**Solution**: Generate at runtime like Arabia does with GenerateCompositionMaps():

```lua
-- Compress maps to data-driven format
function _GenerateCIVMaps()
    -- Maps store civ → Unit_Types key
    -- Generated from DLC_CIV_COMPOSITION data
    CIV_MELEE_MAP = {}
    CIV_RANGED_MAP = {}
    REINFORCE_MELEE_MAP = {}
    REINFORCE_RANGED_MAP = {}
    
    for civ, comp_data in pairs(DLC_CIV_COMPOSITION) do
        if comp_data.melee_key then
            CIV_MELEE_MAP[civ] = comp_data.melee_key
        end
        if comp_data.ranged_key then
            CIV_RANGED_MAP[civ] = comp_data.ranged_key
        end
        -- ... etc
    end
end
```

**Estimated Savings**: 40–60 lines (remove ~140-line manual maps, replace with ~20-line generator)

### 5b. Compress SetupVariables_data()

**Problem**: ~250 lines of repetitive SGroup creation.

**Solution**: Use batch helpers more aggressively:

```lua
function SetupVariables_data()
    AI_Difficulty = GetAIDifficulty(player6)
    Difficulty_Init()
    
    -- Batch SGroup creation
    sg_player_team = SGroup_CreateIfNotFound("sg_player_team")
    sg_garrison = SGroup_CreateIfNotFound("sg_garrison")
    
    -- Phase 1 groups (4 players × 6 groups each = 24 groups)
    for i = 1, 4 do
        _SGroupBatch("sg_player" .. i .. "_", {"start", "scout", "reinforcements", "unique", "villagers", "reinforcements_cp"})
    end
    
    -- ... (condense similarly)
end

-- Batch helper for varied names
local function _SGroupBatchList(prefix, suffixes)
    for _, suffix in ipairs(suffixes) do
        _G[prefix .. suffix] = SGroup_CreateIfNotFound(prefix .. suffix)
    end
end
```

**Estimated Savings**: 60–80 lines (compress ~120 lines of creation calls to ~30 lines of batched calls)

**Phase 5 Total Savings**: 100–140 lines ✅

---

## Phase 6: Test Functions & Final Cleanup (100–150 lines)

### Current State
Lines ~2800–2948: Test functions (Test_SpawnDLCGroup, Test_AllDLCCivs, Test_ListDLCCivs, Difficulty_Upgrades_Phase1-4)

### 6a. Remove Test Functions (for Production)
- Move Test_SpawnDLCGroup, Test_AllDLCCivs, Test_ListDLCCivs to debug file or disable with `if DLC_DEBUG then` wrapper
- These are for validation only, not needed in production

**Estimated Savings**: 60–80 lines

### 6b. Compress Difficulty_Upgrades Functions
- Consolidate repeated `if DC.ai_upgrade_tier == "..."` blocks
- Use table-driven approach instead of if-chains

**Example Before:**
```lua
function Difficulty_Upgrades_Phase1()
    if DC.ai_upgrade_tier == "ridiculous" then 
        Player_CompleteUpgrade(player6, UPG.COMMON.UPGRADE_UNIT_ARCHER_3)
        Player_CompleteUpgrade(player6, UPG.COMMON.UPGRADE_MELEE_ARMOR_I)
        -- ... 10 more upgrades
    elseif DC.ai_upgrade_tier == "outrageous_plus" then 
        Player_CompleteUpgrade(player6, UPG.CHINESE.UPGRADE_UNIT_REPEATER_CROSSBOW_3_CHI)
        -- ... 12 more upgrades
    else
        Player_CompleteUpgrade(player6, UPG.COMMON.UPGRADE_UNIT_SPEARMAN_2)
        -- ...
    end
end
```

**Example After** (table-driven):
```lua
local UPGRADE_TIERS = {
    ridiculous = {
        {player = 6, upgrade = UPG.COMMON.UPGRADE_UNIT_ARCHER_3},
        {player = 6, upgrade = UPG.COMMON.UPGRADE_MELEE_ARMOR_I},
        -- ... compressed list
    },
    outrageous_plus = {...},
}

function Difficulty_Upgrades_Phase1()
    local upgrades = UPGRADE_TIERS[DC.ai_upgrade_tier] or UPGRADE_TIERS["default"]
    for _, entry in ipairs(upgrades) do
        Player_CompleteUpgrade(entry.player, entry.upgrade)
    end
    Rule_AddOneShot(Difficulty_Upgrades_Phase2, 600)
end
```

**Estimated Savings**: 40–70 lines

### 6c. General Cleanup
- Remove surplus blank lines between sections
- Compress remaining verbose comments

**Estimated Savings**: 20–30 lines

**Phase 6 Total Savings**: 120–180 lines ✅

---

## Summary: Projected Savings

| Phase | Description | Lines Saved | Running Total |
|-------|-------------|-------------|---------------|
| **1** | Spawn_Compositions & constants compaction | 200–300 | 200–300 |
| **2** | AGS_ENTITY_TABLE data-driven (MAJOR) | 300–400 | 500–700 |
| **3** | Restriction profile helper extraction | 150–200 | 650–900 |
| **4** | CBA_SIEGE_TABLE template generation | 100–150 | 750–1050 |
| **5** | CIV maps auto-generation + SetupVariables | 100–140 | 850–1190 |
| **6** | Test functions + Difficulty_Upgrades cleanup | 120–180 | 970–1370 |
| **Total** | **All phases combined** | **~1050–1370** | **~50% achieved** |

---

## Risks & Mitigation

| Risk | Mitigation |
|------|-----------|
| Breaking data-driven generation | Test all 22 civs in mission log before commit |
| Lost functionality in helpers | Comprehensive grep verify all exports present |
| Player confusion (fewer detailed comments) | Move to reference docs (MOD-INDEX.md) |
| Unit/SGroup name typos in batch creation | Use consistent naming pattern, validate with grep |

---

## Parallel Reference: Arabia Precedent

**Arabia mod results** (proven safe):\
✅ 1591 → 795 lines (50.0% reduction)\
✅ All exports verified present\
✅ Game mission log proof (validators PASS)\
✅ No functional regressions

**Techniques reused for Japan:**
1. ✅ Template + Override (AGS_ENTITY_TABLE & CBA_SIEGE_TABLE)
2. ✅ Extracted helpers (_ApplySiegeRestrictions, _ApplyEngineerRestrictions)
3. ✅ Data-driven map generation (CIV_MELEE_MAP, CIV_RANGED_MAP)
4. ✅ Batch SGroup creation
5. ✅ Removed excess comments, consolidated sections

---

## Next Steps

1. **Review this plan** — Verify phases align with user intent
2. **Confirm implementation approach** — Data-driven generation preferred?
3. **Set backup timestamp** — `cp coop_4_japanese_data.scar coop_4_japanese_data.scar.bak`
4. **Execute phases 1–6** in sequence with validation checks
5. **Game test** — Verify mission initialization, all validators pass
6. **Update MOD-INDEX.md** — Reflect new 50% reduction in reference

---

## Attachments

- **MOD-INDEX reference**: `docs/game_systems/mods/MOD-INDEX.md` (section: Japan scenario)
- **Arabia precedent**: `docs/game_systems/mods/arabia-mod-index.md` (section: optimization patterns)
- **Codebase patterns**: `.github/copilot-instructions.md` (section: SCAR/Lua standards, file-split architecture)
