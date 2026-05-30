# Phase 1: Command-Writer Mapping & Ownership Attribution

## Overview

**Goal:** Design explicit ownership model for patrol_sg to prevent multi-writer conflicts and thrashing.

**Scope:** Define which module owns the right to command patrol_sg at each moment, establish priority tiers, and design anti-thrash guards.

---

## Current State: Four Independent Writers

### Writer #1: Patrol Waypoint Cycle
- **Location:** `patrol.scar` lines 88-130
- **Function:** `_AI_IssuePatrolOrder(player)`
- **Trigger:** PatrolArmies rule (8s interval)
- **Action:** Cycles through 4 waypoints, checks boundary, falls back to base on rejection
- **Command:** `Cmd_Move(ai.patrol_sg, target_pos)` (line 127)
- **Ownership Attribution:** Sets `ai.patrol_last_order_source = "patrol_waypoint"` (currently missing)

### Writer #2: MAA State Machine
- **Location:** `maa.scar` lines 17-162
- **Function:** Per-state handlers (IDLE, SCOUTING, ENEMY_FOUND, RETREATING, RALLYING, REGROUPED, ENGAGING)
- **Trigger:** OnPlay rule tick (0.125s heartbeat, but suppressed by hold_timer)
- **Action:** State transitions and direct unit movement based on threat detection
- **Command:** Implicit `Cmd_Move` calls within state handlers
- **Ownership Attribution:** Sets `ai.patrol_last_order_source = "maa_state_<state>"` (currently missing)

### Writer #3: Army Dispatch (ManageArmies)
- **Location:** `army.scar` lines 140-158
- **Function:** `_AI_ManageArmies` rule
- **Trigger:** ManageArmies rule (10s interval)
- **Action:** Retargets patrol_sg to army staging when dispatch ready, or to active army location
- **Command:** Retarget patrol to new objective position
- **Ownership Attribution:** Sets `ai.patrol_last_order_source = "main_dispatch"` (line 158, already exists in code!)
- **Hold Timer:** Sets `ai.patrol_order_hold_until = now + 12.0` (line 150)

### Writer #4: Combat Response (AllySupport)
- **Location:** `army.scar` lines 268-278
- **Function:** Reactive combat response when enemies spotted
- **Trigger:** AllySupport rule (8s interval, or OnPlay ticks when conditions met)
- **Action:** Retargets patrol_sg to combat threat location
- **Command:** Retarget patrol to threat position
- **Ownership Attribution:** Sets `ai.patrol_last_order_source = "combat_response"` (line 278, already exists in code!)
- **Hold Timer:** Sets `ai.patrol_order_hold_until = now + 12.0` (line 275)

---

## Priority Tier System (Recommended)

### Tier Assignment (Highest to Lowest Priority)

```
TIER 1: COMBAT_RESPONSE
  - Owner: AllySupport rule
  - Right: Can override anything when threat detected
  - Duration: 12s hold
  - Justification: Existential threat takes precedence
  - Rationale: If enemies are attacking, patrol must respond immediately

TIER 2: MAIN_DISPATCH
  - Owner: ManageArmies rule
  - Right: Can override Tier 3-4; blocked by Tier 1
  - Duration: 12s hold
  - Justification: Strategic army objectives drive campaign
  - Rationale: Early aggression/defense more important than routine patrol

TIER 3: MAA_STATE
  - Owner: MAA state machine (within OnPlay rule)
  - Right: Can override Tier 4; blocked by Tier 1-2
  - Duration: Until next state transition (~4-8s typically)
  - Justification: Tactical responses to threats
  - Rationale: State changes should persist unless higher priority takes over

TIER 4: PATROL_WAYPOINT
  - Owner: PatrolArmies rule
  - Right: Lowest priority; baseline cycling
  - Duration: 8s (until next cycle)
  - Justification: Default behavior when no dispatch/threat
  - Rationale: Keep patrol active but respect all strategic/tactical directives
```

---

## Ownership Model: Lease & Release Pattern

### Data Structure Addition (state.scar)

```lua
-- Add to player.ai state table (already partially in place):
ai.patrol_last_order_source = "none"  -- Currently set by army.scar (✓ exists)
ai.patrol_command_owner_tier = 0       -- NEW: Priority tier (0=none, 1=combat, 2=dispatch, 3=maa, 4=patrol)
ai.patrol_command_lease_until = nil    -- NEW: When current owner lease expires
ai.patrol_command_target = nil         -- NEW: Last commanded target
ai.patrol_command_timestamp = 0        -- NEW: Timestamp of last command
```

### Ownership Guard Function

```lua
-- Add to patrol.scar or utility.scar:
function _AI_AcquirePatrolLease(player, new_tier, new_source, hold_duration)
  -- Check if higher-priority owner holds the lease
  if ai.patrol_command_owner_tier > new_tier then
    return false  -- Cannot acquire; higher priority owns it
  end
  
  -- Acquire the lease
  ai.patrol_command_owner_tier = new_tier
  ai.patrol_last_order_source = new_source
  ai.patrol_command_lease_until = World_GetGameTime() + hold_duration
  ai.patrol_command_timestamp = World_GetGameTime()
  
  return true  -- Lease acquired
end

function _AI_ReleasePatrolLease(player, source)
  -- Only the owner can release
  if ai.patrol_last_order_source ~= source then
    return false  -- Not the owner
  end
  
  ai.patrol_command_owner_tier = 0
  ai.patrol_last_order_source = "none"
  ai.patrol_command_lease_until = nil
  
  return true
end

function _AI_IsPatrolLeaseExpired(player)
  if ai.patrol_command_lease_until == nil then
    return true
  end
  return World_GetGameTime() >= ai.patrol_command_lease_until
end

function _AI_GetPatrolLeaseOwner(player)
  return ai.patrol_last_order_source
end
```

---

## Integration Points: Writer By Writer

### Writer #1: Patrol Waypoint (TIER 4)

**Location:** `patrol.scar` line 88-130

**Before:** (Current unguarded code)
```lua
function _AI_IssuePatrolOrder(player)
  ...
  local target_pos = waypoints[wp_index]
  
  if _AI_IsInsideKeepAttackBoundary(player, target_pos) then
    target_pos = hold_pos  -- Fallback
  end
  
  Cmd_Move(ai.patrol_sg, target_pos, false)  -- ❌ No guard, always issues
end
```

**After:** (With ownership guard)
```lua
function _AI_IssuePatrolOrder(player)
  -- Check if higher-priority owner holds lease
  if not _AI_IsPatrolLeaseExpired(player) and 
     _AI_GetPatrolLeaseOwner(player) ~= "patrol_waypoint" then
    -- Cannot issue; release priority owner's lease if they held patrol
    return
  end
  
  -- Acquire patrol lease for 8s (until next cycle)
  if not _AI_AcquirePatrolLease(player, 4, "patrol_waypoint", 8.0) then
    return  -- Cannot acquire lease (higher priority owner active)
  end
  
  ...
  local target_pos = waypoints[wp_index]
  
  if _AI_IsInsideKeepAttackBoundary(player, target_pos) then
    target_pos = hold_pos
    _AI_LogBoundaryBlock(player, "patrol_waypoint_rejected", target_pos)
  end
  
  Cmd_Move(ai.patrol_sg, target_pos, false)
  ai.patrol_command_target = target_pos  -- Track for telemetry
end
```

### Writer #2: MAA State Machine (TIER 3)

**Location:** `maa.scar` line 17-162

**Issue:** State machine doesn't currently issue direct Cmd_Move calls; it sets state transitions. However, it interacts with Writer #3 (dispatch retarget).

**Action:** Add guard before any MAA-driven command:
```lua
function _AI_MAA_OnTick(player)
  ...
  
  -- Check if lease expired or no owner (our turn to command)
  if not _AI_IsPatrolLeaseExpired(player) and 
     _AI_GetPatrolLeaseOwner(player) ~= "maa_state" then
    -- Higher priority owner holding lease, skip state tick
    return
  end
  
  -- Proceed with state machine
  ...
end
```

**Effect:** MAA state transitions will now respect combat/dispatch priority, reducing erratic behavior.

### Writer #3: Army Dispatch (TIER 2)

**Location:** `army.scar` line 140-158

**Before:** (Current code)
```lua
if maa_can_join or maa_retarget then
  ...
  ai.patrol_order_hold_until = World_GetGameTime() + 12.0  -- ✓ Already sets hold
  ai.patrol_last_order_source = "main_dispatch"  -- ✓ Already sets source
  -- Issue new dispatch target
  Cmd_Move(ai.patrol_sg, dispatch_target, false)
end
```

**After:** (With priority guard)
```lua
if maa_can_join or maa_retarget then
  -- Check if combat response (higher priority) is active
  local combat_owner = _AI_GetPatrolLeaseOwner(player)
  if combat_owner == "combat_response" and not _AI_IsPatrolLeaseExpired(player) then
    return  -- Combat owner has priority, skip dispatch
  end
  
  -- Acquire dispatch lease for 12s
  if not _AI_AcquirePatrolLease(player, 2, "main_dispatch", 12.0) then
    return  -- Cannot acquire (but this should succeed unless combat_response blocks it)
  end
  
  ...
  Cmd_Move(ai.patrol_sg, dispatch_target, false)
  ai.patrol_command_target = dispatch_target
end
```

### Writer #4: Combat Response (TIER 1)

**Location:** `army.scar` line 268-278

**Before:** (Current code)
```lua
if threat_detected then
  ...
  ai.patrol_order_hold_until = World_GetGameTime() + 12.0
  ai.patrol_last_order_source = "combat_response"
  Cmd_Move(ai.patrol_sg, threat_pos, false)
end
```

**After:** (With highest priority)
```lua
if threat_detected then
  -- TIER 1: Always acquire lease (overrides all lower tiers)
  _AI_AcquirePatrolLease(player, 1, "combat_response", 12.0)
  
  ...
  Cmd_Move(ai.patrol_sg, threat_pos, false)
  ai.patrol_command_target = threat_pos
  
  -- Log override if we displaced another writer
  if ai.patrol_last_order_source ~= "combat_response" then
    _AI_LogOwnershipOverride(player, "combat_response", ai.patrol_last_order_source, threat_pos)
  end
end
```

---

## Anti-Thrash Guards

### Guard #1: Minimum Command Interval

Prevent same writer from reissuing identical command within 1 second:

```lua
function _AI_ShouldIssueCommand(player, source, new_target)
  local now = World_GetGameTime()
  local last_target = ai.patrol_command_target or Vector_Create(0, 0)
  local time_since_last = now - ai.patrol_command_timestamp
  
  -- If same target and < 1s elapsed, skip
  if Vector_Equal(new_target, last_target) and time_since_last < 1.0 then
    return false
  end
  
  return true
end
```

### Guard #2: Boundary Overwrite Prevention

Don't let boundary rejection cause rapid fallbacks:

```lua
function _AI_IssuePatrolOrder(player)
  ...
  if _AI_IsInsideKeepAttackBoundary(player, target_pos) then
    -- Instead of immediate fallback, skip this cycle if we just fell back
    if ai.patrol_last_order_source == "patrol_waypoint" and
       (World_GetGameTime() - ai.patrol_command_timestamp) < 3.0 then
      -- Fall back was issued < 3s ago, wait before trying another waypoint
      return
    end
    
    target_pos = hold_pos
  end
  ...
end
```

### Guard #3: Hold Timer Mutual Exclusion

Prevent multiple writers from setting conflicting hold times:

```lua
function _AI_SetPatrolHold(player, source, hold_duration)
  local new_hold_until = World_GetGameTime() + hold_duration
  
  -- Only extend hold if source has priority or no hold set
  if ai.patrol_command_lease_until ~= nil and 
     new_hold_until < ai.patrol_command_lease_until then
    -- Existing hold extends further; don't shorten it
    return
  end
  
  ai.patrol_order_hold_until = new_hold_until
  ai.patrol_command_lease_until = new_hold_until
end
```

---

## Telemetry & Debugging

### New Debug Fields

```lua
ai.patrol_command_overwrite_count = 0    -- Counter: How many times was this player's command overwritten?
ai.patrol_lease_conflicts = 0            -- Counter: How many times did lease acquisition fail?
ai.patrol_boundary_rejections = 0        -- Counter: How many waypoints rejected by boundary?
ai.patrol_last_overwrite_by = "none"     -- String: Which writer overwrote us last?
ai.patrol_command_history = {}           -- Array: [timestamp, source, target, result]
```

### New Log Tags

```
[AI_PLAYER][PATROL][LEASE_ACQUIRED]   source=patrol_waypoint tier=4 duration=8.0
[AI_PLAYER][PATROL][LEASE_DENIED]     source=patrol_waypoint tier=4 by_owner=main_dispatch
[AI_PLAYER][PATROL][OVERWRITE]        from=patrol_waypoint to=main_dispatch target=(60,-236)
[AI_PLAYER][PATROL][BOUNDARY_BLOCK]   source=patrol_waypoint waypoint=3/4 distance=85m radius=120m
[AI_PLAYER][PATROL][HOLD_TIMER]       action=set duration=12.0 reason=dispatch_issued
```

### Status Output (debug/status.scar)

```lua
function _AI_PrintPatrolOwnershipStatus(player)
  local owner = _AI_GetPatrolLeaseOwner(player)
  local expires = ai.patrol_command_lease_until or 0
  local now = World_GetGameTime()
  local remaining = math.max(0, expires - now)
  
  print(string.format(
    "[PATROL] P%d owner=%s tier=%d remaining=%.1fs target=(%d,%d) "..
    "overwrites=%d conflicts=%d boundary_rejects=%d",
    World_GetPlayerIndex(player),
    owner,
    ai.patrol_command_owner_tier,
    remaining,
    ai.patrol_command_target.x,
    ai.patrol_command_target.z,
    ai.patrol_command_overwrite_count,
    ai.patrol_lease_conflicts,
    ai.patrol_boundary_rejections
  ))
end
```

---

## Validation Checklist (Before Implementation)

- [ ] Identify all locations where `Cmd_Move(ai.patrol_sg, ...)` is called
- [ ] Verify each location is wrapped with ownership guard
- [ ] Confirm priority tier is correct for each writer
- [ ] Test that Tier 1 (combat) always succeeds
- [ ] Test that Tier 2 (dispatch) succeeds unless combat active
- [ ] Test that Tier 3-4 fail appropriately when higher priority holds lease
- [ ] Verify hold_timer integration (no conflicts)
- [ ] Validate anti-thrash guards prevent rapid rewrites
- [ ] Check debug output shows correct ownership transitions
- [ ] Load test with 8-player scenario

---

## Expected Outcomes After Implementation

### Before (Current Behavior)
- Patrol cycles through waypoints every 8s
- Dispatch overwrites patrol every 10s
- Combat response overwrites both without coordination
- Boundary rejections cause fallback → collides with next cycle
- Hold timers suppress MAA but don't prevent multi-write
- **Result:** Patrol pinned, units idle, thrashing observed

### After (With Ownership Model)
- Patrol cycles only if no higher-priority owner holds lease
- Dispatch acquires lease, holds for 12s, allows patrol to run afterward
- Combat response acquires Tier 1 lease, always succeeds, blocks others
- Boundary rejections don't collide (write interval increases to 3s)
- Hold timers respect ownership tiers
- **Result:** Smooth patrol transitions, clear priority, minimal thrashing

---

## References

- **Writers:** patrol.scar (L88-130), maa.scar (L17-162), army.scar (L140-158, L268-278)
- **Utilities:** utility.scar (L96-117), state.scar (L166-200)
- **Config:** config.scar (L119, L129-131, L158, L169)

