# Stage 1-3 API Reference

**Checkpoint:** 2026-02-25  
**Purpose:** Quick reference for all functions added in Stages 1-3

---

## 🎯 Helper Functions (Stage 2)

### IsCivFamily(player_id, family)

**Purpose:** Check if player's resolved civ belongs to a civ family  
**DLC-Safe:** Yes (includes all DLC variants)  
**Returns:** boolean

```lua
if IsCivFamily(player.id, "english") then
  -- True for english, lancaster
end

if IsCivFamily(player.id, "chinese") then
  -- True for chinese, chinese_ha_01
end
```

**When to use:**
- Shared behavior across a family (walls, siege, upgrades)
- Civ-neutral checks (any french is allowed)

---

### IsCivExact(player_id, civ_name)

**Purpose:** Check exact raceName (variant-specific)  
**DLC-Safe:** No (only matches exact variant)  
**Returns:** boolean

```lua
if IsCivExact(player.id, "abbasid_ha_01") then
  -- True only for Ayyubids, not base Abbasid
end

if IsCivExact(player.id, "french_ha_01") then
  -- True only for French Ha variant
end
```

**When to use:**
- Variant-specific effects (unique units, special upgrades)
- Blueprint overrides (Ayyubids use different SBPs)

---

### IsCivFamilyAny(player_id, families)

**Purpose:** Check if resolved civ matches any family in list  
**DLC-Safe:** Yes  
**Returns:** boolean

```lua
if IsCivFamilyAny(player.id, {"chinese", "mongol", "byzantine"}) then
  -- True if any of those families
end
```

**When to use:**
- Multi-family checks (exclude specific families)
- Roster checks (which civs get this behavior)

---

## 🎯 Restriction Functions (Stage 2-3)

### ApplyLandmarkRestrictions(player_id, restriction_table, item_state)

**Purpose:** Apply a list of landmark restrictions from data table  
**Parameters:**
- `player_id` — player to restrict
- `restriction_table` — LANDMARK_KEEP_RESTRICTIONS, LANDMARK_AGE4_RESTRICTIONS, etc.
- `item_state` — ITEM_LOCKED, ITEM_REMOVED, ITEM_DEFAULT

```lua
-- In Mission_SetRestrictions:
if AI_Difficulty <= 1 then
  ApplyLandmarkRestrictions(player.id, LANDMARK_KEEP_RESTRICTIONS, ITEM_REMOVED)
end
```

---

### ApplyHouseOfWisdomRestrictions(player_id, item_state)

**Purpose:** Apply House of Wisdom Age 4 upgrade restrictions  
**Parameters:**
- `player_id` — player to restrict
- `item_state` — ITEM_LOCKED, ITEM_REMOVED, ITEM_DEFAULT

```lua
-- In Mission_SetRestrictions:
ApplyHouseOfWisdomRestrictions(player.id, ITEM_LOCKED)
```

---

### ApplyRestrictionProfile(player_id, profile_name)

**Purpose:** Apply a named restriction profile (Stage 4 target)  
**Profiles:**
- `"starting"` — All restrictions at game start
- `"siege_unlocked"` — Post-objective siege available
- `"engineers_unlocked"` — Hard+ engineers available
- `"workshop_unlocked"` — Hardest only, workshop available

```lua
-- Stage 4 will use:
ApplyRestrictionProfile(player.id, "engineers_unlocked")
```

**Status:** Placeholder in Stage 3; full implementation in Stage 4

---

## 🎯 Validator Functions (Stage 2-3)

### Validator_PlayerCivDump()

**Purpose:** Log all players' resolved civs and composition maps  
**Called from:** Mission_SetupVariables (debug only)

```lua
Output example:
[DLC-DUMP] Player 1 | raw: lancaster | resolved: english | melee: start_player_melee_inf | ...
[DLC-DUMP] Player 2 | raw: chinese_ha_01 | resolved: chinese | melee: start_player_melee | ...
```

---

### Validator_RestrictionParity()

**Purpose:** Validate that all locked items have unlocks (except BALANCE_LOCKS)  
**Returns:** `{ ok=true, violations={}, balance_count=N }` or `{ ok=false, violations={...} }`

```lua
local result = Validator_RestrictionParity()
if not result.ok then
  print("⚠️ Parity violations found:", result.violations)
else
  print("✅ All restrictions have unlocks or are balanced")
end
```

---

## 🎯 Testing Functions (Stage 3)

### Simulate_PlayerProgression(civ_name, start_difficulty)

**Purpose:** Test harness — simulate a player's journey through all phases  
**Parameters:**
- `civ_name` — civ to simulate (e.g., "english", "mongol_ha_gol")
- `start_difficulty` — starting AI_Difficulty (1-6)

```lua
Simulate_PlayerProgression("english", 2)  -- English at Hard

-- Output:
-- [PROG-SIM] === Simulating english progression (AI_Difficulty=2) ===
-- [PROG-SIM] Phase 1: Starting restrictions applied
--   - Siege: NO
--   - Engineers: NO
--   - Age4: NO
--   - Workshop: NO
-- [PROG-SIM] Phase 3: Hard+ reached (engineers unlocked)
--   - Engineers: NOW AVAILABLE
--   - Age4: NOW RESTRICTED
-- [PROG-SIM] === End simulation ===
```

---

## 🎯 Resolver Functions (Stage 1)

### ResolveCivKey(raceName, _depth)

**Purpose:** Resolve a DLC civ to its parent key in AGS_ENTITY_TABLE  
**Returns:** Valid raceName key or nil

```lua
local resolved = ResolveCivKey("lancaster")
-- Returns: "english"

local resolved = ResolveCivKey("mongol_ha_gol")
-- Returns: "mongol"
```

**Used internally by:** GetPlayerCiv(), composition map generation

---

### GetPlayerCiv(player_id)

**Purpose:** Resolve and cache a player's civ key  
**Returns:** Valid AGS_ENTITY_TABLE key
**Caches:** Result in DLC_PLAYER_CIV_CACHE per player

```lua
local civ = GetPlayerCiv(player.id)
-- Returns: "english" for player with lancaster
-- Cached for next call (no re-resolution)
```

---

### AGS_GetCivilizationEntity(raceName, shortName)

**Purpose:** Safe wrapper for blueprint lookup with override precedence  
**Returns:** Blueprint entity

```lua
-- Safe lookup with override check:
local bp = AGS_GetCivilizationEntity("abbasid_ha_01", "castle")
-- Checks: DLC_CIV_OVERRIDES["abbasid_ha_01"]["castle"]
-- Falls back: AGS_ENTITY_TABLE["abbasid"]["castle"]
```

---

## 📊 Data Structures

### CIV_CAPABILITIES (Stage 3)

Describes what each civ can do at each phase:

```lua
CIV_CAPABILITIES["english"] = {
  siege = false,        -- Siege units available
  engineers = false,    -- Siege engineers tech available
  age4 = false,         -- Age 4 advancement available
  workshop = false,     -- Siege workshop available
}

-- Updated during progression:
Simulate_PlayerProgression("english", 2)
-- After hard unlock:
-- CIV_CAPABILITIES["english"].engineers = true
-- CIV_CAPABILITIES["english"].age4 = true
```

---

### BALANCE_LOCKS (Stage 3)

Explicit balance decisions (locked but intentional):

```lua
BALANCE_LOCKS = {
  ["siege_workshop"] = "Locked at difficulty >= 5; intentionally hardest unlock",
  ["unit_mangonel_3_buildable_abb_ha_01"] = "Ayyubids field construct; balance lock",
  -- ... 5 more
}
```

**Purpose:** Distinguish bugs (unlock missing) from design (intentional lock)

---

### Restriction_Profile (Stage 3)

Named profiles for each game phase:

```lua
Restriction_Profile = {
  starting = { name = "starting", unlocked = {} },
  siege_unlocked = { name = "siege_unlocked", unlocked = { "siege_squad" } },
  engineers_unlocked = { name = "engineers_unlocked", unlocked = { "siege_squad", "siege_engineers_upg" } },
  workshop_unlocked = { name = "workshop_unlocked", unlocked = { "siege_squad", "siege_engineers_upg", "siege_workshop" } },
}
```

---

## 🔧 Debug Functions

### DebugPrint_Resolver(msg)

**Purpose:** Conditional print (only when DLC_DEBUG=true)  
**Toggle:** Set `DLC_DEBUG = true` in data.scar

```lua
DebugPrint_Resolver("ResolveCivKey: 'lancaster' direct match in AGS_ENTITY_TABLE")
-- Output only if DLC_DEBUG=true
```

---

## 📋 Quick Usage Examples

### Adding a New DLC Civ

```lua
-- In data.scar DLC Registration section:
RegisterDLCCiv({
  attribName = "new_variant_ha_01",
  parent = "base_civ",
  melee_key = "start_player_melee_inf",  -- Optional
  overrides = {                           -- Optional; only different items
    unique_building = "custom_building_blueprint",
  },
})

-- To test:
Simulate_PlayerProgression("new_variant_ha_01", 2)
```

### Adding a Restriction

```lua
-- Add to BALANCE_LOCKS if intentional:
BALANCE_LOCKS["my_item"] = "Reason why permanently locked"

-- Add to appropriate data table if difficulty-gated:
-- LANDMARK_KEEP_RESTRICTIONS, LANDMARK_AGE4_RESTRICTIONS, etc.

-- In Mission_SetRestrictions:
ApplyLandmarkRestrictions(player.id, MY_TABLE, ITEM_LOCKED)
```

### Adding an Unlock

```lua
-- In Phase2_CaptureSiege_OnComplete (or appropriate objective):
if IsCivFamily(player.id, "english") then
  Player_SetEntityProductionAvailability(player.id, bp, ITEM_DEFAULT)
end

-- Then add to MANIFEST for future reference
```

---

## 🚨 Common Mistakes

❌ **Don't:**
```lua
if Player_GetRaceName(player.id) == "english" then
  -- Won't work for lancaster!
end
```

✅ **Do:**
```lua
if IsCivFamily(player.id, "english") then
  -- Works for english + lancaster
end
```

---

❌ **Don't:**
```lua
if IsCivFamily(player.id, "french_ha_01") then
  -- Wrong for variant checking; includes base french!
end
```

✅ **Do:**
```lua
if IsCivExact(player.id, "french_ha_01") then
  -- Only French_ha_01
end
```

---

## 📖 Related Documentation

- [japan-stage1-summary.md](japan-stage1-summary.md) — Resolver architecture
- [japan-stage2-summary.md](japan-stage2-summary.md) — Helpers + audit
- [japan-stage3-summary.md](japan-stage3-summary.md) — Profiles + validation
- [MOD-INDEX.md](MOD-INDEX.md) — Reference copy (preferred for Copilot)

---

**Last updated:** 2026-02-25  
**API Status:** ✅ Stages 1-3 complete; Stage 4 in progress

