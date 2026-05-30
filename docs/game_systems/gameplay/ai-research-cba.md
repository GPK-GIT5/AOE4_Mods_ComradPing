# AI Systems Research — Official AI Foundations for Onslaught Development

> Dedicated research file for advancing custom AI behaviors in Onslaught multiplayer matches.
> Canonical sources in this document are official engine APIs and base-game SCAR systems; Onslaught runtime files are implementation context only.

## Source-of-Truth Policy

- Canonical: `game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api`, official base-game AI scripts under `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/**`, and official encounter plans under `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/**`.
- Supporting: AGS AI integration patterns in `Gamemodes/Dependencies/Advanced Game Settings/assets/scar/ai/ags_ai.scar`.
- Non-canonical context: Onslaught runtime and debug scripts, including `cba_ai_player.scar`, are treated as current implementation snapshots, not source of truth.

---

## Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Engine AI API Surface](#2-engine-ai-api-surface)
3. [Official Army & Encounter System](#3-official-army--encounter-system)
4. [Encounter Plans](#4-encounter-plans)
5. [WaveGenerator System](#5-wavegenerator-system)
6. [AGS AI Patterns](#6-ags-ai-patterns)
7. [Onslaught Implementation Snapshot (Non-Canonical)](#7-onslaught-implementation-snapshot-non-canonical)
8. [Debug & Test Infrastructure](#8-debug--test-infrastructure)
9. [Multiplayer Considerations](#9-multiplayer-considerations)
10. [Key Patterns & Recipes](#10-key-patterns--recipes)
11. [Development Opportunities](#11-development-opportunities)
12. [File Reference Map](#12-file-reference-map)

---

## 1. Architecture Overview

AoE4 AI operates on three layers, each relevant to custom multiplayer AI development:

```
┌────────────────────────────────────────────────┐
│  Layer 3: SCAR Scripts (Lua)                   │
│  army.scar, wave_generator.scar, encounters    │
│  custom modules (Onslaught, AGS, etc.)        │
├────────────────────────────────────────────────┤
│  Layer 2: Engine AI Systems (C++)              │
│  AIPlayer, AIEncounter, StateTree, Homebase    │
│  Production Scoring, Formation Coordinators    │
├────────────────────────────────────────────────┤
│  Layer 1: Core Simulation                      │
│  Entities, Squads, Players, Pathfinding, FOW   │
└────────────────────────────────────────────────┘
```

**Layer 2** is exposed via the `AIPlayer_*`, `AIEncounter_*`, `AI_*`, and `AIProductionScoring_*` families in `Essence_ScarFunctions.api`. **Layer 3** scripts call into Layer 2 to orchestrate high-level behaviors like army waves, encounter plans, and building construction.

Onslaught's `cba_ai_player.scar` is currently a **Stage 1 military controller** that intentionally bypasses skirmish AI economy logic and uses direct squad commands + timed rules instead of the StateTree/Encounter system. This is an implementation snapshot, not canonical AI behavior.

---

## 2. Engine AI API Surface

### 2.1 AI Core (`AI_*`) — 30+ functions

| Function | Purpose | Multiplayer Safe |
|----------|---------|:---:|
| `AI_IsAIPlayer(player)` | Detect AI-occupied slot | ✓ |
| `AI_IsLocalAIPlayer(player)` | AI running on local machine (MP host check) | ✓ |
| `AI_Enable(player, bool)` | Enable/disable AI for a player | ✓ |
| `AI_EnableAll(bool)` | Global AI toggle | ✓ |
| `AI_PauseCurrentTasks(player, bool)` | Pause/unpause AI task execution | ✓ |
| `AI_SetDifficulty(player, level)` | Set difficulty (0-3 typical) | ✓ |
| `AI_GetDifficulty(player)` | Read current difficulty | ✓ |
| `AI_GetPersonality(player)` | Get personality name | ✓ |
| `AI_LockSquad(player, squad)` | Lock squad from AI control | ✓ |
| `AI_LockSquads(player, sgroup)` | Lock SGroup from AI control | ✓ |
| `AI_LockEntity(player, entity)` | Lock entity from AI control | ✓ |
| `AI_GetAndReserveNextTaskID(player)` | Reserve ID for SCAR-created encounters | ✓ |
| `AI_FindConstructionLocation(player, ebp, pos)` | Find valid build position | ✓ |
| `AI_FindClosestOpenPositionForStructure(player, ebp, pos)` | Alt build-pos finder | ✓ |
| `AI_EnableEconomyOverride(player, name, bool)` | Toggle economy override | ✓ |
| `AI_RestartSCAR(player)` | Restart AI SCAR logic | ✓ |
| `AI_SetAITargetable(player, bool)` | Control whether other AIs target this player | ✓ |
| `AI_PlayerAddExclusionArea(player, pos, noPath, noTarget)` | Pathfinding exclusion | ✓ |
| `AI_PlayerRemoveExclusionArea(player, pos, noPath, noTarget)` | Remove exclusion | ✓ |
| `AI_FindBestProducibleSquadPBGforSquadTypes(player, types)` | Best producible unit for types | ✓ |
| `AI_FindBestProducibleEntityPBGforEntityTypes(player, types)` | Best producible building for types | ✓ |
| `AI_SetAISquadCombatRangePolicyTaskOverride(squad, policy)` | Override squad combat range | ✓ |

### 2.2 AIPlayer (`AIPlayer_*`) — 50+ functions

| Function | Purpose |
|----------|---------|
| `AIPlayer_GetLocalFromPlayer(player)` | Get AIPlayer handle from Player |
| `AIPlayer_GetLocal(playerId)` | Get AIPlayer from numeric ID |
| `AIPlayer_GetOrCreateHomebase(player, pos)` | Create/get homebase at position |
| `AIPlayer_SetSquadHomebase(player, sgroup, hbID)` | Assign squads to homebase |
| `AIPlayer_SetEntityHomebase(player, egroup, hbID)` | Assign buildings to homebase |
| `AIPlayer_RemoveSquadHomebase(player, sgroup)` | Remove squad homebase assignment |
| `AIPlayer_RemoveEntityHomebase(player, egroup)` | Remove entity homebase assignment |
| `AIPlayer_SetGathererDistributionOverride(player, dist)` | Set gatherer distribution (0.0 = none) |
| `AIPlayer_SetRequiresStatsUpdate(player)` | Force stats squad update |
| `AIPlayer_SetAllowResourceGatheringOutsideLeash(player, bool)` | Resource gathering beyond leash |
| `AIPlayer_IsPointThreatened(player, pos, filterBuildings, fitness)` | Threat detection at position |
| `AIPlayer_GetAnchorPosition(player)` | Get AI anchor/HQ position |
| `AIPlayer_FindClosestSiegeTarget(player, eg, sections, unbreached, pos)` | Wall siege targeting |
| `AIPlayer_GetKnownResourceDeposits(player, type, depleted)` | Known resource deposits |
| `AIPlayer_EnemyTerritoryDetected(player)` | Has enemy territory been seen |
| `AIPlayer_GetDistanceToEnemyTerritory(player, pos)` | Distance to enemy territory |
| `AIPlayer_CanSeeEntity(player, entity)` | FOW visibility check |
| `AIPlayer_GetOpponentPlayerCount(player)` | Count of opponents |
| `AIPlayer_GetOpponentPlayerAtIndex(player, idx)` | Get opponent by index |
| `AIPlayer_CachedPathCrossesEnemyTerritory(player, id, dist, unused)` | Path through enemy |
| `AIPlayer_PushScoreMultiplier(player, key, mult, id)` | Adjust target scoring weight |
| `AIPlayer_PopScoreMultiplier(player, key, id)` | Remove scoring weight |
| `AIPlayer_PushUnitTypeScoreMultiplier(player, type, mult, id)` | Unit type scoring |
| `AIPlayer_SetStrategicBaseIntention(player, name, value)` | Set strategic intention |
| `AIPlayer_UpdateSkirmishProduction(player)` | Force production update |
| `AIPlayer_UpdateSkirmishAttackAndCaptureTasks(player)` | Force attack task update |
| `AIPlayer_UpdateSkirmishScoutingTasks(player)` | Force scout task update |
| `AIPlayer_UpdateGathering(player)` | Force gathering update |
| `AIPlayer_ResetEnemySquadsVisibility(player, enemy)` | Reset enemy visibility |

**StateModel Access** (get/set internal AI state variables):
- `AIPlayer_GetStateModelBool(player, key)` / `AIPlayer_SetStateModelBool(player, key, val)` (set via `Player_SetStateModelBool`)
- `AIPlayer_GetStateModelFloat(player, key)` / `AIPlayer_GetStateModelInt(player, key)`
- `AIPlayer_GetStateModelPBG(player, key)`
- `AIPlayer_GetStateModelEntityTarget(player, key)`
- `AIPlayer_GetStateModelTargetListEntries(player, key)`
- `AIPlayer_GetStateModelAISquadListEntries(player, key)`

### 2.3 AIEncounter (`AIEncounter_*`) — 110+ functions

The encounter system is the engine's military behavior orchestrator. Key subsystems:

| Subsystem | Functions | Purpose |
|-----------|-----------|---------|
| **Core** | `Cancel`, `Pause`, `Trigger`, `ForceComplete`, `GetEncounterFromID`, `IsValid` | Lifecycle |
| **TargetGuidance** | `SetTargetPosition`, `SetTargetEntity`, `SetTargetSquad`, `SetTargetArea`, `SetTargetLeash`, patrol variants | Where to fight |
| **EngagementGuidance** | `EnableAggressiveEngagementMove`, `SetMaxEngagementTime`, `SetMaxIdleTime`, `EnableConstruction`, `EnableSetupLocations`, `SetCoordinatedSetup` | How to fight |
| **CombatGuidance** | `AddForcedCombatTarget*`, `ClearForcedCombatTargets`, `SetCombatRangePolicy`, `SetSpreadAttackers`, `EnableCombatGarrison` | Combat targeting |
| **FallbackGuidance** | `SetFallbackCapacityPercentage`, `SetFallbackCombatRating`, `SetRetreatHealthPercentage`, `SetReinforceHealthPercentage`, `SetEntitiesRemainingThreshold`, `EnableReinforceDuringCombat` | When to retreat |
| **MoveGuidance** | `EnableAggressiveMove`, `SetSquadCoherenceRadius` | Movement behavior |
| **ResourceGuidance** | `SquadGroup`, `EntityGroup`, `ClearSquads`, `ClearEntities`, `SetResourceMoney` | Resource allocation |
| **TacticFilter** | `SetPriority`, `SetAbilityPriority`, `SetTacticGuidance`, `SetAbilityGuidance`, `SetTargetPolicy` | Tactic/ability control |
| **FormationGuidance** | `SetFormUpAt*`, `SetFormUpAtTimeOutParams`, formation phase exit/setup | Formation control |
| **FormationPhase** | `GetEndPosition`, `GetEndReason`, `GetEnemiesAtEnd`, `GetSquadsAvailableAtEnd` | Phase result queries |
| **FormationTaskState** | `SimpleMelee`, `MinRange`, `SetupRanged`, `Move`, `TransportMove` | Task state definitions |
| **Notification** | `SetPlayerEventEncounterID`, `SetEnableSnipedCallbacks`, `ClearCallbacks` | Encounter events |
| **Debug** | `SetDebugName`, `LogDebug` | Debugging |

### 2.4 AIProductionScoring (`AIProductionScoring_*`) — 40+ functions

Production scoring drives what the AI builds/researches. Composable scoring functions:

| Function | Purpose |
|----------|---------|
| `AlliedCombatFitness(player, min, max, armyType, highGood)` | Score based on allied combat strength |
| `CounterScore(player, baseContribution)` | Counter-unit scoring |
| `PopulationPercentage(player, target, dropoff, group, usePop)` | Pop-cap-aware production |
| `PresenceOfEnemyTypes(player, weights, squadTypes)` | React to enemy composition |
| `PresenceOfMyTypes(player, weights, squadTypes)` | Avoid over-producing specific types |
| `LuaScoringFunction(player, luaFunc)` | **Custom Lua scoring callback** |
| `TimeToAcquire(player, maxSecs, gather, build, requirements)` | Time-based feasibility |
| `UnderCountLimit(player, maxAlive, maxEverProduced, group)` | Hard cap on production |
| `MaxPopCapPercentage(player, target, group)` | Population ceiling |
| `MinimumGameTime(player, minTime)` | Age/time gating |
| `MaximumGameTime(player, maxTime)` | Time-limited production |
| `CanPushProductionScoringFunction(player)` | Check if scoring is ready |
| `MultiplyListScoringFunction(player, functions)` | Compose: multiply scores |
| `MaxScoringFunction(player, functions)` | Compose: take max score |
| `ClampedScoringFunction(player, min, max, inner)` | Compose: clamp score range |

**Key insight**: `AIProductionScoring_LuaScoringFunction` allows injecting custom Lua logic into the production scoring pipeline. This is the primary extension point for custom unit composition strategies.

---

## 3. Official Army & Encounter System

### 3.1 Army Lifecycle (`army.scar`)

The Army system manages groups of AI-controlled units through staged combat behaviors.

**Initialization**: `Army_Init(params)` creates an army with:
- `player` — must be an AI player
- `units` — UnitTable for what to spawn
- `spawn` — CombatArena for spawn location
- `targets` — list of CombatArenas to attack
- `targetOrder` — `LINEAR`, `LOOP`, `PATROL`, or `RANDOM`
- Callbacks: `onVictoryFunction`, `onDeathFunction`, `onBlockedFunction`, `onCompleteFunction`

**Combat Arena Parameters** (default values):
```lua
combatRangeAtTarget = 35
combatRangeEnRoute = 35
leashBuffer = 10
attackMoveAtTarget = true
attackMoveEnRoute = true
attackUnitsEnRoute = true
attackUnitsAtTarget = true
attackBuildingsEnRoute = BUILDINGS_ALL
attackBuildingsAtTarget = BUILDINGS_ALL
idleTime = 0
holdPositionWhileWaiting = false
ramsBuiltWhenBlocked = 1
ramPassengerCount = 8
siegeTowerPassengerCount = 8
openPathThreshold = 120
brokenWallThreshold = 30
```

**Building Engagement Presets**:
| Preset | Clears? | Excluded |
|--------|:-------:|----------|
| `BUILDINGS_NONE` | No | All buildings |
| `BUILDINGS_ALL` | Yes | Settlements, walls |
| `BUILDINGS_ALL_BUT_TC` | Yes | Settlements, walls, town centers |
| `BUILDINGS_THREATENING` | Yes | Houses, tents, farms, settlements, walls, production, economy, research |
| `BUILDINGS_IMPORTANT` | Yes | Houses, tents, farms, settlements, walls |

Each preset has paired `formationCoordinatorEnRoute` and `formationCoordinatorAtTarget` blueprints from `BP_GetAIFormationCoordinatorBlueprint`.

### 3.2 ArmyEncounterFamily (`army_encounter.scar`)

Manages clusters of StateTree encounters created from a single Army dispatch:
- `ArmyEncounterFamily:new(army, stateModels)` — create family
- `:start()` — divides squads into clusters via `SGroup_DivideIntoClusters(sg, true, 50)`, creates parent + child encounters
- `:stop()` — cancels all encounters via `AIEncounter_Cancel`
- `:markDone(callbackID)` — handle encounter completion; promotes children to parent when parent finishes
- Uses `AI_GetAndReserveNextTaskID` for encounter IDs
- Notifications bridge back to Army system via callback IDs and `EventRule_GetNextUniqueRuleID`

**Encounter end reasons** tracked in `endReasonResults`:
- `victory`, `complete`, `death`, `timeout`, `blocked`, `stopped`

---

## 4. Encounter Plans

Registered via `Encounter_RegisterPlan()`. Each plan defines phases with `startFunction`, `aiNotificationFunction`, and `endFunction`.

### 4.1 Attack Plan (`plan_attack.scar`)

Single-phase plan ("Main") for offensive operations.

**Goal Data**:
```lua
{
    target = REQUIRED,          -- Position or entity
    attackMove = false,         -- attack-move style (false = ignore en route)
    maxIdleTime = 5,            -- seconds idle before plan checks
    archerRepositioning = nil,  -- seconds between repo; nil = disabled
    cavalryCanBuildRams = true, -- cavalry builds rams against walls
    shouldHoldWhileWaiting = false,
    tactics = {},               -- tactic overrides
    fallback = {},              -- fallback parameters
}
```

**Attack move styles**:
- `attackMoveStyle_attackEverything` — engage everything en route
- `attackMoveStyle_ignoreEverything` — move directly to target

### 4.2 Defend Plan (`plan_defend.scar`)

Holds position and engages threats within a radius.

### 4.3 Move Plan (`plan_move.scar`)

Non-combat movement to a target position. Used for transports and repositioning.

### 4.4 TownLife Plan (`plan_townlife.scar`)

Economy/idle behavior within a homebase radius. Supports construction activity via `AIEncounter_EngagementGuidance_EnableConstruction`.

### 4.5 DoNothing Plan (`plan_donothing.scar`)

Idle holding pattern. Units stay in place.

---

## 5. WaveGenerator System

`wave_generator.scar` manages spawning units, staging them, and launching assault waves.

### 5.1 Unit Type Registry

```lua
-- category → build_time mapping
scar_spearman    = { category = "infantry",  build_time = 15 }
scar_manatarms   = { category = "infantry",  build_time = 22 }
scar_archer      = { category = "ranged",    build_time = 15 }
scar_crossbowman = { category = "ranged",    build_time = 22 }
scar_horseman    = { category = "cavalry",   build_time = 22 }
scar_knight      = { category = "cavalry",   build_time = 35 }
scar_ram         = { category = "siege",     build_time = 30 }
scar_mangonel    = { category = "siege",     build_time = 40 }
scar_trebuchet   = { category = "siege",     build_time = 40 }
scar_bombard     = { category = "siege",     build_time = 45 }
scar_monk        = { category = "religious", build_time = 30 }
```

### 5.2 Spawn Categories

```lua
barracks       = { "infantry" }
archery_range  = { "ranged" }
stable         = { "cavalry" }
siege_workshop = { "siege" }
town_center    = { "town_center" }
monastery      = { "religious" }
universal      = { "infantry", "ranged", "cavalry", "siege", "town_center", "religious" }
```

### 5.3 Customization Points

- `WaveGenerator_OverrideUnitBuildTime(type, time)` — override spawn cooldown
- `WaveGenerator_OverrideBuildingSpawnType(building, categories)` — remap building production capabilities
- `WaveGenerator_Init(data)` — full initialization with staging_army, assault_army, auto_launch
- `ignore_build_times` — flag for instant spawning
- `use_separate_spawns` — spawn from nearby buildings instead of central point
- `auto_launch_after_prepare` / `auto_launch_after_ready` — automated wave dispatch timing

---

## 6. AGS AI Patterns

`ags_ai.scar` demonstrates critical patterns for multiplayer AI integration:

### 6.1 Module Registration

```lua
AGS_AI_MODULE = "AGS_AI"
Core_RegisterModule(AGS_AI_MODULE)

function AGS_AI_UpdateModuleSettings()
    if not AGS_GLOBAL_SETTINGS.Multiplayer then
        Core_UnregisterModule(AGS_AI_MODULE)
        return
    end
end
```

### 6.2 Homebase Assignment (spawned units)

```lua
function AGS_AI_AssignSpawnedUnits(player, sgroup)
    if AI_IsAIPlayer(player.id) then
        local aiPlayer = AIPlayer_GetLocalFromPlayer(player.id)
        if aiPlayer ~= nil then
            local base_pos = Player_GetStartingPosition(player.id)
            local homebase_id = AIPlayer_GetOrCreateHomebase(player.id, base_pos)
            AIPlayer_SetSquadHomebase(player.id, sgroup, homebase_id)
            AIPlayer_SetRequiresStatsUpdate(player.id)
        end
    end
end
```

### 6.3 State Model Bool Patterns

```lua
-- Disable wonder construction for AI
Player_SetStateModelBool(player.id, "ai_do_not_construct_wonders", true)

-- Disable all AI construction (Nomad mode)
Player_SetStateModelBool(player.id, "ai_do_not_construct", true)
```

### 6.4 FOW Reveal for Mongols (Stone Vision)

```lua
function AGS_AI_ApplyAdjustment_StoneVision(player)
    local civ = Player_GetRaceName(player.id)
    if civ == "mongol" then
        local sites = AIPlayer_GetKnownResourceDeposits(player.id, "stone", false)
        for _, deposit in ipairs(sites) do
            local pos = Entity_GetPosition(deposit)
            FOW_RevealArea(pos, 10, -1, player.id)
        end
    end
end
```

### 6.5 AI Garrison Behavior (King of the Hill)

```lua
function AGS_AI_ApplyAdjustment_HideKing(player)
    -- Find king unit, move to keep/TC, garrison
    local sg_king = Player_GetSquadsByType(player.id, "king")
    if SGroup_CountSpawned(sg_king) > 0 then
        local keep_pos = Player_GetStartingPosition(player.id)
        Cmd_Garrison(sg_king, keep_pos, false)
    end
end
```

### 6.6 Resource Gifting (Nomad)

```lua
function AGS_AI_ApplyAdjustment_Nomad(player)
    Player_SetStateModelBool(player.id, "ai_do_not_construct", true)
    Player_AddResource(player.id, RT_Food, 150)
    Player_AddResource(player.id, RT_Wood, 150)
end
```

---

## 7. Onslaught Implementation Snapshot (Non-Canonical)

This section documents observed behavior in current Onslaught scripts for integration planning. It is not a source-of-truth specification.

### 7.1 Module Lifecycle

```
EarlyInitializations → detect AI slots via AI_IsAIPlayer()
PresetFinalize       → suppress economy, grant resources, claim units, register rules
OnPlay               → deploy scouts, seed initial foundations
OnGameOver           → remove rules, unpause AI tasks, cleanup
```

### 7.2 Timed Rule System

| Rule | Interval | Purpose |
|------|----------|---------|
| `_AI_Rule_BuildMilitaryBuildings` | 15.0s | Place barracks foundations |
| `_AI_Rule_ProduceUnits` | 8.0s | Spawn infantry at completed buildings |
| `_AI_Rule_ManageArmies` | 10.0s | Check staging → dispatch |
| `_AI_Rule_AllySupport` | 12.0s | Detect threatened allies, redirect forces |
| `_AI_Rule_ScoutPatrol` | 45.0s | Deploy/manage scout patrols |
| `_AI_Rule_BuildOutposts` | 60.0s | Outpost ring expansion |
| `_AI_Rule_ResourceTopup` | 120.0s | Periodic resource grant |
| `_AI_Rule_PatrolArmies` | 20.0s | Patrol army waypoint cycling |
| `_AI_Rule_VillagerConstruction` | 2.0s | Villager construction supervision |

### 7.3 Economy Suppression

- `AI_DisableAllEconomyOverrides(player.id)` — disable AI economy logic
- `AIPlayer_SetGathererDistributionOverride(player.id, 0.0)` — zero gathering
- `AI_PauseCurrentTasks(player.id, true)` — pause native AI tasks during construction
- `Player_SetResource` — grant 100,000 of each resource type
- Periodic top-up every 120 seconds

### 7.4 Building System

**Foundation Placement Pipeline**:
1. Calculate target position from zone center (angular offset per building count)
2. `Entity_CalcConstructionPlacement(ebp, player, pos)` — primary validation
3. `AI_FindConstructionLocation(player, ebp, pos)` — fallback position finder
4. `Entity_CreateFacing(ebp, player, pos, facing, true)` → `Entity_Spawn` → `Entity_SnapToGridAndGround`
5. Track in `construction_queue`; EGroup per building for `Cmd_Construct`

**Construction Management**:
- Villagers assigned via `Cmd_Construct` (position-targeted) or entity-targeted build
- Stall detection: no progress after `_AI_CONSTRUCT_STALL_TIMEOUT` (20s)
- Command path switching when accepted commands show no progress after 6s
- `_AI_MAX_PENDING_FOUNDATIONS` = 3 to avoid overcommitting builders

### 7.5 Unit Production

- Stage 1: infantry only (100% spearman from barracks)
- `Cardinal_ConvertTypeToSquadBlueprint(type, player)` for civ-appropriate unit
- `UnitEntry_DeploySquads` for batch spawning (5 per cycle)
- Produced units moved to staging SGroup then rally toward center

### 7.6 Army Dispatch

- Threshold system: `LOW=30`, `MED=50`, `HIGH=70` (configurable via AGS_GLOBAL_SETTINGS.AIAggression)
- When staging count ≥ threshold: create army SGroup, `Cmd_AttackMove` to target
- `_AI_FindBestAttackTarget(player)` — target selection (falls back to map center)

### 7.7 Ally Support

- `AIPlayer_IsPointThreatened(player.id, ally_pos, true, 60.0)` — threat detection
- Fallback: check ally keep HP loss
- Redirect idle armies first, or dispatch half-threshold staging force

### 7.8 Per-Player State Structure

```lua
player.ai = {
    label = "P1",
    buildings = { barracks = { count, entities }, ... },
    total_buildings = 0,
    staging_sg = SGroup,
    armies = { { sg, target, dispatch_time }, ... },
    patrol_sg = SGroup,
    patrol_waypoint_idx = 1,
    villager_sg = SGroup,
    construction_queue = { { entity, ebp, pos, type_key, zone, eg_name }, ... },
    production_egroups = { barracks = { eg_name, ... }, ... },
    squad_threshold = 50,
    spawned = { infantry = 0, ranged = 0, cavalry = 0, siege = 0 },
    primary_zone_count = 0,
    stage = 1,
    outpost_count = 0,
    scouts_deployed = false,
    current_construct_entity = nil,
    ai_tasks_paused = false,
}
```

### 7.9 External Debug Lock

```lua
_AI_DEBUG_EXTERNAL_LOCK = false
_AI_DEBUG_EXTERNAL_LOCK_REASON = ""
```
When true, all timed rules skip execution. Used by debug harnesses for deterministic test control.

---

## 8. Debug & Test Infrastructure

### 8.1 AI Player Debug Suite (`cba_debug_ai_player.scar`)

11-phase verification suite with validation profiles ("normal" vs "harness"):

| Phase | Name | Validates |
|-------|------|-----------|
| 0 | Bootstrap | AI player detection, state initialization, module registration |
| 1 | Economy | Resource suppression, gatherer distribution override |
| 2 | Building | Foundation placement, zone center computation, build queue |
| 3 | Production | Unit spawning, ratio tracking, staging group population |
| 4 | Army | Dispatch threshold, army creation, attack-move commands |
| 5 | AllySupport | Threat detection, force redirection, support dispatch |
| 6 | Scouts | Scout deployment, patrol waypoint generation |
| 7 | Outposts | Ring placement, outpost count tracking |
| 8 | EventHandlers | GE_ConstructionComplete, entity kill batch handler |
| 9 | Integration | Full lifecycle end-to-end, rule coexistence |
| 10 | StartingUnits | Villager/MaA claim, no-spawn policy verification |

**Console**:
- `Debug_AIPlayerTest()` — run all phases
- `Debug_AIPlayerTest_Phase(n)` — run specific phase
- `Debug_AIPlayerStatus()` — print live AI state

**Key helpers**: `_DAI_Assert(cond, msg)`, `_DAI_Skip(reason)`, `_DAI_FindAIPlayer()` scanner

### 8.2 AI Behavior Visual Suite (`cba_debug_ai_behavior.scar`)

8 interactive visual scenario tests:

| # | Scenario | Tests |
|---|----------|-------|
| 1 | TargetPriority | Army targets correct enemy position |
| 2 | ResourceSpending | Economy suppression effective |
| 3 | PopulationCap | Production stops at pop cap |
| 4 | MultiThreat | Response to simultaneous attacks |
| 5 | SiegeCounterPlay | AI reaction to siege weapons |
| 6 | RecoveryPipeline | Recovery after army wipe |
| 7 | HolySite | Sacred site patrol behavior |
| 8 | StateConsistency | State integrity across multiple cycles |

**Console**: `Debug_AIBehavior()`, `Debug_AIBehavior_Scenario(n)`

Uses `Debug_AskYesNo()` for interactive visual confirmation by observer.

---

## 9. Multiplayer Considerations

### 9.1 Local AI Detection

```lua
-- CRITICAL: In multiplayer, only the host runs AI logic
if AI_IsLocalAIPlayer(player.id) then
    -- safe to issue AI commands
end
```

`AI_IsAIPlayer()` returns true on all machines, but `AI_IsLocalAIPlayer()` returns true only on the machine actually running that AI. All AI commands must be issued only from the host.

### 9.2 Sync Safety

- All `AI_*`, `AIPlayer_*`, `AIEncounter_*` calls are engine-synchronized
- `pcall()` wrapping is critical — AI API calls can fail when player is eliminated or entity is destroyed
- `World_GetRand()` is sync-safe (deterministic across all machines)
- Do NOT use `math.random()` in any code that affects game state

### 9.3 AI + Human Team Coordination

In Onslaught, AI players are on the same team as humans:
- `player.AGS_Team.allies` contains teammate references
- AI detects ally threats via `AIPlayer_IsPointThreatened`
- AI redirects armies to support allies under attack
- Resource grants don't affect human teammates

### 9.4 Building Limit Integration

- `player.obj_buildingLimit_count` — external building cap from cba_options
- `CBA_Options_GetPlayerProdLimit(player)` — production building limit
- `player.obj_buildingLimit_outpost_count` — outpost-specific cap
- AI building counts must respect the shared Onslaught building limit system

---

## 10. Key Patterns & Recipes

### 10.1 AI Player Detection Loop

```lua
_ai_players = {}
for i, player in ipairs(PLAYERS) do
    if player ~= nil and player.id ~= nil then
        local ok, is_ai = pcall(AI_IsAIPlayer, player.id)
        if ok and is_ai then
            table.insert(_ai_players, player)
        end
    end
end
```

### 10.2 Safe AI Command Pattern

```lua
local function safe_ai_cmd(func, ...)
    local ok, result = pcall(func, ...)
    if not ok then
        print("[AI_PLAYER] WARNING: " .. tostring(result))
    end
    return ok, result
end
```

### 10.3 Building Foundation Pipeline

```lua
-- 1. Validate position
local ok, calc = pcall(Entity_CalcConstructionPlacement, ebp, player.id, candidate)
if ok and calc.success then
    candidate = calc.position
end
-- 2. Fallback
if not validated then
    local ok2, pos = pcall(AI_FindConstructionLocation, player.id, ebp, candidate)
end
-- 3. Create
local ok3, entity = pcall(Entity_CreateFacing, ebp, player.id, pos, facing, true)
pcall(Entity_Spawn, entity)
pcall(Entity_SnapToGridAndGround, entity, false)
```

### 10.4 Difficulty Scaling Pattern

```lua
local difficulty = AI_GetDifficulty(player.id)
local multiplier = 1.0
if difficulty == 1 then multiplier = 0.75       -- Easy
elseif difficulty == 2 then multiplier = 1.0     -- Normal
elseif difficulty == 3 then multiplier = 1.5     -- Hard
elseif difficulty == 4 then multiplier = 2.0     -- Hardest
end
```

### 10.5 Encounter Creation from SCAR

```lua
local taskID = AI_GetAndReserveNextTaskID(player.id)
local encounter = AIEncounter_GetEncounterFromID(player.id, taskID)
if encounter then
    AIEncounter_TargetGuidance_SetTargetPosition(encounter, target_pos)
    AIEncounter_TargetGuidance_SetTargetArea(encounter, 35)
    AIEncounter_TargetGuidance_SetTargetLeash(encounter, 50)
    AIEncounter_EngagementGuidance_SetMaxEngagementTime(encounter, 120)
    AIEncounter_CombatGuidance_SetCombatRangePolicy(encounter, rangePolicy)
    AIEncounter_Trigger(encounter)
end
```

### 10.6 WaveGenerator Integration

```lua
Army_InitSystem()
local assault = Army_Init({
    player = player.id,
    targets = { target_area },
    targetOrder = TARGET_ORDER_LINEAR,
    spawn = spawn_area,
    combatRange = 35,
    leashRange = 50,
})
local wg = WaveGenerator_Init({
    player = player.id,
    spawn = spawn_area,
    assault_army = assault,
    units = {
        { type = "scar_spearman", count = 10 },
        { type = "scar_archer", count = 5 },
    },
    auto_launch_after_ready = 10,
})
WaveGenerator_Prepare(wg)
```

---

## 11. Development Opportunities

### 11.1 Stage 2+ Expansion

Observed current Onslaught implementation is Stage 1 only (infantry from barracks). Planned progression:
- **Stage 2**: Add archery range + stable production, mixed composition ratios
- **Stage 3**: Siege workshop, trebuchet targeting of enemy keeps
- **Stage 4**: Adaptive composition based on enemy unit types (counter-unit logic)

### 11.2 Encounter System Integration

Currently uses simple `Cmd_AttackMove` for army dispatch. Could leverage:
- `ArmyEncounterFamily` for proper squad clustering and coordinated engagement
- Encounter plans (Attack/Defend) for smarter fallback and retreat behavior
- Formation coordinators for siege approach patterns
- `AIEncounter_FallbackGuidance_*` for retreat-when-losing behavior

### 11.3 Production Scoring Integration

`AIProductionScoring_LuaScoringFunction` could replace the ratio-based production system with:
- Counter-unit scoring based on enemy composition
- Population-aware scaling
- Time-gated unit unlocks (e.g., siege only after Age III)

### 11.4 Homebase Integration

AGS pattern of `AIPlayer_GetOrCreateHomebase` + `AIPlayer_SetSquadHomebase` could:
- Give the native AI awareness of custom-spawned units
- Allow skirmish AI subroutines (production, scouting) to operate alongside custom logic
- Enable `SetAllowResourceGatheringOutsideLeash` for mixed economy/military modes

### 11.5 Threat-Aware Positioning

Engine APIs available but unused:
- `AIPlayer_IsPointThreatened` — already used for ally support; extend to staging area safety
- `AIPlayer_GetDistanceToEnemyTerritory` — avoid building in forward positions
- `AIPlayer_CachedPathCrossesEnemyTerritory` — route safety for army movements
- `AIPlayer_FindClumpContainingPosition` — detect enemy groupings for engagement

### 11.6 Advanced Tactical Behaviors

- `AI_SetAISquadCombatRangePolicyTaskOverride` — control melee vs ranged engagement per squad
- `AIEncounter_TacticFilter_SetAbilityGuidance` — control when units use special abilities
- `AIEncounter_EngagementGuidance_SetCoordinatedSetup` — synchronized attack positioning
- `AIEncounter_FormationTaskStateGuidance_MinRange*` — keep ranged units at distance

### 11.7 Patrol Enhancement

Sacred site positions already discovered. Could improve patrol with:
- Weighted waypoint cycling (prioritize contested areas)
- Dynamic re-pathing when threats detected
- Multi-patrol-group coordination (flanking)

---

## 12. File Reference Map

### Official Engine

| File | Content |
|------|---------|
| `game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api` | All engine SCAR functions (AI_*, AIPlayer_*, AIEncounter_*, AIProductionScoring_*) |
| `game_data/extracted/aoe4/scardocs/Essence_Constants.api` | Engine constants (command types, game events, resource types) |

### Official SCAR Scripts

| File | Content |
|------|---------|
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/army.scar` | Army system, combat arena params, building presets |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/army_encounter.scar` | ArmyEncounterFamily, StateTree encounter bridge |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/wave_generator.scar` | WaveGenerator: unit types, spawn categories, wave lifecycle |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/ai_encounter_util.scar` | Encounter creation utilities |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/combat_fitness_util.scar` | Combat fitness calculations |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/ai/combat_fitness_consts.scar` | Combat fitness constants |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/plan_attack.scar` | Attack encounter plan |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/plan_defend.scar` | Defend encounter plan |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/plan_move.scar` | Move encounter plan |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/plan_townlife.scar` | TownLife encounter plan |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/encounterplans/plan_donothing.scar` | DoNothing encounter plan |
| `game_data/extracted/aoe4/scar_dump/scar gameplay/cardinal_encounter.scar` | Cardinal encounter system core |

### Onslaught Implementation Snapshots (Non-Canonical)

| File | Content |
|------|---------|
| `Gamemodes/Onslaught/assets/scar/gameplay/cba_ai_player.scar` | Staged military AI controller |
| `Gamemodes/Onslaught/assets/scar/debug/cba_debug_ai_player.scar` | 11-phase verification suite |
| `Gamemodes/Onslaught/assets/scar/debug/cba_debug_ai_behavior.scar` | 8 visual behavior scenarios |

### AGS AI

| File | Content |
|------|---------|
| `Gamemodes/Dependencies/Advanced Game Settings/assets/scar/ai/ags_ai.scar` | AGS multiplayer AI adjustments |

### Workspace References

| File | Content |
|------|---------|
| `docs/game_systems/gameplay/ai.md` | Comprehensive AI & encounter plans reference |
| `docs/game_systems/systems/ai-patterns.md` | AI patterns index, campaign AI usage |

---

*Last updated: Session research compilation*
