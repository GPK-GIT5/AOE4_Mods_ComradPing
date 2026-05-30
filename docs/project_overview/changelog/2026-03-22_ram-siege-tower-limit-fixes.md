# Ram/Siege Tower Limit Fixes — 2026-03-22

## Issues Fixed

### 1. **Field-Built Entities Not Counted in Limits** (CRITICAL)
- **Problem**: `CBA_Options_RamLimit_Recount()` and `CBA_Options_SiegeTowerLimit_Recount()` only counted squads (workshop-produced units)
- **Impact**: Field-built rams from Mongol, Abbasid, Byzantine (fire rams), and other faction field-construction were ignored, allowing players to bypass the limit
- **Fix**: Updated both recount functions to iterate `Player_GetEntities()` in addition to `Player_GetSquads()`, counting field-built siege entity types

### 2. **Construction Cancellation Not Always Registered** (CRITICAL)
- **Problem**: `CBA_Options_SiegeLimit_ConstructionCancelled()` only recounted if `Entity_IsEBPOfType(context.pbg, "siege")` matched
- **Impact**: Some field-built entity types (particularly during construction scaffold phase) may not have `"siege"` type, causing cancellation to be silently ignored and counts to drift
- **Fix**: Removed the type guard; now ALWAYS recount all limits when ANY construction is cancelled, regardless of entity type

### 3. **Pending Units Not Counted (Construction Time Gap)**
- **Problem**: Long-construction field-built units (e.g., Mongol trebs) weren't blocked until construction completed; players could queue unlimited while waiting
- **Impact**: Players could queue 3x the ram/siege tower limit by spamming production while slow field-constructions were in progress
- **Fix**: Implemented pending unit tracking:
  - `ConstructionStart`: Increment `player.ramLimit_pending` or `player.siegeTowerLimit_pending`
  - `ConstructionCancelled`: Decrement pending (with bounds checking)
  - `ConstructionComplete`: Decrement pending when construction finishes

### 4. **ApplyThreshold Functions Ignored Pending Counts**
- **Problem**: `CBA_Options_RamLimit_ApplyThreshold()` and `CBA_Options_SiegeTowerLimit_ApplyThreshold()` only checked `count`, not `count + pending`
- **Impact**: Even with pending tracking implemented, pending units weren't factored into lock decisions
- **Fix**: Updated both functions to sum live counts and pending counts before comparing to max:
  ```lua
  local count = (player.ramLimit_count or 0) + (player.ramLimit_pending or 0)
  ```

## Changes Made

### File: `Gamemodes/Onslaught/assets/scar/gameplay/cba_options.scar`

1. **Added event handler registration** (line 51):
   - `Rule_AddGlobalEvent(CBA_Options_SiegeLimit_ConstructionComplete, GE_ConstructionComplete)`

2. **Updated `CBA_Options_SiegeLimit_ConstructionStart()`** (lines 838-869):
   - Always recount (removed `if Entity_IsEBPOfType` guard)
   - Added pending unit tracking on construction start
   - Track ram and siege tower types during construction phase

3. **Updated `CBA_Options_SiegeLimit_ConstructionCancelled()`** (lines 871-895):
   - Always recount (removed `if Entity_IsEBPOfType` guard)
   - Added pending unit decrement on cancellation
   - Bounds-checked to prevent negative values

4. **New handler: `CBA_Options_SiegeLimit_ConstructionComplete()`** (lines 897-922):
   - Decrements pending counts when field-built units complete construction
   - Recounts to capture the newly-completed squad
   - Re-applies thresholds

5. **Updated `CBA_Options_RamLimit_Recount()`** (lines 1347-1378):
   - Added iteration of `Player_GetEntities()` with field-built ram type checks
   - Now counts both workshop squads AND field-constructed entities

6. **Updated `CBA_Options_SiegeTowerLimit_Recount()`** (lines 1380-1407):
   - Added iteration of `Player_GetEntities()` with siege tower type checks
   - Now counts both workshop squads AND field-constructed entities

7. **Updated `CBA_Options_RamLimit_ApplyThreshold()`** (lines 1448-1457):
   - Changed: `local count = player.ramLimit_count or 0`
   - To: `local count = (player.ramLimit_count or 0) + (player.ramLimit_pending or 0)`
   - Comment explains pending represents in-construction scaffolds

8. **Updated `CBA_Options_SiegeTowerLimit_ApplyThreshold()`** (lines 1459-1468):
   - Changed: `local count = player.siegeTowerLimit_count or 0`
   - To: `local count = (player.siegeTowerLimit_count or 0) + (player.siegeTowerLimit_pending or 0)`
   - Comment explains pending represents in-construction scaffolds

## Testing Recommendations

### Scenario 1: Field-Built Rams (Mongol)
- Build 3 Mongol trebs field-constructed
- Verify ram limit locks at threshold (should block after limit)
- Cancel one mid-construction
- Verify new treb can be started (pending count properly decremented)

### Scenario 2: Mixed Production Sources  
- Build workshop rams + field-constructed rams simultaneously
- Verify both types count toward limit
- Should lock when total (workshop + field) reaches max

### Scenario 3: Siege Tower Limits
- Build field-constructed siege towers (if faction supports)
- Verify separate ST limit is enforced
- Try to stack with ram production (should have independent limits)

### Scenario 4: Construction Cancellation
- Queue field-constructed units
- Cancel construction before completion
- Verify locks release immediately and new units can queue

## Root Cause Analysis

The root issue was a **fundamental design mismatch**:
- Ram/ST limits were meant to use a separate tracking system from main siege limits
- But the counting functions were incomplete (squad-only, not entity-aware)
- And the event handlers had defensive type guards that silently skipped non-siege-typed entities during construction

Field-built units exist as **entities** during construction, then become **squads** after completion. The original code only tracked squads, completely missing the construction phase units that take up production time slots.
