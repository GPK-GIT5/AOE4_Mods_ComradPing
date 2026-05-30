# SCAR Scripting Basics — AoE4

Quick reference for SCAR (Scripting At Relic) — the Lua-based scripting language used in Age of Empires IV.

---

## Module System

Every SCAR file uses a module pattern:

```lua
-- Register the module with the core system
Core_RegisterModule("MyModule")

-- Called during game initialization
function MyModule_OnInit()
    -- Setup code
end

-- Called when game starts (after camera intro)
function MyModule_Start()
    -- Start objectives, rules, etc.
end

-- Called when game ends
function MyModule_OnGameOver()
    -- Cleanup
end

-- Called when a player is defeated
function MyModule_OnPlayerDefeated(player, reason)
    -- Handle player elimination
end
```

---

## Mission Script Lifecycle

Campaign missions follow this sequence:

```lua
function Mission_SetupPlayers()
    -- Very early — gather player IDs
    player1 = World_GetPlayerAt(1)
    player2 = World_GetPlayerAt(2)
end

function Mission_SetupVariables()
    -- Initialize globals, SGroups, EGroups, tables
end

function Mission_Preset()
    -- Before camera intro — spawn starting units, apply upgrades
end

function Mission_PreStart()
    -- After camera, before HUD — register objectives
end

function Mission_Start()
    -- Player has control — start objectives and rules
end
```

---

## Rules System

Rules are the event & timer system:

```lua
-- Run a function every N seconds
local ruleID = Rule_AddInterval(MyFunction, 5)  -- every 5 seconds

-- Run a function once after N seconds
Rule_AddOneShot(MyFunction, 10)  -- after 10 seconds

-- Run on a game event
Rule_AddGlobalEvent(OnEntityKilled, GE_EntityKilled)

-- Remove rules
Rule_Remove(MyFunction)
Rule_RemoveWithID(ruleID)
Rule_RemoveGlobalEvent(OnEntityKilled)

-- Rule callbacks with context and data
Rule_AddInterval(MyCallback, 2, { customData = "value" })

function MyCallback(context, data)
    -- context = the data table you passed
    -- data = engine-provided data (for events)
end
```

---

## Groups (SGroup & EGroup)

Groups are the primary way to reference collections:

```lua
-- Create groups
local sg = SGroup_CreateIfNotFound("my_squads")
local eg = EGroup_CreateIfNotFound("my_entities")

-- Add units
SGroup_Add(sg, squad)
EGroup_Add(eg, entity)

-- Count
local count = SGroup_Count(sg)

-- Iterate
SGroup_ForEach(sg, function(sgroupid, itemindex, squad)
    local health = Squad_GetHealthPercentage(squad)
end)

-- Filter by blueprint
SGroup_Filter(sg, BP_GetSquadBlueprint("unit_spearman_4_eng"), FILTER_KEEP)

-- Check state
if SGroup_IsAlive(sg) and not SGroup_IsEmpty(sg) then
    -- group has living units
end

-- Clear and destroy
SGroup_Clear(sg)       -- remove all members
SGroup_Destroy(sg)     -- destroy the group object
```

---

## Commands (Cmd_)

Issue orders to units:

```lua
-- Move to position/marker
Cmd_Move(sg_mySquads, mkr_destination, false)  -- false = don't queue

-- Attack-move
Cmd_AttackMove(sg_army, mkr_target, false)

-- Attack specific target
Cmd_Attack(sg_archers, eg_target)

-- Garrison units into a building
Cmd_Garrison(sg_infantry, eg_castle, false, false, true)

-- Use ability
Cmd_Ability(sg_monks, BP_GetAbilityBlueprint("ability_monk_convert"))

-- Stop all actions
Cmd_Stop(sg_mySquads)

-- Build structure
Cmd_BuildStructure(player, sg_villagers, 
    BP_GetEntityBlueprint("building_house_eng"), 
    pos, false)
```

---

## Spawning Units

```lua
-- Get blueprints
local sbp = BP_GetSquadBlueprint("unit_spearman_4_eng")
local ebp = BP_GetEntityBlueprint("building_barracks_eng")

-- Spawn a squad at a marker
local sg = SGroup_CreateIfNotFound("spawned_squad")
UnitEntry_DeploySquads(player1, sg, {{sbp = sbp, numSquads = 3}}, mkr_spawn)

-- Spawn an entity (building)
local eg = EGroup_CreateIfNotFound("spawned_building")
local pos = Marker_GetPosition(mkr_building_site)
local entity = Entity_Create(ebp, player1, pos, false)
Entity_Spawn(entity)
Entity_BuildImmediate(entity)
```

---

## Objectives

```lua
-- Define objective data
OBJ_DefendBase = {
    Type = OT_Primary,
    Title = Loc_FormatText(11198772, "Defend the base"),
    Description = Loc_FormatText(11198773, "Hold against enemy attacks"),
    DataTemplate = DT_PRIMARY_DEFAULT,
    Icon = "icons/objectives/defend",
    TitlePosition = World_Pos(100, 0, 200),
}

-- Register the objective
Obj_Create(player1, "DefendBase", OBJ_DefendBase)

-- Start the objective (visible to player)
Objective_Start(OBJ_DefendBase, true, true)  -- showTitle, playSound

-- Complete or fail
Objective_Complete(OBJ_DefendBase, true, true)
Objective_Fail(OBJ_DefendBase, true, true)

-- Add timer
Objective_StartTimer(OBJ_DefendBase, COUNTER_TimerDecreasing, 300)  -- 5 min countdown
```

---

## Player Resources

```lua
-- Get current resources
local food = Player_GetResource(player1, RT_Food)
local gold = Player_GetResource(player1, RT_Gold)
local wood = Player_GetResource(player1, RT_Wood)
local stone = Player_GetResource(player1, RT_Stone)

-- Add resources
Player_AddResource(player1, RT_Food, 500)
Player_AddResource(player1, RT_Gold, 200)

-- Set resources directly
Player_SetResource(player1, RT_Food, 1000)

-- Check population
local currentPop = Player_GetPopCapCurrent(player1)
local maxPop = Player_GetPopCapMax(player1)
```

---

## Positions & Markers

```lua
-- Create a world position
local pos = World_Pos(100.0, 0.0, 200.0)

-- Get position from marker
local pos = Marker_GetPosition(mkr_spawn_point)

-- Distance check
local dist = World_DistancePointToPoint(pos1, pos2)

-- Proximity check (is any unit near a marker?)
if Prox_AreSquadsNearMarker(sg_mySquads, mkr_target, ANY) then
    -- at least one squad is near the marker
end
```

---

## Game Events

```lua
-- Listen for entity kills
Rule_AddGlobalEvent(OnUnitKilled, GE_EntityKilled)

function OnUnitKilled(context)
    local victim = context.victim           -- entity that died
    local killer = context.killer           -- entity that killed it
    local victimOwner = context.victimOwner -- player who owned the victim
    
    if victimOwner == player1 then
        -- player's unit was killed
    end
end

-- Listen for construction complete
Rule_AddGlobalEvent(OnBuildingFinished, GE_ConstructionComplete)

function OnBuildingFinished(context)
    local entity = context.entity
    local player = context.player
    
    if Entity_IsOfType(entity, "wonder") then
        -- a wonder was completed
    end
end

-- Listen for age-up
Rule_AddGlobalEvent(OnAgeUp, GE_PlayerPhaseUp)

function OnAgeUp(context)
    local player = context.player
    local age = Player_GetCurrentAge(player)
end
```

---

## Modifiers

```lua
-- Increase gather rate for a player
Modify_PlayerResourceRate(player1, RT_Food, 1.5, MUT_Multiplication)

-- Make units invulnerable
SGroup_SetInvulnerable(sg_mySquads, true, 0.0)

-- Lock/unlock production
Player_SetEntityProductionAvailability(player1, ebp_keep, ITEM_LOCKED)
Player_SetEntityProductionAvailability(player1, ebp_keep, ITEM_DEFAULT)

-- Lock/unlock upgrades  
Player_SetUpgradeAvailability(player1, ubp_upgrade, ITEM_LOCKED)
```

---

## Camera Control

```lua
-- Move camera to a position
Camera_MoveTo(pos)

-- Enable/disable camera input
Camera_SetInputEnabled(true)   -- player can control camera
Camera_SetInputEnabled(false)  -- lock camera

-- Cinematic camera pan
Camera_QueueRelativeSplinePanPos(pos1, pos2, duration)
```

---

## Fog of War

```lua
-- Reveal entire map
FOW_RevealAll()

-- Reveal area around a position
FOW_RevealArea(pos, 50, -1)  -- radius 50, infinite duration

-- Enable/disable FOW tint
FOW_EnableTint(true)
```

---

## Common Patterns

### Check & React Loop
```lua
Rule_AddInterval(MonitorBase, 2)  -- check every 2 seconds

function MonitorBase()
    if SGroup_IsEmpty(sg_defenders) then
        -- base has fallen
        Objective_Fail(OBJ_DefendBase)
        Rule_Remove(MonitorBase)
    elseif SGroup_GetAvgHealth(sg_defenders) < 0.3 then
        -- defenders are low — send reinforcements
        SpawnReinforcements()
    end
end
```

### Delayed One-Shot Chain
```lua
function Phase1()
    -- do something
    Rule_AddOneShot(Phase2, 10)  -- 10 seconds later
end

function Phase2()
    -- do next thing
    Rule_AddOneShot(Phase3, 15)  -- 15 seconds later
end
```

### Army System Usage
```lua
local army = Army_Init({
    name = "EnemyArmy",
    player = player2,
    units = {
        {sbp = BP_GetSquadBlueprint("unit_spearman_4_eng"), numSquads = 5},
        {sbp = BP_GetSquadBlueprint("unit_archer_2_eng"), numSquads = 3},
    },
    spawn = mkr_enemy_spawn,
    targets = {mkr_target1, mkr_target2, mkr_player_base},
    targetOrder = ARMY_TARGETING_CYCLE,
    combatRange = 40,
    leashRange = 60,
})
```
