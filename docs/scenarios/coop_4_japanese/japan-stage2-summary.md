# Japan Scenario DLC Civ Support - Stage 2 Summary

Date: 2026-02-25
Scope: Stage 2 (Registry consolidation, data-driven restrictions, debug harness, documentation)

## What Changed

### 1. Registry Consolidation (Family Helpers)
- Added `IsCivFamily(player_id, family)` — resolved civ matches a base family (DLC-safe).
- Added `IsCivExact(player_id, civ_name)` — raw raceName matches exactly (variant-specific).
- Added `IsCivFamilyAny(player_id, families)` — resolved civ matches any in a list.
- Replaced ~30 ad-hoc `resolved_civ ==` / `player_civ ==` checks in main.scar and objectives.scar.

### 2. Data-Driven Landmark Restrictions
- `LANDMARK_KEEP_RESTRICTIONS` — 9 entries: keeps locked at Intermediate.
- `LANDMARK_AGE4_RESTRICTIONS` — 16 entries: Age 4 landmarks locked at Hard+.
- `HOUSE_OF_WISDOM_AGE4_RESTRICTIONS` — 2 entries (abbasid, abbasid_ha_01) with upgrade lists.
- `ApplyLandmarkRestrictions(player_id, table, state)` — apply from data table.
- `ApplyHouseOfWisdomRestrictions(player_id, state)` — apply HoW upgrades from data table.
- `_ResolveGlobalPath(path)` — safely walk "EBP.CIV.BUILDING_FOO" strings at runtime.
- Replaced two large if-chains in `Mission_SetRestrictions` with data-driven calls.

### 3. Debug & Test Harness
- `DLC_DEBUG` flag (default `false`) — enables verbose print output.
- `DebugPrint_Resolver(msg)` — conditional `[DLC-DBG]` print.
- `Validator_PlayerCivDump()` — logs all human players' raw civ, resolved civ, and composition map entries. Hooked into `Mission_SetupVariables`.
- `ResolveCivKey` instrumented with debug logging at each resolution step.
- `RegisterDLCCiv` instrumented with registration confirmation logging.

### 4. DLC Override Documentation
- Expanded `RegisterDLCCiv()` docstring with override precedence rules.
- Documented when to use overrides vs relying on parent inheritance.

## Key Files Touched
- `scar/coop_4_japanese_data.scar` — helpers, data tables, debug harness, registration docs
- `coop_4_japanese.scar` — restriction calls converted to data-driven, helper usage, DynastyUI fix
- `scar/coop_4_japanese_objectives.scar` — helper usage in siege unlock logic, mangonel buildable parity fix
- `scar/coop_4_japanese_spawns.scar` — village reinforcement civ checks converted to helpers

## DLC Civ Coverage (unchanged from Stage 1)
- mongol_ha_gol → mongol
- byzantine_ha_mac → byzantine
- japanese_ha_sen → japanese
- sultanate_ha_tug → sultanate
- lancaster → english
- templar → hre

---

# DLC Civ Resolver — Architecture Guide

## Overview

The DLC Civ Resolution System allows DLC civilizations (variants) to automatically
inherit blueprints, composition maps, and behavior from a base ("parent") civ
without duplicating the entire AGS_ENTITY_TABLE. It provides:

1. **Parent inheritance** — DLC civs resolve to a base civ for blueprint lookup.
2. **Sparse overrides** — only blueprints that differ from the parent need entries.
3. **Composition inheritance** — starting army and reinforcement roles inherit or override per role.
4. **Family helpers** — simple API for civ checks that work for base AND DLC civs.
5. **Debug harness** — toggle verbose logging with one flag.

## Resolution Flow (ResolveCivKey)

```
Player_GetRaceName(player_id)
  → lowercased raw civ (e.g. "lancaster")
  → ResolveCivKey(raw_civ)
      1. Is raw_civ a key in AGS_ENTITY_TABLE?
         YES → return raw_civ (direct match, e.g. "english")
         NO  → continue
      2. Is raw_civ in DLC_CIV_PARENT_MAP?
         YES → recurse: ResolveCivKey(parent, depth+1)
         NO  → return nil (unresolvable → error)
      3. Depth guard: DLC_RESOLVE_MAX_DEPTH (4) prevents infinite loops.
  → resolved civ key (e.g. "english")
  → cached in DLC_PLAYER_CIV_CACHE[player_id]
```

Once resolved, `GetPlayerCiv(player_id)` returns the cached key on future calls.

## Blueprint Lookup Precedence (AGS_GetCivilizationEntity)

When looking up a blueprint shortName (e.g. "castle") for a player:

```
1. DLC_CIV_OVERRIDES[raw_civ][shortName]
   → variant-specific blueprint (highest priority)
2. AGS_ENTITY_TABLE[resolved_civ][shortName]
   → parent/base civ blueprint (normal path)
3. Error — key missing entirely
```

Most DLC civs have zero overrides and go straight to step 2.

## Composition Map Generation

`GenerateCompositionMaps()` runs after all data tables are defined. For each registered
DLC civ, it populates these maps by checking the DLC spec first, then falling back to
the parent's entry:

| Map | Purpose |
|-----|---------|
| `CIV_MELEE_MAP` | Starting melee army Unit_Types key |
| `CIV_RANGED_MAP` | Starting ranged army Unit_Types key |
| `UNIQUE_UNIT_MELEE` | Unique melee unit entry |
| `UNIQUE_UNIT_RANGED` | Unique ranged unit entry |
| `REINFORCE_MELEE_MAP` | Reinforcement melee Unit_Types key |
| `REINFORCE_RANGED_MAP` | Reinforcement ranged Unit_Types key |

Runtime lookups use `ResolveCivMapKey(map, raw_civ, default_key)` which walks the
parent chain if the exact civ isn't in the map.

## Helper Functions Quick Reference

| Function | Checks | Use When |
|----------|--------|----------|
| `IsCivFamily(player_id, "english")` | Resolved civ == family | Shared behavior (walls, siege, upgrades) |
| `IsCivExact(player_id, "french_ha_01")` | Raw raceName == exact | Variant-specific (unique landmarks, DLC-only blueprints) |
| `IsCivFamilyAny(player_id, {"chinese","mongol"})` | Resolved civ in list | Multi-family checks |
| `GetPlayerCiv(player_id)` | Resolved + cached | Direct access to resolved key |
| `GetPlayerRawCiv(player_id)` | Lowercased raw | When you need the original DLC raceName |

## How to Add a New DLC Civ

### Step 1: Register

Add a `RegisterDLCCiv()` call in the "DLC Civ Registrations" section of data.scar:

```lua
RegisterDLCCiv({
    attribName = "english_ha_02",    -- raceName from Player_GetRaceName
    parent     = "english",           -- base civ key in AGS_ENTITY_TABLE
    -- Optional: only if this variant has DIFFERENT blueprints
    overrides  = {
        castle = "building_defense_keep_custom_eng_ha_02",
    },
    -- Optional: composition role overrides (nil = inherit from parent)
    melee_key  = "start_player_melee_inf",
})
```

### Step 2: Verify

1. Set `DLC_DEBUG = true` in data.scar.
2. Launch the scenario with the new DLC civ selected.
3. Check the warnings log for:
   - `[DLC-DBG] RegisterDLCCiv: 'english_ha_02' -> parent 'english'`
   - `[DLC-DBG] ResolveCivKey: 'english_ha_02' -> parent 'english' (depth 0)`
   - `[DLC-DUMP]` output from `Validator_PlayerCivDump` showing all resolved values.
4. Confirm blueprints load correctly in-game.
5. Set `DLC_DEBUG = false` before shipping.

### Step 3: Add Restrictions (if needed)

If the DLC variant has unique landmarks, add entries to the appropriate data table
(`LANDMARK_KEEP_RESTRICTIONS`, `LANDMARK_AGE4_RESTRICTIONS`, or
`HOUSE_OF_WISDOM_AGE4_RESTRICTIONS`). Use the exact `attribName` as the `civ` field.

### What NOT to Do

- **Don't** duplicate the full parent's AGS_ENTITY_TABLE into overrides.
- **Don't** add raw `player_civ ==` checks — use `IsCivFamily` or `IsCivExact`.
- **Don't** edit `DLC_CIV_PARENT_MAP` directly — use `RegisterDLCCiv`.
- **Don't** create circular parent chains (depth guard will catch it, but still).

## Data Table Reference

| Table | Location | Count | Purpose |
|-------|----------|-------|---------|
| `AGS_ENTITY_TABLE` | data.scar ~L594 | ~20 civs | Blueprint shortName → attribName |
| `DLC_CIV_PARENT_MAP` | generated by RegisterDLCCiv | 6 entries | DLC raceName → parent |
| `DLC_CIV_OVERRIDES` | generated by RegisterDLCCiv | sparse | Variant-specific blueprint overrides |
| `DLC_CIV_COMPOSITION` | generated by RegisterDLCCiv | 6 entries | Per-role composition specs |
| `LANDMARK_KEEP_RESTRICTIONS` | data.scar ~L32 | 9 entries | Keep landmarks locked at Intermediate |
| `LANDMARK_AGE4_RESTRICTIONS` | data.scar ~L44 | 16 entries | Age 4 landmarks locked at Hard+ |
| `HOUSE_OF_WISDOM_AGE4_RESTRICTIONS` | data.scar ~L63 | 2 entries | HoW Age 4 upgrades |

## Debug Checklist

- [ ] Set `DLC_DEBUG = true`
- [ ] Launch scenario with target DLC civ
- [ ] Check `[DLC-DBG]` logs for registration and resolution
- [ ] Check `[DLC-DUMP]` logs for player dump (all maps resolved)
- [ ] Verify restrictions apply correctly (landmarks locked/unlocked)
- [ ] Verify siege unlock in Phase 2 objective completion
- [ ] Set `DLC_DEBUG = false` before publishing

---

# Regression Sweep Results (Stage 2)

## Audit 1: Restriction/Unlock Parity

### Intermediate+ (AI_Difficulty >= 1)

| # | Restriction (main.scar) | Unlock (objectives.scar) | Status |
|---|------------------------|--------------------------|--------|
| 1 | Mangonel (all) L170 | L1193 ITEM_DEFAULT | OK |
| 2 | Mangonel Buildable (abbasid+mongol) L173 | **L1194 added** | **FIXED** (was missing) |
| 3 | Nest of Bees (chi+mon+byz) L177 | L1199 | OK |
| 4 | Nest of Bees Clocktower (chinese exact) L180 | L1201 | OK |
| 5 | Ribauldequin (not chinese) L185 | L1207 | OK |
| 6 | Royal Ribauldequin (french) L188 | L1210 | OK |
| 7 | Ram Tower (abbasid_ha_01) L193 | L1215 | OK |
| 8 | Mongol Double (mongol) L203 | L1225 | OK |
| 9 | Byzantine Outpost Mangonel L208 | L1230 | OK |

### Hard+ (AI_Difficulty >= 2)

| # | Restriction | Unlock | Status |
|---|------------|--------|--------|
| 10 | Siege Engineers (not sultanate) L217 | L1239 | OK |
| 11 | Siege Engineers Sul (sultanate) L219 | L1241 | OK |
| 12 | Improved Siege Engineers Mon L223 | L1246 | NOTE: ITEM_REMOVED → ITEM_DEFAULT (asymmetric, likely intentional) |
| 13 | Abbasid buildables L228-229 | L1250-1251 | OK |
| 14 | Ayyubids buildables L233-235 | L1255-1257 | OK |

### Hardest+ (AI_Difficulty >= 5/6)

| # | Restriction | Unlock | Status |
|---|------------|--------|--------|
| 15 | Workshop (all) >=5 L242 | ==6 L1264 | NOTE: Locked at >=5, unlocked only at ==6. Difficulty 5 perma-locks workshops. Verify this is intended. |

## Audit 2: Remaining Hardcoded Civ Checks

| Location | Code | Status |
|----------|------|--------|
| main.scar L244-266 | `player_civ == "english"` etc. | Commented-out block (`--[[ ]]`), dead code — no action needed |
| main.scar L625 | `Player_GetRaceName == "chinese"` in DynastyUI_unlocked | **FIXED** → `IsCivFamily(player.id, "chinese")` |
| spawns.scar L312+ | `player1_civ == "malian"` (×4 players) | **FIXED** → `IsCivFamily` |
| spawns.scar L328+ | `player2_civ == "chinese"` (×2 players) | **FIXED** → `IsCivFamily` |
| spawns.scar L319+ | `player1_civ == "french_ha_01"` (×4 players) | **FIXED** → `IsCivExact` (variant-specific SBP) |

## Audit 3: Spawn_Village_South_Players

All 12 hardcoded civ checks converted:
- `"malian"` → `IsCivFamily` (shared behavior, future DLC-safe)
- `"chinese"` → `IsCivFamily` (covers chinese_ha_01)
- `"french_ha_01"` → `IsCivExact` (uses FRENCH_HA_01-specific villager SBP)
- Removed 4 unused `local playerN_civ` variables

## Audit 4: DynastyUI_unlocked

- Converted `Player_GetRaceName(player.id) == "chinese"` → `IsCivFamily(player.id, "chinese")`
- This means chinese_ha_01 players will also get dynasty unlocks
- Note: If chinese_ha_01 uses different dynasty upgrade BP names, this may need IsCivExact + separate handling

## Items Flagged for Future Review

1. **Workshop parity (difficulty 5 vs 6)**: Workshops locked at >=5 but only unlocked at ==6. If intentional, add a comment explaining the design.
2. **Mongol improved siege engineers**: Uses ITEM_REMOVED (restriction) vs ITEM_DEFAULT (unlock). Asymmetric but functional — ITEM_DEFAULT restores after ITEM_REMOVED.
3. **DynastyUI chinese_ha_01 compatibility**: Verify that `player_dynasty1_chi`/`player_dynasty2_chi` upgrades and `dynasty_N_was_completed_chi` state models work for chinese_ha_01.

