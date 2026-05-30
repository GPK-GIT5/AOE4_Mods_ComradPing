# Common SCAR Patterns — From Official Scripts

Reusable code patterns extracted from Relic's official campaign and gameplay scripts.

---

## 1. Win Condition Pattern (Annihilation)

From `annihilation.scar`:

```lua
Core_RegisterModule("MyWinCondition")

function MyWinCondition_OnInit()
    Rule_AddGlobalEvent(MyWinCondition_OnEntityKilled, GE_EntityKilled)
end

function MyWinCondition_OnGameOver()
    Rule_RemoveGlobalEvent(MyWinCondition_OnEntityKilled)
end

function MyWinCondition_OnEntityKilled(context)
    MyWinCondition_CheckCondition(context.victimOwner)
end

function MyWinCondition_CheckCondition(player)
    if Player_IsAlive(player) then
        local squads = Player_GetSquads(player)
        if SGroup_Count(squads) == 0 then
            Core_SetPlayerDefeated(player, Loc_Empty(), WR_ANNIHILATION)
        end
    end
end
```

---

## 2. Patrol AI Pattern

From `abb_bonus_patrol.scar`:

```lua
function CreatePatrol(player, unitTable, sgroupName, markerStem, numMarkers)
    local patrol = {
        sgroup = SGroup_CreateIfNotFound(sgroupName),
        markers = {},
        currentIndex = 1,
    }
    
    -- Build marker list
    for i = 1, numMarkers do
        table.insert(patrol.markers, Marker_FromName(markerStem .. i, ""))
    end
    
    -- Spawn units at first marker
    UnitEntry_DeploySquads(player, patrol.sgroup, unitTable, patrol.markers[1])
    
    -- Start patrol monitor
    Rule_AddInterval(MonitorPatrol, 2, { patrol = patrol })
end

function MonitorPatrol(context, data)
    local patrol = context.patrol
    
    if SGroup_IsEmpty(patrol.sgroup) then
        Rule_RemoveMe()
        return
    end
    
    -- If arrived at current waypoint, advance to next
    if Prox_AreSquadsNearMarker(patrol.sgroup, patrol.markers[patrol.currentIndex], ANY) then
        patrol.currentIndex = patrol.currentIndex + 1
        if patrol.currentIndex > #patrol.markers then
            patrol.currentIndex = 1
        end
        Cmd_AttackMove(patrol.sgroup, patrol.markers[patrol.currentIndex], false)
    end
end
```

---

## 3. Army Setup Pattern

From `abb_bonus_capture.scar` and `army.scar`:

```lua
function SetupArmy()
    local army = Army_Init({
        name = "AttackForce",
        player = player2,
        units = {
            {sbp = BP_GetSquadBlueprint("unit_spearman_4_abb"), numSquads = 8},
            {sbp = BP_GetSquadBlueprint("unit_archer_2_abb"), numSquads = 4},
            {sbp = BP_GetSquadBlueprint("unit_horseman_2_abb"), numSquads = 3},
        },
        spawn = mkr_army_spawn,
        targets = {mkr_target_town, mkr_target_base},
        targetOrder = ARMY_TARGETING_CYCLE,
        combatRange = 40,
        leashRange = 60,
        attackMove = true,
    })
    return army
end

-- Check army state
function MonitorArmy()
    if Army_IsDead(my_army) then
        -- respawn or handle defeat
    elseif Army_IsComplete(my_army) then
        -- all targets cleared
    end
end

-- Add reinforcements
Army_AddSGroup(my_army, sg_reinforcements)

-- Dissolve army (return units to pool)
local sg_returned = SGroup_CreateIfNotFound("returned_units")
Army_Dissolve(my_army, sg_returned)
```

---

## 4. Objective Lifecycle Pattern

From `objectives.scar` and campaign scripts:

```lua
function RegisterObjectives()
    -- Define the objective
    OBJ_DestroyEnemy = {
        Type = OT_Primary,
        Title = LOC("Destroy the enemy base"),
        Description = LOC("Eliminate all enemy structures"),
        DataTemplate = DT_PRIMARY_DEFAULT,
        Icon = "icons/objectives/destroy",
    }
    
    -- Optional secondary
    OBJ_RescuePrisoners = {
        Type = OT_Secondary, 
        Title = LOC("Rescue prisoners"),
        Description = LOC("Free 3 prisoner groups"),
        DataTemplate = DT_SECONDARY_DEFAULT,
    }
    
    Obj_Create(player1, "DestroyEnemy", OBJ_DestroyEnemy)
    Obj_Create(player1, "RescuePrisoners", OBJ_RescuePrisoners)
end

function StartObjectives()
    Objective_Start(OBJ_DestroyEnemy, true, true)
    Objective_Start(OBJ_RescuePrisoners, false, false)
    
    -- Monitor completion
    Rule_AddInterval(CheckDestroyEnemy, 5)
    Rule_AddInterval(CheckRescuePrisoners, 3)
end

function CheckDestroyEnemy()
    if EGroup_IsEmpty(eg_enemy_buildings) then
        Objective_Complete(OBJ_DestroyEnemy, true, true)
        Rule_Remove(CheckDestroyEnemy)
        -- Trigger victory
    end
end

function CheckRescuePrisoners()
    local rescued = SGroup_Count(sg_rescued_prisoners)
    Obj_SetCounterCount(OBJ_RescuePrisoners, rescued)
    
    if rescued >= 3 then
        Objective_Complete(OBJ_RescuePrisoners, true, true)
        Rule_Remove(CheckRescuePrisoners)
    end
end
```

---

## 5. Wave Spawning Pattern

Common in campaign defense missions:

```lua
local wave_data = {
    {
        delay = 60,
        units = {
            {sbp = BP_GetSquadBlueprint("unit_spearman_4_eng"), numSquads = 6},
            {sbp = BP_GetSquadBlueprint("unit_archer_2_eng"), numSquads = 4},
        }
    },
    {
        delay = 120,
        units = {
            {sbp = BP_GetSquadBlueprint("unit_knight_4_eng"), numSquads = 4},
            {sbp = BP_GetSquadBlueprint("unit_crossbowman_4_eng"), numSquads = 6},
        }
    },
}

local current_wave = 1

function StartWaves()
    Rule_AddOneShot(SpawnWave, wave_data[1].delay)
end

function SpawnWave()
    local wave = wave_data[current_wave]
    local sg = SGroup_CreateIfNotFound("wave_" .. current_wave)
    
    UnitEntry_DeploySquads(player2, sg, wave.units, mkr_wave_spawn)
    Cmd_AttackMove(sg, mkr_player_base, false)
    
    current_wave = current_wave + 1
    if current_wave <= #wave_data then
        Rule_AddOneShot(SpawnWave, wave_data[current_wave].delay)
    end
end
```

---

## 6. Skirmish Army Pattern

From `abb_m1_tyre.scar` — armies that attack and retreat:

```lua
function InitSkirmishArmy()
    skirmish = {
        army = nil,
        retreatHealth = 0.4,
        isRetreating = false,
        reinforceDelay = 60,
    }
    
    skirmish.army = Army_Init({
        name = "Skirmishers",
        player = player2,
        units = GetSkirmishUnits(),
        spawn = mkr_skirmish_spawn,
        targets = {mkr_skirmish_target},
    })
    
    Rule_AddInterval(MonitorSkirmishing, 2)
end

function MonitorSkirmishing()
    if Army_IsDead(skirmish.army) then
        -- Respawn after delay
        Rule_AddOneShot(RespawnSkirmishers, skirmish.reinforceDelay)
        Rule_Remove(MonitorSkirmishing)
        return
    end
    
    local sg = Army_GetSGroup(skirmish.army)
    if SGroup_GetAvgHealth(sg) < skirmish.retreatHealth and not skirmish.isRetreating then
        -- Retreat
        skirmish.isRetreating = true
        Army_Dissolve(skirmish.army, sg)
        Cmd_Move(sg, mkr_retreat_point, false, true)
    end
end
```

---

## 7. Difficulty Scaling Pattern

From multiple campaign scripts:

```lua
function GetDifficultyMultiplier()
    local difficulty = Game_GetSPDifficulty()
    if difficulty == GD_EASY then
        return 0.5
    elseif difficulty == GD_NORMAL then
        return 1.0
    elseif difficulty == GD_HARD then
        return 1.5
    elseif difficulty == GD_EXPERT then
        return 2.0
    end
    return 1.0
end

function ScaleEnemyUnits(baseCount)
    return math.floor(baseCount * GetDifficultyMultiplier())
end

function ModifyHealthByDifficulty(sgroup)
    local mult = GetDifficultyMultiplier()
    SGroup_ForEach(sgroup, function(sgroupid, itemindex, squad)
        local maxHP = Squad_GetHealthMax(squad)
        Squad_SetHealth(squad, maxHP * mult)
    end)
end
```

---

## 8. Event Cue / Notification Pattern

```lua
function ShowEventCue(title, description, icon)
    local eventCue = {
        title = title,
        description = description,  
        sfx = "sfx_ui_event_queue_high_priority_play",
        icon = icon or "icons/events/default",
        style = ECV_Queue,
        lifetime = 15,
    }
    
    UI_CreateEventCueClickable(
        -1,                          -- player (-1 = local)
        eventCue.lifetime,           -- duration
        0,                           -- repeat
        eventCue.title,
        eventCue.description,
        eventCue.icon,
        eventCue.sfx,
        0, 0,                        -- red, green
        255, 255,                    -- blue, alpha
        ECV_Queue,
        nothing                      -- callback
    )
end
```

---

## 9. Construction Monitor Pattern

From `annihilation.scar`:

```lua
Rule_AddGlobalEvent(OnConstructionComplete, GE_ConstructionComplete)

function OnConstructionComplete(context)
    local entity = context.entity
    local player = context.player
    
    -- Track market construction for tribute
    if Entity_IsOfType(entity, "market") then
        player_has_market[Player_GetID(player)] = true
    end
    
    -- Track landmark completion
    if Entity_IsOfType(entity, "landmark") then
        OnLandmarkBuilt(player, entity)
    end
end
```

---

## 10. Diplomacy / Relationship Pattern

```lua
-- Set players as allies
Player_ObserveRelationship(player1, player2, R_ALLY)
Player_ObserveRelationship(player2, player1, R_ALLY)

-- Set as enemies
Player_ObserveRelationship(player1, player3, R_ENEMY)
Player_ObserveRelationship(player3, player1, R_ENEMY)

-- Check relationship
if Player_GetRelationship(player1, player2) == R_ALLY then
    -- they are allies
end

-- Convert AI player to passive
AI_Enable(player2, false)  -- disable AI

-- Gift resources to ally
Player_GiftResource(player1, player2, RT_Food, 200)
```
