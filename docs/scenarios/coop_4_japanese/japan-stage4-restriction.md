    # Stage 4 Restriction Audit & Refactoring Plan

**Date:** 2026-02-25  
**Status:** Pre-Implementation (Ready for Stage 4)  
**Scope:** Unify 22 scattered difficulty-based restriction checks into 4 unified restriction profiles

---

## Conversation Summary

### Progression to Date

**Stages 1–3: COMPLETE ✅**

- **Stage 1:** DLC resolver foundation + parent map composition (lancaster→english, templar→hre, 6 DLC civs registered)
- **Stage 2:** Registry consolidation + data-driven restrictions (ApplyLandmarkRestrictions, ApplyHouseOfWisdomRestrictions, 13 hardcoded checks converted)
- **Stage 3:** Restriction profiles + validators + progression harness (BALANCE_LOCKS, Validator_RestrictionParity, Simulate_PlayerProgression, ApplyRestrictionProfile stubs)

**Validation:** All console tests passed (Stage 1-3). Mission executed cleanly with no SCAR errors. 4-player co-op completed successfully with correct player DLC resolution and composition map inheritance.

---

## Stage 4 Audit: Restriction Points

### Overview

- **Total Restriction Methods:** 22 distinct logic blocks
- **Files Involved:** 2 (coop_4_japanese.scar: 16 points, coop_4_japanese_objectives.scar: 6 points)
- **Current Pattern:** Scattered `if AI_Difficulty >= N` checks with inline `Player_SetEntityProductionAvailability()` calls
- **Target Pattern:** Unified `ApplyRestrictionProfile(player, profile_name)` calls

---

## Restriction Points by Profile

### Profile: `starting` (Initial state, applied to all players)

| ID | File | Lines | Description | Current Pattern | Scope |
|----|------|-------|-------------|-----------------|-------|
| 1.1 | main.scar | 108–110 | Disable stone/palisade walls | Always applied | non-mongol |
| 1.2 | main.scar | 113 | Disable docks | Always applied | all |
| 1.3 | main.scar | 118 | Starting upgrades | Always applied | all |
| 2.5 | main.scar | 150–152 | Apply Keep landmark restrictions | `if AI_Difficulty <= 1` → LANDMARK_KEEP_RESTRICTIONS | data-driven |

**Summary:** Static locks (walls, docks) + data-driven landmark table based on early-difficulty state.

---

### Profile: `siege_unlocked` (Intermediate difficulty tier, triggered by objective)

| ID | File | Lines | Description | Current Pattern | Scope |
|----|------|-------|-------------|-----------------|-------|
| 3.1 | main.scar | 158–166 | Lock mangonel, nestofbees, ribauldequin, ram tower | `if AI_Difficulty >= 1` → multiple `Player_SetSquadProductionAvailability()` | family-specific |
| 3.2 | main.scar | 180–184 | Lock mongol double units + engineers | `if AI_Difficulty >= 1` + IsCivFamily | mongol only |
| 3.3 | main.scar | 186–188 | Lock byzantine outpost mangonel | `if AI_Difficulty >= 1` + IsCivFamily | byzantine only |
| 5.1 | objectives.scar | 1193–1231 | Unlock siege units (Phase2_CaptureSiege_OnComplete) | Objective trigger → ITEM_DEFAULT | inverse of 3.1-3.3 |

**Summary:** Siege units start locked (intermediate+), unlocked when Phase 2 objective completes. Faction-specific variants (mongol, byzantine, abbasid, chinese, french).

---

### Profile: `engineers_unlocked` (Hard difficulty tier, tied to objective)

| ID | File | Lines | Description | Current Pattern | Scope |
|----|------|-------|-------------|-----------------|-------|
| 2.2 | main.scar | 132–139 | Disable monk conversion | `if AI_Difficulty >= 2` | all (special: abbasid) |
| 4.1 | main.scar | 193–210 | Lock/unlock siege engineers + field constructs | `if AI_Difficulty >= 2` → Phase2_CaptureSiege_OnComplete | family-specific |
| 4.3 | main.scar | 227–234 | Restrict players max age to Castle | `if AI_Difficulty >= 2` | all (player1-4) |
| 4.4 | main.scar | 237–240 | Apply Age 4 landmark + HoW restrictions | `if AI_Difficulty >= 2` → data-driven tables | data-driven |
| 5.2 | objectives.scar | 1240–1265 | Unlock siege engineers + field constructs | Objective trigger → ITEM_DEFAULT | family-specific |

**Summary:** Engineers locked at Hard+. Max age capped to Castle. Age 4 landmarks/upgrades restricted. All unlocked by objective completion.

---

### Profile: `workshop_unlocked` (Hardest difficulty only)

| ID | File | Lines | Description | Current Pattern | Scope |
|----|------|-------|-------------|-----------------|-------|
| 4.2 | main.scar | 213–220 | Unlock siege workshop | `if AI_Difficulty >= 5` → ITEM_DEFAULT | all |

**Summary:** Workshop available only on Hardest (AI_Difficulty == 6 → difficulty >= 5). Unlocked by objective trigger.

---

## Risk Assessment

| Risk | Severity | Mitigation |
|------|----------|-----------|
| **State Tracking Bugs** | HIGH | Implement `PLAYER_RESTRICTION_STATE` cache per player; validate on each profile application |
| **Balance Lock Violations** | HIGH | Validate against BALANCE_LOCKS whitelist in Validator_RestrictionState(); fail if violation detected |
| **Objective Trigger Timing** | MEDIUM | Ensure Phase2_CaptureSiege_OnComplete correctly calls ApplyRestrictionProfile() for both engineers + workshop phases |
| **Civ-Family Mismatches** | MEDIUM | Use IsCivFamily() consistently; catch variants (lancaster→english, templar→hre, mongol_ha_gol→mongol) |
| **Age Cap Enforcement** | LOW | Player_SetMaximumAge() has clear semantics; apply once per player at profile transition |
| **Console Testing Blind Spots** | MEDIUM | Test all 6 difficulty tiers (0–6) + all civ families + objective trigger sequences |

---

## Implementation Sequence

### Step 4.1: Profile Implementation (data.scar)
Expand `Restriction_Profile` with actual callback logic:
```lua
Restriction_Profile = {
    starting = {
        apply = function(player) 
            -- Disable walls, docks, apply keep landmarks
        end
    },
    siege_unlocked = {
        apply = function(player)
            -- Unlock siege units (inverse of locks)
        end
    },
    -- ... etc
}
```

### Step 4.2: Player State Tracking (data.scar)
```lua
PLAYER_RESTRICTION_STATE = {}
function GetPlayerProfile(player_id) return PLAYER_RESTRICTION_STATE[player_id] or "starting" end
function SetPlayerProfile(player_id, profile) PLAYER_RESTRICTION_STATE[player_id] = profile end
```

### Step 4.3: Replace Main.scar Checks
Replace 16 scattered `if AI_Difficulty >= N` blocks with structured `ApplyRestrictionProfile()` calls at mission setup + objective callbacks.

### Step 4.4: Replace Objectives.scar Callbacks
Phase2_CaptureSiege_OnComplete: Replace 40+ lines of unlock logic with:
```lua
function Phase2_CaptureSiege_OnComplete()
    for _, player in pairs(PLAYERS) do
        if AI_Difficulty >= 2 then
            ApplyRestrictionProfile(player, "engineers_unlocked")
        else
            ApplyRestrictionProfile(player, "siege_unlocked")
        end
        if AI_Difficulty >= 5 then
            ApplyRestrictionProfile(player, "workshop_unlocked")
        end
    end
end
```

### Step 4.5: Validation & Console Tests
```lua
print("[TEST-S4a] profile_initialized: " .. (_CountKeys(PLAYER_RESTRICTION_STATE) > 0 and "PASS" or "FAIL"))
print("[TEST-S4b] validator_state: " .. (Validator_RestrictionState() and "PASS" or "FAIL"))
print("[TEST-S4c] balance_locks_honored: " .. (Validator_RestrictionParity().ok and "PASS" or "FAIL"))
```

---

## Success Criteria

✅ All 22 hardcoded checks replaced with `ApplyRestrictionProfile()` calls  
✅ `Validator_RestrictionState()` returns PASS for all 6 difficulty tiers  
✅ 4-player co-op completes without new errors  
✅ Objective triggers correctly transition profiles  
✅ All 7 balance locks remain enforced  
✅ Civ-family variants behave identically to base families  

---

## Existing Reference Documentation

**Checkpoint Files (Stages 1–3):**
- `docs/scenarios/coop_4_japanese/japan-checkpoint-stage3.md` — Detailed rollback guide + verification steps
- `docs/scenarios/coop_4_japanese/CHECKPOINT-STAGE3-HASHES.json` — SHA256 checksums for integrity
- `docs/scenarios/coop_4_japanese/japan-checkpoint-stage3-manifest.md` — Line-by-line file breakdown
- `docs/scenarios/coop_4_japanese/japan-guide-api-reference.md` — Function quick reference

**Configuration:**
- `.github/copilot-instructions.md` — Console-only mode rules + mandatory constraints (80 lines)

**Data Files (Audit):**
- `mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_data.scar` (2,341 lines)
  - LANDMARK_KEEP_RESTRICTIONS, LANDMARK_AGE4_RESTRICTIONS, HOUSE_OF_WISDOM_AGE4_RESTRICTIONS
  - ApplyLandmarkRestrictions(), ApplyHouseOfWisdomRestrictions()
  - BALANCE_LOCKS (7 items)
  - Validator_RestrictionParity(), Validator_CivRegistry()
  - CIV_CAPABILITIES model (stubs only, not yet populated)
  - Restriction_Profile table (definitions only, apply logic not implemented)

---

## Console Testing Commands (Stage 4)

**Pre-Implementation Baseline:**
```
DLC_DEBUG = true
print("[TEST-S4-baseline] Current profile state: " .. _CountKeys(PLAYER_RESTRICTION_STATE) .. " players tracked")
Validator_RestrictionParity()
Validator_CivRegistry()
```

**Post-Implementation Validation:**
```
Simulate_PlayerProgression("english", 1)  -- Easy: siege_unlocked
Simulate_PlayerProgression("english", 6)  -- Hardest: all profiles
print(Validator_RestrictionState() and "PASS" or "FAIL")
```

---

## Estimated Effort

| Task | Time | Notes |
|------|------|-------|
| Profile implementation (4.1) | 30 min | Straightforward; follow existing data-driven pattern |
| State tracking (4.2) | 15 min | Simple table + 2 utility functions |
| Main.scar refactoring (4.3) | 60 min | Replace 16 blocks (mostly line-for-line) |
| Objectives.scar refactoring (4.4) | 45 min | Replace 2 large callback blocks |
| Validation + testing (4.5) | 30 min | Console tests + 1 full play-through |
| **Total** | **~180 min (~3 hrs)** | Can complete in 4–5 focused user iterations |

---

## Key Decisions (Documented)

1. **Single entry point:** All restrictions apply through `ApplyRestrictionProfile(player, profile_name)` — eliminates scattered checks ✅
2. **Phase model:** 4 discrete phases (starting, siege_unlocked, engineers_unlocked, workshop_unlocked) map cleanly to difficulty tiers ✅
3. **Per-player state:** Each player tracked independently in `PLAYER_RESTRICTION_STATE` — allows future async unlocks ✅
4. **Balance lock enforcement:** `Validator_RestrictionParity()` whitelist honored during profile applies — fail fast on violations ✅
5. **Backward compatible:** Existing objective logic preserved; only check patterns refactored ✅

---

## Cross-References

- **Stage 1-2 Implementation:** See japan-checkpoint-stage3.md for integration points + file edits
- **DLC Resolver Architecture:** See japan-guide-api-reference.md for AGS_GetCivilizationEntity, IsCivFamily, etc.
- **Console Safety Rules:** See .github/copilot-instructions.md for all AoE4 Console Command Generation constraints
- **Test Session Logs:** 
  - `AoE4_02_25_20h-19m-20s/scarlog.2026-02-25.20-19-20.txt` — Stage 1–3 validation (7 balance locks detected, all profiles tested)
  - `AoE4_02_25_21h-10m-47s/scarlog.2026-02-25.21-10-47.txt` — Full Stage 1–2 console test sequence (22 commands, all PASS)

---

## Notes for Implementation

- Do **NOT** modify existing data tables (LANDMARK_KEEP, LANDMARK_AGE4, HOUSE_OF_WISDOM) — they work correctly and are already data-driven
- Focus on **replacing hardcoded checks** in Mission_SetRestrictions() and objective callbacks
- Ensure `ApplyRestrictionProfile()` is **idempotent** — calling it twice with same profile should not break state
- Validate `PLAYER_RESTRICTION_STATE` after each profile change to catch bugs early
- Keep console-safe testing in mind — all test commands must follow the 6-item validation checklist in copilot-instructions.md

---

**Next Steps:** Proceed to Step 4.1 (Profile Implementation) when ready.

