# SCAR Engine API — Typed Signatures Reference

Last Updated: 2026-05-14
Source: `scardocs/Essence_ScarFunctions.api` (API date 2026-05-07)

**1976 engine API functions** with typed parameter signatures.
Companion to [scar-api-functions.md](scar-api-functions.md) which provides curated categories and usage patterns.

---

## Namespace Summary

| Namespace | Count |
|-----------|-------|
| `Entity` | 230 |
| `Squad` | 201 |
| `UI` | 125 |
| `Player` | 114 |
| `AIEncounter` | 111 |
| `Misc` | 107 |
| `AI` | 102 |
| `World` | 84 |
| `AIPlayer` | 74 |
| `LocalCommand` | 66 |
| `AIProductionScoring` | 62 |
| `Game` | 62 |
| `BP` | 58 |
| `AISquad` | 48 |
| `Camera` | 47 |
| `Obj` | 44 |
| `SGroup` | 33 |
| `EGroup` | 30 |
| `FOW` | 26 |
| `Sim` | 24 |
| `Event` | 23 |
| `Marker` | 23 |
| `Sound` | 19 |
| `DisplayAdapterDatabase` | 13 |
| `Weapon` | 12 |
| `HintPoint` | 12 |
| `dr` | 10 |
| `Scar` | 10 |
| `MapIcon` | 9 |
| `RenderStats` | 9 |
| `Cursor` | 9 |
| `Territory` | 9 |
| `Terrain` | 8 |
| `Subtitle` | 8 |
| `fx` | 7 |
| `Path` | 7 |
| `Loc` | 7 |
| `ShaderStats` | 7 |
| `Setup` | 6 |
| `LCWatcher` | 6 |
| `PerfStats` | 5 |
| `Modifier` | 5 |
| `Decal` | 5 |
| `RulesProfiler` | 5 |
| `PlayerColour` | 4 |
| `AITactic` | 4 |
| `Formation` | 4 |
| `App` | 4 |
| `Physics` | 3 |
| `ResourceContainer` | 3 |
| `Splat` | 3 |
| `StateTree` | 3 |
| `SynchronizedCommand` | 3 |
| `Vector` | 3 |
| `SBP` | 3 |
| `EBP` | 3 |
| `ActionMarker` | 3 |
| `Debug` | 3 |
| `MemoryStats` | 3 |
| `PBG` | 3 |
| `Enum` | 2 |
| `TerrainHighlight` | 2 |
| `Ghost` | 2 |
| `Taskbar` | 2 |
| `SitRep` | 2 |
| `Loadout` | 2 |
| `Cheat` | 2 |
| `WinWarning` | 2 |
| `network` | 2 |
| `scartype` | 2 |
| `MovieCapture` | 2 |
| `render` | 1 |
| `Vaulting` | 1 |
| `UIWarning` | 1 |
| `AIAbilityEncounter` | 1 |
| `Toggle` | 1 |
| `dca` | 1 |
| `cmdline` | 1 |
| `Team` | 1 |
| `Command` | 1 |
| `Hold` | 1 |
| `inv` | 1 |
| `statgraph` | 1 |
| `IsEconomyClassStructure` | 1 |
| `lockstep` | 1 |
| `AIStateTree` | 1 |
| `IsSecuringStructure` | 1 |
| `IsSecuringStructurePlacedOnPoint` | 1 |
| `IsStructure` | 1 |
| `AllMarkers` | 1 |
| `SquadGroup` | 1 |

---

## ActionMarker (3 functions)

### `ActionMarker_SetVisible`
```lua
ActionMarker_SetVisible(String name, Boolean visible)
```
Set whether or not an action marker is visible.

### `ActionMarker_StartAction`
```lua
ActionMarker_StartAction(String name)
```
Start the given action marker's FX.

### `ActionMarker_StopAction`
```lua
ActionMarker_StopAction(String name)
```
Stop the given action marker's FX.

## AI (102 functions)

### `AI_AddHeavyCoverEbpOccupancyOverride`
```lua
AI_AddHeavyCoverEbpOccupancyOverride(PlayerID pPlayer, ScarEntityPBG ebp, Integer occupancyOverride)
```
overrides the Heavy Cover Occupancy for the passed EBP

### `AI_AddPrefab`
```lua
AI_AddPrefab(PlayerID player, String name, String behaviourName, Real radius, Integer minDifficulty, Integer maxDifficulty, Boolean canReassign, Boolean active)
```
Adds a prefab to the AIPrefab system. Target must be set up in a follow up call with returned ID

### `AI_AreThereAnyDeepwaterFish`
```lua
AI_AreThereAnyDeepwaterFish(PlayerID aiPlayer)
```
Returns whether or not there are any deepwater fish deposits on the map.

### `AI_CacheCombatFeatureTrainingData`
```lua
AI_CacheCombatFeatureTrainingData(Integer conflictID, PlayerID playerA, PlayerID playerB)
```
Log the combat result features of all squads owned by a player for a given conflict

### `AI_CalculateCombatFitnessEstimate`
```lua
AI_CalculateCombatFitnessEstimate(SGroupID teamASquads, EGroupID teamAEntities, PropertyBagGroup teamAPBGs, SGroupID teamBSquads, EGroupID teamBEntities, PropertyBagGroup teamBPBGs, PlayerID aiPlayerA, PlayerID playerB, Boolean playerAIsAttacker)
```
Get combat fitness estimate. Return value will be between 1.0 and 0.0. 1.0 means teamA wins outright, 0.0 means teamB wins outright.

### `AI_CanEntityCauseSuppression`
```lua
AI_CanEntityCauseSuppression(PlayerID aiPlayer, EntityID entity)
```
Checks if this entity can cause suppression

### `AI_CanLoadSquadAndAttackCurrentTarget`
```lua
AI_CanLoadSquadAndAttackCurrentTarget(EntityID entity, SquadID squad, Boolean bCheckSquadState, Boolean bOverload)
```
Check if the entity can load squad and shoot its target after loading (This function should only be called by AI)

### `AI_CanSquadCauseSuppression`
```lua
AI_CanSquadCauseSuppression(PlayerID aiPlayer, SquadID pSquad)
```
Checks if this squad can cause suppression

### `AI_CanSquadDecrew`
```lua
AI_CanSquadDecrew(SquadID pDriverSquad, EntityID pDecrewTargetEntity)
```
Checks if this squad can decrew the entity

### `AI_ClearCombatTrainingCacheEntry`
```lua
AI_ClearCombatTrainingCacheEntry(Integer conflictID)
```
Clear a combat entry from the cache, typically done instead of logging it

### `AI_ClearPBGRepairPriority`
```lua
AI_ClearPBGRepairPriority(PlayerID pPlayer, String pbgShortname)
```
This clears the repair priority value for a given squad or building PBG.

### `AI_ClearPrefabAIIntents`
```lua
AI_ClearPrefabAIIntents(UniqueID prefabId, PlayerID player)
```
Clear all intents associated with this AIPrefab

### `AI_CombatFitnessCharacterizesSquad`
```lua
AI_CombatFitnessCharacterizesSquad(PlayerID player, PropertyBagGroup squadPBG)
```
Returns true if the configured input feature calculators characterizes this squad

### `AI_CombatFitnessGetDefensiveUpgradesForStructureArchetypeMember`
```lua
AI_CombatFitnessGetDefensiveUpgradesForStructureArchetypeMember(PropertyBagGroup memberPBG)
```
Returns the defensive upgrades for this structure archetype member

### `AI_CombatFitnessGetHealerPBGs`
```lua
AI_CombatFitnessGetHealerPBGs()
```
Returns healer feature option pbgs

### `AI_CombatFitnessGetOffensiveUpgradesForStructureArchetypeMember`
```lua
AI_CombatFitnessGetOffensiveUpgradesForStructureArchetypeMember(PropertyBagGroup memberPBG)
```
Returns the offensive upgrades for this structure archetype member

### `AI_CombatFitnessGetPlayerUpgrades`
```lua
AI_CombatFitnessGetPlayerUpgrades()
```
Returns the player upgrades configured in the player upgrade input calculator

### `AI_CombatFitnessGetSquadArchetypeNames`
```lua
AI_CombatFitnessGetSquadArchetypeNames()
```
Returns squad pbgs for all squad archetypes

### `AI_CombatFitnessGetSquadArchetypePBGs`
```lua
AI_CombatFitnessGetSquadArchetypePBGs(String archtypeNameStr)
```
Returns squad pbgs for a given archetype (assuming that archetype is composed of squad pbgs)

### `AI_CombatFitnessGetStructureArchetypePBGs`
```lua
AI_CombatFitnessGetStructureArchetypePBGs(String archtypeNameStr)
```
Returns entity pbgs for a given archetype (assuming that archetype is composed of entity pbgs)

### `AI_ConvertToSimEntity`
```lua
AI_ConvertToSimEntity(EntityID pAIEntity)
```
Converts an AIEntity into an Entity

### `AI_ConvertToSimPlayer`
```lua
AI_ConvertToSimPlayer(PlayerID pAIPlayer)
```
Converts an AIPlayer into a Player

### `AI_ConvertToSimSquad`
```lua
AI_ConvertToSimSquad(SquadID pAISquad)
```
Converts an AISquad into a Squad

### `AI_CreateAICombatFitnessLogs`
```lua
AI_CreateAICombatFitnessLogs()
```
Create the combat feature logs in the game log directory

### `AI_CreateEncounter`
```lua
AI_CreateEncounter(PlayerID pPlayer, Integer encounterType)
```
Create a new encounter for player

### `AI_DebugAttackEncounterPositionScoringEnable`
```lua
AI_DebugAttackEncounterPositionScoringEnable(Boolean enable)
```
Enables/disables debugging of AI Attack Encounter Encounter Position Scoring

### `AI_DebugAttackEncounterPositionScoringIsEnabled`
```lua
AI_DebugAttackEncounterPositionScoringIsEnabled()
```
Returns true if AI Attack Encounter Position Scoring is enabled

### `AI_DebugLogGroupCombatRatings`
```lua
AI_DebugLogGroupCombatRatings(SGroupID sgroup, EGroupID egroup, PlayerID player)
```
Prints detailed rating debug info in the AILog for all squads and entities in the groups

### `AI_DebugLogPBGCombatRatings`
```lua
AI_DebugLogPBGCombatRatings(PropertyBagGroup pbgList, PlayerID player)
```
Prints detailed rating debug info in the AILog for all the PBGs in the list

### `AI_DebugLuaEnable`
```lua
AI_DebugLuaEnable(Boolean enable)
```
Enables/disables AI Lua Debugging

### `AI_DebugLuaIsEnabled`
```lua
AI_DebugLuaIsEnabled()
```
Returns true if AI Lua Debugging is enabled

### `AI_DebugRatingEnable`
```lua
AI_DebugRatingEnable(Boolean enable)
```
Enables/disables AI Construction Debugging

### `AI_DebugRatingIsEnabled`
```lua
AI_DebugRatingIsEnabled()
```
Returns true if AI Construction Debugging is enabled

### `AI_DebugRenderAllTaskChildrenEnable`
```lua
AI_DebugRenderAllTaskChildrenEnable(Boolean enable)
```
Enables/disables AI Rendering of All Task Children

### `AI_DebugRenderAllTaskChildrenIsEnabled`
```lua
AI_DebugRenderAllTaskChildrenIsEnabled()
```
Returns true if AI Rendering of All Task Children is enabled

### `AI_DebugSkirmishForwardDeployEnable`
```lua
AI_DebugSkirmishForwardDeployEnable(Boolean enable)
```
Enables/disables AI Skirmish ForwardDeploy Debugging

### `AI_DebugSkirmishForwardDeployIsEnabled`
```lua
AI_DebugSkirmishForwardDeployIsEnabled()
```
Returns true if AI Skirmish ForwardDeploy Debugging is enabled

### `AI_DisableAllEconomyOverrides`
```lua
AI_DisableAllEconomyOverrides(PlayerID pPlayer)
```
Disable all of the economy overrides for the AI player

### `AI_DoString`
```lua
AI_DoString(Integer playerID, String string)
```
Execute a string as lua in the given player's AI LuaConfig

### `AI_DoWeHaveWaterLanes`
```lua
AI_DoWeHaveWaterLanes(PlayerID aiPlayer)
```
Returns whether or not we are on a map with water lanes.

### `AI_Enable`
```lua
AI_Enable(PlayerID pPlayer, Boolean enable)
```
Enables or Disables an AI player

### `AI_EnableAll`
```lua
AI_EnableAll(Boolean enable)
```
Enables or Disables all AI players

### `AI_EnableEconomyOverride`
```lua
AI_EnableEconomyOverride(PlayerID pPlayer, String overrideName, Boolean enable)
```
Enable or disable the economy override for the AI player

### `AI_FindAISquadByID`
```lua
AI_FindAISquadByID(PlayerID pPlayer, Integer UID)
```
Finds an AISquad owned by the specified player

### `AI_FindBestProducibleEntityPBGforEntityTypes`
```lua
AI_FindBestProducibleEntityPBGforEntityTypes(PlayerID player, String entityTypeNames)
```
Find the current best producible Entity PBG corresponding to the specified Entity Types.

### `AI_FindBestProducibleSquadPBGforSquadTypes`
```lua
AI_FindBestProducibleSquadPBGforSquadTypes(PlayerID player, String squadTypeNames)
```
Find the current best producible Squad PBG corresponding to the specified Squad Types.

### `AI_FindClosestOpenPositionForAbility`
```lua
AI_FindClosestOpenPositionForAbility(ConstTargetHandle caster, PropertyBagGroup pAbilityPBG, Position posIn)
```
Find the closest open position from a given position for a given ability blueprint

### `AI_FindClosestOpenPositionForAbilityWithinRange`
```lua
AI_FindClosestOpenPositionForAbilityWithinRange(ConstTargetHandle caster, PropertyBagGroup pAbilityPBG, Position posIn, Integer minDist, Integer maxDist)
```
Find the closest open position from a given position and ability blueprint, taking into account a min

### `AI_FindClosestOpenPositionForStructure`
```lua
AI_FindClosestOpenPositionForStructure(PlayerID aiPlayer, PropertyBagGroup pEntityPBG, Position posIn)
```
Find the closest open position from a given position for a given Entity blueprint

### `AI_FindConstructionLocation`
```lua
AI_FindConstructionLocation(PlayerID pPlayer, PropertyBagGroup pPbg, Position position)
```
Find a valid construction location for a pbg, using a spiral search. Returns INVALID_POS if it fails.

### `AI_GetAbilityMaxNumTargets`
```lua
AI_GetAbilityMaxNumTargets(ScarAbilityPBG ability)
```
Returns the maximum number of targets for the given ability, or -1 if the ability is invalid.

### `AI_GetAllMilitaryPointsOfType`
```lua
AI_GetAllMilitaryPointsOfType(PlayerID pAIPlayer, AIMilitaryTargetType type, EGroupID egroup)
```
Stores entities of a specific type owned by a player in an egroup parameter

### `AI_GetAndReserveNextTaskID`
```lua
AI_GetAndReserveNextTaskID(PlayerID player)
```
Get and reserve the next available AITaskID (which can be used to create an AIEncounter from SCAR).

### `AI_GetAnySquadCombatTarget`
```lua
AI_GetAnySquadCombatTarget(SquadID pSquad)
```
Returns the current squad target for the given squad (null if no target, or target is non-squad entity)

### `AI_GetDebugAIPlayerID`
```lua
AI_GetDebugAIPlayerID()
```
Get current AI player ID

### `AI_GetDifficulty`
```lua
AI_GetDifficulty(PlayerID pPlayer)
```
Gets the difficulty level of this AI player

### `AI_GetPersonality`
```lua
AI_GetPersonality(PlayerID pPlayer)
```
Get the personality name of this AI player

### `AI_GetPersonalityLuaFileName`
```lua
AI_GetPersonalityLuaFileName(PlayerID pPlayer)
```
Get the personality lua file name of this AI player

### `AI_GetWaterLanesCount`
```lua
AI_GetWaterLanesCount()
```
Returns the amount of water lanes on the map.

### `AI_IsAIPlayer`
```lua
AI_IsAIPlayer(PlayerID pPlayer)
```
Returns true if player is an AI player

### `AI_IsAITargetable`
```lua
AI_IsAITargetable(PlayerID pPlayer)
```
Returns true if player is an AIPlayer and is targetable by other AI players.

### `AI_IsDebugDisplay`
```lua
AI_IsDebugDisplay(PlayerID pPlayer)
```
Checks if the AI debug display is enabled

### `AI_IsEnabled`
```lua
AI_IsEnabled(PlayerID pPlayer)
```
Returns true if player is a AIPlayer and is enabled

### `AI_IsLocalAIPlayer`
```lua
AI_IsLocalAIPlayer(PlayerID pPlayer)
```
Returns true if the player is an AIPlayer running on the local machine

### `AI_IsPositionNearInSupplySector`
```lua
AI_IsPositionNearInSupplySector(PlayerID aiPlayer, Position position)
```
Returns true when position in a sector that is adjacent to an in-supply sector

### `AI_IsSquadValid`
```lua
AI_IsSquadValid(SquadID pSquadAI)
```
Checks if this is a valid AISquad

### `AI_LockEntity`
```lua
AI_LockEntity(PlayerID pPlayer, EntityID pEntity)
```
Locks the entity and disables its tactics (if any) and the AI will no longer use this object

### `AI_LockSquad`
```lua
AI_LockSquad(PlayerID pPlayer, SquadID pSquad)
```
Locks the squad and disables its tactics (if any) and the AI will no longer use this object

### `AI_LockSquads`
```lua
AI_LockSquads(PlayerID pPlayer, SGroupID squads)
```
Locks the squads and disables its tactics (if any) and the AI will no longer use these objects

### `AI_LogCombatTrainingData`
```lua
AI_LogCombatTrainingData(Integer conflictID, PlayerID playerA, PlayerID playerB, Real score)
```
Log the combat input features of all squads owned by two players for a given conflict

### `AI_PauseCurrentTasks`
```lua
AI_PauseCurrentTasks(PlayerID pPlayer, Boolean pause)
```
Pauses or unpauses currently running tasks

### `AI_PlayerAddExclusionArea`
```lua
AI_PlayerAddExclusionArea(PlayerID pPlayer, Position position, Real noPathRadius, Real noTargetRadius)
```
Add an Exclusion area to the AI Player

### `AI_PlayerRemoveExclusionArea`
```lua
AI_PlayerRemoveExclusionArea(PlayerID pPlayer, Position position, Real noPathRadius, Real noTargetRadius)
```
Remove the Exclusion area from the AI Player

### `AI_ProductionGroupMaxNum`
```lua
AI_ProductionGroupMaxNum(PlayerID aiPlayer, ProductionGroupID prodGroupID)
```
Returns the count of specified PBG that the AI player is observing.

### `AI_ProductionGroupMaxNumProduced`
```lua
AI_ProductionGroupMaxNumProduced(PlayerID aiPlayer, ProductionGroupID prodGroupID)
```
Returns the count of specified PBG that the AI player is observing.

### `AI_ProductionGroupPBGIndex`
```lua
AI_ProductionGroupPBGIndex(PlayerID aiPlayer, ProductionGroupID prodGroupID, PropertyBagGroup pbg)
```
Returns the index of the provided PBG within its production group.

### `AI_PushPrefabAIIntent`
```lua
AI_PushPrefabAIIntent(UniqueID prefabId, PlayerID player, String aiPrefabIntentBagName)
```
Push an ai intent to an existing AIPrefab. Requires an ai_prefab_intent pbg name

### `AI_RemoveCapturePointHighPriority`
```lua
AI_RemoveCapturePointHighPriority(PlayerID pPlayer, EntityID pEntity)
```
This clears the importance bonus on this capture point

### `AI_RestartSCAR`
```lua
AI_RestartSCAR(PlayerID pPlayer)
```
Restarts the AI

### `AI_RestoreDefaultPersonalitySettings`
```lua
AI_RestoreDefaultPersonalitySettings(PlayerID pPlayer)
```
Restores the default personality and difficulty settings of this AI player

### `AI_SetAISquadCombatRangePolicyTaskOverride`
```lua
AI_SetAISquadCombatRangePolicyTaskOverride(SquadID pSquadAI, CombatRangePolicy policy)
```
Set Combat Range Policy for the AISquad, overrides the one set at Encounter/task level

### `AI_SetAITargetable`
```lua
AI_SetAITargetable(PlayerID pPlayer, Boolean targetable)
```
Enables or Disables an AI player to be targetable by other AI players.

### `AI_SetCapturePointAsHighPriority`
```lua
AI_SetCapturePointAsHighPriority(PlayerID pPlayer, EntityID pEntity)
```
This sets importance bonus of the given capture point

### `AI_SetDebugDisplay`
```lua
AI_SetDebugDisplay(PlayerID pPlayer, Boolean enable)
```
Enable or disable the AI debug display

### `AI_SetDifficulty`
```lua
AI_SetDifficulty(PlayerID pPlayer, Integer difficultyLevel)
```
Set the difficulty level of this AI player

### `AI_SetPBGRepairPriority`
```lua
AI_SetPBGRepairPriority(PlayerID pPlayer, String pbgShortname, Real priorityValue)
```
This sets the repair priority value for a given squad or building PBG.

### `AI_SetPersonality`
```lua
AI_SetPersonality(PlayerID pPlayer, String personalityName)
```
Set the personality name of this AI player

### `AI_SetPrefabActive`
```lua
AI_SetPrefabActive(UniqueID prefabId, PlayerID player, Boolean active)
```
Set the active status of an existing AIPrefab

### `AI_SetPrefabCanReassign`
```lua
AI_SetPrefabCanReassign(UniqueID prefabId, PlayerID player, Boolean canReassign)
```
Set the can_reassign state of an existing AIPrefab

### `AI_SetPrefabSelection_SGroup`
```lua
AI_SetPrefabSelection_SGroup(UniqueID prefabId, PlayerID player, SGroupID squads)
```
Set the squad selection of an existing AIPrefab by SGROUP

### `AI_SetPrefabTarget_EGroup`
```lua
AI_SetPrefabTarget_EGroup(UniqueID prefabId, PlayerID player, EGroupID entities)
```
Set the target of an existing AIPrefab by EGROUP

### `AI_SetPrefabTarget_Position`
```lua
AI_SetPrefabTarget_Position(UniqueID prefabId, PlayerID player, Position position)
```
Set the target of an existing AIPrefab by Position

### `AI_SetPrefabTarget_SGroup`
```lua
AI_SetPrefabTarget_SGroup(UniqueID prefabId, PlayerID player, SGroupID squads)
```
Set the target of an existing AIPrefab by SGROUP

### `AI_SetPrefabTarget_Waypoints`
```lua
AI_SetPrefabTarget_Waypoints(UniqueID prefabId, PlayerID player, String waypointName)
```
Set the target of an existing AIPrefab via waypoints

### `AI_SetResourceIncomeDesire`
```lua
AI_SetResourceIncomeDesire(PlayerID player, Integer resourceType, Real desiredIncome)
```
Set an AI Player's desired income of specified resource type at specified value. This will affect the AI resource gathering, building construction and production priority in trying to achieve the specified resource income.

### `AI_ToggleDebugAIPlayer`
```lua
AI_ToggleDebugAIPlayer()
```
Set current debug AI player to the next AI player

### `AI_ToggleDebugDisplay`
```lua
AI_ToggleDebugDisplay(PlayerID pPlayer)
```
Toggles the AI debug display

### `AI_UnlockAll`
```lua
AI_UnlockAll(PlayerID pPlayer)
```
Unlocks all designer locked squads for player

### `AI_UnlockEntity`
```lua
AI_UnlockEntity(PlayerID pPlayer, EntityID pEntity)
```
Unlocks this entity so that AI can use it again

### `AI_UnlockSquad`
```lua
AI_UnlockSquad(PlayerID pPlayer, SquadID pSquad)
```
Unlocks the given squad so the AI can use it again

### `AI_UnlockSquads`
```lua
AI_UnlockSquads(PlayerID pPlayer, SGroupID squads)
```
Locks the squads and disables its tactics (if any) and the AI will no longer use these objects

### `AI_UpdateStatics`
```lua
AI_UpdateStatics(PlayerID pPlayer)
```
Re-updates the AI in regards to all the static objects in the world (if SCAR creates new strategic points dynamically this will need to be called)

## AIAbilityEncounter (1 functions)

### `AIAbilityEncounter_AbilityGuidance_SetAbilityPBG`
```lua
AIAbilityEncounter_AbilityGuidance_SetAbilityPBG(AIEncounterID pEncounter, PropertyBagGroup abilityPBG)
```
Set ability for ability encounter

## AIEncounter (111 functions)

### `AIEncounter_Cancel`
```lua
AIEncounter_Cancel(AIEncounterID pEncounter)
```
Ends the encounter and deletes it.

### `AIEncounter_CombatGuidance_AddForcedCombatTargetEGroup`
```lua
AIEncounter_CombatGuidance_AddForcedCombatTargetEGroup(AIEncounterID pEncounter, EGroupID egroup)
```
add the EGroup to the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_AddForcedCombatTargetEntity`
```lua
AIEncounter_CombatGuidance_AddForcedCombatTargetEntity(AIEncounterID pEncounter, EntityID pEntity)
```
add the Entity to the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_AddForcedCombatTargetSGroup`
```lua
AIEncounter_CombatGuidance_AddForcedCombatTargetSGroup(AIEncounterID pEncounter, SGroupID sgroup)
```
add the SGroup to the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_AddForcedCombatTargetSquad`
```lua
AIEncounter_CombatGuidance_AddForcedCombatTargetSquad(AIEncounterID pEncounter, SquadID pSquad)
```
add the Squad to the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_ClearForcedCombatTargets`
```lua
AIEncounter_CombatGuidance_ClearForcedCombatTargets(AIEncounterID pEncounter)
```
Clear the encounter Forced Combat Targets

### `AIEncounter_CombatGuidance_EnableCombatGarrison`
```lua
AIEncounter_CombatGuidance_EnableCombatGarrison(AIEncounterID pEncounter, Boolean enable)
```
Enables/disables squads in combat garrisoning.

### `AIEncounter_CombatGuidance_RemoveForcedCombatTargetEGroup`
```lua
AIEncounter_CombatGuidance_RemoveForcedCombatTargetEGroup(AIEncounterID pEncounter, EGroupID egroup)
```
remove the EGroup from the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_RemoveForcedCombatTargetEntity`
```lua
AIEncounter_CombatGuidance_RemoveForcedCombatTargetEntity(AIEncounterID pEncounter, EntityID pEntity)
```
remove the Entity from the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_RemoveForcedCombatTargetSGroup`
```lua
AIEncounter_CombatGuidance_RemoveForcedCombatTargetSGroup(AIEncounterID pEncounter, SGroupID sgroup)
```
remove the SGroup from the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_RemoveForcedCombatTargetSquad`
```lua
AIEncounter_CombatGuidance_RemoveForcedCombatTargetSquad(AIEncounterID pEncounter, SquadID pSquad)
```
remove the Squad from the Encounter forced target list. NOTE: supported only by the Attack Encounter

### `AIEncounter_CombatGuidance_SetCombatRangePolicy`
```lua
AIEncounter_CombatGuidance_SetCombatRangePolicy(AIEncounterID pEncounter, CombatRangePolicy policy)
```
Set Combat Range Policy for the encounter

### `AIEncounter_CombatGuidance_SetSpreadAttackers`
```lua
AIEncounter_CombatGuidance_SetSpreadAttackers(AIEncounterID pEncounter, Boolean value)
```
Set if the Attack Encounter should spread the attackers on multiple targets

### `AIEncounter_DefenseGuidance_EnableIdleGarrison`
```lua
AIEncounter_DefenseGuidance_EnableIdleGarrison(AIEncounterID pEncounter, Boolean enable)
```
Enables/disables idle squads garrisoning.

### `AIEncounter_EngagementGuidance_AddEncouterSetupLocation`
```lua
AIEncounter_EngagementGuidance_AddEncouterSetupLocation(AIEncounterID pEncounter, Position pos, Position facingDir)
```
Adds a setup location and facing direction for this encounter not specifically assigned to any squad

### `AIEncounter_EngagementGuidance_ClearSetupLocationOverrides`
```lua
AIEncounter_EngagementGuidance_ClearSetupLocationOverrides(AIEncounterID pEncounter)
```
clears the encounter setup locations

### `AIEncounter_EngagementGuidance_EnableAggressiveEngagementMove`
```lua
AIEncounter_EngagementGuidance_EnableAggressiveEngagementMove(AIEncounterID pEncounter, Boolean enable)
```
Enable / disable aggressive move into engagement area

### `AIEncounter_EngagementGuidance_EnableConstruction`
```lua
AIEncounter_EngagementGuidance_EnableConstruction(AIEncounterID pEncounter, Boolean enable)
```
Enable construction in Town Life encounters

### `AIEncounter_EngagementGuidance_EnableSetupLocations`
```lua
AIEncounter_EngagementGuidance_EnableSetupLocations(AIEncounterID pEncounter, Boolean enable)
```
Enable setup locations in attack and defend encounters

### `AIEncounter_EngagementGuidance_SetAllowResourceGatheringOutsideLeash`
```lua
AIEncounter_EngagementGuidance_SetAllowResourceGatheringOutsideLeash(AIEncounterID pEncounter, Boolean allowOutsideLeash)
```
Sets a TownLife Encounter whether to allow resource gathering from deposits outside of Encounter leash.

### `AIEncounter_EngagementGuidance_SetAllowReturnToPreviousStages`
```lua
AIEncounter_EngagementGuidance_SetAllowReturnToPreviousStages(AIEncounterID pEncounter, Boolean enable)
```
Enable encounter to return to previous stages if they fail to meet conditions for current stage.

### `AIEncounter_EngagementGuidance_SetCoordinatedSetup`
```lua
AIEncounter_EngagementGuidance_SetCoordinatedSetup(AIEncounterID pEncounter, Boolean enable)
```
Enable coordinated arrival in attack encounters

### `AIEncounter_EngagementGuidance_SetEnableSniperReactions`
```lua
AIEncounter_EngagementGuidance_SetEnableSniperReactions(AIEncounterID pEncounter, Boolean enable)
```
Enables/disables sniper reactions

### `AIEncounter_EngagementGuidance_SetEnableSubEngagementAreas`
```lua
AIEncounter_EngagementGuidance_SetEnableSubEngagementAreas(AIEncounterID pEncounter, Boolean enable)
```
Enables/disables SubEngagementAreas

### `AIEncounter_EngagementGuidance_SetMaxEngagementTime`
```lua
AIEncounter_EngagementGuidance_SetMaxEngagementTime(AIEncounterID pEncounter, Real seconds)
```
Sets max time, in seconds, to accomplish encounter, once the target is engaged.

### `AIEncounter_EngagementGuidance_SetMaxIdleTime`
```lua
AIEncounter_EngagementGuidance_SetMaxIdleTime(AIEncounterID pEncounter, Real seconds)
```
Sets max time, in seconds, to remain idle at encounter target, once engaged.

### `AIEncounter_EngagementGuidance_SetSetupLocationSbpPriority`
```lua
AIEncounter_EngagementGuidance_SetSetupLocationSbpPriority(AIEncounterID pEncounter, ScarSquadPBG sbp, Real priority)
```
set the sbp setup location priority override

### `AIEncounter_EngagementGuidance_SetSquadSetupLocation`
```lua
AIEncounter_EngagementGuidance_SetSquadSetupLocation(AIEncounterID pEncounter, SquadID pSquad, Position pos, Position facingDir)
```
set the squad setup location and facing direction

### `AIEncounter_FallbackGuidance_EnableReinforceDuringCombat`
```lua
AIEncounter_FallbackGuidance_EnableReinforceDuringCombat(AIEncounterID pEncounter, Boolean value)
```
Enable/Disable Reinforce during combat

### `AIEncounter_FallbackGuidance_SetEntitiesRemainingThreshold`
```lua
AIEncounter_FallbackGuidance_SetEntitiesRemainingThreshold(AIEncounterID pEncounter, Real value)
```
Set entities remaining threshold of encounter [-1 to N] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetFallbackCapacityPercentage`
```lua
AIEncounter_FallbackGuidance_SetFallbackCapacityPercentage(AIEncounterID pEncounter, Real value)
```
Set capacity threshold [-1 to 1] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetFallbackCombatRating`
```lua
AIEncounter_FallbackGuidance_SetFallbackCombatRating(AIEncounterID pEncounter, Real value)
```
Set combat rating threshold of area [0.0 to 1.0] to fallback at. (0.0 disables)

### `AIEncounter_FallbackGuidance_SetFallbackSquadHealthPercentage`
```lua
AIEncounter_FallbackGuidance_SetFallbackSquadHealthPercentage(AIEncounterID pEncounter, Real fallbackStartValue, Real fallbackEndValue)
```
Set Squad health threshold [-1 to 1] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetFallbackSquadShieldPercentage`
```lua
AIEncounter_FallbackGuidance_SetFallbackSquadShieldPercentage(AIEncounterID pEncounter, Real fallbackStartValue, Real fallbackEndValue)
```
Set Squad Shield threshold [-1 to 1] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetFallbackVehicleHealthPercentage`
```lua
AIEncounter_FallbackGuidance_SetFallbackVehicleHealthPercentage(AIEncounterID pEncounter, Real fallbackStartValue, Real fallbackEndValue)
```
Set Vehicle health threshold [-1 to 1] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetGlobalFallbackPercentage`
```lua
AIEncounter_FallbackGuidance_SetGlobalFallbackPercentage(AIEncounterID pEncounter, Real value)
```
Set global fallback threshold (negative for individual squad).

### `AIEncounter_FallbackGuidance_SetGlobalFallbackRetreat`
```lua
AIEncounter_FallbackGuidance_SetGlobalFallbackRetreat(AIEncounterID pEncounter, Boolean value)
```
Set global retreat type (true for retreat; false for fallback).

### `AIEncounter_FallbackGuidance_SetReinforceHealthPercentage`
```lua
AIEncounter_FallbackGuidance_SetReinforceHealthPercentage(AIEncounterID pEncounter, Real value)
```
Set the Reinforce Health Percentage [-1 to 1] (negative disables retreat)

### `AIEncounter_FallbackGuidance_SetReinforceMaxDistance`
```lua
AIEncounter_FallbackGuidance_SetReinforceMaxDistance(AIEncounterID pEncounter, Real value)
```
Set the Max Reinforce Distance (negative value: no distance constrain)

### `AIEncounter_FallbackGuidance_SetReinforceMinHealthRatioToReachReinforcePoint`
```lua
AIEncounter_FallbackGuidance_SetReinforceMinHealthRatioToReachReinforcePoint(AIEncounterID pEncounter, Real value)
```
Set the Min Health Ratio Required To Reach Reinforce Point [0.0, 1.0] (negative value: no constrain)

### `AIEncounter_FallbackGuidance_SetRetreatCapacityPercentage`
```lua
AIEncounter_FallbackGuidance_SetRetreatCapacityPercentage(AIEncounterID pEncounter, Real value)
```
Set combat rating threshold of area [-1 to 1] to fallback at. (negative disables)

### `AIEncounter_FallbackGuidance_SetRetreatCombatRating`
```lua
AIEncounter_FallbackGuidance_SetRetreatCombatRating(AIEncounterID pEncounter, Real value)
```
Set combat rating threshold of area [0.0 to 1.0] to retreat at. (0.0 disables)

### `AIEncounter_FallbackGuidance_SetRetreatHealthPercentage`
```lua
AIEncounter_FallbackGuidance_SetRetreatHealthPercentage(AIEncounterID pEncounter, Real value)
```
Set retreat health threshold of area [-1 to 1] (negative disables)

### `AIEncounter_FallbackGuidance_SetTargetPosition`
```lua
AIEncounter_FallbackGuidance_SetTargetPosition(AIEncounterID pEncounter, Position pos)
```
Set fallback target.

### `AIEncounter_ForceComplete`
```lua
AIEncounter_ForceComplete(AIEncounterID pEncounter)
```
Asks the encounter to terminate in its next update (allows PhaseEncounter to set its exit info)

### `AIEncounter_FormationGuidance_SetFormUpAtBuildingOfType`
```lua
AIEncounter_FormationGuidance_SetFormUpAtBuildingOfType(AIEncounterID encounter, String unitTypeList)
```
Set formup type for formation encounter to be at building of type from AE tuning list (must set before triggering)

### `AIEncounter_FormationGuidance_SetFormUpAtEntityTarget`
```lua
AIEncounter_FormationGuidance_SetFormUpAtEntityTarget(AIEncounterID encounter, EntityID entity)
```
Set formup entity for formation encounter (must set before triggering)

### `AIEncounter_FormationGuidance_SetFormUpAtPositionTarget`
```lua
AIEncounter_FormationGuidance_SetFormUpAtPositionTarget(AIEncounterID encounter, Position postion)
```
Set formup position for formation encounter (must set before triggering)

### `AIEncounter_FormationGuidance_SetFormUpAtSquadAverage`
```lua
AIEncounter_FormationGuidance_SetFormUpAtSquadAverage(AIEncounterID encounter)
```
Set formup position for formation encounter at the average of current squad positions (must set before triggering)

### `AIEncounter_FormationGuidance_SetFormUpAtTimeOutParams`
```lua
AIEncounter_FormationGuidance_SetFormUpAtTimeOutParams(AIEncounterID encounter, Real timeoutSeconds, Real requiredSquadsPercent)
```
Set formup position timeout and % squads that must arrive or else it will fail.  Setting zero for timeout means infinite

### `AIEncounter_FormationPhase_GetEndPosition`
```lua
AIEncounter_FormationPhase_GetEndPosition(AITaskID encounterID)
```
Get the average position of squads of this finished formation phase encounter (may be the same as target if successful).  You should call AIEncounter_FormationPhase_HasValidExitInfo before this to avoid an error

### `AIEncounter_FormationPhase_GetEndReason`
```lua
AIEncounter_FormationPhase_GetEndReason(AITaskID encounterID)
```
Get the end position of this finished formation phase move encounter (may be the same as target if successful)

### `AIEncounter_FormationPhase_GetEnemiesAtEnd`
```lua
AIEncounter_FormationPhase_GetEnemiesAtEnd(AITaskID encounterID, SGroupID enemySquads, EGroupID enemyBuildings)
```
Get Groups containing the enemies encountered by this formation phase encounter (encounter must have completed) false indicates the exit info was not available for this encounter

### `AIEncounter_FormationPhase_GetExitCombatFitnessResult`
```lua
AIEncounter_FormationPhase_GetExitCombatFitnessResult(AITaskID encounterID)
```
Get the combat fitness result for a finished phase encounter, will only be valid for exit states CombatFitnessThreshold or WasAttacked.  -1.0f means invalid.

### `AIEncounter_FormationPhase_GetSquadsAvailableAtEnd`
```lua
AIEncounter_FormationPhase_GetSquadsAvailableAtEnd(AITaskID encounterID, SGroupID squadsAvailable, SGroupID squadsUnavailable)
```
Get SGRoups containing the squads who made it to the destination of a formation phase move encounter and those who didn't (encounter must have completed) false indicates the exit info was not available for this encounter

### `AIEncounter_FormationPhase_HasValidExitInfo`
```lua
AIEncounter_FormationPhase_HasValidExitInfo(AITaskID encounterID)
```
Query if there is valid exit info for this encounter (will only return true for phase encounters)

### `AIEncounter_FormationPhaseGuidance_SetCombatCoordinator`
```lua
AIEncounter_FormationPhaseGuidance_SetCombatCoordinator(AIEncounterID encounter, PropertyBagGroup coordinatorPBG)
```
Assign a property bag contains data to support sub task coordination for combat encounters

### `AIEncounter_FormationPhaseGuidance_SetCombatExitParams`
```lua
AIEncounter_FormationPhaseGuidance_SetCombatExitParams(AIEncounterID encounter, Real timeoutSeconds, Boolean testTargetDestroyed, Boolean testEnemySquadsCleared, Boolean testEnemyBuildingsCleared, Real enemyScanRange, String excludeBuildingTypeNames)
```
Set params for terminating a formation phase encounter based on combat, fallback params can also be used

### `AIEncounter_FormationPhaseGuidance_SetMoveEnemiesExitParams`
```lua
AIEncounter_FormationPhaseGuidance_SetMoveEnemiesExitParams(AIEncounterID encounter, Real enemyScanRange, Real combatFitnessThreshold, Real enemyFormationHeading, Real enemyFormationPosition, Real enemyFormationDistance, String excludeBuildingTypeNames)
```
Set params for terminating a formation phase encounter that is moving somewhere and encounters enemies

### `AIEncounter_FormationPhaseGuidance_SetMoveExitParams`
```lua
AIEncounter_FormationPhaseGuidance_SetMoveExitParams(AIEncounterID encounter, Real timeoutSeconds, Real requiredSquadsPercent, Real wasRecentlyAttackedSecs)
```
Set params for terminating a formation phase encounter that is moving somewhere

### `AIEncounter_FormationTaskStateGuidance_MinRange`
```lua
AIEncounter_FormationTaskStateGuidance_MinRange(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, Real repositionIntervalSecs, Boolean useTactics, String unitTypeNames, PropertyBagGroup targetPriorityPBG)
```
Specify data for formation encounter to create a formation min range task state

### `AIEncounter_FormationTaskStateGuidance_MinRangeWithProtect`
```lua
AIEncounter_FormationTaskStateGuidance_MinRangeWithProtect(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, Real repositionIntervalSecs, Boolean useTactics, String unitTypeNames, PropertyBagGroup targetPriorityPBG, Integer protectMinSquads, Integer protectMaxSquads, Real protectProportionSquads, Real protectDistance, Real protectRepositionThreshold, Real protectRepositionIntervalSecs, String protectUnitTypeNames)
```
Specify data for formation encounter to create a formation min range task state with protect task

### `AIEncounter_FormationTaskStateGuidance_Move`
```lua
AIEncounter_FormationTaskStateGuidance_Move(AIEncounterID encounter, Boolean attackMove, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, String unitTypeNames)
```
Specify data for formation encounter to create a formation move task state

### `AIEncounter_FormationTaskStateGuidance_SetupRanged`
```lua
AIEncounter_FormationTaskStateGuidance_SetupRanged(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, String unitTypeNames, PropertyBagGroup targetPriorityPBG)
```
Specify data for formation encounter to create a formation setup ranged task state

### `AIEncounter_FormationTaskStateGuidance_SetupRangedWithProtect`
```lua
AIEncounter_FormationTaskStateGuidance_SetupRangedWithProtect(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, String unitTypeNames, PropertyBagGroup targetPriorityPBG, Integer protectMinSquads, Integer protectMaxSquads, Real protectProportionSquads, Real protectDistance, Real protectRepositionThreshold, Real protectRepositionIntervalSecs, String protectUnitTypeNames)
```
Specify data for formation encounter to create a formation setup ranged task state and along with a formation of other units to protect it

### `AIEncounter_FormationTaskStateGuidance_SimpleMelee`
```lua
AIEncounter_FormationTaskStateGuidance_SimpleMelee(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, String unitTypeNames, PropertyBagGroup targetPriorityPBG)
```
Specify data for formation encounter to create a formation simple melee task state

### `AIEncounter_FormationTaskStateGuidance_TransportMove`
```lua
AIEncounter_FormationTaskStateGuidance_TransportMove(AIEncounterID encounter, Integer priority, Integer minSquads, Integer maxSquads, Integer maxTasks, String unitTypeNames, Integer minPassengerSquads, Integer maxPassengerSquadsPerTransport, PropertyBagGroup unloadAbilityPBG, String passengerUnitTypeNames, PropertyBagGroup targetPriorityPBG)
```
Specify data for formation encounter to create a formation transport move task state

### `AIEncounter_GetEncounterFromID`
```lua
AIEncounter_GetEncounterFromID(PlayerID player, AITaskID taskID)
```
Returns the encounter pointer from the ID, always test for nil before using...

### `AIEncounter_IsAIPlayerValid`
```lua
AIEncounter_IsAIPlayerValid(AIEncounterID pEncounter)
```
Returns true if enconter has a valid AI player

### `AIEncounter_IsValid`
```lua
AIEncounter_IsValid(UniqueID PlayerUniqueID, AITaskID encounterTaskID)
```
Determines if encounter is still valid.  Must be true before calling any other of the AIEncounter_* function.  Return true if valid, false otherwise.

### `AIEncounter_LogDebug`
```lua
AIEncounter_LogDebug(PlayerID pPlayer, Integer encounterID, String debugString)
```
in non RTM builds, if verboseEncounterLogging is enabled, will spew string to AI log file

### `AIEncounter_MoveGuidance_EnableAggressiveMove`
```lua
AIEncounter_MoveGuidance_EnableAggressiveMove(AIEncounterID pEncounter, Boolean enable)
```
Enable / disable aggressive movements on way to engagement targets

### `AIEncounter_MoveGuidance_SetSquadCoherenceRadius`
```lua
AIEncounter_MoveGuidance_SetSquadCoherenceRadius(AIEncounterID pEncounter, Real radius)
```
Set radius (follow distance) for coordinated move phase (<= 0 disables coordinated movement)

### `AIEncounter_Notify_ClearCallbacks`
```lua
AIEncounter_Notify_ClearCallbacks(AIEncounterID pEncounter)
```
Clears all notification callbacks for encounter

### `AIEncounter_Notify_SetEnableSnipedCallbacks`
```lua
AIEncounter_Notify_SetEnableSnipedCallbacks(AIEncounterID pEncounter, Boolean value)
```
enables/disabled the sniped callback

### `AIEncounter_Notify_SetPlayerEventEncounterID`
```lua
AIEncounter_Notify_SetPlayerEventEncounterID(AIEncounterID pEncounter, Integer id)
```
Sets the ID for the notification event sent out by encounter

### `AIEncounter_Pause`
```lua
AIEncounter_Pause(AIEncounterID pEncounter, Boolean bPause)
```
Pause/Unpause this encounter

### `AIEncounter_ResourceGuidance_CalculateEstimatedSquadProductionTime`
```lua
AIEncounter_ResourceGuidance_CalculateEstimatedSquadProductionTime(AIEncounterID pEncounter, String pbgShortname, Boolean canAffordNowOnly)
```
Calculates approximately how long it will take for a specified Encounter to produce a specified squad.

### `AIEncounter_ResourceGuidance_ClearEntities`
```lua
AIEncounter_ResourceGuidance_ClearEntities(AIEncounterID pEncounter)
```
Removes all resource entities from encounter.

### `AIEncounter_ResourceGuidance_ClearSquads`
```lua
AIEncounter_ResourceGuidance_ClearSquads(AIEncounterID pEncounter)
```
Removes all resource squads from encounter.

### `AIEncounter_ResourceGuidance_EntityGroup`
```lua
AIEncounter_ResourceGuidance_EntityGroup(AIEncounterID pEncounter, EGroupID entities)
```
Sets the resource entities for encounter.

### `AIEncounter_ResourceGuidance_IsSquadGroupEqual`
```lua
AIEncounter_ResourceGuidance_IsSquadGroupEqual(AIEncounterID pEncounter, SGroupID squads)
```
Checks if a squad group is equal to the resource squads of an encounter.

### `AIEncounter_ResourceGuidance_SetResourceMoney`
```lua
AIEncounter_ResourceGuidance_SetResourceMoney(AIEncounterID pEncounter, ResourceAmount resourceAmount)
```
Sets the resource money for an encounter.

### `AIEncounter_ResourceGuidance_SquadGroup`
```lua
AIEncounter_ResourceGuidance_SquadGroup(AIEncounterID pEncounter, SGroupID squads)
```
Sets the resource squads for encounter.

### `AIEncounter_SetDebugName`
```lua
AIEncounter_SetDebugName(AIEncounterID pEncounter, String name)
```
Set encounter name for debugging.

### `AIEncounter_TacticFilter_Reset`
```lua
AIEncounter_TacticFilter_Reset(AIEncounterID pEncounter)
```
Reset all tactic filters for encounter

### `AIEncounter_TacticFilter_ResetAbilityGuidance`
```lua
AIEncounter_TacticFilter_ResetAbilityGuidance(AIEncounterID pEncounter)
```
Reset all tactic ability constraints for encounter

### `AIEncounter_TacticFilter_ResetAbilityPriority`
```lua
AIEncounter_TacticFilter_ResetAbilityPriority(AIEncounterID pEncounter, PropertyBagGroup abilityPBG)
```
Reset ability priority for all squads in encounter

### `AIEncounter_TacticFilter_ResetPriority`
```lua
AIEncounter_TacticFilter_ResetPriority(AIEncounterID pEncounter, AITacticType tactic)
```
Reset tactic priority for all squads in encounter

### `AIEncounter_TacticFilter_ResetTacticGuidance`
```lua
AIEncounter_TacticFilter_ResetTacticGuidance(AIEncounterID pEncounter)
```
Reset all tactic constraints for encounter

### `AIEncounter_TacticFilter_ResetTargetGuidance`
```lua
AIEncounter_TacticFilter_ResetTargetGuidance(AIEncounterID pEncounter)
```
Reset all tactic target constraints for encounter

### `AIEncounter_TacticFilter_SetAbilityGuidance`
```lua
AIEncounter_TacticFilter_SetAbilityGuidance(AIEncounterID pEncounter, PropertyBagGroup ability, Integer maxCasters, Real retrySecs, Real waitSelfSecs, Real waitEncounterSecs, Real timeoutSecs, Boolean initialWait, Real maxRange, Real castChanceOverride)
```
Set tactic ability constraints for encounter

### `AIEncounter_TacticFilter_SetAbilityPriority`
```lua
AIEncounter_TacticFilter_SetAbilityPriority(AIEncounterID pEncounter, PropertyBagGroup abilityPBG, Real priority)
```
Set ability priority for all squads in encounter; negative priority disables

### `AIEncounter_TacticFilter_SetAbilityPriorityForSquad`
```lua
AIEncounter_TacticFilter_SetAbilityPriorityForSquad(AIEncounterID pEncounter, SquadID squad, PropertyBagGroup abilityPBG, Real priority)
```
Set ability priority for squad in encounter

### `AIEncounter_TacticFilter_SetDefaultAbilityGuidance`
```lua
AIEncounter_TacticFilter_SetDefaultAbilityGuidance(AIEncounterID pEncounter, Integer maxCasters, Real retrySecs, Real waitSelfSecs, Real waitEncounterSecs, Real timeoutSecs, Boolean initialWait, Real maxRange, Real castChanceOverride)
```
Set default tactic ability constraints for encounter (ability specific guidance takes priority over defaults)

### `AIEncounter_TacticFilter_SetDefaultTacticGuidance`
```lua
AIEncounter_TacticFilter_SetDefaultTacticGuidance(AIEncounterID pEncounter, Integer maxUsers, Real retrySecs, Real waitSecs, Real timeoutSecs, Boolean initialWait, Real maxRange)
```
Set default tactic constraints for encounter (tactic specific guidance takes priority over defaults)

### `AIEncounter_TacticFilter_SetPriority`
```lua
AIEncounter_TacticFilter_SetPriority(AIEncounterID pEncounter, AITacticType tactic, Real priority)
```
Set tactic priority for all squads in encounter; negative priority disables

### `AIEncounter_TacticFilter_SetPriorityForSquad`
```lua
AIEncounter_TacticFilter_SetPriorityForSquad(AIEncounterID pEncounter, SquadID squad, AITacticType tactic, Real priority)
```
Set tactic priority for squads in encounter

### `AIEncounter_TacticFilter_SetTacticGuidance`
```lua
AIEncounter_TacticFilter_SetTacticGuidance(AIEncounterID pEncounter, AITacticType tactic, Integer maxUsers, Real retrySecs, Real waitSecs, Real timeoutSecs, Boolean initialWait, Real maxRange)
```
Set tactic constraints for encounter

### `AIEncounter_TacticFilter_SetTargetPolicy`
```lua
AIEncounter_TacticFilter_SetTargetPolicy(AIEncounterID pEncounter, TargetPreference policy)
```
Set tactic target priority for encounter

### `AIEncounter_TargetGuidance_DisableSquadPatrol`
```lua
AIEncounter_TargetGuidance_DisableSquadPatrol(AIEncounterID pEncounter, SquadID pSquad)
```
Disables the patrol for the passed Squad

### `AIEncounter_TargetGuidance_SetPatrolPathByName`
```lua
AIEncounter_TargetGuidance_SetPatrolPathByName(AIEncounterID pEncounter, String pathName, Real delaySecs, Boolean invertPathAtEnd, Boolean startInverted)
```
Sets target patrol path for encounter

### `AIEncounter_TargetGuidance_SetPatrolWander`
```lua
AIEncounter_TargetGuidance_SetPatrolWander(AIEncounterID pEncounter, Real delaySecs, Integer radiusMode, Real radiusOverride, Boolean overrideCenter, Position centerOverride)
```
Sets random wander target patrol for encounter; delaySecs is the time in secs to pause at each random point

### `AIEncounter_TargetGuidance_SetSquadPatrolPathByName`
```lua
AIEncounter_TargetGuidance_SetSquadPatrolPathByName(AIEncounterID pEncounter, SquadID pSquad, String pathName, Real delaySecs, Boolean invertPathAtEnd, Boolean startInverted)
```
Sets target patrol path for the squad

### `AIEncounter_TargetGuidance_SetSquadPatrolWander`
```lua
AIEncounter_TargetGuidance_SetSquadPatrolWander(AIEncounterID pEncounter, SquadID pSquad, Real delaySecs, Integer radiusMode, Real radiusOverride, Boolean overrideCenter, Position centerOverride)
```
Sets random wander target patrol for the squad; delaySecs is the time in secs to pause at each random point

### `AIEncounter_TargetGuidance_SetTargetArea`
```lua
AIEncounter_TargetGuidance_SetTargetArea(AIEncounterID pEncounter, Real radius)
```
Sets engagement area radius around the target.

### `AIEncounter_TargetGuidance_SetTargetEntity`
```lua
AIEncounter_TargetGuidance_SetTargetEntity(AIEncounterID pEncounter, EntityID entity)
```
Sets target Entity for encounter

### `AIEncounter_TargetGuidance_SetTargetLeash`
```lua
AIEncounter_TargetGuidance_SetTargetLeash(AIEncounterID pEncounter, Real radius)
```
Sets leash radius around target where squads should stay within.

### `AIEncounter_TargetGuidance_SetTargetPosition`
```lua
AIEncounter_TargetGuidance_SetTargetPosition(AIEncounterID pEncounter, Position pos)
```
Sets target position for encounter

### `AIEncounter_TargetGuidance_SetTargetSquad`
```lua
AIEncounter_TargetGuidance_SetTargetSquad(AIEncounterID pEncounter, SquadID squad)
```
Sets target Squad for encounter

### `AIEncounter_Trigger`
```lua
AIEncounter_Trigger(AIEncounterID pEncounter)
```
Set encounter name for debugging.

## AIPlayer (74 functions)

### `AIPlayer_CachedPathCrossesEnemyTerritory`
```lua
AIPlayer_CachedPathCrossesEnemyTerritory(PlayerID aiPlayer, Integer requestingID, Real minDistToEnemyTerritory, Boolean unused)
```
Checks if the cached path crosses known enemy territory

### `AIPlayer_CanAISquadLockTacticItem`
```lua
AIPlayer_CanAISquadLockTacticItem(EntityID tacticItemEntity, SquadID lockingAISquad)
```
Checks if the squad can lock the tactic item

### `AIPlayer_CanSeeEntity`
```lua
AIPlayer_CanSeeEntity(PlayerID aiPlayer, EntityID canSee)
```
Test if player can see entity

### `AIPlayer_ClearCachedPath`
```lua
AIPlayer_ClearCachedPath(PlayerID player, Integer requestingID)
```
Delete the cached path with this ID, please remember to do this

### `AIPlayer_EnemyTerritoryDetected`
```lua
AIPlayer_EnemyTerritoryDetected(PlayerID player)
```
returns true if enemy territory has been detected

### `AIPlayer_FindClosestSiegeTarget`
```lua
AIPlayer_FindClosestSiegeTarget(PlayerID player, EGroupID eGroup, Integer minSections, Boolean unbreached, Position refPosition)
```
Tests to see if any entity in the group is part of a wall that matches the supplied conditions eGroup contains list of entities to test, minSections is minimum number of connected wall sections, unbreached means all sections must be unbroken.  Returns closest entity to refPosition

### `AIPlayer_FindClumpContainingPosition`
```lua
AIPlayer_FindClumpContainingPosition(PlayerID aiPlayer, Position pos, Integer targetFilterFlags)
```
Find a clump containing the given position, or return -1 if there isn't one.

### `AIPlayer_GetAnchorPosition`
```lua
AIPlayer_GetAnchorPosition(PlayerID aiPlayer)
```
Returns the anchor build position

### `AIPlayer_GetBestClumpForPositionIdx`
```lua
AIPlayer_GetBestClumpForPositionIdx(PlayerID pPlayer, Position position, PropertyBagGroup pAbilityPBG, Real minRange, Real maxRange, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of enemy squads within the given tolerance to the position passed in

### `AIPlayer_GetBestClumpForSquadIdx`
```lua
AIPlayer_GetBestClumpForSquadIdx(PlayerID pPlayer, SquadID pSquad, PropertyBagGroup pAbilityPBG, Real minRange, Real maxRange, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of enemy squads within the given tolerance to the AI squad

### `AIPlayer_GetBestClumpIdx`
```lua
AIPlayer_GetBestClumpIdx(PlayerID pPlayer, Real minRange, Real maxRange, Real clumpSelectionGlobalBestMinRatio, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of allied or enemy squads within the given tolerance to the AI player

### `AIPlayer_GetBestClumpIdxForAbility`
```lua
AIPlayer_GetBestClumpIdxForAbility(PlayerID pPlayer, PropertyBagGroup pAbilityPBG, Real minRange, Real maxRange, Real clumpSelectionGlobalBestMinRatio, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of allied or enemy squads within the given tolerance to the AI player

### `AIPlayer_GetBestOwnedClumpIdx`
```lua
AIPlayer_GetBestOwnedClumpIdx(PlayerID pPlayer, Real minRange, Real maxRange, Real clumpSelectionGlobalBestMinRatio, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of owned squads within the given tolerance to the AI player

### `AIPlayer_GetBestOwnedClumpIdxForAbility`
```lua
AIPlayer_GetBestOwnedClumpIdxForAbility(PlayerID pPlayer, PropertyBagGroup pAbilityPBG, Real minRange, Real maxRange, Real clumpSelectionGlobalBestMinRatio, Integer targetFilterFlags, Integer minNumSquads)
```
returns a 0-based index of the best clump of owned squads within the given tolerance to the AI player

### `AIPlayer_GetCachedPathLength`
```lua
AIPlayer_GetCachedPathLength(PlayerID player, Integer requestingID)
```
Get the distance of the path requested with the given ID. < 0 means invalid request.

### `AIPlayer_GetCachedPathPoints`
```lua
AIPlayer_GetCachedPathPoints(PlayerID player, Integer requestingID)
```
Return the path points of the calculated path from a previous pathfinding request if the result was successful and the path has at least two points.

### `AIPlayer_GetCapturePoints`
```lua
AIPlayer_GetCapturePoints(PlayerID aiPlayer, StackVar relationshipEnum, Boolean onlyCanPlaceSecuringStructure, EGroupID egroupOut)
```
Returns an EGroup containing all capture points on the map owned by a player with the specified

### `AIPlayer_GetClumpPosition`
```lua
AIPlayer_GetClumpPosition(PlayerID pPlayer, Integer clumpIndex, Integer targetFilterFlags)
```
Used for tactics; returns a "special error position" on failure that's nowhere inside the world

### `AIPlayer_GetDistanceToEnemyTerritory`
```lua
AIPlayer_GetDistanceToEnemyTerritory(PlayerID player, Position position)
```
returns how close a position is to enemy territory

### `AIPlayer_GetDynamicMultiplier`
```lua
AIPlayer_GetDynamicMultiplier(PlayerID aiPlayer, Key tableName)
```
Calculate product of all multipliers in tableName

### `AIPlayer_GetDynamicUnitTypeMultipliersForEntity`
```lua
AIPlayer_GetDynamicUnitTypeMultipliersForEntity(PlayerID aiPlayer, Entity& targetEntity)
```
Calculate product of all unit type multipliers that match the entity's unit types

### `AIPlayer_GetDynamicUnitTypeMultipliersForSquad`
```lua
AIPlayer_GetDynamicUnitTypeMultipliersForSquad(PlayerID aiPlayer, Squad& targetSquad)
```
Calculate product of all unit type multipliers that match a unit type of an entity in the squad

### `AIPlayer_GetKnownResourceDeposits`
```lua
AIPlayer_GetKnownResourceDeposits(PlayerID aiPlayer, String resourceType, Boolean includeDepleted)
```
Returns a list of all resource deposit entities seen by the AI player

### `AIPlayer_GetLocal`
```lua
AIPlayer_GetLocal(Integer playerId)
```
Returns the local AIPlayer given a PlayerId (1000 and up)

### `AIPlayer_GetLocalFromPlayer`
```lua
AIPlayer_GetLocalFromPlayer(PlayerID pPlayerIn)
```
Returns the local AIPlayer given a Player pointer

### `AIPlayer_GetNumPBG`
```lua
AIPlayer_GetNumPBG(PlayerID aiPlayer, Integer countType, PropertyBagGroup pbg)
```
Returns the count of specified PBG that the AI player is observing.

### `AIPlayer_GetOpponentPlayerAtIndex`
```lua
AIPlayer_GetOpponentPlayerAtIndex(PlayerID aiPlayer, Integer index)
```
Returns the Player at specified index out of all opponent players.  Use in conjunction with `AIPlayer_GetOpponentPlayerCount`.

### `AIPlayer_GetOpponentPlayerCount`
```lua
AIPlayer_GetOpponentPlayerCount(PlayerID aiPlayer)
```
Returns the number of opponent Players to the specified AIPlayer.

### `AIPlayer_GetOrCreateHomebase`
```lua
AIPlayer_GetOrCreateHomebase(PlayerID aiPlayer, Position targetPosition)
```
Get a homebase at the given position. If one doesn't exist it will be created.

### `AIPlayer_GetOwnedClumpPosition`
```lua
AIPlayer_GetOwnedClumpPosition(PlayerID pPlayer, Integer clumpIndex)
```
Used for tactics; returns a "special error position" on failure that's nowhere inside the world

### `AIPlayer_GetOwnedMilitaryPointEntitiesInRange`
```lua
AIPlayer_GetOwnedMilitaryPointEntitiesInRange(EntityPBG militaryPointPBG, Position position, Number range)
```
Returns an EGroup listing all military points owned by a player within a certain range of the position passed in that match a certain type

### `AIPlayer_GetPositionsOfMilitaryPointsWithRelation`
```lua
AIPlayer_GetPositionsOfMilitaryPointsWithRelation(PlayerID aiPlayer, StackVar relationshipEnum)
```
Returns all positions of military points allied with a player

### `AIPlayer_GetSquadPBGProductionUtility`
```lua
AIPlayer_GetSquadPBGProductionUtility(PlayerID aiPlayer, ScarSquadPBG squadPBG)
```
Returns the utility of building the squad specified by the PBG, or 0 if not found

### `AIPlayer_GetStateModelAISquadListEntries`
```lua
AIPlayer_GetStateModelAISquadListEntries(PlayerID aiPlayer, String key)
```
Returns a table of squad ids from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelBool`
```lua
AIPlayer_GetStateModelBool(PlayerID aiPlayer, String key)
```
Returns a boolean value from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelEntityTarget`
```lua
AIPlayer_GetStateModelEntityTarget(PlayerID aiPlayer, String key)
```
Returns an Entity* value from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelFloat`
```lua
AIPlayer_GetStateModelFloat(PlayerID aiPlayer, String key)
```
Returns a float value from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelInt`
```lua
AIPlayer_GetStateModelInt(PlayerID aiPlayer, String key)
```
Returns an integer value from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelPBG`
```lua
AIPlayer_GetStateModelPBG(PlayerID aiPlayer, String key)
```
Returns a PropertyBagGroup value from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_GetStateModelTargetListEntries`
```lua
AIPlayer_GetStateModelTargetListEntries(PlayerID aiPlayer, String key)
```
Returns a table of targets from the AIPlayer's state model corresponding to the given key.

### `AIPlayer_IsDamagedStructureOnPathToTarget`
```lua
AIPlayer_IsDamagedStructureOnPathToTarget(PlayerID aiPlayer, SquadID squad, PropertyBagGroup structurePbg, Real damagePercentage, Real searchRadius, Position targetPosition)
```
Has path to target passes through a netural damaged structure

### `AIPlayer_IsOnAnIsland`
```lua
AIPlayer_IsOnAnIsland()
```
Returns whether the player is on an island (naval map) or not

### `AIPlayer_IsPathProcessed`
```lua
AIPlayer_IsPathProcessed(PlayerID aiPlayer, Integer requestedPathRequestID)
```
Has the requested path been processed

### `AIPlayer_IsPointThreatened`
```lua
AIPlayer_IsPointThreatened(PlayerID aiPlayer, Position pos, Boolean filterEnemyBuildings, Real thresholdFitness)
```
Returns whether or not a point is threatened (from the perspective of the player passed in)

### `AIPlayer_IsTacticItemLocked`
```lua
AIPlayer_IsTacticItemLocked(PlayerID player, EntityID tacticItemEntity)
```
Checks if a tactic item is locked

### `AIPlayer_IsTacticItemLockedByAISquad`
```lua
AIPlayer_IsTacticItemLockedByAISquad(EntityID tacticItemEntity, SquadID lockingAISquad)
```
Checks if a tactic item is locked by the squad

### `AIPlayer_LockTacticItemForAISquad`
```lua
AIPlayer_LockTacticItemForAISquad(EntityID tacticItemEntity, SquadID lockingAISquad)
```
Locks a tactic item for the passed player

### `AIPlayer_PopScoreMultiplier`
```lua
AIPlayer_PopScoreMultiplier(PlayerID aiPlayer, Key tuningValueName, AIScoreMultiplierID id)
```
Remove a multiplier previously applied to change the weight of a criteria in target scoring

### `AIPlayer_PopUnitTypeScoreMultiplier`
```lua
AIPlayer_PopUnitTypeScoreMultiplier(PlayerID aiPlayer, Key unitTypeName, AIScoreMultiplierID id)
```
Remove a multiplier previously applied to a unit type for target scoring

### `AIPlayer_ProcessedPathSuccessful`
```lua
AIPlayer_ProcessedPathSuccessful(PlayerID aiPlayer, Integer processedPathRequestID)
```
Was the processed path successful? Only supply requestID for a processed path

### `AIPlayer_PushScoreMultiplier`
```lua
AIPlayer_PushScoreMultiplier(PlayerID aiPlayer, Key tuningValueName, Real multiplier, AIScoreMultiplierID multiplierID)
```
Add a multiplier to change the weight of a criteria in target scoring

### `AIPlayer_PushUnitTypeScoreMultiplier`
```lua
AIPlayer_PushUnitTypeScoreMultiplier(PlayerID aiPlayer, Key unitTypeName, Real multiplier, AIScoreMultiplierID multiplierID)
```
Add a multiplier to give weight to a unit type in target scoring

### `AIPlayer_RemoveEntityHomebase`
```lua
AIPlayer_RemoveEntityHomebase(PlayerID aiPlayer, EGroupID eGroup)
```
Remove entities (buildings) homebase assignment. Entities must be owned by player.

### `AIPlayer_RemoveSquadHomebase`
```lua
AIPlayer_RemoveSquadHomebase(PlayerID aiPlayer, SGroupID sGroup)
```
Remove squads homebase assignment. Squads must be owned by player.

### `AIPlayer_RequestHighPath`
```lua
AIPlayer_RequestHighPath(PlayerID player, Integer requestingID, Position start, Position end, PropertyBagGroup pathingEntityPBG, Boolean requiresPartialPath)
```
Request a high path between the start and destination, supply a unique ID and the PBG of the largest entity that will be following the path.

### `AIPlayer_ResetAbilityPriorityOverride`
```lua
AIPlayer_ResetAbilityPriorityOverride(PlayerID player, PropertyBagGroup abilityPBG)
```
Clears the ability priority override

### `AIPlayer_ResetAIAbilityPriorityOverride`
```lua
AIPlayer_ResetAIAbilityPriorityOverride(PlayerID player, PropertyBagGroup aiAbilityPBG)
```
Clears the ability priority override for all the abilities contained in the AIAbilityBag

### `AIPlayer_ResetEnemySquadsVisibility`
```lua
AIPlayer_ResetEnemySquadsVisibility(PlayerID player, PlayerID enemyPlayer)
```
Temporarily hides all of the known squads belonging to the enemy player for the specified AI

### `AIPlayer_SetAbilityPriorityOverride`
```lua
AIPlayer_SetAbilityPriorityOverride(PlayerID player, PropertyBagGroup abilityPBG, Real priority)
```
Sets the ability priority override for all the AISquads owned by the player. -1 to disable the ability. NOTE: Encounter overrides have higher priority.

### `AIPlayer_SetAIAbilityPriorityOverride`
```lua
AIPlayer_SetAIAbilityPriorityOverride(PlayerID player, PropertyBagGroup aiAbilityPBG, Real priority)
```
Sets the ability priority override for all the abilities contained in the AIAbilityBag for all the AISquads owned by the player. -1 to disable the ability. NOTE: Encounter overrides have higher priority.

### `AIPlayer_SetEntityHomebase`
```lua
AIPlayer_SetEntityHomebase(PlayerID aiPlayer, EGroupID eGroup, Integer homeBaseID)
```
Add entities (buildings) to a homebase. Entities must be owned by player.

### `AIPlayer_SetGathererDistributionOverride`
```lua
AIPlayer_SetGathererDistributionOverride(PlayerID aiPlayer, Real luaGatherDistro)
```
Set the target distribution of how the ai player should use their units for gathering

### `AIPlayer_SetMarkerToUpdateCachedPathToHQ`
```lua
AIPlayer_SetMarkerToUpdateCachedPathToHQ(Player, MarkerID marker, Real pathCheckIntervalSecs)
```
Setup a cached path that periodically updates its path between specified marker and self HQ. This allows the AI to detect whenever pathability is changed to this marker (e.g. being walled off).

### `AIPlayer_SetMarkerToUpdateCachedPathToPosition`
```lua
AIPlayer_SetMarkerToUpdateCachedPathToPosition(Player, MarkerID toMarker, Position fromPosition, Real pathCheckIntervalSecs)
```
Setup a cached path that periodically updates its path between specified marker and position. This allows the AI to detect whenever pathability is changed to between the marker and position (e.g. being walled off).

### `AIPlayer_SetRequiresStatsUpdate`
```lua
AIPlayer_SetRequiresStatsUpdate(PlayerID player)
```
marks the player to force the stats squads to update

### `AIPlayer_SetSquadHomebase`
```lua
AIPlayer_SetSquadHomebase(PlayerID aiPlayer, SGroupID sGroup, Integer homeBaseID)
```
Add squads to a homebase. Squads must be owned by player.

### `AIPlayer_SetStrategicBaseIntention`
```lua
AIPlayer_SetStrategicBaseIntention(PlayerID player, String intentionName, Real value)
```
Set the base strategic intention of a player

### `AIPlayer_ToggleDrawCachedPath`
```lua
AIPlayer_ToggleDrawCachedPath(Integer requestingID, Boolean on)
```
Toggle debug draw for the specified path, -1 will draw all of them

### `AIPlayer_UnLockTacticItemForAISquad`
```lua
AIPlayer_UnLockTacticItemForAISquad(EntityID tacticItemEntity, SquadID lockingAISquad)
```
UnLocks a tactic item for the passed player

### `AIPlayer_UpdateGathering`
```lua
AIPlayer_UpdateGathering(PlayerID pPlayer)
```
Updates what the skirmish AI is wanting to gather

### `AIPlayer_UpdateSkirmishAttackAndCaptureTasks`
```lua
AIPlayer_UpdateSkirmishAttackAndCaptureTasks(PlayerID pPlayer)
```
Requests the skirmish AI to update attack encounters and capture tasks

### `AIPlayer_UpdateSkirmishPlayerAbilities`
```lua
AIPlayer_UpdateSkirmishPlayerAbilities(PlayerID pPlayer)
```
Requests the skirmish AI to update player abilities

### `AIPlayer_UpdateSkirmishProduction`
```lua
AIPlayer_UpdateSkirmishProduction(PlayerID pPlayer)
```
Updates what the skirmish AI is trying to produce

### `AIPlayer_UpdateSkirmishScoutingTasks`
```lua
AIPlayer_UpdateSkirmishScoutingTasks(PlayerID pPlayer)
```
Requests the skirmish AI to update scout encounters

## AIProductionScoring (62 functions)

### `AIProductionScoring_AlliedCombatFitness`
```lua
AIProductionScoring_AlliedCombatFitness(PlayerID aiPlayer, Real minFitness, Real maxFitness, Integer aiArmyType, Boolean highFitnessIsGood)
```
Create a AlliedCombatFitness scoring function.

### `AIProductionScoring_AlliedCombatFitnessVsStrongestEnemy`
```lua
AIProductionScoring_AlliedCombatFitnessVsStrongestEnemy(PlayerID aiPlayer, Real minFitness, Real maxFitness, Integer aiArmyType, Boolean highFitnessIsGood)
```
Create a AlliedCombatFitness scoring function (versus strongest enemy).

### `AIProductionScoring_AlliedCombatFitnessVsWeakestEnemy`
```lua
AIProductionScoring_AlliedCombatFitnessVsWeakestEnemy(PlayerID aiPlayer, Real minFitness, Real maxFitness, Integer aiArmyType, Boolean highFitnessIsGood)
```
Create a AlliedCombatFitness scoring function (versus the weakest enemy).

### `AIProductionScoring_AmountOfResourceNeeded`
```lua
AIProductionScoring_AmountOfResourceNeeded(PlayerID aiPlayer, Real maxResources)
```
Create an AmountOfResourceNeeded scoring function.

### `AIProductionScoring_CanPushProductionScoringFunction`
```lua
AIProductionScoring_CanPushProductionScoringFunction(PlayerID aiPlayer)
```
Check if now is an appropriate time to be making scoring functions.

### `AIProductionScoring_ClampedScoringFunction`
```lua
AIProductionScoring_ClampedScoringFunction(PlayerID aiPlayer, Real min, Real max, ScoringFunction* innerScoringFunction)
```
Create a ClampedScoringFunction scoring function.

### `AIProductionScoring_CounterScore`
```lua
AIProductionScoring_CounterScore(PlayerID aiPlayer, Real baseScoreContributuion)
```
Create a CounterScore scoring function

### `AIProductionScoring_DeficiencyScore`
```lua
AIProductionScoring_DeficiencyScore(PlayerID aiPlayer, Real weight)
```
Create a DropOffScore scoring function.

### `AIProductionScoring_EntityCombatUpgrade`
```lua
AIProductionScoring_EntityCombatUpgrade(PlayerID aiPlayer)
```
Create a EntityCombatUpgrade scoring function.

### `AIProductionScoring_GroupNotProducedRecently`
```lua
AIProductionScoring_GroupNotProducedRecently(PlayerID aiPlayer, Real timePeriodSeconds)
```
Create an GroupNotProducedRecently scoring function.

### `AIProductionScoring_HasProductionQueue`
```lua
AIProductionScoring_HasProductionQueue(PlayerID aiPlayer)
```
Create a HasProductionQueue scoring function

### `AIProductionScoring_IncreaseOverTime`
```lua
AIProductionScoring_IncreaseOverTime(PlayerID aiPlayer, Real minGameTime, Real increasePerSecond)
```
Create a MinimumGameTime scoring function.

### `AIProductionScoring_InversePercentOfResourcesOwned`
```lua
AIProductionScoring_InversePercentOfResourcesOwned(PlayerID aiPlayer)
```
Create an InversedPercentOfResourcesOwned scoring function

### `AIProductionScoring_InverseRandomIntScore`
```lua
AIProductionScoring_InverseRandomIntScore(PlayerID aiPlayer)
```
Create an InverseRandomIntScore scoring function.

### `AIProductionScoring_IslandNeedingExpansionBase`
```lua
AIProductionScoring_IslandNeedingExpansionBase(PlayerID aiPlayer)
```
Create an IslandNeedingExpansionBase scoring function.

### `AIProductionScoring_LackOfSecuredResourceDeposits`
```lua
AIProductionScoring_LackOfSecuredResourceDeposits(PlayerID aiPlayer, ResourceType resourceType, Real scarceAmount, Real wellOffAmount)
```
Create a LackOfSecuredResourceDeposits scoring function.

### `AIProductionScoring_LowResourceIncome`
```lua
AIProductionScoring_LowResourceIncome(PlayerID aiPlayer, Real resourceIncomePerSecond)
```
Create an LowResourceIncome scoring function.

### `AIProductionScoring_LuaScoringFunction`
```lua
AIProductionScoring_LuaScoringFunction(PlayerID aiPlayer, LuaFunction scoringFunction)
```
Create a LuaScoringFunction scoring function.

### `AIProductionScoring_MaximumGameTime`
```lua
AIProductionScoring_MaximumGameTime(PlayerID aiPlayer, Real maxGameTime)
```
Create a MaximumGameTime scoring function.

### `AIProductionScoring_MaxPopCapPercentage`
```lua
AIProductionScoring_MaxPopCapPercentage(PlayerID aiPlayer, Real targetPopulationPercentageAlive, Boolean groupPopulation)
```
Create a MaxPopCapPercentage scoring function

### `AIProductionScoring_MaxScoringFunction`
```lua
AIProductionScoring_MaxScoringFunction(PlayerID aiPlayer, vector< ScoringFunction*> innerScoringFunction)
```
Create a MaxScoringFunction scoring function.

### `AIProductionScoring_MaxWeaponDamage`
```lua
AIProductionScoring_MaxWeaponDamage(PlayerID aiPlayer, Real maxDamage)
```
Create a MaxWeaponDamage scoring function.

### `AIProductionScoring_MilitaryPlayerUpgrade`
```lua
AIProductionScoring_MilitaryPlayerUpgrade(PlayerID aiPlayer, Real upgradeExponent)
```
Create a MilitaryPlayerUpgrade scoring function.

### `AIProductionScoring_MinimumGameTime`
```lua
AIProductionScoring_MinimumGameTime(PlayerID aiPlayer, Real minGameTime)
```
Create a MinimumGameTime scoring function.

### `AIProductionScoring_MinimumTeamControlledSacredSites`
```lua
AIProductionScoring_MinimumTeamControlledSacredSites(PlayerID aiPlayer, Integer targetAmount)
```
Create an AIMinimumTeamControlledSacredSites scoring function.

### `AIProductionScoring_MultipleProduced`
```lua
AIProductionScoring_MultipleProduced(PlayerID aiPlayer, Real additionalFactor)
```
Create a MultipleProduced scoring function

### `AIProductionScoring_MultiplyListScoringFunction`
```lua
AIProductionScoring_MultiplyListScoringFunction(PlayerID aiPlayer, vector< ScoringFunction*> innerScoringFunction)
```
Create a MultiplyListScoringFunction scoring function.

### `AIProductionScoring_NavalTransportRequired`
```lua
AIProductionScoring_NavalTransportRequired(PlayerID aiPlayer)
```
Create a NavalTransportRequired scoring function.

### `AIProductionScoring_NotProducedEver`
```lua
AIProductionScoring_NotProducedEver(PlayerID aiPlayer)
```
Create an NotProducedEver scoring function.

### `AIProductionScoring_NotProducedRecently`
```lua
AIProductionScoring_NotProducedRecently(PlayerID aiPlayer, Real timePeriodSeconds)
```
Create an NotProducedRecently scoring function.

### `AIProductionScoring_NoUpgradeProductionBlockedByThisProduction`
```lua
AIProductionScoring_NoUpgradeProductionBlockedByThisProduction(PlayerID aiPlayer, String type)
```
Create a IsUpgradeProductionTypeBlockedByThisProduction scoring function.

### `AIProductionScoring_OneStructureFromGroupAtATime`
```lua
AIProductionScoring_OneStructureFromGroupAtATime(PlayerID aiPlayer)
```
Create an OneStructureFromGroupAtATime scoring function.

### `AIProductionScoring_OnlyProduceOneAtATime`
```lua
AIProductionScoring_OnlyProduceOneAtATime(PlayerID aiPlayer)
```
Create a OnlyProduceOneAtATime scoring function.

### `AIProductionScoring_PercentOfResourcesOwned`
```lua
AIProductionScoring_PercentOfResourcesOwned(PlayerID aiPlayer)
```
Create a PercentOfResourcesOwned scoring function

### `AIProductionScoring_PlannedPlacementScore`
```lua
AIProductionScoring_PlannedPlacementScore(PlayerID aiPlayer, Real minPlacementScore)
```
Create a PlannedPlacementScore scoring function.

### `AIProductionScoring_PlannedPlacementScoreIsMoreThan`
```lua
AIProductionScoring_PlannedPlacementScoreIsMoreThan(PlayerID aiPlayer, Real minPlacementScore)
```
Create a PlannedPlacementScoreMoreThan scoring function.

### `AIProductionScoring_PlannedPlacementScoreValid`
```lua
AIProductionScoring_PlannedPlacementScoreValid(PlayerID aiPlayer)
```
Create a PlannedPlacementScoreValid scoring function.

### `AIProductionScoring_PlayerGatheringUpgrade`
```lua
AIProductionScoring_PlayerGatheringUpgrade(PlayerID aiPlayer, Real improvementScalingFactor, Real approxDistToDeposit)
```
Create a PlayerGatheringUpgrade scoring function

### `AIProductionScoring_PlayersAndCapturePointsOnDifferentIslands`
```lua
AIProductionScoring_PlayersAndCapturePointsOnDifferentIslands(PlayerID aiPlayer)
```
Create an AIPlayersAndCapturePointsOnDifferentIslands scoring function.

### `AIProductionScoring_PlayersOnDifferentIslands`
```lua
AIProductionScoring_PlayersOnDifferentIslands(PlayerID aiPlayer)
```
Create an AIPlayersOnDifferentIslands scoring function.

### `AIProductionScoring_PopCapGenerator`
```lua
AIProductionScoring_PopCapGenerator(PlayerID aiPlayer)
```
Create a PopCapGenerator scoring function.

### `AIProductionScoring_PopulationPercentage`
```lua
AIProductionScoring_PopulationPercentage(PlayerID aiPlayer, Real targetPopulationPercentageAlive, Real scoreDropOffFactor, Boolean groupPopulation, Boolean useSquadPopulation)
```
Create a PopulationPercentage scoring function

### `AIProductionScoring_PresenceOfEnemyTypes`
```lua
AIProductionScoring_PresenceOfEnemyTypes(PlayerID aiPlayer, Real weights, Boolean squadTypes)
```
Create a PresenceOfEnemyTypes scoring function

### `AIProductionScoring_PresenceOfMyTypes`
```lua
AIProductionScoring_PresenceOfMyTypes(PlayerID aiPlayer, Real weights, Boolean squadTypes)
```
Create a PresenceOfMyTypes scoring function

### `AIProductionScoring_PresenceOfUpgradeableSquads`
```lua
AIProductionScoring_PresenceOfUpgradeableSquads(PlayerID aiPlayer, Real weight)
```
Create a PresenceOfUpgradeableSquads scoring function.

### `AIProductionScoring_ProductionQueueContention`
```lua
AIProductionScoring_ProductionQueueContention(PlayerID aiPlayer, Real contentionThreshold, Real normalFactor)
```
Create a ProductionQueueContention scoring function.

### `AIProductionScoring_RandomChoiceFromRange`
```lua
AIProductionScoring_RandomChoiceFromRange(PlayerID aiPlayer, Integer iterations, Integer range, Integer choice)
```
Create an RandomChoiceFromRange scoring function.

### `AIProductionScoring_RandomIntScore`
```lua
AIProductionScoring_RandomIntScore(PlayerID aiPlayer)
```
Create an RandomIntScore scoring function.

### `AIProductionScoring_RemainingPersonnelPopCap`
```lua
AIProductionScoring_RemainingPersonnelPopCap(PlayerID aiPlayer, Real requiredRemainingPop)
```
Create an RemainingPersonnelPopCap scoring function.

### `AIProductionScoring_ResourceGeneratorScore`
```lua
AIProductionScoring_ResourceGeneratorScore(PlayerID aiPlayer, Real depletionTimeThreshold)
```
Create a ResourceGeneratorScore scoring function.

### `AIProductionScoring_ScarcityAndDeficiencyScore`
```lua
AIProductionScoring_ScarcityAndDeficiencyScore(PlayerID aiPlayer)
```
Create a DropOffScore scoring function.

### `AIProductionScoring_ShouldConsiderDeepwaterFishDeposits`
```lua
AIProductionScoring_ShouldConsiderDeepwaterFishDeposits(PlayerID aiPlayer)
```
Create a ShouldConsiderFishDeposits scoring function.

### `AIProductionScoring_ShouldConsiderLimitedNaval`
```lua
AIProductionScoring_ShouldConsiderLimitedNaval(PlayerID aiPlayer)
```
Create an AIShouldConsiderLimitedNaval scoring function.

### `AIProductionScoring_ShouldConsiderNaval`
```lua
AIProductionScoring_ShouldConsiderNaval(PlayerID aiPlayer)
```
Create an AIShouldConsiderNaval scoring function.

### `AIProductionScoring_ShouldNotConsiderNaval`
```lua
AIProductionScoring_ShouldNotConsiderNaval(PlayerID aiPlayer, Boolean shouldIncludeLimitedNaval)
```
Returns 1 if not a naval map, 0 otherwise

### `AIProductionScoring_StrategicIntention`
```lua
AIProductionScoring_StrategicIntention(PlayerID aiPlayer, Real weights)
```
Create a StrategicIntention scoring function

### `AIProductionScoring_TierUpgrade`
```lua
AIProductionScoring_TierUpgrade(PlayerID aiPlayer, Real weight)
```
Create a TierUpgrade scoring function.

### `AIProductionScoring_TimeToAcquire`
```lua
AIProductionScoring_TimeToAcquire(PlayerID aiPlayer, Real maxTimeSeconds, Boolean includeTimeToGather, Boolean includeTimeToBuildThis, Boolean includeTimeToBuildRequirements)
```
Create a TimeToAcquire scoring function

### `AIProductionScoring_TradeRouteExistsScore`
```lua
AIProductionScoring_TradeRouteExistsScore(PlayerID aiPlayer, Boolean landRoute)
```
Create a ResourceDesireVsIncome scoring function.

### `AIProductionScoring_UnderCountLimit`
```lua
AIProductionScoring_UnderCountLimit(PlayerID aiPlayer, Integer maxAlive, Integer maxEverProduced, Boolean groupPopulation)
```
Create a UnderCountLimit scoring function

### `AIProductionScoring_UnderCountLimitFromStateModel`
```lua
AIProductionScoring_UnderCountLimitFromStateModel(PlayerID aiPlayer, String keyMaxAlive)
```
Create a UnderCountLimit scoring function

### `AIProductionScoring_VehicleUnderCountLimit`
```lua
AIProductionScoring_VehicleUnderCountLimit(PlayerID aiPlayer, Boolean groupPopulation, Boolean maxCap)
```
Create an VehicleUnderCountLimit scoring function.

## AISquad (48 functions)

### `AISquad_ClearStateModelEnumTableTarget`
```lua
AISquad_ClearStateModelEnumTableTarget(SquadID aiSquad, String key, Integer tableRowIndex)
```
Clears a TargetHandle value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_ClearStateModelTarget`
```lua
AISquad_ClearStateModelTarget(SquadID aiSquad, String key)
```
Clears a TargetHandle value in the AISquad's state model corresponding to the given key.

### `AISquad_FindBestIsolatedSquadTarget`
```lua
AISquad_FindBestIsolatedSquadTarget(SquadID aiSquad, SGroupID targetSquads, TargetPreference tacticTargetPolicy, Boolean targetAllies)
```
Find the best squad target which is not part of a clump.

### `AISquad_FindBestSquadTarget`
```lua
AISquad_FindBestSquadTarget(SquadID aiSquad, SGroupID targetSquads, TargetPreference tacticTargetPolicy)
```
returns the best squad target in the sgroup based on the passed tacticTargetPolicy

### `AISquad_FindFilteredCoverCompareCurrent`
```lua
AISquad_FindFilteredCoverCompareCurrent(PlayerID player, SquadID aiSquad, Real maxPathDistanceFromGoal, Boolean compareToCurrentCover)
```
Tries to find cover within a certain radius of a position, traveling a max distance to get there, and possibly comparing against current position's cover. If no cover is found, it returns an invalid position

### `AISquad_FindSafePositionInEncounterLeash`
```lua
AISquad_FindSafePositionInEncounterLeash(SquadID aiSquad, Real maxRadius)
```
returns the safest position for the AISquad in the current encounter leash area

### `AISquad_GetClosestCuttableObstruction`
```lua
AISquad_GetClosestCuttableObstruction(SquadID pSquad, Real radius)
```
Returns the closest cuttable obstruction entity to the given squad

### `AISquad_GetClosestObstruction`
```lua
AISquad_GetClosestObstruction(SquadID pSquad, Real radius, Boolean bFilterAllied)
```
Returns the closest obstruction entity to the given squad

### `AISquad_GetClosestObstructionOfType`
```lua
AISquad_GetClosestObstructionOfType(SquadID pSquad, Real radius, PropertyBagGroup pbgtype)
```
Returns the closest obstruction entity to the given squad

### `AISquad_GetClumpFarBound`
```lua
AISquad_GetClumpFarBound(SquadID aiSquad, Integer clumpIndex, Integer targetFilterFlags)
```
Get the position on the far side of the given clump relative to the given squad.

### `AISquad_GetCurrentFallBackPosition`
```lua
AISquad_GetCurrentFallBackPosition(SquadID aiSquad)
```
returns the current fallback position

### `AISquad_GetStateModelBool`
```lua
AISquad_GetStateModelBool(SquadID aiSquad, String key)
```
Returns a boolean value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelEntityTarget`
```lua
AISquad_GetStateModelEntityTarget(SquadID aiSquad, String key)
```
Returns an Entity value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelEnumTableBool`
```lua
AISquad_GetStateModelEnumTableBool(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a boolean value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTableEntityTarget`
```lua
AISquad_GetStateModelEnumTableEntityTarget(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns an Entity value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTableFloat`
```lua
AISquad_GetStateModelEnumTableFloat(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a float value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTableInt`
```lua
AISquad_GetStateModelEnumTableInt(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns an integer value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTablePBG`
```lua
AISquad_GetStateModelEnumTablePBG(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a pbg value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTablePlayerTarget`
```lua
AISquad_GetStateModelEnumTablePlayerTarget(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a Player value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTableSquadTarget`
```lua
AISquad_GetStateModelEnumTableSquadTarget(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a Squad value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelEnumTableVector3f`
```lua
AISquad_GetStateModelEnumTableVector3f(SquadID aiSquad, String key, Integer tableRowIndex)
```
Returns a Vector3f value from the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_GetStateModelFloat`
```lua
AISquad_GetStateModelFloat(SquadID aiSquad, String key)
```
Returns a float value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelInt`
```lua
AISquad_GetStateModelInt(SquadID aiSquad, String key)
```
Returns an integer value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelPBG`
```lua
AISquad_GetStateModelPBG(SquadID aiSquad, String key)
```
Returns a pbg value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelPlayerTarget`
```lua
AISquad_GetStateModelPlayerTarget(SquadID aiSquad, String key)
```
Returns a Player value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelSquadTarget`
```lua
AISquad_GetStateModelSquadTarget(SquadID aiSquad, String key)
```
Returns a Squad value from the AISquad's state model corresponding to the given key.

### `AISquad_GetStateModelVector3f`
```lua
AISquad_GetStateModelVector3f(SquadID aiSquad, String key)
```
Returns a Vector3f value from the AISquad's state model corresponding to the given key.

### `AISquad_HasBeenAttacked`
```lua
AISquad_HasBeenAttacked(SquadID pAISquad, Integer historyTicks)
```
Checks if the squad has been attacked within this time

### `AISquad_HasFiredWeapon`
```lua
AISquad_HasFiredWeapon(SquadID pAISquad, Integer historyTicks)
```
Checks if the squad has fired its weapon within this time

### `AISquad_HasPathWithinDistance`
```lua
AISquad_HasPathWithinDistance(SquadID aiSquad, Position targetPosition, Real maxDistance)
```
Returns true if a path shorter than maxDistance between the AISquad and the target exists

### `AISquad_IsRunningSquadTacticAbility`
```lua
AISquad_IsRunningSquadTacticAbility(SquadID aiSquad, PropertyBagGroup abilityPBG)
```
returns true if the AISquad is currently running the AISquadAbilityTactic for the passed abilityPBG

### `AISquad_SetStateModelBool`
```lua
AISquad_SetStateModelBool(SquadID aiSquad, String key, Boolean value)
```
Sets a boolean value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelEntityTarget`
```lua
AISquad_SetStateModelEntityTarget(SquadID aiSquad, String key, EntityID value)
```
Sets an Entity TargetHandle value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelEnumTableBool`
```lua
AISquad_SetStateModelEnumTableBool(SquadID aiSquad, String key, Integer tableRowIndex, Boolean value)
```
Sets a boolean value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTableEntityTarget`
```lua
AISquad_SetStateModelEnumTableEntityTarget(SquadID aiSquad, String key, Integer tableRowIndex, EntityID value)
```
Sets an Entity TargetHandle value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTableFloat`
```lua
AISquad_SetStateModelEnumTableFloat(SquadID aiSquad, String key, Integer tableRowIndex, Real value)
```
Sets a float value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTableInt`
```lua
AISquad_SetStateModelEnumTableInt(SquadID aiSquad, String key, Integer tableRowIndex, Integer value)
```
Sets an integer value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTablePBG`
```lua
AISquad_SetStateModelEnumTablePBG(SquadID aiSquad, String key, Integer tableRowIndex, PropertyBagGroup value)
```
Sets a pbg value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTablePlayerTarget`
```lua
AISquad_SetStateModelEnumTablePlayerTarget(SquadID aiSquad, String key, Integer tableRowIndex, PlayerID value)
```
Sets a Player TargetHandle value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTableSquadTarget`
```lua
AISquad_SetStateModelEnumTableSquadTarget(SquadID aiSquad, String key, Integer tableRowIndex, SquadID value)
```
Sets a Squad TargetHandle value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelEnumTableVector3f`
```lua
AISquad_SetStateModelEnumTableVector3f(SquadID aiSquad, String key, Integer tableRowIndex, Position value)
```
Sets a Vector3f value in the AISquad's state model corresponding to the given key and table row index (0 based).

### `AISquad_SetStateModelFloat`
```lua
AISquad_SetStateModelFloat(SquadID aiSquad, String key, Real value)
```
Sets a float value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelInt`
```lua
AISquad_SetStateModelInt(SquadID aiSquad, String key, Integer value)
```
Sets an integer value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelPBG`
```lua
AISquad_SetStateModelPBG(SquadID aiSquad, String key, PropertyBagGroup value)
```
Sets a pbg value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelPlayerTarget`
```lua
AISquad_SetStateModelPlayerTarget(SquadID aiSquad, String key, PlayerID value)
```
Sets a Player TargetHandle value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelSquadTarget`
```lua
AISquad_SetStateModelSquadTarget(SquadID aiSquad, String key, SquadID value)
```
Sets a Squad TargetHandle value in the AISquad's state model corresponding to the given key.

### `AISquad_SetStateModelVector3f`
```lua
AISquad_SetStateModelVector3f(SquadID aiSquad, String key, Position value)
```
Sets a Vector3f value in the AISquad's state model corresponding to the given key.

### `AISquad_ShouldFallBackOrBraceSelf`
```lua
AISquad_ShouldFallBackOrBraceSelf(SquadID pAISquad)
```
Checks if the squad should fall back or brace itself given the current situation.

## AIStateTree (1 functions)

### `AIStateTree_SpawnRootControllerWithStateModelTunings`
```lua
AIStateTree_SpawnRootControllerWithStateModelTunings(PlayerID pPlayer, String openingBranchName, Boolean keepAlive, ScarAIStateModelTuningsPBG stateModelTuningsScarPBG, SGroupID stateModelSGroupListTunings, EGroupID stateModelEGroupListTunings, Position stateModelPositionTargetListTunings, MarkerID stateModelMarkerTargetListTunings, String list stateModelEntityTypeListTunings, LuaMap<ScarAIFormationCoordinatorPBG> stateModelCoordinatorPBGListTunings, Boolean stateModelBoolTunings, Real stateModelFloatTunings, Integer stateModelIntTunings)
```
On the AIPlayer statetree, spawn a Root Controller with tunings that can be pushed onto the Root Controller's StateModel.

## AITactic (4 functions)

### `AITactic_AdjustJumpSlideAbilityTarget`
```lua
AITactic_AdjustJumpSlideAbilityTarget(SquadID aiSquad, PropertyBagGroup abilityPBG, Real slideOffset, Position targetPosition)
```
calculates a valid target position for a jump slide ability

### `AITactic_AICommandSquadMove`
```lua
AITactic_AICommandSquadMove(SquadID aiSquad, Position target, Real acceptableProximity, Boolean reverseMove)
```
Issue an AI move command to a squad

### `AITactic_GetObjectiveTimerSeconds`
```lua
AITactic_GetObjectiveTimerSeconds(Integer objectiveID)
```
Get the number of seconds on an objective timer.

### `AITactic_GetTacticPriority`
```lua
AITactic_GetTacticPriority(SquadID pSquad, AITacticType tacticType)
```
Get tactic priority for a squad.

## AllMarkers (1 functions)

### `AllMarkers_FromName`
```lua
AllMarkers_FromName(String name, String type)
```
Returns all ScarMarkers from the Scenario Editor with the given name. If you don't care about the type, pass in an empty string ( "" )

## App (4 functions)

### `App_ClearMovieModeFramerate`
```lua
App_ClearMovieModeFramerate()
```
Remove the movie mode framerate restriction

### `app_currenttime`
```lua
app_currenttime()
```
Return the current app time

### `app_setidealframerate`
```lua
app_setidealframerate(Integer frameRate)
```
Set the ideal frame rate for the game. Set to 0 if an unbounded frame rate is desired.

### `App_SetMovieModeFramerate`
```lua
App_SetMovieModeFramerate(Integer frameRate)
```
Run the game at specified frame rate (for capturing movies). Only works with 60 or 120, other rates are defaulted to 60. Setting it to 0 disables movie mode

## BP (58 functions)

### `BP_GenerateWave`
```lua
BP_GenerateWave(Player& player, String waveBpShortName, Real resourceMultiplier)
```
Returns a table containing the unit composition of a wave. A list of units and the number of them that should spawned for a wave. Returns a table with rows containing the following fields - int id = the group idx that this entry came from in the wave bag - int archetypeGroupId = the enum id of the unit group defined in the wave bag for this entry - int archetypeId - the archetype that that has been chosen out of the archetypeGroupId - int count - the number of units to spawn - ScarSquadPBG sbp - the blueprint of the unit to spawn

### `BP_GetAbilityBlueprint`
```lua
BP_GetAbilityBlueprint(String pbgShortname)
```
Returns an ability property bag group.

### `BP_GetAbilityBlueprintByPbgID`
```lua
BP_GetAbilityBlueprintByPbgID(Integer pbgID)
```
Returns an ability property bag group.

### `BP_GetAIAbilityBlueprint`
```lua
BP_GetAIAbilityBlueprint(String pbgShortname)
```
Returns an AIAbility property bag group.

### `BP_GetAIAbilityBlueprintByPbgID`
```lua
BP_GetAIAbilityBlueprintByPbgID(Integer pbgID)
```
Returns an AIAbility property bag group.

### `BP_GetAIFormationCoordinatorBlueprint`
```lua
BP_GetAIFormationCoordinatorBlueprint(String pbgShortname)
```
Returns an AIFormationCoordinator property bag group.

### `BP_GetAIFormationCoordinatorBlueprintByPbgID`
```lua
BP_GetAIFormationCoordinatorBlueprintByPbgID(Integer pbgID)
```
Returns an AIFormationCoordinator property bag group.

### `BP_GetAIFormationTargetPriorityBlueprint`
```lua
BP_GetAIFormationTargetPriorityBlueprint(String pbgShortname)
```
Returns an AIFormationTargetPriority property bag group.

### `BP_GetAIFormationTargetPriorityBlueprintByPbgID`
```lua
BP_GetAIFormationTargetPriorityBlueprintByPbgID(Integer pbgID)
```
Returns an AIFormationTargetPriority property bag group.

### `BP_GetAIStateModelTuningsBlueprint`
```lua
BP_GetAIStateModelTuningsBlueprint(String pbgShortname)
```
Returns an AIStateModelTunings property bag group.

### `BP_GetAIStateModelTuningsBlueprintByPbgID`
```lua
BP_GetAIStateModelTuningsBlueprintByPbgID(Integer pbgID)
```
Returns an AIStateModelTunings property bag group.

### `BP_GetBlueprintArchetypeTypename`
```lua
BP_GetBlueprintArchetypeTypename(FamilyIndex index)
```
Returns the string name of the BLUEPRINT_ARCHETYPE enum entry

### `BP_GetEntityArchetypeBlueprintForPlayer`
```lua
BP_GetEntityArchetypeBlueprintForPlayer(Player& player, FamilyIndex index)
```
Returns an entity blueprint of type BLUEPRINT_ARCHETYPE index for the associated race for the player.

### `BP_GetEntityArchetypeBlueprintForRace`
```lua
BP_GetEntityArchetypeBlueprintForRace(ScarRacePBG racePBG, FamilyIndex index)
```
Returns an entity blueprint of type BLUEPRINT_ARCHETYPE index for the associated race.

### `BP_GetEntityBlueprint`
```lua
BP_GetEntityBlueprint(String pbgShortname)
```
Returns an entity property bag group.

### `BP_GetEntityBlueprintByPbgID`
```lua
BP_GetEntityBlueprintByPbgID(Integer pbgID)
```
Returns an entity property bag group.

### `BP_GetEntityBPBuildTime`
```lua
BP_GetEntityBPBuildTime(ScarEntityPBG entityBag)
```
Returns the unmodified build time in seconds from cost_ext for a given entity blueprint.

### `BP_GetEntityBPCost`
```lua
BP_GetEntityBPCost(ScarEntityPBG entityBag)
```
Returns the resource costs from cost_ext for a given entity blueprint.

### `BP_GetEntityBPDefaultSpeed`
```lua
BP_GetEntityBPDefaultSpeed(ScarEntityPBG entityBag, Boolean getModifiedSpeed, PlayerID player)
```
Returns the default movement speed from moving_ext for a given entity blueprint. If getModifiedSpeed is true, the value will be modified by any speed_maximum_modifier applied to the player for the given entity blueprint.

### `BP_GetEntityChildBlueprintAtIndex`
```lua
BP_GetEntityChildBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns the child blueprint of the specified entity blueprint at specified index.

### `BP_GetEntityChildBlueprintCount`
```lua
BP_GetEntityChildBlueprintCount(String pbgShortname)
```
Returns the number of child blueprints of the specified entity blueprint.

### `BP_GetEntityParentBlueprintAtIndex`
```lua
BP_GetEntityParentBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns the parent blueprint of the specified entity blueprint at specified index

### `BP_GetEntityParentBlueprintCount`
```lua
BP_GetEntityParentBlueprintCount(String pbgShortname)
```
Returns the number of parent blueprints of the specified entity blueprint.

### `BP_GetEntityTypeExtRaceBlueprintAtIndex`
```lua
BP_GetEntityTypeExtRaceBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns race blueprint associated with an entity blueprint type_ext at specified index.

### `BP_GetEntityTypeExtRaceCount`
```lua
BP_GetEntityTypeExtRaceCount(String pbgShortname)
```
Returns the number of race blueprints associated with an entity blueprint type_ext.

### `BP_GetEntityUIInfo`
```lua
BP_GetEntityUIInfo(ScarEntityPBG ebp)
```
Returns a table containing the ui_ext info for given entity

### `BP_GetMapPoolBlueprint`
```lua
BP_GetMapPoolBlueprint(String pbgShortname)
```
Returns a map pool property bag group.

### `BP_GetMapPoolBlueprintByPbgID`
```lua
BP_GetMapPoolBlueprintByPbgID(Integer pbgID)
```
Returns a map pool property bag group.

### `BP_GetMoveTypeBlueprint`
```lua
BP_GetMoveTypeBlueprint(String pbgShortname)
```
Returns a move type property bag group.

### `BP_GetMoveTypeBlueprintByPbgID`
```lua
BP_GetMoveTypeBlueprintByPbgID(Integer pbgID)
```
Returns a move type property bag group.

### `BP_GetName`
```lua
BP_GetName(PropertyBagGroup pbg)
```
Return the short name of the group

### `BP_GetPassTypeBlueprint`
```lua
BP_GetPassTypeBlueprint(String pbgShortname)
```
Returns an pass type property bag group.

### `BP_GetPassTypeBlueprintByPbgID`
```lua
BP_GetPassTypeBlueprintByPbgID(Integer pbgID)
```
Returns an pass type property bag group.

### `BP_GetPropertyBagGroupCount`
```lua
BP_GetPropertyBagGroupCount(PropertyBagGroupType type)
```
Return the number of property bag groups of the same type

### `BP_GetPropertyBagGroupPathName`
```lua
BP_GetPropertyBagGroupPathName(PropertyBagGroupType type, Integer index)
```
Return the path name of the group at the specified index

### `BP_GetReticuleBlueprint`
```lua
BP_GetReticuleBlueprint(String pbgShortname)
```
Returns a UIReticuleBag property bag group.

### `BP_GetSimulationFloatProperty`
```lua
BP_GetSimulationFloatProperty(String propertyName)
```
Returns the float value stored for the given property name in the AE simulation tuning.

### `BP_GetSimulationIntProperty`
```lua
BP_GetSimulationIntProperty(String propertyName)
```
Returns the int value stored for the given property name in the AE simulation tuning.

### `BP_GetSlotItemBlueprint`
```lua
BP_GetSlotItemBlueprint(String pbgShortname)
```
Returns a slot item property bag group.

### `BP_GetSlotItemBlueprintByPbgID`
```lua
BP_GetSlotItemBlueprintByPbgID(Integer pbgID)
```
Returns a slot item property bag group.

### `BP_GetSquadArchetypeBlueprintForPlayer`
```lua
BP_GetSquadArchetypeBlueprintForPlayer(Player& player, FamilyIndex index)
```
Returns a squad blueprint of type BLUEPRINT_ARCHETYPE index for the associated race of the player.

### `BP_GetSquadArchetypeBlueprintForRace`
```lua
BP_GetSquadArchetypeBlueprintForRace(ScarRacePBG racePBG, FamilyIndex index)
```
Returns a squad blueprint of type BLUEPRINT_ARCHETYPE index for the associated race.

### `BP_GetSquadBlueprint`
```lua
BP_GetSquadBlueprint(String pbgShortname)
```
Returns a squad property bag group.

### `BP_GetSquadBlueprintByPbgID`
```lua
BP_GetSquadBlueprintByPbgID(String pbgID)
```
Returns a squad property bag group.

### `BP_GetSquadChildBlueprintAtIndex`
```lua
BP_GetSquadChildBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns the child blueprint of the specified squad blueprint at specified index.

### `BP_GetSquadChildBlueprintCount`
```lua
BP_GetSquadChildBlueprintCount(String pbgShortname)
```
Returns the number of child blueprints of the specified squad blueprint.

### `BP_GetSquadParentBlueprintAtIndex`
```lua
BP_GetSquadParentBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns the parent blueprint of the specified squad blueprint at specified index

### `BP_GetSquadParentBlueprintCount`
```lua
BP_GetSquadParentBlueprintCount(String pbgShortname)
```
Returns the number of parent blueprints of the specified squad blueprint.

### `BP_GetSquadTypeExtRaceBlueprintAtIndex`
```lua
BP_GetSquadTypeExtRaceBlueprintAtIndex(String pbgShortname, Integer index)
```
Returns race blueprint associated with a squad blueprint squad_type_ext at specified index.

### `BP_GetSquadTypeExtRaceCount`
```lua
BP_GetSquadTypeExtRaceCount(String pbgShortname)
```
Returns the number of race blueprints associated with a squad blueprint squad_type_ext.

### `BP_GetSquadUIInfo`
```lua
BP_GetSquadUIInfo(ScarSquadPBG sbp, ScarRacePBG rbp)
```
Returns a table containing the ui_ext info for given squad and race

### `BP_GetType`
```lua
BP_GetType(StackVar v)
```
Returns the type of a blueprint.

### `BP_GetUpgradeBlueprint`
```lua
BP_GetUpgradeBlueprint(String pbgShortname)
```
Returns an upgrade property bag group.

### `BP_GetUpgradeBlueprintByPbgID`
```lua
BP_GetUpgradeBlueprintByPbgID(Integer pbgID)
```
Returns an upgrade property bag group.

### `BP_GetUpgradeUIInfo`
```lua
BP_GetUpgradeUIInfo(ScarUpgradePBG ubp)
```
Returns a table containing the ui_ext info for given upgrade

### `BP_GetWeaponBlueprint`
```lua
BP_GetWeaponBlueprint(String pbgShortname)
```
Returns a weapon property bag group.

### `BP_GetWeaponBlueprintByPbgID`
```lua
BP_GetWeaponBlueprintByPbgID(Integer pbgID)
```
Returns a weapon property bag group.

### `BP_IsUpgradeOfType`
```lua
BP_IsUpgradeOfType(ScarUpgradePBG upgradePBG, String key)
```
Returns true if the UpgradePGB's list of types includes the given type

## Camera (47 functions)

### `Camera_ClampToMarker`
```lua
Camera_ClampToMarker(MarkerID marker)
```
Clamps the camera's target position to a marker.

### `Camera_ExecuteBSplinePan`
```lua
Camera_ExecuteBSplinePan(Real totalT, Boolean controlRotation)
```
Execute spline pan based on queued control points. Use B-Spline interpolation of points

### `Camera_ExecuteCaptureCameraPan`
```lua
Camera_ExecuteCaptureCameraPan(StackVarTable cameraPanTable)
```
Executes a camera pan that was captured using the Capture Tool. Expects that the "camera_spline" Camera set was pushed to the CameraSwitchboard, using Camera_Push("camera_spline") Returns the duration of the spline, so that the user can call Camera_Pop()

### `Camera_ExecuteCatromSplinePan`
```lua
Camera_ExecuteCatromSplinePan(Real totalT, Boolean controlRotation)
```
Execute spline pan based on queued control points. Use Catmull-Rom interpolation of points

### `Camera_ExecuteLinearSplinePan`
```lua
Camera_ExecuteLinearSplinePan(Real totalT, Boolean controlRotation)
```
Execute spline pan based on queued control points. Use linear interpolation between points

### `Camera_FocusOnPosition`
```lua
Camera_FocusOnPosition(Position position)
```
Focus the camera on the specified position.

### `Camera_FollowEntity`
```lua
Camera_FollowEntity(EntityID entity)
```
Make the camera follow the specified entity.

### `Camera_FollowSelection`
```lua
Camera_FollowSelection()
```
Make the camera follow the current full selection.

### `Camera_FollowSquad`
```lua
Camera_FollowSquad(SquadID squad)
```
Make the camera follow the specified squad.

### `Camera_GetCurrentPos`
```lua
Camera_GetCurrentPos()
```
Get the current position for the camera. (Where the the camera currently is.)

### `Camera_GetCurrentTargetPos`
```lua
Camera_GetCurrentTargetPos()
```
Get the current target position for the camera. (Where the the camera currently is.)

### `Camera_GetDeclination`
```lua
Camera_GetDeclination()
```
Get the current camera declination (tilt).

### `Camera_GetDefaultOrbit`
```lua
Camera_GetDefaultOrbit()
```
Get the default camera orbit (rotation).

### `Camera_GetOrbit`
```lua
Camera_GetOrbit()
```
Get the current camera orbit (rotation).

### `Camera_GetPivot`
```lua
Camera_GetPivot()
```
Get the pivot of the camera. (The position about which the camera is pivoting).

### `Camera_GetTargetPos`
```lua
Camera_GetTargetPos()
```
Get the desired target position for the camera. (Where the camera is trying to get to.)

### `Camera_GetZoomDist`
```lua
Camera_GetZoomDist()
```
Get the current zoom distance for the camera.

### `Camera_HideMesh`
```lua
Camera_HideMesh()
```
Hide the camera mesh.

### `Camera_IsInputEnabled`
```lua
Camera_IsInputEnabled()
```
Returns the enabled/disabled state of the camera input.  (not deterministic)

### `Camera_IsMeshShown`
```lua
Camera_IsMeshShown()
```
Is the camera mesh being shown?

### `Camera_QueueRelativeSplinePanPos`
```lua
Camera_QueueRelativeSplinePanPos(Position deltaPos)
```
Queue a spline control point by position relative to the last queued position. Pan is deferred until requested by an execution function

### `Camera_QueueSplinePanPos`
```lua
Camera_QueueSplinePanPos(Position pos)
```
Queue a spline control point by absolute position. Pan is deferred until requested by an execution function

### `Camera_ResetFocus`
```lua
Camera_ResetFocus()
```
Make the camera stop following anything.

### `Camera_ResetOrbit`
```lua
Camera_ResetOrbit()
```
Set the current camera orbit relative to the current orbit (relative rotation).

### `Camera_ResetToDefault`
```lua
Camera_ResetToDefault()
```
Reset camera position to default home position

### `Camera_SetDeclination`
```lua
Camera_SetDeclination(Real declination)
```
Set the current camera declination (tilt).

### `Camera_SetDefaultDeclination`
```lua
Camera_SetDefaultDeclination(Real declination)
```
Set the default camera declination (tilt).

### `Camera_SetDefaultOrbit`
```lua
Camera_SetDefaultOrbit(Real orbit)
```
Set the default camera orbit (rotation).

### `Camera_SetDefaultZoomDist`
```lua
Camera_SetDefaultZoomDist(Real distance)
```
Set the default zoom distance for the camera.

### `Camera_SetFov`
```lua
Camera_SetFov(Real fov)
```
Set the current camera field of view (fov)

### `Camera_SetInputEnabled`
```lua
Camera_SetInputEnabled(Boolean enabled)
```
Enables/disables camera input.

### `Camera_SetOrbit`
```lua
Camera_SetOrbit(Real orbit)
```
Set the current camera orbit (rotation).

### `Camera_SetOrbitRelative`
```lua
Camera_SetOrbitRelative(Real deltaOrbit)
```
Set the current camera orbit relative to the current orbit (relative rotation).

### `Camera_SetZoomDist`
```lua
Camera_SetZoomDist(Real distance)
```
Set the current zoom distance for the camera.

### `Camera_ShowMesh`
```lua
Camera_ShowMesh()
```
Show the camera mesh.

### `Camera_StartDeltaOrbit`
```lua
Camera_StartDeltaOrbit(Real deltaOrbit, Real totalT)
```
Orbit the camera a given number of degrees clockwise from the current orbit position in a given amount of time.

### `Camera_StartOrbit`
```lua
Camera_StartOrbit(Real endOrbit, Real totalT)
```
Orbit the camera to an end orbit position from the current orbit position in a given amount of time. Will choose shortest rotational direction.

### `Camera_StartPan`
```lua
Camera_StartPan(Position startPos, Position endPos, Real totalT, Real zoomDistance)
```
Pan the camera between two positions in a given amount of time. Interpolates the camera to the given zoom.

### `Camera_StartPanTo`
```lua
Camera_StartPanTo(Position endPos, Real totalT, Real zoomDistance)
```
Pan the camera to a position in a given amount of time from the position in front of the queue.

### `Camera_StartRelativePan`
```lua
Camera_StartRelativePan(Position deltaPos, Real totalT, Real zoomDistance)
```
Pan the camera by some amount in a given amount of time. This is relative to the position in front of the queue.

### `Camera_StartRelativeZoomDist`
```lua
Camera_StartRelativeZoomDist(Real deltaZoomDist, Real totalT)
```
Start a transition to a relative zoom distance over a certain amount of time.

### `Camera_StartZoomDist`
```lua
Camera_StartZoomDist(Real startZoomDist, Real endZoomDist, Real totalT)
```
Start a transition from one zoom distance to another over a certain amount of time.

### `Camera_StartZoomDistTo`
```lua
Camera_StartZoomDistTo(Real endZoomDist, Real totalT)
```
Start a transition to a zoom distance over a certain amount of time.

### `Camera_StopPan`
```lua
Camera_StopPan()
```
Stop an ongoing camera pan.

### `Camera_ToggleDebugCamera`
```lua
Camera_ToggleDebugCamera()
```
Toggle the debug free camera

### `Camera_ToggleMeshShown`
```lua
Camera_ToggleMeshShown(Boolean show)
```
Toggle the camera mesh.

### `Camera_Unclamp`
```lua
Camera_Unclamp()
```
Frees up the camera (so it's not clamped to a marker anymore).

## Cheat (2 functions)

### `Cheat_GrantAllRibbonsAndMedals`
```lua
Cheat_GrantAllRibbonsAndMedals()
```
Cheat to award all ribbons and medals

### `Cheat_ResetAchievementProgress`
```lua
Cheat_ResetAchievementProgress()
```
Cheat to reset all achievement progress

## cmdline (1 functions)

### `cmdline_string`
```lua
cmdline_string(String name)
```
Get the value for a command line arg.

## Command (1 functions)

### `Command_PlayerBroadcastMessage`
```lua
Command_PlayerBroadcastMessage(PlayerID player, PlayerID dest, Integer messageType, String message)
```
Send a message to a player with generic type a body

## Cursor (9 functions)

### `Cursor_Distance`
```lua
Cursor_Distance()
```
Toggle cursor position distance drawring

### `Cursor_GetClearWeaponShotHistory`
```lua
Cursor_GetClearWeaponShotHistory()
```
Toggle clearing of cursor over entity weapon shot history debug display

### `Cursor_GetDrawWeaponShotHistory`
```lua
Cursor_GetDrawWeaponShotHistory()
```
Toggle cursor over entity weapon shot history debug display

### `cursor_hide`
```lua
cursor_hide()
```
Hide the cursor

### `Cursor_Info`
```lua
Cursor_Info()
```
Toggle cursor position information

### `cursor_setposition`
```lua
cursor_setposition(Real x, Real y)
```
Set the cursor position

### `cursor_show`
```lua
cursor_show()
```
Show the cursor

### `Cursor_WeaponInfo`
```lua
Cursor_WeaponInfo()
```
Toggle cursor over entity weapon information

### `Cursor_WeaponRanges`
```lua
Cursor_WeaponRanges()
```
Toggle cursor over entity weapon range information

## dca (1 functions)

### `dca_get_variable_value`
```lua
dca_get_variable_value(EntityID pEntity, String variableName)
```
Get dca variable value for an entity. Can be used to validate presentation state from lua.

## Debug (3 functions)

### `Debug_IgnoreMouseOverCheck`
```lua
Debug_IgnoreMouseOverCheck()
```
Toggles on or off under mouse check. If ignoring mouse check, all entities will have the enabled debug info displayed

### `Debug_ToggleControlAll`
```lua
Debug_ToggleControlAll()
```
Allows the local player to issue commands to any unit regardless of ownership.

### `Debug_ToggleDebugTest`
```lua
Debug_ToggleDebugTest()
```
Toggles on or off all debug test activity

## Decal (5 functions)

### `Decal_Create`
```lua
Decal_Create(String decalName, Position position, Real xScale, Real yScale, Real zScale, Real rotationDegrees, Integer r, Integer g, Integer b, Integer a)
```
Add a decal to the terrain. Returns a unique decal id allow for future removal via Decal_Destroy

### `Decal_Destroy`
```lua
Decal_Destroy(Integer decalID)
```
Destroy a decal by unique id

### `Decal_GetInvalidID`
```lua
Decal_GetInvalidID()
```
Get the Decal ID that represents an invalid decal (useful to check if creation failed)

### `Decal_GetNextDecalId`
```lua
Decal_GetNextDecalId()
```
Returns the current decal id in use; used in conjunction with Decal_RemoveAllDecalsAfterId

### `Decal_RemoveAllDecalsAfterId`
```lua
Decal_RemoveAllDecalsAfterId(Integer id)
```
Erases all placed decals after id (inclusive); used in conjunction with Decal_GetNextDecalId

## DisplayAdapterDatabase (13 functions)

### `DisplayAdapterDatabase_CheckBoolOverride`
```lua
DisplayAdapterDatabase_CheckBoolOverride(String setting)
```
Query the display adapter database for a boolean setting override.

### `DisplayAdapterDatabase_CheckFloatOverride`
```lua
DisplayAdapterDatabase_CheckFloatOverride(String setting)
```
Query the display adapter database for a floating-point setting override.

### `DisplayAdapterDatabase_CheckIntOverride`
```lua
DisplayAdapterDatabase_CheckIntOverride(String setting)
```
Query the display adapter database for an integer setting override.

### `DisplayAdapterDatabase_CheckMinimumDriverVersion`
```lua
DisplayAdapterDatabase_CheckMinimumDriverVersion()
```
Output the installed display adapter driver version, the required version for the current adapter, and whether or not the installed version is equal to or greater than the required one.

### `DisplayAdapterDatabase_CheckUint16Override`
```lua
DisplayAdapterDatabase_CheckUint16Override(String setting)
```
Query the display adapter database for a uint16 setting override.

### `DisplayAdapterDatabase_CheckUint8Override`
```lua
DisplayAdapterDatabase_CheckUint8Override(String setting)
```
Query the display adapter database for a uint8 setting override.

### `DisplayAdapterDatabase_CheckUintOverride`
```lua
DisplayAdapterDatabase_CheckUintOverride(String setting)
```
Query the display adapter database for a uint32 setting override.

### `DisplayAdapterDatabase_GetAdapterFromID`
```lua
DisplayAdapterDatabase_GetAdapterFromID(String vendor, String device, String subsystem, String revision)
```
Query the display adapter database for information about a specified adapter.

### `DisplayAdapterDatabase_GetAdapterID`
```lua
DisplayAdapterDatabase_GetAdapterID()
```
Output basic information about the current display adapter.

### `DisplayAdapterDatabase_GetAdapterMinimumDriverVersion`
```lua
DisplayAdapterDatabase_GetAdapterMinimumDriverVersion(String vendor, String device, String subsystem, String revision)
```
Query the display adapter database for the minimum required driver version for a specified adapter.

### `DisplayAdapterDatabase_GetCurrentAdapterPerformanceClass`
```lua
DisplayAdapterDatabase_GetCurrentAdapterPerformanceClass()
```
Query the display adapter database for the performance class of the currently-installed display adapter.

### `DisplayAdapterDatabase_GetDriverInfo`
```lua
DisplayAdapterDatabase_GetDriverInfo()
```
Output basic information about the currently installed display adapter driver.

### `DisplayAdapterDatabase_GetPerformanceClass`
```lua
DisplayAdapterDatabase_GetPerformanceClass(Real relativePerformance)
```
Query the display adapter database for the performance class given a relative performance percentage.

## dr (10 functions)

### `dr_clear`
```lua
dr_clear(String frame)
```
Clear debug rendering.

### `dr_drawCircle`
```lua
dr_drawCircle(String frame, Real x, Real y, Real z, Real radius, Integer r, Integer g, Integer b)
```
Draw a circle, positioned in 3D, aligned to scren.

### `dr_drawline`
```lua
dr_drawline(Position pos0, Position pos1, Integer r, Integer g, Integer b, StackVar svar)
```
Draw line. If you don't pass in a name, TerrainLine is used.

### `dr_setautoclear`
```lua
dr_setautoclear(String frame, Boolean bEnable)
```
Set auto clear for named frame.

### `dr_setdisplay`
```lua
dr_setdisplay(String frame, Boolean bEnable)
```
Set display of named frame.

### `dr_terraincircle`
```lua
dr_terraincircle(Position pos, Real radius, Real r, Real g, Real b, Integer divs, String frame)
```
Draw circle on terrain.

### `dr_terraincirclewithlifetime`
```lua
dr_terraincirclewithlifetime(Position pos, Real radius, Real r, Real g, Real b, Integer divs, String frame, Real lifetime)
```
Draw circle on terrain with lifetime.

### `dr_terrainrect`
```lua
dr_terrainrect(Position pos, Real w, Real h, Real r, Real g, Real b, Real rads)
```
Draw rectangle on terrian.

### `dr_text2d`
```lua
dr_text2d(String frame, Real x, Real y, String cmd, Integer r, Integer g, Integer b)
```
Draw text, positioned in 2D, aligned to the screen.

### `dr_text3d`
```lua
dr_text3d(String frame, Real x, Real y, Real z, String cmd, Integer r, Integer g, Integer b)
```
Draw text, positioned in 3D, aligned to screen.

## EBP (3 functions)

### `EBP_Exists`
```lua
EBP_Exists(String pbgShortname)
```
Returns true if an entity blueprint exists with the given name.

### `EBP_IsOfRace`
```lua
EBP_IsOfRace(String pbgShortname, ScarRacePBG race)
```
Returns whether the entity blueprint is of specified race

### `EBP_PopulationCost`
```lua
EBP_PopulationCost(PropertyBagGroup ebpUnit, PlayerID player, CapType type)
```
get Entity blueprint pop cost, use CT_Personnel, CT_Vehicle, CT_Medic for captype

## EGroup (30 functions)

### `EGroup_Add`
```lua
EGroup_Add(EGroupID group, EntityID entity)
```
Adds an entity to the end of a group if the group doesnt already have it.

### `EGroup_AddEGroup`
```lua
EGroup_AddEGroup(EGroupID group, EGroupID grouptoadd)
```
Appends the entities in one group to another group.

### `EGroup_Clear`
```lua
EGroup_Clear(EGroupID egroup)
```
Removes all entities from a group

### `EGroup_Compare`
```lua
EGroup_Compare(EGroupID group1, EGroupID group2)
```
Returns true if the contents of the two groups are equal. Order of the entities does not matter.

### `EGroup_Count`
```lua
EGroup_Count(EGroupID egroup)
```
Returns the total number of spawned and despawned entities in a group.

### `EGroup_CountDeSpawned`
```lua
EGroup_CountDeSpawned(EGroupID egroup)
```
Returns the number of despawned entities in a group.

### `EGroup_CountSpawned`
```lua
EGroup_CountSpawned(EGroupID egroup)
```
Returns the number of spawned entities in a group.

### `EGroup_Create`
```lua
EGroup_Create(String name)
```
Returns a new entity group with the given name.

### `EGroup_CreateUniqueWithPrefix`
```lua
EGroup_CreateUniqueWithPrefix(String prefix)
```
Returns a new entity group with an autogenerated unique name, optionally prefixed by the string passed in.

### `EGroup_Destroy`
```lua
EGroup_Destroy(EGroupID egroup)
```
Manually destroy a group that you don't need anymore.

### `EGroup_Exists`
```lua
EGroup_Exists(String name)
```
Returns true if the entity group with the given name exists

### `EGroup_Filter_Internal`
```lua
EGroup_Filter_Internal(EGroupID group, StackVar blueprints, ScarFilterType filterType, StackVar optionalSplitGroup)
```
Internal implementation of EGroup_Filter for the purposes of optional arguments. Don't use directly, use EGroup_Filter

### `EGroup_FilterResource`
```lua
EGroup_FilterResource(EGroupID group, String name, EGroupID resource)
```
Filters EGroup with given name out of given EGroup into the resource EGroup.

### `EGroup_ForEach`
```lua
EGroup_ForEach(EGroupID egroup, StackVarFunction f)
```
Call a lua function for each item in a group. Function will recieve (groupid, itemindex, itemid) and should return true to break or false to continue.

### `EGroup_ForEachAllOrAny`
```lua
EGroup_ForEachAllOrAny(EGroupID egroup, Boolean all, StackVarFunction f)
```
Call a lua function for each item in a group. Function will receive (groupid, itemindex, itemid) and should return a bool.

### `EGroup_ForEachAllOrAnyEx`
```lua
EGroup_ForEachAllOrAnyEx(EGroupID egroup, Boolean all, StackVarFunction f, Boolean spawned, Boolean despawned)
```
Same as EGroup_ForEachAllOrAny except you have a choice to iterate over spawned entities, despawned entities, or both.

### `EGroup_ForEachEx`
```lua
EGroup_ForEachEx(EGroupID egroup, StackVarFunction f, Boolean spawned, Boolean despawned)
```
Same as EGroup_ForEach except you have a choice to iterate over spawned entities, despawned entities, or both.

### `EGroup_FromName`
```lua
EGroup_FromName(String name)
```
Find an entity group with a given name.

### `EGroup_GetClosestEntityInternal`
```lua
EGroup_GetClosestEntityInternal(EGroupID group, Vector3f position)
```
Returns the closest entity of an entity group to the given position.

### `EGroup_GetDeSpawnedEntityAt`
```lua
EGroup_GetDeSpawnedEntityAt(EGroupID group, Integer int)
```
Returns the despawned entity at the given index.

### `EGroup_GetEntityAt`
```lua
EGroup_GetEntityAt(EGroupID group, Integer int)
```
Returns the entity at the given index.

### `EGroup_GetName`
```lua
EGroup_GetName(EGroupID egroup)
```
Returns the name of a given entity group.

### `EGroup_GetPosition`
```lua
EGroup_GetPosition(EGroupID group)
```
Returns the center position of an entity group.

### `EGroup_GetSpawnedEntityAt`
```lua
EGroup_GetSpawnedEntityAt(EGroupID group, Integer int)
```
Returns the spawned entity at the given index.

### `EGroup_Intersection`
```lua
EGroup_Intersection(EGroupID group, EGroupID grouptointersect)
```
Performs a group intersection.

### `EGroup_IsValid`
```lua
EGroup_IsValid(Integer egroupID)
```
Check to see if an egroup still exists without needing the name.

### `EGroup_Remove`
```lua
EGroup_Remove(EGroupID group, EntityID entity)
```
Removes an entity from a group.

### `EGroup_RemoveAllMatching`
```lua
EGroup_RemoveAllMatching(EGroupID group, EGroupID grouptocompare)
```
Removes any entites that exist in both groups.

### `EGroup_RemoveNonHoldEntities`
```lua
EGroup_RemoveNonHoldEntities(EGroupID egroup)
```
Removes all the entities from the EGroup that don't have HoldExt on them

### `EGroup_SortBasedOnHealth`
```lua
EGroup_SortBasedOnHealth(EGroupID egroup, Boolean ascending)
```
Sorts the EGroup based on health

## Entity (230 functions)

### `Entity_ActiveCommandIs`
```lua
Entity_ActiveCommandIs(EntityID entity, EntityCommandType cmdtype)
```
Returns true if the active command is of the type we specified

### `Entity_AddAbility`
```lua
Entity_AddAbility(EntityID entity, ScarAbilityPBG ability)
```
Allows the entity to use this ability

### `Entity_AddResource`
```lua
Entity_AddResource(EntityID entity, Integer type, Real amount)
```
Add a specific amount of a certain resource type to an entity.

### `Entity_AdjustAbilityCooldown`
```lua
Entity_AdjustAbilityCooldown(EntityID entity, Integer tickAmount)
```
Advance ability cooldown

### `Entity_BuildCycleList`
```lua
Entity_BuildCycleList()
```
Builds the cycle list based on current tagged entity

### `Entity_CalcConstructionPlacement`
```lua
Entity_CalcConstructionPlacement(ScarEntityPBG ebp, PlayerID ructingPlayer, Position inputPosition)
```
Returns where a construction command would place a given ebp if the command was targeted at a given world position. Ignores checks for fog of war and unexplored areas since scripts often want to spawn entities in places the player cannot see. Returns a table with the following fields: - ScarPosition position: the position the building would be placed at - ScarPosition heading: the heading the building would be placed at. You can create a look-at position by adding position and facing together. - Boolean success: whether or not the construction placement would succeed

### `Entity_CalculatePassableSpawnPosition`
```lua
Entity_CalculatePassableSpawnPosition(EntityID entity, Position pos)
```
pass in a entity and position to resolve the position into a open space position, if the position is not free, position returned will try to be the closest position near the original position

### `Entity_CanAttackNow`
```lua
Entity_CanAttackNow(EntityID attacker, Position target)
```
Returns whether an entity can attack a target without moving or turning.

### `Entity_CancelProductionQueueItem`
```lua
Entity_CancelProductionQueueItem(EntityID entity, Integer index)
```
Cancels an item in a production queue.  Index 0 is the currently producing item.

### `Entity_CanCurrentlyBeDamaged`
```lua
Entity_CanCurrentlyBeDamaged(EntityID entity)
```
Check if an entity can currently be damaged.

### `Entity_CanLoadSquad`
```lua
Entity_CanLoadSquad(EntityID entity, SquadID squad, Boolean assumeEmpty, Boolean assumeVisible)
```
Check if the entity can load squad or not

### `Entity_CanSeeEntity`
```lua
Entity_CanSeeEntity(EntityID entity, EntityID target)
```
Returns true if the distance between a target entity and the source entity is less than it entity's sight distance.  There is no LOS or FOW check.

### `Entity_CanSeeSquad`
```lua
Entity_CanSeeSquad(EntityID entity, SquadID target)
```
Returns true if the distance between a target squad and the source entity is less than it entity's sight distance.  There is no LOS or FOW check.

### `Entity_CanTargetEntity`
```lua
Entity_CanTargetEntity(Entity& entity, Entity& target, Boolean checkFOW)
```
Check if an entity can target and attack another entity.

### `Entity_ClearPendingDeathFlag`
```lua
Entity_ClearPendingDeathFlag(EntityID entity)
```
Clear the pending death flag manually. Should be used when campaign leaders are revived.

### `Entity_ClearPostureSuggestion`
```lua
Entity_ClearPostureSuggestion(EntityID entity)
```
Clears any previous posture suggestions made to an entity

### `Entity_ClearStateModelEnumTableTarget`
```lua
Entity_ClearStateModelEnumTableTarget(EntityID entity, String key, Integer tableRowIndex)
```
Clears a TargetHandle value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_ClearStateModelTarget`
```lua
Entity_ClearStateModelTarget(EntityID entity, String key)
```
Clears a TargetHandle value in the entity's state model corresponding to the given key.

### `Entity_ClearTagDebug`
```lua
Entity_ClearTagDebug()
```
Clears the tagged entity used for debugging

### `Entity_CompleteUpgrade`
```lua
Entity_CompleteUpgrade(EntityID pEntity, ScarUpgradePBG upgradePBG)
```
Instantly adds an upgrade to a given entity

### `Entity_ConvertBlueprint`
```lua
Entity_ConvertBlueprint(Entity& entity, PropertyBagGroup pbg)
```
Converts Entity's blueprint to the specified blueprint.

### `Entity_Create`
```lua
Entity_Create(ScarEntityPBG ebp, PlayerID player, Position pos, Boolean snapToTerrain)
```
Creates an entity at a given position and assigns it to a given player. This function does not spawn the entity so you will need to call Entity_Spawn to see this entity

### `Entity_CreateFacing`
```lua
Entity_CreateFacing(ScarEntityPBG ebp, PlayerID player, Position pos, Position toward, Boolean snapToTerrain)
```
Creates an entity at a given position facing a target location and assigns it to a given player. This function does not spawn the entity so you will need to call Entity_Spawn to see this entity

### `Entity_CycleDebug`
```lua
Entity_CycleDebug()
```
Cycle through the existing list built for the originally tagged entity

### `Entity_DeSpawn`
```lua
Entity_DeSpawn(EntityID entity)
```
DeSpawn the entity at its current position

### `Entity_Destroy`
```lua
Entity_Destroy(EntityID entity)
```
Remove an entity from the world and destroy it.

### `Entity_DisableCancelConstructionCommand`
```lua
Entity_DisableCancelConstructionCommand(EntityID entity, Boolean disable)
```
Forces the cancel construction command to be disabled, meaning you can't cancel construction for this

### `Entity_DoBurnDamage`
```lua
Entity_DoBurnDamage(EntityID entity, Real val, Boolean ignoreMaxDamagePerSecond)
```
Adjusts the entity's burn level by val

### `Entity_EnableAttention`
```lua
Entity_EnableAttention(EntityID entity, Boolean attentive)
```
Sets whether an entity pays attention to its surroundings

### `Entity_EnableProductionQueue`
```lua
Entity_EnableProductionQueue(EntityID entity, Boolean enable)
```
Sets whether an entity can produce anything (including upgrades)

### `Entity_EnableStrategicPoint`
```lua
Entity_EnableStrategicPoint(EntityID entity, Boolean enable)
```
Sets whether an strategic point is active

### `Entity_ExtensionCount`
```lua
Entity_ExtensionCount()
```
Returns total entity extension count.

### `Entity_ExtensionEnabled`
```lua
Entity_ExtensionEnabled(EntityID pEntity, ComponentDependencyIndex extID)
```
Returns true if the entity has the specific extension enabled.

### `Entity_ExtensionExecuting`
```lua
Entity_ExtensionExecuting(EntityID pEntity, ComponentDependencyIndex extID)
```
Returns true if the specified extension on the entity will update every frame.

### `Entity_ExtensionName`
```lua
Entity_ExtensionName(EntityID pEntity, ComponentDependencyIndex extID)
```
Returns a string name of the given extension on the entity.

### `Entity_ForceConstruct`
```lua
Entity_ForceConstruct(EntityID e)
```
Force constructs this entity but only if its a building

### `Entity_ForceSelfConstruct`
```lua
Entity_ForceSelfConstruct(EntityID e)
```
Force a building to self construct if it's a building

### `Entity_FromID`
```lua
Entity_FromID(Integer id)
```
Get an entity from a mission editor ID.

### `Entity_GetActiveCommand`
```lua
Entity_GetActiveCommand(EntityID entity)
```
Returns the active entity command.

### `Entity_GetAttackTarget`
```lua
Entity_GetAttackTarget(EntityID entity, SGroupID sgroup)
```
Find the entity target. If found, the target squad is added to the sgroup. Entity targets like buildings are ignored.

### `Entity_GetAttackTargetEntity`
```lua
Entity_GetAttackTargetEntity(EntityID entity)
```
Returns the entity targeted by the given entity.

### `Entity_GetAttackTargetSquad`
```lua
Entity_GetAttackTargetSquad(EntityID entity)
```
Returns the squad targeted by the given entity.

### `Entity_GetBlueprint`
```lua
Entity_GetBlueprint(EntityID entity)
```
Returns the entity's blueprint

### `Entity_GetBuildingProgress`
```lua
Entity_GetBuildingProgress(EntityID pEntity)
```
Returns the construction progress (with range [0.0, 1.0] for a given entity.  Returns 0.0 if the entity is not a building.

### `Entity_GetCoverValue`
```lua
Entity_GetCoverValue(EntityID entity)
```
Get cover safety value from the where the entity is standing. The safety value is number from -.5 to .5.

### `Entity_GetDebugEntity`
```lua
Entity_GetDebugEntity()
```
Get the currently tagged debug entity

### `Entity_GetFenceEntityCount`
```lua
Entity_GetFenceEntityCount(PropertyBagGroup ebp, Position startPos, Position endPos)
```
Returns number of entities that will be placed if this ebp is built in a fence.

### `Entity_GetFilledHoldSquadSlots`
```lua
Entity_GetFilledHoldSquadSlots(EntityID entity)
```
Returns the number of filled slots for squads in a hold in the HoldExtInfo

### `Entity_GetHeading`
```lua
Entity_GetHeading(EntityID entity)
```
Returns the heading of the entity.  The heading is currently a lua table with three entries (x, y, z)

### `Entity_GetHealth`
```lua
Entity_GetHealth(EntityID entity)
```
Returns the health of an entity.

### `Entity_GetHealthMax`
```lua
Entity_GetHealthMax(EntityID entity)
```
Returns the max health of an entity.

### `Entity_GetHealthPercentage`
```lua
Entity_GetHealthPercentage(EntityID entity)
```
Returns the percentage health, taking into account destructible buildings

### `Entity_GetID`
```lua
Entity_GetID(EntityID entity)
```
Returns the entities unique id in the world

### `Entity_GetInvulnerableMinCap`
```lua
Entity_GetInvulnerableMinCap(EntityID entity)
```
Returns the invulnerable point in terms of percentage

### `Entity_GetLastAttacker`
```lua
Entity_GetLastAttacker(EntityID entity, SGroupID sgroup)
```
Find the last squad attacker on this entity. If found, the squad is added to the sgroup

### `Entity_GetLastAttackers`
```lua
Entity_GetLastAttackers(EntityID entity, SGroupID group, Real timeSeconds)
```
Find the squad attackers on this entity from the last seconds specified. The sgroup is cleared, then any squads found are added to the sgroup. Building attackers are ignored.

### `Entity_GetLastEntityAttackers`
```lua
Entity_GetLastEntityAttackers(EntityID entity, EGroupID group, Real timeSeconds)
```
Find the entity attackers on this entity from the last seconds specified. The sgroup is cleared, then any squads found are added to the sgroup. Building attackers are ignored.

### `Entity_GetMaxCaptureCrewSize`
```lua
Entity_GetMaxCaptureCrewSize(EntityID entity)
```
Gets the maximum capture crew size from a recrewable entity

### `Entity_GetMaxHoldSquadSlots`
```lua
Entity_GetMaxHoldSquadSlots(EntityID entity)
```
Returns the number of specified slots for squads in a hold in the HoldExtInfo

### `Entity_GetMeleeBlocksPerAttacks`
```lua
Entity_GetMeleeBlocksPerAttacks(Entity entity)
```
Returns the number of blocks the entity will perform per number of attacks

### `Entity_GetNumInteractors`
```lua
Entity_GetNumInteractors(EntityID entity, String interactionType)
```
Returns the number of entities connected to an entity via the interaction system.

### `Entity_GetOnFireHealthPercentThreshold`
```lua
Entity_GetOnFireHealthPercentThreshold(EntityID entity)
```
Get the entity health percentage where it can be set on fire

### `Entity_GetPlayerOwner`
```lua
Entity_GetPlayerOwner(EntityID entity)
```
Returns the Player owner of the given entity. Entity MUST NOT be owned by the world.

### `Entity_GetPosition`
```lua
Entity_GetPosition(EntityID entity)
```
Returns the position of the entity.  The position is currently a lua table with three entries (x, y, z)

### `Entity_GetProductionQueueItem`
```lua
Entity_GetProductionQueueItem(EntityID entity, Integer index)
```
Returns the blueprint for a production queue item with index.

### `Entity_GetProductionQueueItemType`
```lua
Entity_GetProductionQueueItemType(EntityID entity, Integer index)
```
Returns the production type (PITEM_Upgrade, PITEM_Spawn, PITEM_SquadUpgrade, PITEM_SquadReinforce, PITEM_PlayerUpgrade) for a production queue item with index.

### `Entity_GetProductionQueueSize`
```lua
Entity_GetProductionQueueSize(EntityID entity)
```
Returns the number of items in the entities production queue.

### `Entity_GetProjectileBlocksPerAttacks`
```lua
Entity_GetProjectileBlocksPerAttacks(Entity entity)
```
Returns the number of blocks the entity will perform per number of attacks

### `Entity_GetRallyPointPositions`
```lua
Entity_GetRallyPointPositions(EntityID entity)
```
Returns a table of positions for each rally point set on the provided entity.  Entries in the table are named "position1", "position2", etc.

### `Entity_GetRangedBlocksPerAttacks`
```lua
Entity_GetRangedBlocksPerAttacks(Entity entity)
```
Returns the number of blocks the entity will perform per number of attacks

### `Entity_GetRemainingResourceDepositAmount`
```lua
Entity_GetRemainingResourceDepositAmount(EntityID entity)
```
Get remaining resource amount of the given entity.

### `Entity_GetResource`
```lua
Entity_GetResource(EntityID entity, Integer resourceType)
```
Returns the amount of a certain resource that an entity has.

### `Entity_GetSightInnerHeight`
```lua
Entity_GetSightInnerHeight(EntityID entity)
```
Returns the inner sight height for this entity

### `Entity_GetSightInnerRadius`
```lua
Entity_GetSightInnerRadius(EntityID entity)
```
Returns the inner sight radius for this entity

### `Entity_GetSightOuterHeight`
```lua
Entity_GetSightOuterHeight(EntityID entity)
```
Returns the outer sight height for this entity

### `Entity_GetSightOuterRadius`
```lua
Entity_GetSightOuterRadius(EntityID entity)
```
Returns the outer sight radius for this entity

### `Entity_GetSquad`
```lua
Entity_GetSquad(EntityID pEntity)
```
Returns the Squad for the passed Entity. (May be nullptr)

### `Entity_GetSquadsHeld`
```lua
Entity_GetSquadsHeld(EntityID pEntity, SGroupID sgroup)
```
Adds squads held by an entity to an SGroup

### `Entity_GetStateModelBool`
```lua
Entity_GetStateModelBool(EntityID entity, String key)
```
Returns a boolean value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelEntityTarget`
```lua
Entity_GetStateModelEntityTarget(EntityID entity, String key)
```
Returns an Entity value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelEnumTableBool`
```lua
Entity_GetStateModelEnumTableBool(EntityID entity, String key, Integer tableRowIndex)
```
Returns a boolean value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTableEntityTarget`
```lua
Entity_GetStateModelEnumTableEntityTarget(EntityID entity, String key, Integer tableRowIndex)
```
Returns an Entity value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTableFloat`
```lua
Entity_GetStateModelEnumTableFloat(EntityID entity, String key, Integer tableRowIndex)
```
Returns a float value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTableInt`
```lua
Entity_GetStateModelEnumTableInt(EntityID entity, String key, Integer tableRowIndex)
```
Returns an integer value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTablePlayerTarget`
```lua
Entity_GetStateModelEnumTablePlayerTarget(EntityID entity, String key, Integer tableRowIndex)
```
Returns a Player value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTableSquadTarget`
```lua
Entity_GetStateModelEnumTableSquadTarget(EntityID entity, String key, Integer tableRowIndex)
```
Returns a Squad value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelEnumTableVector3f`
```lua
Entity_GetStateModelEnumTableVector3f(EntityID entity, String key, Integer tableRowIndex)
```
Returns a Vector3f value from the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_GetStateModelFloat`
```lua
Entity_GetStateModelFloat(EntityID entity, String key)
```
Returns a float value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelInt`
```lua
Entity_GetStateModelInt(EntityID entity, String key)
```
Returns an integer value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelPlayerTarget`
```lua
Entity_GetStateModelPlayerTarget(EntityID entity, String key)
```
Returns a Player value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelSquadTarget`
```lua
Entity_GetStateModelSquadTarget(EntityID entity, String key)
```
Returns a Squad value from the entity's state model corresponding to the given key.

### `Entity_GetStateModelVector3f`
```lua
Entity_GetStateModelVector3f(EntityID entity, String key)
```
Returns a Vector3f value from the entity's state model corresponding to the given key.

### `Entity_GetStateTreeTargeting_EntityTarget`
```lua
Entity_GetStateTreeTargeting_EntityTarget(Entity& entity, String type, String key)
```
Returns an Entity value from the entity's StateTree EntityTargetingExt with the given type and key.

### `Entity_GetStateTreeTargeting_PlayerTarget`
```lua
Entity_GetStateTreeTargeting_PlayerTarget(Entity& entity, String type, String key)
```
Returns an Player value from the entity's StateTree EntityTargetingExt with the given type and key.

### `Entity_GetStateTreeTargeting_SquadTarget`
```lua
Entity_GetStateTreeTargeting_SquadTarget(Entity& entity, String type, String key)
```
Returns an Squad value from the entity's StateTree EntityTargetingExt with the given type and key.

### `Entity_GetStateTreeTargeting_Vector3f`
```lua
Entity_GetStateTreeTargeting_Vector3f(Entity& entity, String type, String key)
```
Returns an Vector3f value from the entity's StateTree EntityTargetingExt with the given type and key.

### `Entity_GetStrategicPointSecureCount`
```lua
Entity_GetStrategicPointSecureCount(EntityID entity)
```
Returns the number of entities or squads currently securing this strategic point

### `Entity_GetTargetingType`
```lua
Entity_GetTargetingType(Entity& entity)
```
Get the entity's targeting type - auto, manual, or none

### `Entity_GetWeaponBlueprint`
```lua
Entity_GetWeaponBlueprint(EntityID entity, Integer hardPointIndex)
```
Returns a weapon hardpoint  ( 0 indexed )

### `Entity_GetWeaponHardpointCount`
```lua
Entity_GetWeaponHardpointCount(EntityID entity)
```
Returns how many hardpoints an entity has

### `Entity_HandleAllAsserts`
```lua
Entity_HandleAllAsserts()
```
Call HandleAssert on an EntityAssertHandler for each entity

### `Entity_HasAbility`
```lua
Entity_HasAbility(EntityID entity, ScarAbilityPBG ability)
```
Tests to see if an entity has an ability

### `Entity_HasBlueprint`
```lua
Entity_HasBlueprint(EntityID entity, EBP/EntityType/Table blueprints)
```
Checks whether an entity is of any of the Blueprints or EntityTypes specified.

### `Entity_HasProductionQueue`
```lua
Entity_HasProductionQueue(EntityID entity)
```
Returns true if an entity has a production queue.

### `Entity_HasUpgrade`
```lua
Entity_HasUpgrade(EntityID pEntity, ScarUpgradePBG upgradePBG)
```
Return true if the entity has purchased the specified upgrade.

### `Entity_InstantCaptureStrategicPoint`
```lua
Entity_InstantCaptureStrategicPoint(EntityID entity, PlayerID player)
```
Strategic point will be captured instantly by the team of the supplied player

### `Entity_InstantConvertBuildingToFieldSupport`
```lua
Entity_InstantConvertBuildingToFieldSupport(EntityID building, PlayerID owner)
```
instantly converts a building into a fieldsupport

### `Entity_InstantRevertOccupiedBuilding`
```lua
Entity_InstantRevertOccupiedBuilding(EntityID entity)
```
Reverts an occupied building

### `Entity_IsAbilityActive`
```lua
Entity_IsAbilityActive(EntityID entity, ScarAbilityPBG pbg)
```
True if the ability is active

### `Entity_IsActive`
```lua
Entity_IsActive(EntityID pEntity)
```
Returns true if entity is alive and spawned

### `Entity_IsAlive`
```lua
Entity_IsAlive(EntityID pEntity)
```
Returns true if entity is still alive

### `Entity_IsAttacking`
```lua
Entity_IsAttacking(EntityID entity, Real time)
```
Returns true if the entity is attacking within the time

### `Entity_IsBuilding`
```lua
Entity_IsBuilding(EntityID e)
```
Returns true if the given entity is a building

### `Entity_IsBurnable`
```lua
Entity_IsBurnable(EntityID e)
```
Returns true if the entity can be set on fire

### `Entity_IsBurning`
```lua
Entity_IsBurning(EntityID e)
```
Returns true if the given entity is burning (buildings on fire or non-buildings with burn_exts)

### `Entity_IsCamouflaged`
```lua
Entity_IsCamouflaged(EntityID entity)
```
Returns whether the entity is camouflaged.

### `Entity_IsCapturableBuilding`
```lua
Entity_IsCapturableBuilding(EntityID entity)
```
Returns true if the entity is a capturable building

### `Entity_IsCasualty`
```lua
Entity_IsCasualty(EntityID entity)
```
Returns true if entity is a casualty else false

### `Entity_IsCuttable`
```lua
Entity_IsCuttable(EntityID entity)
```
Returns whether this entity is cuttable

### `Entity_IsDemolitionReady`
```lua
Entity_IsDemolitionReady(EntityID entity)
```
Returns whether this entity's demolition charges are ready to be detonated

### `Entity_IsDoingAbility`
```lua
Entity_IsDoingAbility(EntityID entity, ScarAbilityPBG pbg)
```
True if entity is currently performing the given ability

### `Entity_IsEBPBuilding`
```lua
Entity_IsEBPBuilding(ScarEntityPBG ebp)
```
Returns true if the given blueprint is a building

### `Entity_IsEBPObjCover`
```lua
Entity_IsEBPObjCover(ScarEntityPBG ebp)
```
Returns true if the given blueprint is objcover

### `Entity_IsEBPOfType`
```lua
Entity_IsEBPOfType(ScarEntityPBG ebp, String type)
```
Returns true if the given blueprint is of the given type. Types are defined in type_ext/unit_type_list

### `Entity_IsHardpointActive`
```lua
Entity_IsHardpointActive(EntityID entity, Integer hardPointIndex)
```
Returns whether a hardpoint is active ( 0 indexed )

### `Entity_IsHoldingAny`
```lua
Entity_IsHoldingAny(EntityID entity)
```
Check if the entity has a hold on anything

### `Entity_IsInBackground`
```lua
Entity_IsInBackground(EntityID pEntity)
```
Returns whether or not the entity is in the background.

### `Entity_IsInfantry`
```lua
Entity_IsInfantry(EntityID pEntity)
```
Returns whether an entity is an infantry unit

### `Entity_IsInHold`
```lua
Entity_IsInHold(EntityID entity)
```
Checks if an entity is in a hold

### `Entity_IsInvincible`
```lua
Entity_IsInvincible(EntityID entity)
```
Returns whether this entity is invincible.  An invincible entity can never take damage and can never die.

### `Entity_IsInvulnerable`
```lua
Entity_IsInvulnerable(EntityID entity)
```
get if an entity is invulnerable

### `Entity_IsMoving`
```lua
Entity_IsMoving(EntityID pEntity)
```
Returns whether an entity is moving.

### `Entity_IsOfType`
```lua
Entity_IsOfType(EntityID entity, String type)
```
Determines if this entity is of the given type. Types are defined in type_ext/unit_type_list

### `Entity_IsOnWalkableWall`
```lua
Entity_IsOnWalkableWall(EntityID entity)
```
Returns if an Entity is currently on walkable wall.

### `Entity_IsPartOfSquad`
```lua
Entity_IsPartOfSquad(EntityID pEntity)
```
Returns true if the entity is part of a squad

### `Entity_IsPlane`
```lua
Entity_IsPlane(EntityID pEntity)
```
Returns whether an entity is a plane (has a flight extension)

### `Entity_IsPlannedStructure`
```lua
Entity_IsPlannedStructure(EntityID entity)
```
Returns whether an entity is a planned structure.

### `Entity_IsProducingSquad`
```lua
Entity_IsProducingSquad(EntityID entity, ScarSquadPBG pbg)
```
Returns whether a particular squad blueprint is being produced by a given entity

### `Entity_IsProductionQueueAvailable`
```lua
Entity_IsProductionQueueAvailable(EntityID entity)
```
Returns true if an entity has a production queue and if the queue is available

### `Entity_IsResourceGenerator`
```lua
Entity_IsResourceGenerator(EntityID entity)
```
Returns true if the entity is a resource generator and has resources remaining

### `Entity_IsSlotItem`
```lua
Entity_IsSlotItem(EntityID entity)
```
Return true if the entity is a slot item

### `Entity_IsSpawned`
```lua
Entity_IsSpawned(EntityID entity)
```
if entity is spawned return true

### `Entity_IsStartingPosition`
```lua
Entity_IsStartingPosition(EntityID entity)
```
Returns true if the entity is a starting position

### `Entity_IsStrategicPoint`
```lua
Entity_IsStrategicPoint(EntityID pEntity)
```
Returns true if the entity is a strategic point.

### `Entity_IsStrategicPointCapturedBy`
```lua
Entity_IsStrategicPointCapturedBy(EntityID entity, PlayerID player)
```
Returns true if strategic point is captured by the team of the player provided.

### `Entity_IsSyncWeapon`
```lua
Entity_IsSyncWeapon(EntityID entity)
```
Return true if the entity is a team weapon

### `Entity_IsUnderAttack`
```lua
Entity_IsUnderAttack(EntityID entity, Real time)
```
Returns true if the entity is under attack.

### `Entity_IsUnderAttackByPlayer`
```lua
Entity_IsUnderAttackByPlayer(EntityID entity, PlayerID pAttackerOwner, Real time)
```
Returns true if the entity is under attack by a certain player

### `Entity_IsUnderAttackFromDirection`
```lua
Entity_IsUnderAttackFromDirection(EntityID entity, Integer offset, Real timeSeconds)
```
Returns true if the entity was under attack from a certain direction (8 offset types, see ScarUtil.scar)

### `Entity_IsUnderConstruction`
```lua
Entity_IsUnderConstruction(EntityID entity)
```
Returns true if the entity is under construction.

### `Entity_IsUnderRepair`
```lua
Entity_IsUnderRepair(EntityID entity)
```
Returns true if the entity is being repaired.

### `Entity_IsValid`
```lua
Entity_IsValid(Integer id)
```
Check if an entity with the given ID can be found in the world

### `Entity_IsVaultable`
```lua
Entity_IsVaultable(EntityID pEntity)
```
Returns whether an entity can be vaulted

### `Entity_IsVehicle`
```lua
Entity_IsVehicle(EntityID pEntity)
```
Returns whether an entity is a vehicle

### `Entity_IsVictoryPoint`
```lua
Entity_IsVictoryPoint(EntityID pEntity)
```
Returns true if entityID is a victory point

### `Entity_Kill`
```lua
Entity_Kill(EntityID entity)
```
Kill the entity.  Sets health to 0, and triggers death effects.

### `Entity_OverrideScreenName`
```lua
Entity_OverrideScreenName(EntityID entity, String overrideName)
```
Overrides the entity blueprint's ui screen name for the entity instance provided as the first parameter. Loc_GetString can be used to get the localized string to pass in as the second parameter.

### `Entity_Population`
```lua
Entity_Population(EntityID entity, CapType type)
```
get entity pop cost, use CT_Personnel, CT_Vehicle, CT_Medic for captype

### `Entity_Precache`
```lua
Entity_Precache(ScarEntityPBG ebp, Integer skinItemDefinitionID, PlayerID player, String resourceContainerCacheName, String source, String id)
```
Precache entity resources and listen for event GE_EntityPrecached that it is done

### `Entity_QueueProductionItemByPBG`
```lua
Entity_QueueProductionItemByPBG(EntityID entity, ProductionItemType itemType, PropertyBagGroup pbg)
```
Pushes the provided pbg onto the entity's production queue and returns if it was successfully added. Also need to specify a itemType for the pbg (PITEM_Upgrade, PITEM_Spawn, PITEM_SquadUpgrade, PITEM_SquadReinforce,  PITEM_PlayerUpgrade)

### `Entity_RagDoll`
```lua
Entity_RagDoll(EntityID entity)
```
trigger the RagDoll skeleton driving.

### `Entity_RemoveAbility`
```lua
Entity_RemoveAbility(EntityID entity, ScarAbilityPBG ability)
```
Removes an ability that was previously added by Entity_AddAbility. You cannot remove static abilities (from AE: ability_ext)

### `Entity_RemoveBoobyTraps`
```lua
Entity_RemoveBoobyTraps(EntityID pEntityTarget)
```
Removes all booby-traps on this entity

### `Entity_RemoveDemolitions`
```lua
Entity_RemoveDemolitions(EntityID entity)
```
Removes all demolition charges on an entity

### `Entity_RemoveUpgrade`
```lua
Entity_RemoveUpgrade(EntityID entity, ScarUpgradePBG upgrade)
```
Removes an upgrade from an entity

### `Entity_RequiresSlottedSplineUpdateAfterBlueprintConversion`
```lua
Entity_RequiresSlottedSplineUpdateAfterBlueprintConversion(EntityID entity)
```
Returns true if you should call Misc_UpdateSlottedSplinesContainingEGroupAfterBlueprintConversion with an egroup containing this entity after blueprint converting it. Make sure to batch together all your entities when using that function to reduce duplicated work.

### `Entity_ResetMeleeBlocksPerAttacks`
```lua
Entity_ResetMeleeBlocksPerAttacks(Entity& entity)
```
Reset melee block rate to AE tuned values

### `Entity_ResetProjectileBlocksPerAttacks`
```lua
Entity_ResetProjectileBlocksPerAttacks(Entity& entity)
```
Reset Projectile block rate to AE tuned values

### `Entity_ResetRangedBlocksPerAttacks`
```lua
Entity_ResetRangedBlocksPerAttacks(Entity& entity)
```
Reset ranged block rate to AE tuned values

### `Entity_RestoreTargetingType`
```lua
Entity_RestoreTargetingType(Entity& entity)
```
Restore the targeting type to the default found in the ebp

### `Entity_SetAnimatorAction`
```lua
Entity_SetAnimatorAction(EntityID pEntity, String actionName)
```
Trigger animation action for an entity. Please only use this for simple animations

### `Entity_SetAnimatorActionParameter`
```lua
Entity_SetAnimatorActionParameter(EntityID pEntity, String actionParameterName, String actionParameterValue)
```
Set animation action parameter for an entity. Please only use this for simple animations

### `Entity_SetAnimatorEvent`
```lua
Entity_SetAnimatorEvent(EntityID pEntity, String eventName)
```
Set animation event for an entity. Please only use this for simple animations

### `Entity_SetAnimatorState`
```lua
Entity_SetAnimatorState(EntityID pEntity, String stateMachineName, String stateName)
```
Set animation state of a state machine for an entity. Please only use this for simple animations

### `Entity_SetAnimatorVariable`
```lua
Entity_SetAnimatorVariable(EntityID pEntity, String variableName, Real value)
```
Set animation variable value for an entity. Please only use this for simple animations

### `Entity_SetBackground`
```lua
Entity_SetBackground(EntityID pEntity, Boolean isInBackground)
```
Sets the entity to be in the background or foreground. By default, all entities are in the foreground

### `Entity_SetCrushable`
```lua
Entity_SetCrushable(EntityID entity, Boolean crushable)
```
Overrides crushable behavior for an entity

### `Entity_SetCrushMode`
```lua
Entity_SetCrushMode(EntityID entity, CrushMode mode)
```
Changes the crush mode of a given entity.  Entity must have a crush extension.

### `Entity_SetDemolitions`
```lua
Entity_SetDemolitions(PlayerID player, EntityID entity, Integer numcharges)
```
Fully wires this entity for demolitions, if it's set up to be demolishable. 'player' is the one that owns the demolitions and can detonate them.

### `Entity_SetEnableCasualty`
```lua
Entity_SetEnableCasualty(Boolean enable, EntityID entity)
```
enable or disable the casualtext

### `Entity_SetExtEnabled`
```lua
Entity_SetExtEnabled(EntityID entity, String extID, Boolean enabled)
```
Enables/disables an extension on the entity.

### `Entity_SetHeading`
```lua
Entity_SetHeading(EntityID entity, Position pos, Boolean bInterpolate)
```
Sets the heading of the entity.  The position is currently a lua table with three entries (x, y, z)

### `Entity_SetHeadingGroundSnapOptional`
```lua
Entity_SetHeadingGroundSnapOptional(EntityID entity, Position pos, Boolean bSnapToGround, Boolean bInterpolate)
```
Sets the heading of the entity.  The position is currently a lua table with three entries (x, y, z)

### `Entity_SetHealth`
```lua
Entity_SetHealth(EntityID entity, Real healthPercent)
```
Set the health of an entity.  healthPercent must be in the range [0.0, 1.0].

### `Entity_SetInvulnerableMinCap`
```lua
Entity_SetInvulnerableMinCap(EntityID entity, Real minHealthPercentage, Real resetTime)
```
Make an entity invulnerable to physical damage when health is below the minimum health percentage

### `Entity_SetLockCurrentTierVisuals`
```lua
Entity_SetLockCurrentTierVisuals(EntityID entity, Boolean lockVisuals)
```
Sets the lockCurrentTierVisuals flag in the TierExt so when an entity gets BP converted it doesn't update the visual assets. Must be called before BP conversion

### `Entity_SetMeleeBlocksPerAttacks`
```lua
Entity_SetMeleeBlocksPerAttacks(Entity entity, Integer blocks, Integer attacks)
```
Set the number of blocks the entity will perform per number of attacks

### `Entity_SetOnFire`
```lua
Entity_SetOnFire(EntityID entity)
```
Sets an object on fire (also works on buildings)

### `Entity_SetPlayerOwner`
```lua
Entity_SetPlayerOwner(EntityID entity, PlayerID owner)
```
Changes the owner of the given squad.

### `Entity_SetPosition`
```lua
Entity_SetPosition(EntityID entity, Position pos)
```
Sets the position of the entity.  The position is currently a lua table with three entries (x, y, z)

### `Entity_SetPositionWithinCell`
```lua
Entity_SetPositionWithinCell(EntityID entity, Position desiredPosition)
```
If the entity is at the same cell as desiredPosition, try to set the entity position to it. If the cell is next to impass, set it to the center of the cell.

### `Entity_SetProjectileBlocksPerAttacks`
```lua
Entity_SetProjectileBlocksPerAttacks(Entity entity, Integer blocks, Integer attacks)
```
Set the number of blocks the entity will perform per number of attacks

### `Entity_SetProjectileCanExplode`
```lua
Entity_SetProjectileCanExplode(EntityID projectile, Boolean canExplode)
```
Sets whether or not a projectile can explode.

### `Entity_SetRangedBlocksPerAttacks`
```lua
Entity_SetRangedBlocksPerAttacks(Entity entity, Integer blocks, Integer attacks)
```
Set the number of blocks the entity will perform per number of attacks

### `Entity_SetRecrewable`
```lua
Entity_SetRecrewable(EntityID entity, Boolean capturable)
```
Sets an entity to be recrewable or not when it becomes abandoned

### `Entity_SetRemainingResourceDepositAmount`
```lua
Entity_SetRemainingResourceDepositAmount(EntityID entity, Real amount)
```
Set remaining resource amount of the given entity.

### `Entity_SetResource`
```lua
Entity_SetResource(EntityID entity, Integer type, Real amount)
```
Sets a specific amount of a certain resource type for an entity.

### `Entity_SetSharedProductionQueue`
```lua
Entity_SetSharedProductionQueue(EntityID entity, Boolean shared)
```
Enables shared team production on a building (teammates can build using THEIR resources)

### `Entity_SetShowSilhouette`
```lua
Entity_SetShowSilhouette(EntityID entity, Boolean show)
```
Show or hide the entity's silhouette when behind other objects

### `Entity_SetStateModelBool`
```lua
Entity_SetStateModelBool(EntityID entity, String key, Boolean value)
```
Sets a boolean value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelEntityTarget`
```lua
Entity_SetStateModelEntityTarget(EntityID entity, String key, EntityID value)
```
Sets an Entity TargetHandle value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelEnumTableBool`
```lua
Entity_SetStateModelEnumTableBool(EntityID entity, String key, Integer tableRowIndex, Boolean value)
```
Sets a boolean value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTableEntityTarget`
```lua
Entity_SetStateModelEnumTableEntityTarget(EntityID entity, String key, Integer tableRowIndex, EntityID value)
```
Sets an Entity TargetHandle value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTableFloat`
```lua
Entity_SetStateModelEnumTableFloat(EntityID entity, String key, Integer tableRowIndex, Real value)
```
Sets a float value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTableInt`
```lua
Entity_SetStateModelEnumTableInt(EntityID entity, String key, Integer tableRowIndex, Integer value)
```
Sets an integer value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTablePlayerTarget`
```lua
Entity_SetStateModelEnumTablePlayerTarget(EntityID entity, String key, Integer tableRowIndex, PlayerID value)
```
Sets a Player TargetHandle value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTableSquadTarget`
```lua
Entity_SetStateModelEnumTableSquadTarget(EntityID entity, String key, Integer tableRowIndex, SquadID value)
```
Sets a Squad TargetHandle value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelEnumTableVector3f`
```lua
Entity_SetStateModelEnumTableVector3f(EntityID entity, String key, Integer tableRowIndex, Position value)
```
Sets a Vector3f value in the entity's state model corresponding to the given key and table row index (0 based).

### `Entity_SetStateModelFloat`
```lua
Entity_SetStateModelFloat(EntityID entity, String key, Real value)
```
Sets a float value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelInt`
```lua
Entity_SetStateModelInt(EntityID entity, String key, Integer value)
```
Sets an integer value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelPlayerTarget`
```lua
Entity_SetStateModelPlayerTarget(EntityID entity, String key, PlayerID value)
```
Sets a Player TargetHandle value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelSquadTarget`
```lua
Entity_SetStateModelSquadTarget(EntityID entity, String key, SquadID value)
```
Sets a Squad TargetHandle value in the entity's state model corresponding to the given key.

### `Entity_SetStateModelVector3f`
```lua
Entity_SetStateModelVector3f(EntityID entity, String key, Position value)
```
Sets a Vector3f value in the entity's state model corresponding to the given key.

### `Entity_SetStayBurningWhileInvulnerable`
```lua
Entity_SetStayBurningWhileInvulnerable(EntityID entity, Boolean shouldStayBurning)
```
Sets a flag that tells a building to keep burning while invulnerable (for atmosphere).

### `Entity_SetStrategicPointNeutral`
```lua
Entity_SetStrategicPointNeutral(EntityID entity)
```
Sets a strategic point to neutral (not owned by any team)

### `Entity_SetStrategicPointReticuleVisible`
```lua
Entity_SetStrategicPointReticuleVisible(EntityID entity, Boolean visible)
```
Sets whether a strategic point's reticule is visible

### `Entity_SetTargetingType`
```lua
Entity_SetTargetingType(Entity& entity, TargetingType type)
```
Set the allowable methods of targeting this entity

### `Entity_SetWorldOwned`
```lua
Entity_SetWorldOwned(EntityID entity)
```
Makes an entity neutral

### `Entity_SimHide`
```lua
Entity_SimHide(EntityID entity, Boolean hide)
```
Shows/hides the entity in the simulation

### `Entity_SnapToGridAndGround`
```lua
Entity_SnapToGridAndGround(EntityID entity, Boolean interpolate)
```
Snaps the entity to the grid and ground.

### `Entity_Spawn`
```lua
Entity_Spawn(EntityID entity)
```
Spawn the entity at its current position

### `Entity_SpawnDoNotAddPathfindingAndCollision`
```lua
Entity_SpawnDoNotAddPathfindingAndCollision(EntityID entity)
```
Spawn the entity at its current position without pathfinding and collision

### `Entity_SpawnToward`
```lua
Entity_SpawnToward(EntityID entity, Position pos, Position toward, String spawnType)
```
Spawn the entity at a given position

### `Entity_StopAbility`
```lua
Entity_StopAbility(EntityID entity, ScarAbilityPBG ability, Boolean bIsEarlyExit)
```
Abruptly stops an active ability

### `Entity_StopFire`
```lua
Entity_StopFire(EntityID entity)
```
Puts out the fire on an object (also works on buildings)

### `Entity_SuggestPosture`
```lua
Entity_SuggestPosture(EntityID entity, Integer posture, Real duration)
```
Suggests a posture to an entity, lasting the passed duration

### `Entity_SupportsDemolition`
```lua
Entity_SupportsDemolition(EntityID entity)
```
Returns whether this entity is set up to have demolitions placed on it

### `Entity_TagDebug`
```lua
Entity_TagDebug(EntityID entity)
```
Tags the entity to be used for debugging

### `Entity_UnloadAllFromHold`
```lua
Entity_UnloadAllFromHold(EntityID entity)
```
Unloads everything in this entity's hold.

### `Entity_VisHide`
```lua
Entity_VisHide(EntityID pEntity, Boolean bHide)
```
Hides or shows an entity visually.

## Enum (2 functions)

### `Enum_ToNumber`
```lua
Enum_ToNumber(StackVar var)
```
Converts any enum value to a number

### `Enum_ToString`
```lua
Enum_ToString(StackVar var)
```
Converts any enum value to a string

## Event (23 functions)

### `Event_CreateAND`
```lua
Event_CreateAND(Function callback, Table data, Table events, Real delay)
```
Creates a Callback Event that triggers when ALL of the specified events are triggered.

### `Event_Death`
```lua
Event_Death(Function callback, EGroupID group, ALL_UNITS/ANY_MEMBER/ANY_SQUAD selection, Boolean repeat, Boolean requireAllEntitiesDead, Table data)
```
Callback given callback function with data, when the certain objects die.

### `Event_Delay`
```lua
Event_Delay(Real seconds)
```
Pauses for a given amount of time. This function MUST be called from a CTRL object in NISlet events only!

### `Event_EncounterCanSeePlayerSquads`
```lua
Event_EncounterCanSeePlayerSquads(Function callback, Table data, SGroupID encounter, PlayerID player, Real delay)
```
Callback given callback function with data, when any squad in the encounter can see any squad owned by the player

### `Event_EnterProximity`
```lua
Event_EnterProximity(Function callback, Table data, ConstTargetHandle target, Boolean arequireAll, Marker location, REAL range, Boolean repeat, Boolean triggerOnEnter)
```
Callback given callback function with data when target enters range

### `Event_ExitProximity`
```lua
Event_ExitProximity(Function callback, Table data, ConstTargetHandle target, Boolean arequireAll, Marker location, REAL range, Boolean repeat, Boolean triggerOnEnter)
```
Callback given callback function with data when target exits range

### `Event_GroupCount`
```lua
Event_GroupCount(Function callback, Table data, EGroupID / SGroup group, Integer amount (value to be compared against), Boolean repeat)
```
Callback given callback function with data, when the amount of objects matches the requested conditions - Note: Does not count team weapons

### `Event_GroupIsDeadOrRetreating`
```lua
Event_GroupIsDeadOrRetreating(Function callback, Table data, EGroupID / SGroup group, Real delay)
```
Callback given callback function with data, when group is dead(empty).

### `Event_GroupLeftAlive`
```lua
Event_GroupLeftAlive(Function callback, Table data, EGroupID / SGroup group, Integer amount, Real delay)
```
Callback given callback function with data, when the amount of entities left in a group drops below amount.

### `Event_IsBeingSkipped`
```lua
Event_IsBeingSkipped()
```
Returns true if the event is being skipped.

### `Event_IsEngaged`
```lua
Event_IsEngaged(Function callback, Table data, Real attackTime, Real delay)
```
Callback given callback function with data, when group is doing an attack or is under attack in the last attackTime seconds.

### `Event_IsOutOfCombat`
```lua
Event_IsOutOfCombat(Function callback, Table data, EGroupID / SGroup group, Real attackTime, Real delay)
```
Callback given callback function with data, when group is out of combat  in the last attackTime seconds.

### `Event_IsSelected`
```lua
Event_IsSelected(Function callback, Table data)
```
Callback when a target element is selected.

### `Event_IsUnderAttack`
```lua
Event_IsUnderAttack(Function callback, Table data, SGroupID = SGroup, EGroupID = EGroup, Real attackTime, PlayerID player, Real delay)
```
Callback given callback function with data, when sgroup or egroup are under attack in the last attackTime seconds.

### `Event_PlayerCanSeeElement`
```lua
Event_PlayerCanSeeElement(Function callback, Table data, PlayerID team, SGroupID element)
```
Callback given callback function with data, when the given player can see the element.

### `Event_Proximity`
```lua
Event_Proximity(Function callback, Table data, ConstTargetHandle target, Marker location, REAL range, Real delay)
```
Callback given callback function with data when target enters location.

### `Event_Save`
```lua
Event_Save(SaveTriggerType type)
```
Starts a save event the same way as Event_Start, but automatically sets highest priority and promotes the request

### `Event_SaveWithName`
```lua
Event_SaveWithName(SaveTriggerType type, String fileName)
```
Starts a save event the same way as Event_Save, but with a filename specified.

### `Event_SGroupCountMember`
```lua
Event_SGroupCountMember(Function callback, Table data, SGroupID group, Integer amount (value to be compared against), Boolean repeat)
```
Callback given callback function with data, when the amount of members left in a squad matches the requested conditions

### `Event_Skip`
```lua
Event_Skip()
```
Completes execution of the event immediately (all calls to Wait() are ignored)

### `Event_Start`
```lua
Event_Start(LuaFunction eventFunction, Integer int)
```
Starts event.  Event will not start until all rules are evaluated for this frame!

### `Event_StartEx`
```lua
Event_StartEx(LuaFunction eventFunction, Integer int, LuaFunction onComplete)
```
Starts an event the same way as Event_Start, but calls a user defined function when the event is over

### `Event_WhileInProximity`
```lua
Event_WhileInProximity(Function callback, Table data, ConstTargetHandle target, Boolean arequireAll, Marker location, REAL range, Boolean repeat, Boolean triggerOnEnter)
```
Callback given callback function with data when target remains in range (called every interval seconds)

## Formation (4 functions)

### `Formation_GetDimensionsAndOffset`
```lua
Formation_GetDimensionsAndOffset(SGroupID sgroup)
```
Calculate the dimensions and centre offset of a formation for given squads.  Returns as a ScarPosition {x = Width, y = Height, z = centre offset along forward (Height) direction}.  Returns a zero vector if error.

### `Formation_OverrideDefaultFormationSpotGenerator`
```lua
Formation_OverrideDefaultFormationSpotGenerator(SGroupID sgroup, String formationPBGNameShort)
```
Override the default spot generator of the squads in 'sgroup' with the spot generator specified in 'formationPBGNameShort'. To set it back to the original default formation spot generator, pass in nil or an empty string for 'formationPBGNameShort'

### `Formation_PlaceSquadsInFormation`
```lua
Formation_PlaceSquadsInFormation(SGroupID sgroup, Position position, Position direction)
```
Calculate formation positions and set the squads' positions to the formation positions

### `Formation_PlaceSquadsInFormationByFormationName`
```lua
Formation_PlaceSquadsInFormationByFormationName(SGroupID sgroup, Position position, Position direction, String formationPBGNameShort)
```
Calculate formation positions and set the squads' positions to the formation positions, using the formation spot generator provided

## FOW (26 functions)

### `FOW_Blockers`
```lua
FOW_Blockers()
```
Toggle blockers info

### `FOW_ForceRevealAllUnblockedAreas`
```lua
FOW_ForceRevealAllUnblockedAreas()
```
Reveal FOW except blockers for all players. Does not create ghosts and ghosts will not be present if undone.

### `FOW_PlayerExploreAll`
```lua
FOW_PlayerExploreAll(PlayerID player)
```
Explores entire map for one player. (Careful where this is used. For example, if used before the first tick, a statetree may change an entity's visual on the first tick, so the ghost's visual will not reflect the entity's.)

### `FOW_PlayerRevealAll`
```lua
FOW_PlayerRevealAll(PlayerID player)
```
Reveal FOW for specified player

### `FOW_PlayerRevealArea`
```lua
FOW_PlayerRevealArea(PlayerID player, Position pos, Real radius, Real durationSecs)
```
Reveals a circular area for the given player over a given duration.

### `FOW_PlayerRevealSGroup`
```lua
FOW_PlayerRevealSGroup(PlayerID player, SGroupID group, Real radius, Real durationSecs)
```
Reveals a SGroup in the Fog of War for a player over a given duration.

### `FOW_PlayerUnExploreAll`
```lua
FOW_PlayerUnExploreAll(PlayerID player)
```
Unexplores entire map for one player.

### `FOW_PlayerUnRevealAll`
```lua
FOW_PlayerUnRevealAll(PlayerID player)
```
Use to undo a FOW_RevealAll for specified player

### `FOW_PlayerUnRevealArea`
```lua
FOW_PlayerUnRevealArea(PlayerID player, Position pos)
```
UnReveals a circular area that was previously revealed for a given player.

### `FOW_PlayerUnRevealSGroup`
```lua
FOW_PlayerUnRevealSGroup(PlayerID player, SGroupID group)
```
UnReveal a SGroup previously revealed to a Player

### `FOW_RevealAll`
```lua
FOW_RevealAll()
```
Reveal FOW for all players

### `FOW_RevealArea`
```lua
FOW_RevealArea(Position pos, Real radius, Real durationSecs)
```
Reveals a circular area for all alive players over a given duration.

### `FOW_RevealEGroup`
```lua
FOW_RevealEGroup(EGroupID group, Real radius, Real durationSecs)
```
Reveals an EGroup in the Fog of War for all alive players over a given duration.

### `FOW_RevealEntity`
```lua
FOW_RevealEntity(EntityID entity, Real radius, Real durationSecs)
```
Reveals an entity in the Fog of War for all alive players over a given duration.

### `FOW_RevealSGroup`
```lua
FOW_RevealSGroup(SGroupID group, Real radius, Real durationSecs)
```
Reveals a SGroup in the Fog of War for all alive players over a given duration.

### `FOW_RevealSquad`
```lua
FOW_RevealSquad(SquadID squad, Real radius, Real durationSecs)
```
Reveals a squad in the Fog of War for all alive players over a given duration.

### `FOW_RevealTerritory`
```lua
FOW_RevealTerritory(PlayerID player, Integer sectorID, Real durationSecs, Boolean mustOwn)
```
Reveals a territory to a player

### `FOW_UIRevealAll`
```lua
FOW_UIRevealAll()
```
Reveal FOW for all players by disabling rendering of FOW without triggering a FOW in the game simulation

### `FOW_UIUnRevealAll`
```lua
FOW_UIUnRevealAll()
```
Use to undo a FOW_UIRevealAll

### `FOW_UIUnRevealAll_Transition`
```lua
FOW_UIUnRevealAll_Transition(Real duration)
```
Use to transition into game

### `FOW_UIUnRevealAllEntities`
```lua
FOW_UIUnRevealAllEntities()
```
Use to unreveal all Entities in FoW

### `FOW_UndoForceRevealAllUnblockedAreas`
```lua
FOW_UndoForceRevealAllUnblockedAreas()
```
Use to undo a FOW_ForceRevealAllUnblockedAreas.

### `FOW_UnExploreAll`
```lua
FOW_UnExploreAll()
```
Unexplores entire map for all players

### `FOW_UnRevealAll`
```lua
FOW_UnRevealAll()
```
Use to undo a FOW_RevealAll

### `FOW_UnRevealArea`
```lua
FOW_UnRevealArea(Position pos)
```
UnReveals a circular area that was previously revealed for all alive players.

### `FOW_UnRevealTerritory`
```lua
FOW_UnRevealTerritory(PlayerID player, Integer sectorID)
```
Unreveals a territory sector

## fx (7 functions)

### `fx_dump`
```lua
fx_dump()
```
force the gamma

### `fx_forcelod`
```lua
fx_forcelod(Integer lod)
```
force the LOD of the FX system (use 0 to enable dynamic LOD)

### `fx_logenable`
```lua
fx_logenable(Boolean enable)
```
enable logging of fx, it it wasn't already

### `fx_refresh`
```lua
fx_refresh()
```
Force effects to be recreated.

### `fx_toggle`
```lua
fx_toggle()
```
toggle effects on or off

### `fx_toggleRendering`
```lua
fx_toggleRendering()
```
toggle effects rendering on or off

### `fx_usedebugshader`
```lua
fx_usedebugshader(Boolean enable)
```
use the debugshader, which will render all fx green

## Game (62 functions)

### `Game_ConvertInputEnabledFlagEnumToInt`
```lua
Game_ConvertInputEnabledFlagEnumToInt(InputEnabledFlag flag)
```
Returns the input enabled flag as an integer.

### `Game_ConvertVisibilityFlagEnumToInt`
```lua
Game_ConvertVisibilityFlagEnumToInt(VisibilityFlag flag)
```
Returns the visibility flag as an integer.

### `Game_DeleteSaveGameDev`
```lua
Game_DeleteSaveGameDev(String filename)
```
deletes save game(s), even if it is not loadable with the current version of the game

### `Game_EnableInput`
```lua
Game_EnableInput(Boolean enable)
```
Enables/Disables all input EXCEPT for ESC and F10.

### `Game_EndSubTextFade`
```lua
Game_EndSubTextFade()
```
Removes title text displayed with Game_SubTextFade(...) immediately

### `Game_EndTextTitleFade`
```lua
Game_EndTextTitleFade()
```
Removes title text displayed with Game_TextTitleFade(...) immediately

### `Game_FastForwardProduction`
```lua
Game_FastForwardProduction(Real secondsForward)
```
Fast forward all production queues as if x seconds passed, returns info about what has been produced Returns a lua table of the format { (string)PlayerID : { (string)EntityProducerName : { "research" : { (string)researchedItemName : (int)number of times researched }, "production" : { (string)producedItemName : (int)number of items produced }, }, }, } for each player present, for each entity that produced after fast forwarding, for each item researched and produced

### `Game_FastForwardResourceIncome`
```lua
Game_FastForwardResourceIncome(Real secondsForward)
```
For all players fast forwards their resource income as if x seconds passed

### `Game_GetAutoSaveCooldownSeconds`
```lua
Game_GetAutoSaveCooldownSeconds()
```
gets the number of seconds before an auto-save can be performed again

### `Game_GetInputEnabledFlag`
```lua
Game_GetInputEnabledFlag()
```
Returns the input enabled flag.

### `Game_GetLocalPlayer`
```lua
Game_GetLocalPlayer()
```
Get the local player. (should only be used for UI purpose) (not deterministic)

### `Game_GetLocalPlayerID`
```lua
Game_GetLocalPlayerID()
```
Get the local player id. (should only be used for UI purpose) (not deterministic)

### `Game_GetSimRate`
```lua
Game_GetSimRate()
```
get the simulation update rate

### `Game_GetSPDifficulty`
```lua
Game_GetSPDifficulty()
```
Returns current single player difficulty. It returns the current difficulty setting value based on the match type. (defined in root\sysconfig.lua) For campaign, it returns the current value of "CampaignDifficulty" setting. For rogue mode, it returns the current value of ""RogueModeDifficulty"" setting.

### `Game_GetTerrainTypeVariables`
```lua
Game_GetTerrainTypeVariables(StackVarTable terrainVars)
```
injects terrain type values into passed table to use for terrain creation

### `Game_GetVisibilityFlag`
```lua
Game_GetVisibilityFlag()
```
Returns the game's visibility flag.

### `Game_HasLocalPlayer`
```lua
Game_HasLocalPlayer()
```
Determine if there is a valid local player. (UI only -- nondeterminstic) (not deterministic)

### `Game_HasMatchTypeFlag`
```lua
Game_HasMatchTypeFlag(Integer matchTypeFlag)
```
check if scenario has the given match type flag

### `Game_IsDataLocked`
```lua
Game_IsDataLocked(String dataID)
```
Returns lock state of stored data at location named by dataID.

### `Game_IsFtue`
```lua
Game_IsFtue()
```
check if scenario has FTUE boolean set in match setup

### `Game_IsPaused`
```lua
Game_IsPaused()
```
Returns whether the game is paused.

### `Game_IsPerformanceTest`
```lua
Game_IsPerformanceTest()
```
Returns true if the we're running the performance test.

### `Game_IsRTM`
```lua
Game_IsRTM()
```
Use to test whether the game is running in RTM mode or not. Using -rtm from the command line will cause this function to also return true in non-RTM builds.

### `Game_IsSaving`
```lua
Game_IsSaving()
```
Checks that the save system has a save queued or is actively saving.

### `Game_LaunchSPGeneratedMap`
```lua
Game_LaunchSPGeneratedMap(String biomePbgName, String layoutPbgName, String sizePbgName, Integer difficulty, StackVarTable terrainResult)
```
load this scenario as an single player match

### `Game_LoadAtmosphereSettings`
```lua
Game_LoadAtmosphereSettings(String fileName, String settingsName)
```
Loads atmosphere settings into the catalogue. This enables Game_TransitionToState to be usable from scar files for skirmish maps.

### `Game_LoadBinaryDataStore`
```lua
Game_LoadBinaryDataStore(String id, String path, Integer expectedVersion)
```
Load binary data store to disk

### `Game_LoadFromFileDev`
```lua
Game_LoadFromFileDev(String filename)
```
load this game as a single player match, full path is expected excluding extension

### `Game_LoadGame`
```lua
Game_LoadGame(String name)
```
load the savegame with the given internal name from Campaign or Skirmish folder depending on currently running scenario

### `Game_LoadSP`
```lua
Game_LoadSP(String scenarioName, Integer difficulty)
```
load this scenario as an single player match

### `Game_LoadTextDataStore`
```lua
Game_LoadTextDataStore(String id, String path)
```
Load text data store to disk

### `Game_LockRandom`
```lua
Game_LockRandom()
```
If you are running something that is non-deterministic like a getlocalplayer conditional, you can lock the random to make sure no one down the callstack will throw the game random index out of sync and cause a sync error. REMEMBER TO UNLOCK WHEN YOU ARE DONE

### `Game_PauseChallengeTracking`
```lua
Game_PauseChallengeTracking()
```
Pauses tracking of challenges.

### `Game_QuitApp`
```lua
Game_QuitApp()
```
Quits the app immediately

### `Game_QuitAppWithCode`
```lua
Game_QuitAppWithCode(Integer exitCode)
```
Quits the app immediately with the given exitCode

### `Game_RemoveTableData`
```lua
Game_RemoveTableData(String path)
```
Removes the data store at the given path.

### `Game_RequestSetLocalPlayer`
```lua
Game_RequestSetLocalPlayer(PlayerID player)
```
Requests the local player to be set on the next update. (not deterministic)

### `Game_ResumeChallengeTracking`
```lua
Game_ResumeChallengeTracking()
```
Resumes tracking of challenges. Note: Paused is not the same as stopped/disabled.

### `Game_RetrieveTableData`
```lua
Game_RetrieveTableData(String dataID, Boolean clearFromStorage)
```
Loads table data stored at datastore[dataID] into global lua table var named <dataID>. Set clearFromStorage to true to clear data from store.

### `Game_SaveBinaryDataStore`
```lua
Game_SaveBinaryDataStore(String id, String path, Integer version)
```
Save binary data store to disk

### `Game_SaveGameExistsDev`
```lua
Game_SaveGameExistsDev(String filename)
```
checks if the save game exists in dev folder and is loadable, filename is expected excluding folder and extension

### `Game_SaveInitAtmosphereSettings`
```lua
Game_SaveInitAtmosphereSettings(String settingsName)
```
Loads the current biome's initial atmosphere settings into the catalogue. This enables Game_TransitionToState to be usable from scar files for skirmish maps.

### `Game_SaveTextDataStore`
```lua
Game_SaveTextDataStore(String id, String path)
```
Save text data store to disk

### `Game_ScreenFade`
```lua
Game_ScreenFade(Real r, Real g, Real b, Real a, Real timeSecs)
```
Fades the screen to a given RGBA colour over a number of seconds

### `Game_SendCustomChallengeEvent`
```lua
Game_SendCustomChallengeEvent(PlayerID player, ChallengeEventType eventType, Real amount)
```
Updates the status of an in-game achievement or challenge.

### `Game_SendTributeSentEvent`
```lua
Game_SendTributeSentEvent(PlayerID player, Real amountsBeforeTax)
```
Sends an event of resource paid in tribute to other player.

### `Game_SetDataLock`
```lua
Game_SetDataLock(String dataID, Boolean lock)
```
sets lock state for stored data at location named by dataID.

### `Game_SetInputEnabledFlag`
```lua
Game_SetInputEnabledFlag(Integer flag)
```
Sets the input enabled flag.

### `Game_SetMapExplored`
```lua
Game_SetMapExplored(PlayerID player)
```
Sets the map explored state for the ExploredAll cheat

### `Game_SetPlayerColour`
```lua
Game_SetPlayerColour(target player, 1 based player colour index.)
```
Set the player color to the given colour index.

### `Game_SetPlayerSlotColour`
```lua
Game_SetPlayerSlotColour(PlayerID player, Integer slotIdx)
```
DEPRECATED! Use Game_SetPlayerColour instead.

### `Game_SetPlayerUISlotColour`
```lua
Game_SetPlayerUISlotColour(PlayerID player, Integer colourSlotIdx)
```
DEPRECATED! Use Game_SetPlayerColour instead.

### `Game_SetSimRate`
```lua
Game_SetSimRate(Real rate)
```
set the simulation update rate

### `Game_SetVisibility`
```lua
Game_SetVisibility(VisibilityFlag flag, Boolean visible)
```
Sets the visibility of the specified game visibility flag.

### `Game_SetVisibilityFlag`
```lua
Game_SetVisibilityFlag(Integer flag)
```
Sets the game visibility flag.

### `Game_ShowPauseMenu`
```lua
Game_ShowPauseMenu()
```
Brings up the pause menu. The game does not get paused until the end of the current sim tick, so anything that comes after Game_ShowPauseMenu in your function will still get executed, as well as any rules set to run during that frame.

### `Game_SkipAllEvents`
```lua
Game_SkipAllEvents(Boolean deleteQueued)
```
Skips all events. Can either delete or skip queued events.

### `Game_SkipEvent`
```lua
Game_SkipEvent()
```
Skips the currently playing event (and stops current sound).

### `Game_StoreTableData`
```lua
Game_StoreTableData(String dataID, RefTable table)
```
Stores provided table into long-lived data store at location named by dataID. This will replace an existing table if one exists.

### `Game_TextTitleFade`
```lua
Game_TextTitleFade(String text, Real fadeIn, Real duration, Real fadeOut)
```
Shows title text that fades in and out over a specified durations

### `Game_TransitionToState`
```lua
Game_TransitionToState(String stateName, Real transitionTimeSec)
```
Transitions to another atmosphere. Overwrites current transitions. Uses predefined atmosphere settings (only compatible with EEditor maps).

### `Game_UnLockRandom`
```lua
Game_UnLockRandom()
```
unlock the random from a previous lockrandom call only

## Ghost (2 functions)

### `Ghost_DisableSpotting`
```lua
Ghost_DisableSpotting()
```
Disable the spotting of enemy entities that may become ghosts in the FoW.

### `Ghost_EnableSpotting`
```lua
Ghost_EnableSpotting()
```
Enable the spotting of enemy entities that may become ghosts in the FoW.

## HintPoint (12 functions)

### `HintPoint_AddToEGroup`
```lua
HintPoint_AddToEGroup(EGroupID egroup, Integer priority, Boolean visible, LuaFunction function, String dataTemplate, String hint, Boolean arrow, Position arrowOffset, Integer actionType, String iconName, Boolean visibleInFOW)
```
Deprecated.

### `HintPoint_AddToEntity`
```lua
HintPoint_AddToEntity(EntityID entity, Integer priority, Boolean visible, LuaFunction function, String dataTemplate, String hint, Boolean arrow, Position arrowOffset, Integer objectiveID, Integer actionType, String iconName, Boolean visibleInFOW)
```
For internal use only.

### `HintPoint_AddToPosition`
```lua
HintPoint_AddToPosition(Position position, Integer priority, Boolean visible, LuaFunction function, String dataTemplate, String hint, Boolean arrow, Position arrowOffset, Integer objectiveID, Integer actionType, String iconName, Boolean visibleInFOW)
```
For internal use only.

### `HintPoint_AddToSGroup`
```lua
HintPoint_AddToSGroup(SGroupID sgroup, Integer priority, Boolean visible, LuaFunction function, String dataTemplate, String hint, Boolean arrow, Position arrowOffset, Integer actionType, String iconName, Boolean visibleInFOW)
```
Deprecated.

### `HintPoint_AddToSquad`
```lua
HintPoint_AddToSquad(SquadID squad, Integer priority, Boolean visible, LuaFunction function, String dataTemplate, String hint, Boolean arrow, Position arrowOffset, Integer objectiveID, Integer actionType, String iconName, Boolean visibleInFOW)
```
For internal use only.

### `HintPoint_ClearFacing`
```lua
HintPoint_ClearFacing(Integer id)
```
Clear the hint point arrow facing value.

### `HintPoint_RemoveAll`
```lua
HintPoint_RemoveAll()
```
Remove all hint points.

### `HintPoint_SetDisplayOffsetInternal`
```lua
HintPoint_SetDisplayOffsetInternal(Integer id, Position offset)
```
Add a projected offset to the specified hint point.

### `HintPoint_SetFacingEntity`
```lua
HintPoint_SetFacingEntity(Integer id, EntityID entity)
```
Face the hint point arrow towards this entity.

### `HintPoint_SetFacingPosition`
```lua
HintPoint_SetFacingPosition(Integer id, Position position)
```
Face the hint point arrow towards this position.

### `HintPoint_SetFacingSquad`
```lua
HintPoint_SetFacingSquad(Integer id, SquadID squad)
```
Face the hint point arrow towards this squad.

### `HintPoint_SetVisibleInternal`
```lua
HintPoint_SetVisibleInternal(Integer id, Boolean visible)
```
Show or hide the specified hint point.

## Hold (1 functions)

### `Hold_Info`
```lua
Hold_Info()
```
Toggle hold info

## inv (1 functions)

### `inv_dump`
```lua
inv_dump()
```
Dump content of inventory to a file

## IsEconomyClassStructure (1 functions)

### `IsEconomyClassStructure_CS`
```lua
IsEconomyClassStructure_CS(PropertyBagGroup pbg)
```
Returns true if the pbg class list contains a type that has economic utility

## IsSecuringStructure (1 functions)

### `IsSecuringStructure_CS`
```lua
IsSecuringStructure_CS(PropertyBagGroup pbg)
```
Can this structure be used to secure territory

## IsSecuringStructurePlacedOnPoint (1 functions)

### `IsSecuringStructurePlacedOnPoint_CS`
```lua
IsSecuringStructurePlacedOnPoint_CS(PropertyBagGroup pbg)
```
Can this structure be used to secure territory

## IsStructure (1 functions)

### `IsStructure_CS`
```lua
IsStructure_CS(PropertyBagGroup pbg)
```
Returns true if this object is a structure (something with a site_ext)

## LCWatcher (6 functions)

### `LCWatcher_Activate`
```lua
LCWatcher_Activate(Boolean on)
```
turns on the watcher and displays the lists if any

### `LCWatcher_AddFilter`
```lua
LCWatcher_AddFilter(String stateName, String filter)
```
Needs the proper luaConfig id, and looks through that list to add the filter.

### `LCWatcher_FilterExists`
```lua
LCWatcher_FilterExists(String stateName, String filter)
```
Needs the proper luaConfig id, returns true if filter exists.

### `LCWatcher_IsActive`
```lua
LCWatcher_IsActive()
```
Returns true if LCWatcher is active.

### `LCWatcher_RemoveFilter`
```lua
LCWatcher_RemoveFilter(String stateName, String filter)
```
Needs the proper luaConfig id, removes filter added by LCWatch_AddFilter.

### `LCWatcher_SelectState`
```lua
LCWatcher_SelectState(String state)
```
Selects a LuaConfig state to watch.  Returns true if state is registered and false if it has not.

## Loadout (2 functions)

### `Loadout_GetEquippedArmyUnitAtIndex`
```lua
Loadout_GetEquippedArmyUnitAtIndex(PlayerID player, Integer index)
```
Get the player's equipped elite at the specified index for their currently set race

### `Loadout_GetEquippedArmyUnitsCount`
```lua
Loadout_GetEquippedArmyUnitsCount(PlayerID player)
```
Get the number of elites currently equipped for the player's current race

## Loc (7 functions)

### `Loc_Empty`
```lua
Loc_Empty()
```
Returns an empty localized string.

### `Loc_FormatInteger`
```lua
Loc_FormatInteger(Integer integer)
```
Returns a localized string containing the integer.

### `Loc_FormatNumber`
```lua
Loc_FormatNumber(Real number, Integer numDecimalPlaces)
```
Returns a localized string containing the number to the specified number of decimal places.

### `Loc_FormatTime_H_M_S`
```lua
Loc_FormatTime_H_M_S(Real secs, Boolean leading_zeroes)
```
Returns a formatted time string in hours, minutes, and seconds. can omit leading zeroes.

### `Loc_FormatTime_M_S`
```lua
Loc_FormatTime_M_S(Real secs, Boolean leading_zeroes)
```
Returns a formatted time string in minutes and seconds. can omit leading zeroes.

### `Loc_FormatTime_M_S_MS`
```lua
Loc_FormatTime_M_S_MS(Real secs, Boolean leading_zeroes)
```
Returns a formatted time string in minutes, seconds, and milliseconds. can omit leading zeroes.

### `Loc_GetString`
```lua
Loc_GetString(StackVar id)
```
Returns the localized string identified by the specified id.

## LocalCommand (66 functions)

### `LocalCommand_Entity`
```lua
LocalCommand_Entity(PlayerID player, EGroupID egroup, EntityCommandType entityCommand)
```
Send a entity command to a entity group(CMD_DefaultAction, CMD_Stop, CMD_Destroy, CMD_BuildSquad, CMD_CancelProduction, CMD_RallyPoint, CMD_AttackForced)

### `LocalCommand_EntityAbility`
```lua
LocalCommand_EntityAbility(PlayerID player, EGroupID egroup, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send an entity ability command (CMD_Ability) to an entity

### `LocalCommand_EntityBuildSquad`
```lua
LocalCommand_EntityBuildSquad(PlayerID player, EGroupID egroup, ScarSquadPBG squadPbg)
```
Send a squad command to a entity group with custom data

### `LocalCommand_EntityEntity`
```lua
LocalCommand_EntityEntity(PlayerID player, EGroupID egroup, EntityCommandType entityCommand, EGroupID target)
```
Send a entity-based command to an entity group.

### `LocalCommand_EntityExt`
```lua
LocalCommand_EntityExt(PlayerID player, EGroupID egroup, EntityCommandType entityCommand, Integer cmdparam, Boolean queued)
```
Send a squad command to a squad group with custom data

### `LocalCommand_EntityPos`
```lua
LocalCommand_EntityPos(PlayerID player, EGroupID egroup, EntityCommandType entityCommand, Position target)
```
Send a position command to an entity group.

### `LocalCommand_EntityPosAbility`
```lua
LocalCommand_EntityPosAbility(PlayerID player, EGroupID egroup, Position pos, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a positional ability command (CMD_Ability) to an entity

### `LocalCommand_EntityPosDirAbility`
```lua
LocalCommand_EntityPosDirAbility(PlayerID player, EGroupID egroup, Position pos, Position dir, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a positional/directional ability command (CMD_Ability) to an entity

### `LocalCommand_EntityPosSquad`
```lua
LocalCommand_EntityPosSquad(PlayerID player, EGroupID egroup, EntityCommandType entityCommand, Position target, SGroupID sgroup)
```
Send a dual target (position and squad) command to an entity group.

### `LocalCommand_EntitySquad`
```lua
LocalCommand_EntitySquad(PlayerID player, EGroupID egroup, EntityCommandType entityCommand, SGroupID target)
```
Send a squad-based command to an entity group.

### `LocalCommand_EntityTargetEntityAbility`
```lua
LocalCommand_EntityTargetEntityAbility(PlayerID player, EGroupID egroup, EntityID entityTarget, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send an entity-targeting ability command (CMD_Ability) to an entity

### `LocalCommand_EntityTargetSquadAbility`
```lua
LocalCommand_EntityTargetSquadAbility(PlayerID player, EGroupID egroup, SquadID squadTarget, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send an squad-targeting ability command (CMD_Ability) to an entity

### `LocalCommand_EntityUpgrade`
```lua
LocalCommand_EntityUpgrade(PlayerID player, EGroupID egroup, ScarUpgradePBG upgrade, Boolean instant, Boolean queued)
```
Send a squad command to a entity group with custom data

### `LocalCommand_Player`
```lua
LocalCommand_Player(PlayerID player, PlayerID dest, PlayerCommandType playerCommand)
```
Send a player command to a player

### `LocalCommand_PlayerAbility`
```lua
LocalCommand_PlayerAbility(PlayerID player, PlayerID dest, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a player ability command (PCMD_Ability) to a player

### `LocalCommand_PlayerEntity`
```lua
LocalCommand_PlayerEntity(PlayerID player, PlayerID dest, PlayerCommandType playerCommand, EGroupID target)
```
Send an entity command to a player.

### `LocalCommand_PlayerExt`
```lua
LocalCommand_PlayerExt(PlayerID player, PlayerID dest, PlayerCommandType playerCommand, Integer cmdparam, Boolean queued)
```
Send a player command to a player with a custom flag

### `LocalCommand_PlayerMultiTargetAbility`
```lua
LocalCommand_PlayerMultiTargetAbility(PlayerID caster, vector<ConstTargetHandle> targets, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a player a command to use a multi-target ability on the given targets.

### `LocalCommand_PlayerPlaceAndConstructEntitiesPlanned`
```lua
LocalCommand_PlayerPlaceAndConstructEntitiesPlanned(PlayerID player, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued, Boolean payOnApply)
```
Place a planned structure

### `LocalCommand_PlayerPlaceAndConstructFencePlanned`
```lua
LocalCommand_PlayerPlaceAndConstructFencePlanned(PlayerID player, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued, Boolean payOnApply)
```
Place a planned fence

### `LocalCommand_PlayerPlaceAndConstructSlottedSplineConstructed`
```lua
LocalCommand_PlayerPlaceAndConstructSlottedSplineConstructed(PlayerID player, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued, Boolean payOnApply)
```
Place a constructed slotted spline

### `LocalCommand_PlayerPlaceAndConstructSlottedSplinePlanned`
```lua
LocalCommand_PlayerPlaceAndConstructSlottedSplinePlanned(PlayerID player, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued, Boolean payOnApply)
```
Place a planned slotted spline

### `LocalCommand_PlayerPos`
```lua
LocalCommand_PlayerPos(PlayerID player, PlayerID dest, PlayerCommandType playerCommand, Position pos)
```
Send a position command to a player.

### `LocalCommand_PlayerPosAbility`
```lua
LocalCommand_PlayerPosAbility(PlayerID player, PlayerID dest, Position pos, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a positional ability command (PCMD_Ability) to a player

### `LocalCommand_PlayerPosDirAbility`
```lua
LocalCommand_PlayerPosDirAbility(PlayerID player, PlayerID dest, Position pos, Position dir, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a positional/directional ability command (PCMD_Ability) to a player

### `LocalCommand_PlayerPosExt`
```lua
LocalCommand_PlayerPosExt(PlayerID player, PlayerID dest, PlayerCommandType playerCommand, Position pos, Integer cmdparam, Boolean queued)
```
Send a position command to a player with extra info

### `LocalCommand_PlayerSquadConstructBuilding`
```lua
LocalCommand_PlayerSquadConstructBuilding(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct the building at specific position and facing

### `LocalCommand_PlayerSquadConstructBuildingCheat`
```lua
LocalCommand_PlayerSquadConstructBuildingCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct the building at specific position and facing

### `LocalCommand_PlayerSquadConstructFence`
```lua
LocalCommand_PlayerSquadConstructFence(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct fences from posStart to posEnd

### `LocalCommand_PlayerSquadConstructFenceCheat`
```lua
LocalCommand_PlayerSquadConstructFenceCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct fences from posStart to posEnd

### `LocalCommand_PlayerSquadConstructField`
```lua
LocalCommand_PlayerSquadConstructField(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct a field ranging from posStart to posEnd

### `LocalCommand_PlayerSquadConstructFieldCheat`
```lua
LocalCommand_PlayerSquadConstructFieldCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a player command to itself to order squads in the sgroup to construct a field ranging from posStart to posEnd

### `LocalCommand_PlayerSquadConstructSlottedSpline`
```lua
LocalCommand_PlayerSquadConstructSlottedSpline(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline from posStart to posEnd.

### `LocalCommand_PlayerSquadConstructSlottedSplineCheat`
```lua
LocalCommand_PlayerSquadConstructSlottedSplineCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position posStart, Position posEnd, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline from posStart to posEnd.

### `LocalCommand_PlayerSquadConstructSlottedSplineDependent`
```lua
LocalCommand_PlayerSquadConstructSlottedSplineDependent(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline dependent entity.

### `LocalCommand_PlayerSquadConstructSlottedSplineDependentCheat`
```lua
LocalCommand_PlayerSquadConstructSlottedSplineDependentCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline dependent entity.

### `LocalCommand_PlayerSquadConstructSlottedSplineReplacer`
```lua
LocalCommand_PlayerSquadConstructSlottedSplineReplacer(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline replacer entity.

### `LocalCommand_PlayerSquadConstructSlottedSplineReplacerCheat`
```lua
LocalCommand_PlayerSquadConstructSlottedSplineReplacerCheat(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facingPos, Boolean queued)
```
Send a command from player to sgroup to build ebp as a slotted spline replacer entity.

### `LocalCommand_PlayerUpgrade`
```lua
LocalCommand_PlayerUpgrade(PlayerID player, ScarUpgradePBG upgrade, Boolean instant, Boolean queued)
```
Sends an upgrade command to a player

### `LocalCommand_Squad`
```lua
LocalCommand_Squad(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, Boolean queued)
```
Send a squad command to a squad group

### `LocalCommand_SquadAbility`
```lua
LocalCommand_SquadAbility(PlayerID player, SGroupID sgroup, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a ability command (SCMD_Ability) to a squad

### `LocalCommand_SquadAttackMovePos`
```lua
LocalCommand_SquadAttackMovePos(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, Position target, String planName, Boolean queued, Boolean split)
```
Send a position ATTACK MOVE command to a squad group with custom data.

### `LocalCommand_SquadEntity`
```lua
LocalCommand_SquadEntity(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, EGroupID target, Boolean queued)
```
Send an entity command to a squad group.

### `LocalCommand_SquadEntityAbility`
```lua
LocalCommand_SquadEntityAbility(PlayerID player, SGroupID sgroup, EGroupID target, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a entity ability command (SCMD_Ability) to a squad

### `LocalCommand_SquadEntityAttack`
```lua
LocalCommand_SquadEntityAttack(PlayerID player, SGroupID sgroup, EGroupID target, Boolean bCheckFOW, Boolean bStationary, String planName, Boolean queued)
```
Send an entity command ATTACK to a squad group.

### `LocalCommand_SquadEntityBool`
```lua
LocalCommand_SquadEntityBool(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, EGroupID target, Boolean cmdparam, Boolean queued)
```
Send a entity command to a squad group with custom BOOLEAN data

### `LocalCommand_SquadEntityExt`
```lua
LocalCommand_SquadEntityExt(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, EGroupID target, Integer cmdparam, Boolean queued)
```
Send a entity command to a squad group with custom data

### `LocalCommand_SquadEntityLoad`
```lua
LocalCommand_SquadEntityLoad(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, EGroupID target, Boolean bOverLoad, Boolean queued)
```
Send special squad command to a squad group with squad load parameters

### `LocalCommand_SquadExt`
```lua
LocalCommand_SquadExt(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, Integer cmdparam, Boolean queued)
```
Send a squad command to a squad group with custom data

### `LocalCommand_SquadMovePos`
```lua
LocalCommand_SquadMovePos(PlayerID player, SGroupID sgroup, Position target, Boolean queued, Boolean reverseMove, Boolean split, Real acceptableProximity)
```
Send a move to position command for a squad group.

### `LocalCommand_SquadMovePosFacing`
```lua
LocalCommand_SquadMovePosFacing(PlayerID player, SGroupID sgroup, Position target, Position facing, Boolean queued, Boolean reverseMove, Boolean split, Real acceptableProximity)
```
Send a move-facing command to a squad group

### `LocalCommand_SquadMultiTargetAbility`
```lua
LocalCommand_SquadMultiTargetAbility(SquadID caster, vector<ConstTargetHandle> targets, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a squad a command to use a multi-target ability on the given targets.

### `LocalCommand_SquadPath`
```lua
LocalCommand_SquadPath(PlayerID pPlayer, SGroupID pSGroup, String pathName, Integer pathIndex, Boolean bFromClosest, LoopType loopType, Boolean bAttackMove, Real pauseTime, Boolean bMoveForward, Boolean queued)
```
Send a squad patrol command (SCMD_Patrol) to a squad

### `LocalCommand_SquadPos`
```lua
LocalCommand_SquadPos(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, Position target, Boolean queued)
```
Send a position command to a squad group.

### `LocalCommand_SquadPosAbility`
```lua
LocalCommand_SquadPosAbility(PlayerID player, SGroupID sgroup, Position pos, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a positional ability command (SCMD_Ability) to a squad

### `LocalCommand_SquadPosExt`
```lua
LocalCommand_SquadPosExt(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, Position target, Integer cmdparam, Boolean queued)
```
Send a position command to a squad group with custom data

### `LocalCommand_SquadPositionAttack`
```lua
LocalCommand_SquadPositionAttack(PlayerID player, SGroupID sgroup, Position target, Boolean bCheckFOW, Boolean bStationary, String planName, Boolean queued)
```
Send an position command ATTACK to a squad group.

### `LocalCommand_SquadRetreatPos`
```lua
LocalCommand_SquadRetreatPos(PlayerID player, SGroupID sgroup, Position target, Boolean queued, Boolean allowNonInteractiveStages)
```
Send a retreat position command to a squad group.

### `LocalCommand_SquadSetCombatStance`
```lua
LocalCommand_SquadSetCombatStance(PlayerID player, SGroupID sgroup, StanceType stanceType, Boolean queued)
```
Send a set CombatStance command to the squads

### `LocalCommand_SquadSetWeaponPreference`
```lua
LocalCommand_SquadSetWeaponPreference(PlayerID player, SGroupID sgroup, WeaponPreference weaponPreference, Boolean queued)
```
Send a set Weapon Preference command to the squads

### `LocalCommand_SquadSquad`
```lua
LocalCommand_SquadSquad(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, SGroupID target, Boolean queued)
```
Send an squad-based command to a squad group.

### `LocalCommand_SquadSquadAbility`
```lua
LocalCommand_SquadSquadAbility(PlayerID player, SGroupID sgroup, SGroupID target, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq, Boolean queued)
```
Send a squad ability command (SCMD_Ability) to a squad

### `LocalCommand_SquadSquadAttack`
```lua
LocalCommand_SquadSquadAttack(PlayerID player, SGroupID sgroup, SGroupID target, Boolean bCheckFOW, Boolean bStationary, String planName, Boolean queued)
```
Send an squad-based command to a squad group.

### `LocalCommand_SquadSquadExt`
```lua
LocalCommand_SquadSquadExt(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, SGroupID target, Integer cmdparam, Boolean queued)
```
Send a squad command to a squad group with custom data

### `LocalCommand_SquadSquadLoad`
```lua
LocalCommand_SquadSquadLoad(PlayerID player, SGroupID sgroup, SquadCommandType squadCommand, SGroupID target, Boolean bOverLoad, Boolean queued)
```
Send special squad command to a squad group with squad load parameters

### `LocalCommand_SquadUpgrade`
```lua
LocalCommand_SquadUpgrade(PlayerID player, SGroupID sgroup, ScarUpgradePBG upgrade, Boolean instant, Boolean queued)
```
Sends an upgrade command to a squad group.

## lockstep (1 functions)

### `lockstep_simulation_presentation_toggle`
```lua
lockstep_simulation_presentation_toggle()
```
Run simulation and presentation in lockstep, with simulation ticked every frame (useful for debugging sync errors)

## MapIcon (9 functions)

### `MapIcon_ClearFacing`
```lua
MapIcon_ClearFacing(Integer id)
```
Clear the map icon facing value.

### `MapIcon_CreateEntity`
```lua
MapIcon_CreateEntity(EntityID entity, String icon, Real scale, Integer red, Integer green, Integer blue, Integer alpha)
```
Create a map icon targetting an entity.

### `MapIcon_CreatePosition`
```lua
MapIcon_CreatePosition(Position position, String icon, Real scale, Integer red, Integer green, Integer blue, Integer alpha)
```
Create a map icon targetting a position.

### `MapIcon_CreateSquad`
```lua
MapIcon_CreateSquad(SquadID squad, String icon, Real scale, Integer red, Integer green, Integer blue, Integer alpha)
```
Create a map icon targetting a squad.

### `MapIcon_Destroy`
```lua
MapIcon_Destroy(Integer id)
```
Remove a map icon.

### `MapIcon_DestroyAll`
```lua
MapIcon_DestroyAll()
```
Remove all map icons.

### `MapIcon_SetFacingEntity`
```lua
MapIcon_SetFacingEntity(Integer id, EntityID entity)
```
Face the map icon towards this entity.

### `MapIcon_SetFacingPosition`
```lua
MapIcon_SetFacingPosition(Integer id, Position position)
```
Face the map icon towards this position.

### `MapIcon_SetFacingSquad`
```lua
MapIcon_SetFacingSquad(Integer id, SquadID squad)
```
Face the map icon towards this squad.

## Marker (23 functions)

### `Marker_Create`
```lua
Marker_Create(String name, String type, Position pos, Position direction, Real radius)
```
Returns a newly created marker with the given attributes [direction] is expecting a direction vector and not a position relative to [pos]

### `Marker_CreateMarkerFromEntityMarker`
```lua
Marker_CreateMarkerFromEntityMarker(EntityID entity, String internalMarker, String newMarker)
```
Finds a marker in an entity, creates a SCAR marker there and returns the new marker's name.

### `Marker_Destroy`
```lua
Marker_Destroy(MarkerID marker)
```
Delete this marker, only recommended for dynamically created markers

### `Marker_DoesNumberAttributeExist`
```lua
Marker_DoesNumberAttributeExist(MarkerID marker, String name)
```
Returns true if a generic number attribute exists for the marker type.

### `Marker_DoesStringAttributeExist`
```lua
Marker_DoesStringAttributeExist(MarkerID marker, String name)
```
Returns true if a generic string attribute exists for the marker type.

### `Marker_Exists`
```lua
Marker_Exists(String name, String type)
```
Returns true if marker exists. If you don't care about the type, pass in an empty string ( "" )

### `Marker_FromName`
```lua
Marker_FromName(String name, String type)
```
Returns a ScarMarker from the Scenario Editor. If you don't care about the type, pass in an empty string ( "" )

### `Marker_GetDirection`
```lua
Marker_GetDirection(MarkerID marker)
```
Returns a vector for the marker direction

### `Marker_GetName`
```lua
Marker_GetName(MarkerID marker)
```
Returns the name of a given marker.  This value gets set in the Scenario Editor.

### `Marker_GetNumberAttribute`
```lua
Marker_GetNumberAttribute(MarkerID marker, String name)
```
Returns a generic number attribute defined in a marker.

### `Marker_GetPosition`
```lua
Marker_GetPosition(MarkerID marker)
```
Returns the position of a given marker.

### `Marker_GetProximityDimensionsOrDefault`
```lua
Marker_GetProximityDimensionsOrDefault(MarkerID marker, Real defaultWidth, Real defaultHeight)
```
Returns the proximity dimensions of a given marker.  If non rectangular, default value is returned Dimensions are 2d but returned in 3d world space (terrain mapped to x,z) This value gets set in the Scenario Editor.

### `Marker_GetProximityRadius`
```lua
Marker_GetProximityRadius(MarkerID marker)
```
Returns the proximity radius of a given marker.  If non circular, default value is returned This value gets set in the Scenario Editor.

### `Marker_GetProximityRadiusOrDefault`
```lua
Marker_GetProximityRadiusOrDefault(MarkerID marker, Real defaultValue)
```
Returns the proximity radius of a given marker.  If non circular, default value is returned This value gets set in the Scenario Editor.

### `Marker_GetStringAttribute`
```lua
Marker_GetStringAttribute(MarkerID marker, String name)
```
Returns a generic string attribute defined in a marker.

### `Marker_GetType`
```lua
Marker_GetType(MarkerID marker)
```
Returns the typename of a given marker. This is the typename from the Scenario Editor (name displayed when placing markers)

### `Marker_HasProximityRange`
```lua
Marker_HasProximityRange(MarkerID marker)
```
Returns if a marker has a defined (non-default) proximity range

### `Marker_InProximity`
```lua
Marker_InProximity(MarkerID marker, Position pos)
```
Returns true if the given position is in the markers proximity radius or proximity rectangle (depending on the type).

### `Marker_SetProximityCircle`
```lua
Marker_SetProximityCircle(MarkerID marker, Real radius)
```
Set the proximity shape of a marker to a circle with size radius

### `Marker_SetProximityPoint`
```lua
Marker_SetProximityPoint(MarkerID marker)
```
Set the proximity shape of a marker to point marker (no proximity)

### `Marker_SetProximityRectangle`
```lua
Marker_SetProximityRectangle(MarkerID marker, Real width, Real height)
```
Set the proximity shape of a marker to a rectangle with dimensions width and height

### `Marker_StartActionAt`
```lua
Marker_StartActionAt(String name, Position pos)
```
Start an Action at the given position.  Returns the id so the Action can be stopped using Marker_StopActionById.

### `Marker_StopActionById`
```lua
Marker_StopActionById(Integer id)
```
Stop an Action by id.  Marker_StartActionAt returns an id that can be used here.

## MemoryStats (3 functions)

### `MemoryStats_Disable`
```lua
MemoryStats_Disable()
```
Disable collecting and displaying render stats

### `MemoryStats_Enable`
```lua
MemoryStats_Enable()
```
Enable collecting and displaying render stats

### `MemoryStats_Toggle`
```lua
MemoryStats_Toggle()
```
Toggle collecting and displaying render stats

## Misc (107 functions)

### `__Internal_Game_Autosave`
```lua
__Internal_Game_Autosave()
```
DO NOT call this function directly, use Event_Save(STT_Auto) instead

### `__Internal_Game_Quicksave`
```lua
__Internal_Game_Quicksave()
```
DO NOT call this function directly, use Event_Save(STT_Quick) instead

### `__Internal_Game_SaveGame`
```lua
__Internal_Game_SaveGame()
```
DO NOT call this function directly, use Event_SaveWithName(STT_Standard) instead

### `__Internal_Game_SaveToFileDev`
```lua
__Internal_Game_SaveToFileDev()
```
DO NOT call this function directly, use Event_SaveWithName(STT_Dev) instead

### `AllMarkersFromName`
```lua
AllMarkersFromName(String name, String type)
```
Returns all ScarMarkers from the Mission Editor with the given name. If you don't care about the type, pass in an empty string ( "" )

### `DrawOBB`
```lua
DrawOBB(RenderModel* pModel, Transform& transform)
```
Draw the ref-posed OBB of a model

### `fatal`
```lua
fatal(lua_State* state)
```
Throws an error to lua and print out the error message

### `fatal`
```lua
fatal(lua_State* state)
```
Throws an error to lua and print out the error message

### `GetCameraNameFromPbgName`
```lua
GetCameraNameFromPbgName(String pbgPath)
```
get camera name from PBG path

### `getgametype`
```lua
getgametype()
```
Gets the type of game we are playing ( GT_SP = 0, GT_MP = 1, GT_Skirmish = 2)

### `getlocalplayer`
```lua
getlocalplayer()
```
Returns the local player index

### `getmapname`
```lua
getmapname()
```
Returns the scenario name (shortname version eg. "2P Semois")

### `GetPhysicsDebug`
```lua
GetPhysicsDebug()
```
Get physics debug toggle value

### `GetPhysicsRaycastAsCapsuleDebug`
```lua
GetPhysicsRaycastAsCapsuleDebug()
```
Get physics debug toggle value

### `getsimrate`
```lua
getsimrate()
```
Returns the current simulation rate.

### `listplayers`
```lua
listplayers()
```
Print all players information.

### `LOC`
```lua
LOC(String string)
```
DEV ONLY: Converts ansi text to localized text.

### `LogPrintTo`
```lua
LogPrintTo(String file, String txt)
```
Print text to specified file

### `MarkerCountFromName`
```lua
MarkerCountFromName(String name, String type)
```
Returns the number of ScarMarkers with the given name If you don't care about the type, pass in an empty string ( "" )

### `memdump`
```lua
memdump()
```
Write the OS map of allocated memory to the log folder

### `memdumpf`
```lua
memdumpf(String foldername)
```
Write the OS map of allocated memory to the log folder

### `mempoolcount`
```lua
mempoolcount()
```
Returns the numbers of memory pools

### `mempoolinuse`
```lua
mempoolinuse(Integer int)
```
Given a poolID it will return the current memory in use

### `mempoolmax`
```lua
mempoolmax(Integer int)
```
Given a poolID it will return the max amount of memory this pool has allocated

### `mempoolname`
```lua
mempoolname(Integer poolid)
```
Given a poolID it will return the name of the pool

### `memshrink`
```lua
memshrink()
```
Ask the OS to reduce the memory allocated to the game

### `memtofile`
```lua
memtofile(String pool)
```
Write to a file all allocation content for specified pool

### `Misc_AbortToFE`
```lua
Misc_AbortToFE()
```
Abort straight out of the game to the frontend, without asking the user

### `Misc_AddEntitiesToGroup`
```lua
Misc_AddEntitiesToGroup(EGroupID group, String entityIDsEncoded, Boolean includeSquads)
```
Appends the provided EntityIDs to the EGroup

### `Misc_AddRestrictCommandsCircle`
```lua
Misc_AddRestrictCommandsCircle(Position position, Real radius)
```
Add another circle in which commands are restricted to.

### `Misc_AddRestrictCommandsMarker`
```lua
Misc_AddRestrictCommandsMarker(MarkerID marker)
```
Add another marker in which commands are restricted to.

### `Misc_AddRestrictCommandsOBB`
```lua
Misc_AddRestrictCommandsOBB(Position minPosition, Position maxPosition)
```
Add another AABB in which commands are restricted to.

### `Misc_AddSquadsToGroup`
```lua
Misc_AddSquadsToGroup(SGroupID group, String entityIDsEncoded)
```
Appends the provided SquadIDs to the SGroup

### `Misc_AppendToFile`
```lua
Misc_AppendToFile(String filename, String text)
```
Appends given string to a file expects to receive a filename with an alias conserves existing file content \return Number returned is # bytes successfully written

### `Misc_AreDefaultCommandsEnabled`
```lua
Misc_AreDefaultCommandsEnabled()
```
Returns the enabled/disabled state of the right-click command input.  (not deterministic)

### `Misc_ClearControlGroup`
```lua
Misc_ClearControlGroup(Integer groupIndex)
```
Clears a specific control group.

### `Misc_ClearSelection`
```lua
Misc_ClearSelection()
```
Clears the current selection.

### `Misc_ClearSubselection`
```lua
Misc_ClearSubselection()
```
Clears the current sub selection.

### `Misc_DetectKeyboardInput`
```lua
Misc_DetectKeyboardInput(Real sinceTime)
```
Returns true if the app has had any keyboard input in the last second

### `Misc_DetectMouseInput`
```lua
Misc_DetectMouseInput(Real sinceTime)
```
Returns true if the app has had any mouse input in the last second

### `Misc_DoesPositionHaveAssociatedDistrict`
```lua
Misc_DoesPositionHaveAssociatedDistrict(Position pos)
```
Checks if the given position has an associated district.

### `Misc_DoWeaponHitEffectOnEntity`
```lua
Misc_DoWeaponHitEffectOnEntity(EntityID entity, Position pos, ScarWeaponPBG weaponPBG, Boolean penetrated)
```
Do weapon hit effect on the entity from the view camera origin

### `Misc_DoWeaponHitEffectOnPosition`
```lua
Misc_DoWeaponHitEffectOnPosition(Position pos, ScarWeaponPBG weaponPBG, Boolean penetrated)
```
Do weapon hit effect on the ground

### `Misc_EnablePerformanceTest`
```lua
Misc_EnablePerformanceTest(Boolean toEnable)
```
Turn on or off the performance test monitoring

### `Misc_FindDepositsCloseToSquad`
```lua
Misc_FindDepositsCloseToSquad(EGroupID group, SquadID squad, Real searchRange)
```
Find deposits within the specified range of a squad

### `Misc_FindDepositsOfTypeCloseToPosition`
```lua
Misc_FindDepositsOfTypeCloseToPosition(ResourceType resourceType, EBP gathererEBP, Position position, Number searchRange)
```
Finds resource deposits of given type within the specified range of a position, that can be collected by the provided gathererEBP

### `Misc_GetCommandLineString`
```lua
Misc_GetCommandLineString(String option)
```
Returns the string argument for a command line option. ex: for "-init test.lua" it would return "test.lua"

### `Misc_GetControlGroupContents`
```lua
Misc_GetControlGroupContents(Integer groupIndex, SGroupID squads, EGroupID nonSquadEntities)
```
Returns contents of a control group (0 to 9). Squads are put into an sgroup, and non-squad entities are put into an egroup.

### `Misc_GetDistrictGeneratorFromPosition`
```lua
Misc_GetDistrictGeneratorFromPosition(Position pos)
```
Return the entity generating the district containing the given position. Use with Misc_DoesPositionHaveAssociatedDistrict

### `Misc_GetDistrictValueFromPosition`
```lua
Misc_GetDistrictValueFromPosition(Position pos)
```
Return the district value of the district containing the given position. Use with Misc_DoesPositionHaveAssociatedDistrict

### `Misc_GetEntityControlGroup`
```lua
Misc_GetEntityControlGroup(EntityID entity)
```
Returns the control group index that this entity belongs to, from 0 to 9, or -1 if none.

### `Misc_GetFileSize`
```lua
Misc_GetFileSize(String filename)
```
returns the size of the file expects to receive a filename with an alias \return file size OR 0 if the file can not be read

### `Misc_GetHiddenPositionOnPath`
```lua
Misc_GetHiddenPositionOnPath(Integer checkType, Position origin, Position destination, Integer ebpID, Real stepDistance, Real cameraPadding, PlayerID FOWPlayer, Boolean debugDisplay)
```
Returns a hidden position on path from origin to destination. If there's none, it returns the origin position

### `Misc_GetMouseOnTerrain`
```lua
Misc_GetMouseOnTerrain()
```
Returns the world position of the mouse on the terrain (not deterministic)

### `Misc_GetMouseOverEntity`
```lua
Misc_GetMouseOverEntity()
```
Returns the entity under the mouse (if any) (not deterministic)

### `Misc_GetMouseOverSquad`
```lua
Misc_GetMouseOverSquad()
```
Returns the entity squad under the mouse (if any) (not deterministic)

### `Misc_GetScreenCenterPosition`
```lua
Misc_GetScreenCenterPosition()
```
Returns the world position of the the center of the screen

### `Misc_GetSelectedEntities`
```lua
Misc_GetSelectedEntities(EGroupID group, Boolean subselection)
```
Clears a given group and adds the current full selection (or subselection if true) to the group.

### `Misc_GetSelectedSquads`
```lua
Misc_GetSelectedSquads(SGroupID group, Boolean subselection)
```
Clears a given group and adds the current full selection (or subselection if true) to the group.

### `Misc_GetSimDefaultStepsPerSecond`
```lua
Misc_GetSimDefaultStepsPerSecond()
```
Returns the default simulation rate.

### `Misc_GetSimRate`
```lua
Misc_GetSimRate()
```
Returns the current simulation rate.

### `Misc_GetSquadControlGroup`
```lua
Misc_GetSquadControlGroup(SquadID squad)
```
Returns the control group index that this squad belongs to, from 0 to 9, or -1 if none.

### `Misc_IsCommandLineOptionSet`
```lua
Misc_IsCommandLineOptionSet(String option)
```
Returns true if -option is specified on the command line

### `Misc_IsDevMode`
```lua
Misc_IsDevMode()
```
Returns whether the game is running in dev mode.

### `Misc_IsEntityOnScreen`
```lua
Misc_IsEntityOnScreen(EntityID entity, Real percent)
```
Check if the squad is on screen currently (not deterministic)

### `Misc_IsEntitySelected`
```lua
Misc_IsEntitySelected(EntityID entity)
```
Returns true if the specified entity is currently selected.

### `Misc_IsMouseOverEntity`
```lua
Misc_IsMouseOverEntity()
```
Returns true if the mouse is over an entity (not deterministic)

### `Misc_IsMouseOverSquad`
```lua
Misc_IsMouseOverSquad()
```
Returns true if the mouse is over a squad (not deterministic)

### `Misc_IsPosOnScreen`
```lua
Misc_IsPosOnScreen(Position pos, Real percent)
```
Check if position is on screen, (1 being the entire screen, 0.5 being 50% of the screen from the center point)

### `Misc_IsSelectionInputEnabled`
```lua
Misc_IsSelectionInputEnabled()
```
Returns the enabled/disabled state of the selection input.  (not deterministic)

### `Misc_IsSquadOnScreen`
```lua
Misc_IsSquadOnScreen(SquadID squad, Real percent)
```
Check if the entity is on screen currently (not deterministic)

### `Misc_IsSquadSelected`
```lua
Misc_IsSquadSelected(SquadID squad)
```
Returns true if the specified squad is currently selected.

### `Misc_QueryDataDirectory`
```lua
Misc_QueryDataDirectory(String pathQuery, Boolean recursiveFind)
```
Assumes 'data:' as root; Returns a table containing the names of files matching the supplied path.

### `Misc_QueryDirectory`
```lua
Misc_QueryDirectory(String pathQuery, Boolean recursiveFind)
```
Returns a table containing the names of files matching the supplied path.

### `Misc_ReadFile`
```lua
Misc_ReadFile(String filename)
```
Reads the file as string expects to receive a filename with an alias \return file content OR empty string if the file can not be read

### `Misc_RemoveCommandRestriction`
```lua
Misc_RemoveCommandRestriction()
```
Remove all command restrictions.

### `Misc_RemoveFile`
```lua
Misc_RemoveFile(String filename)
```
Deletes the given file expects to receive a filename with an alias \return true if file was deleted or did not exist in the first place, false otherwise

### `Misc_RestrictCommandsToMarker`
```lua
Misc_RestrictCommandsToMarker(MarkerID marker)
```
Set the marker in which commands are restricted to.

### `Misc_Screenshot`
```lua
Misc_Screenshot()
```
Save a screenshot

### `Misc_ScreenshotExt`
```lua
Misc_ScreenshotExt(String fileExtension)
```
Set the graphic file type for screenshot (.jpg, .tga)

### `Misc_SelectEntity`
```lua
Misc_SelectEntity(EntityID entity)
```
Set the full selection to the specified entity.

### `Misc_SelectSquad`
```lua
Misc_SelectSquad(SquadID squad, Boolean selected)
```
Set the full selection to the specified entity.

### `Misc_SetCurrentAutotest`
```lua
Misc_SetCurrentAutotest(String description)
```
Sets the current autotest being used.  Used to set default text in the crash reports

### `Misc_SetDefaultCommandsEnabled`
```lua
Misc_SetDefaultCommandsEnabled(Boolean enabled)
```
Enables/disables right-click command input.

### `Misc_SetDesignerSplatsVisibility`
```lua
Misc_SetDesignerSplatsVisibility(Boolean bVisible)
```
Shows or hides designer splats, which are splats in the UI folder

### `Misc_SetEntityControlGroup`
```lua
Misc_SetEntityControlGroup(EntityID entity, Integer groupIndex)
```
Makes an entity belong to a specific control group. If it already belongs to another control group, it's removed from that one before being added to the new one.

### `Misc_SetEntitySelectable`
```lua
Misc_SetEntitySelectable(EntityID entity, Boolean selectable)
```
Disable/enable selectability of the specified entity.

### `Misc_SetSelectionInputEnabled`
```lua
Misc_SetSelectionInputEnabled(Boolean enabled)
```
Enables/disables selection input.

### `Misc_SetSimRate`
```lua
Misc_SetSimRate(Real rate)
```
Set the simulation rate

### `Misc_SetSquadControlGroup`
```lua
Misc_SetSquadControlGroup(SquadID squad, Integer groupIndex)
```
Makes a squad belong to a specific control group. If it already belongs to another control group, it's removed from that one before being added to the new one.

### `Misc_SetSquadSelectable`
```lua
Misc_SetSquadSelectable(SquadID squad, Boolean selectable)
```
Disable/enable selectability of the specified squad.

### `Misc_UpdateSlottedSplinesContainingEGroupAfterBlueprintConversion`
```lua
Misc_UpdateSlottedSplinesContainingEGroupAfterBlueprintConversion(EGroupID egroup)
```
Updates the slotted spline system to handle the fact that the entities in the given EGroup have done a blueprint conversion. This must be called after converting slotted spline entities from script.

### `Misc_WriteFile`
```lua
Misc_WriteFile(String filename, String text)
```
Writes the given string to a file expects to receive a filename with an alias overwrites any existing file content \return Number returned is # bytes successfully written

### `quit`
```lua
quit()
```
Exit to windows

### `restart`
```lua
restart()
```
Restart a single player game, skirmish game, or the front end. (doesn't work in multiplayer games)

### `scartype`
```lua
scartype(StackVar v)
```
Returns ST_NIL,ST_BOOLEAN,ST_NUMBER,ST_STRING,ST_TABLE,ST_FUNCTION,ST_SCARPOS,ST_EGROUP,ST_ENTITY,ST_SGROUP,ST_SQUAD,ST_TEAM,ST_MARKER, ST_PBG, or ST_UNKNOWN

### `separated`
```lua
separated(or not, SGroupID smallvector<SGroup, SGroupID sgroup, Boolean spawnedOnly, Real idealSquadRadius)
```
Try to group the squads, returning the squads in groupings that are at least the ideal squad range apart

### `setsimframecap`
```lua
setsimframecap(Real fcap)
```
Set the simulation rate

### `setsimpause`
```lua
setsimpause()
```
Pause the simulation.

### `setsimrate`
```lua
setsimrate(Real rate)
```
Set the simulation rate

### `switchplayer`
```lua
switchplayer(lua_State* state)
```
Change the local player.

### `TimerAdd`
```lua
TimerAdd(String command, Real freqInSec)
```
Add a timer to be triggered every 'freqInSec'. the timer will then run the passed-in command

### `TimerAddFrame`
```lua
TimerAddFrame(String command)
```
Add a timer to be triggered every frame the timer will then run the passed-in command

### `TimerAddOnce`
```lua
TimerAddOnce(String command, Real timeInSec)
```
Add a timer to be triggered once after 'freqInSec' has elapsed. the timer will then run the passed-in command

### `TimerDel`
```lua
TimerDel(String command)
```
Remove specified timer

### `TogglePhysicsDebug`
```lua
TogglePhysicsDebug(Boolean enable)
```
Toggle physics debug drawing

### `TogglePhysicsRaycastAsCapsuleDebug`
```lua
TogglePhysicsRaycastAsCapsuleDebug(Boolean enable)
```
Toggle physics debug drawing

## Modifier (5 functions)

### `Modifier_ApplyToEntity`
```lua
Modifier_ApplyToEntity(ScarModifier modifier, EntityID entity, Real durationSeconds)
```
Applies an entity modifier to an entity. Use a duration of 0 for an indefinite modifier.

### `Modifier_ApplyToPlayer`
```lua
Modifier_ApplyToPlayer(ScarModifier modifier, PlayerID player, Real durationSeconds)
```
Applies a player modifier to a player. Use a duration of 0 for an indefinite modifier.

### `Modifier_ApplyToSquad`
```lua
Modifier_ApplyToSquad(ScarModifier modifier, SquadID squad, Real durationSeconds)
```
Applies a squad modifier to a squad. Use a duration of 0 for an indefinite modifier.

### `Modifier_Create`
```lua
Modifier_Create(ModifierApplicationType applicationType, String modtype, ModifierUsageType usageType, Boolean exclusive, Real value, StackVar v)
```
Returns a modifier that you can apply to stuff.

### `Modifier_IsEnabled`
```lua
Modifier_IsEnabled(EntityID pEntity, String modtype, Boolean bEnabledByDefault)
```
Checks whether the modifier is enabled (requires an Entity and an Entity enable/disable modifier)

## MovieCapture (2 functions)

### `MovieCapture_Start`
```lua
MovieCapture_Start(Boolean lowResolution)
```
Start capturing a movie, optionally downscaling to low resolution.

### `MovieCapture_Stop`
```lua
MovieCapture_Stop()
```
Stop a previously started movie capture.

## network (2 functions)

### `network_show_calls`
```lua
network_show_calls()
```
toggle the outstanding network call information

### `network_show_statgraph`
```lua
network_show_statgraph()
```
toggle the network statgraph

## Obj (44 functions)

### `Obj_Create`
```lua
Obj_Create(PlayerID player, String title, String desc, String icon, String dataTemplate, String faction, ObjectiveType type, Integer parentID, String telemetryTitle)
```
Create an objective and returns the unique ID for it

### `Obj_CreatePopup`
```lua
Obj_CreatePopup(target objective ID, title in the pop up, override the data template defined in the objective with another one specified for this pop up.)
```
Create a center screen objective pop up (via TitleModel).

### `Obj_Delete`
```lua
Obj_Delete(Integer objectiveID)
```
Delete the objective with the specified ID

### `Obj_DeleteAll`
```lua
Obj_DeleteAll()
```
Delete all objectives

### `Obj_GetCounterCount`
```lua
Obj_GetCounterCount(Integer objectiveID)
```
Get the count of the counter on the objective.

### `Obj_GetCounterMax`
```lua
Obj_GetCounterMax(Integer objectiveID)
```
Get the maximum count of the counter on the objective.

### `Obj_GetCounterType`
```lua
Obj_GetCounterType(Integer objectiveID)
```
Get the counter type of an objective.

### `Obj_GetCounterVisible`
```lua
Obj_GetCounterVisible(Integer objectiveID)
```
Get Counter visibility  (not deterministic)

### `Obj_GetProgress`
```lua
Obj_GetProgress(Integer objectiveID)
```
Get objective progress bar value

### `Obj_GetProgressVisible`
```lua
Obj_GetProgressVisible(Integer objectiveID)
```
Get objective progress bar visibility  (not deterministic)

### `Obj_GetSecondaryCounterCount`
```lua
Obj_GetSecondaryCounterCount(Integer objectiveID)
```
Get the count of the counter on the objective.

### `Obj_GetSecondaryCounterMax`
```lua
Obj_GetSecondaryCounterMax(Integer objectiveID)
```
Get the maximum count of the counter on the objective.

### `Obj_GetSecondaryCounterType`
```lua
Obj_GetSecondaryCounterType(Integer objectiveID)
```
Get the counter type of an objective.

### `Obj_GetSecondaryCounterVisible`
```lua
Obj_GetSecondaryCounterVisible(Integer objectiveID)
```
Get Counter visibility  (not deterministic)

### `Obj_GetShowColour`
```lua
Obj_GetShowColour(Integer objectiveID)
```
Set if the Colour should be shown

### `Obj_GetState`
```lua
Obj_GetState(Integer objectiveID)
```
Get objective state ( OS_Off, OS_Incomplete, OS_Complete, OS_Failed ) (not deterministic)

### `Obj_GetVisible`
```lua
Obj_GetVisible(Integer objectiveID)
```
Get objective visibility  (not deterministic)

### `Obj_HideProgress`
```lua
Obj_HideProgress()
```
Hide the objective progress panel.

### `Obj_HideProgressEx`
```lua
Obj_HideProgressEx(Integer progressBarIndex)
```
Hide the specified objective progress panel.

### `Obj_SetColour`
```lua
Obj_SetColour(Integer objectiveID, Integer red, Integer green, Integer blue, Integer alpha)
```
Set colour of objective. In order red, green, blue, alpha.

### `Obj_SetCounterCount`
```lua
Obj_SetCounterCount(Integer objectiveID, Integer count)
```
Set the count of the counter on the objective.

### `Obj_SetCounterMax`
```lua
Obj_SetCounterMax(Integer objectiveID, Integer max)
```
Set the maximum count of the counter on the objective.

### `Obj_SetCounterTimerSeconds`
```lua
Obj_SetCounterTimerSeconds(Integer objectiveID, Real timerSeconds)
```
Set the number of seconds on an objective with a timer. Only used to inform the UI.

### `Obj_SetCounterType`
```lua
Obj_SetCounterType(Integer objectiveID, Integer counterType)
```
Set the counter type of an objective.

### `Obj_SetCounterVisible`
```lua
Obj_SetCounterVisible(Integer objectiveID, Boolean visible)
```
Set Counter visibility

### `Obj_SetDescription`
```lua
Obj_SetDescription(Integer objectiveID, String desc)
```
Set description text localization ID for the objective

### `Obj_SetIcon`
```lua
Obj_SetIcon(Integer objectiveID, String icon)
```
Set icon path for the objective

### `Obj_SetObjectiveFunction`
```lua
Obj_SetObjectiveFunction(Integer id, ObjectiveFn fnType, LuaFunction f)
```
Set callback functions for the objective.  (not deterministic)

### `Obj_SetProgress`
```lua
Obj_SetProgress(Integer objectiveID, Real progress)
```
Set objective progress bar value

### `Obj_SetProgressBlinking`
```lua
Obj_SetProgressBlinking(Boolean blinking)
```
Make the objective progress bar blink or stop blinking.

### `Obj_SetProgressVisible`
```lua
Obj_SetProgressVisible(Integer objectiveID, Boolean visible)
```
Set objective progress bar visibility

### `Obj_SetSecondaryCounterCount`
```lua
Obj_SetSecondaryCounterCount(Integer objectiveID, Integer count)
```
Set the count of the counter on the objective.

### `Obj_SetSecondaryCounterMax`
```lua
Obj_SetSecondaryCounterMax(Integer objectiveID, Integer max)
```
Set the maximum count of the counter on the objective.

### `Obj_SetSecondaryCounterTimerSeconds`
```lua
Obj_SetSecondaryCounterTimerSeconds(Integer objectiveID, Real timerSeconds)
```
Set the number of seconds on an objective with a timer. Only used to inform the UI.

### `Obj_SetSecondaryCounterType`
```lua
Obj_SetSecondaryCounterType(Integer objectiveID, Integer counterType)
```
Set the counter type of an objective.

### `Obj_SetSecondaryCounterVisible`
```lua
Obj_SetSecondaryCounterVisible(Integer objectiveID, Boolean visible)
```
Set Counter visibility

### `Obj_SetShowColour`
```lua
Obj_SetShowColour(Integer objectiveID, Boolean showColour)
```
Set if the Colour should be shown

### `Obj_SetState`
```lua
Obj_SetState(Integer objectiveID, State state)
```
Set objective state ( OS_Off, OS_Incomplete, OS_Complete, OS_Failed )

### `Obj_SetTitle`
```lua
Obj_SetTitle(Integer objectiveID, String title)
```
Set title text localization ID for the objective

### `Obj_SetVisible`
```lua
Obj_SetVisible(Integer objectiveID, Boolean visible)
```
Set objective visibility

### `Obj_ShowProgress`
```lua
Obj_ShowProgress(String title, Real progress)
```
Show the objective progress panel with a progress bar - call repeatedly to update progress.  Value should be normalized between [0 - 1].

### `Obj_ShowProgress2`
```lua
Obj_ShowProgress2(String title, Real progress)
```
Show the objective progress panel with a progress bar - call repeatedly to update progress.  Value should be normalized between [0 - 1].  Appears in center of screen.

### `Obj_ShowProgressEx`
```lua
Obj_ShowProgressEx(Integer progressBarIndex, String title, Real progress, Boolean critical)
```
Show the specified objective progress panel with a progress bar - call repeatedly to update progress. Value should be normalized between [0 - 1].  If critical, progress bar will pulse.

### `Obj_ShowProgressTimer`
```lua
Obj_ShowProgressTimer(Real progress)
```
Show the objective progress panel with a timer icon - call repeatedly to update progress.  Value should be in seconds.

## Path (7 functions)

### `Path_ClearCells`
```lua
Path_ClearCells()
```
Clear entire draw pathfinding cell list

### `Path_DrawImpass`
```lua
Path_DrawImpass()
```
Draw pathfinding impassable map

### `Path_DrawPath`
```lua
Path_DrawPath()
```
Toggle pathfinding entity path

### `Path_DrawPathMap`
```lua
Path_DrawPathMap(Boolean onoff)
```
Draw pathfinding grid overlay

### `Path_ShowCell`
```lua
Path_ShowCell(Integer x, Integer y)
```
Add pathfinding cell to draw cell list

### `Path_ShowPreciseCell`
```lua
Path_ShowPreciseCell(Integer x, Integer y)
```
Add pathfinding precise cell to draw cell list

### `Path_ToggleCollisionCircle`
```lua
Path_ToggleCollisionCircle()
```
Toggle pathfinding collision circles

## PBG (3 functions)

### `PBG_ReloadMouseOverEntity`
```lua
PBG_ReloadMouseOverEntity()
```
Reload mouse over entity's entire list of extension info's

### `PBG_ReloadMouseOverSquad`
```lua
PBG_ReloadMouseOverSquad()
```
Reload mouse over squad's entire list of extension info's

### `PBG_ReloadMouseOverWeapon`
```lua
PBG_ReloadMouseOverWeapon()
```
Reload mouse over squad's weapon property bag

## PerfStats (5 functions)

### `PerfStats_Disable`
```lua
PerfStats_Disable()
```
Disable displaying the Essence Profiler

### `PerfStats_Dump`
```lua
PerfStats_Dump()
```
Dump the Essence Profiler data onto a file

### `PerfStats_Enable`
```lua
PerfStats_Enable()
```
Enable displaying the Essence Profiler

### `PerfStats_IsEnabled`
```lua
PerfStats_IsEnabled()
```
Get perf stats toggle value

### `PerfStats_Toggle`
```lua
PerfStats_Toggle()
```
Toggle displaying the Essence Profiler

## Physics (3 functions)

### `Physics_GetNumRBodies`
```lua
Physics_GetNumRBodies()
```
Returns the number of rigid bodies in the physical world

### `Physics_IsEnabled`
```lua
Physics_IsEnabled()
```
Returns true if the current specs allows for physics to play

### `Physics_PurgeOrphans`
```lua
Physics_PurgeOrphans()
```
Removes all orphaned physics objects from the world.

## Player (114 functions)

### `Player_AddAbility`
```lua
Player_AddAbility(Player& player, ScarAbilityPBG pAbilityPBG)
```
Add an ability to a player

### `Player_AddAbilityLockoutZone`
```lua
Player_AddAbilityLockoutZone(Player& player, ScarAbilityPBG abilityPBG, MarkerID marker)
```
Specifies a marker where an ability cannot be used. This only applies to abilities where you use the cursor to pick a location in the world (like a location to paradrop at).

### `Player_AddUnspentCommandPoints`
```lua
Player_AddUnspentCommandPoints(Player& player, Real points)
```
Gives the player new command points to spent on

### `Player_CanCastAbilityOnEntity`
```lua
Player_CanCastAbilityOnEntity(PlayerID player, ScarAbilityPBG abilityPBG, EntityID targetEntity)
```
Tests if the player can currently use an ability on target entity

### `Player_CanCastAbilityOnPlayer`
```lua
Player_CanCastAbilityOnPlayer(PlayerID player, ScarAbilityPBG abilityPBG, PlayerID targetPlayer)
```
Tests if the player can currently use an ability on target player

### `Player_CanCastAbilityOnPosition`
```lua
Player_CanCastAbilityOnPosition(PlayerID player, ScarAbilityPBG abilityPBG, Position targetPosition)
```
Tests if the player can currently use an ability on target position

### `Player_CanCastAbilityOnSquad`
```lua
Player_CanCastAbilityOnSquad(PlayerID player, ScarAbilityPBG abilityPBG, SquadID targetSquad)
```
Tests if the player can currently use an ability on target squad

### `Player_CanConstruct`
```lua
Player_CanConstruct(PlayerID player, PropertyBagGroup pbg)
```
Tests if the player is able to construct a given blueprint

### `Player_CanPlaceStructureOnPosition`
```lua
Player_CanPlaceStructureOnPosition(PlayerID player, SGroupID sgroup, ScarEntityPBG ebp, Position position, Position facing)
```
Check if a player of specified group can place an entity at the specified position and facing angle.

### `Player_CanSeeEntity`
```lua
Player_CanSeeEntity(PlayerID player, EntityID entity)
```
Returns true if a player can see a given entity (revealed in FOW)

### `Player_CanSeePosition`
```lua
Player_CanSeePosition(PlayerID player, Position pos)
```
Returns true if a player can see a given position.

### `Player_CanSeeSquad`
```lua
Player_CanSeeSquad(PlayerID player, SquadID squad, Boolean all)
```
Returns true if a player can see ALL or ANY units in a given squad (revealed in FOW)

### `Player_ClearAvailabilities`
```lua
Player_ClearAvailabilities(Player& player)
```
Clears item, command and construction menu availabilities for the player.

### `Player_ClearPopCapOverride`
```lua
Player_ClearPopCapOverride(Player& player)
```
Clears the pop cap override so that modifiers can take effect again

### `Player_ClearStateModelEnumTableTarget`
```lua
Player_ClearStateModelEnumTableTarget(Player& player, String key, Integer tableRowIndex)
```
Clears a TargetHandle value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_ClearStateModelTarget`
```lua
Player_ClearStateModelTarget(Player& player, String key)
```
Clears a TargetHandle value in the Player's state model corresponding to the given key.

### `Player_CompleteUpgrade`
```lua
Player_CompleteUpgrade(Player& pPlayer, ScarUpgradePBG pUpgradePBG)
```
Finish upgrade for a player

### `Player_FindFirstEnemyPlayer`
```lua
Player_FindFirstEnemyPlayer(PlayerID player)
```
Searches the player list in the world and returns the id of the first enemy player

### `Player_FindFirstNeutralPlayer`
```lua
Player_FindFirstNeutralPlayer(PlayerID player)
```
Searches the player list in the world and returns the id of the first neutral player

### `Player_FromId`
```lua
Player_FromId(Integer id)
```
Returns a player given a player id from the ME.

### `Player_GetAbilityBPCost`
```lua
Player_GetAbilityBPCost(PlayerID pPlayer, PropertyBagGroup pbg)
```
Returns the modified cost of the given ability including all modifications added by the given player

### `Player_GetAIType`
```lua
Player_GetAIType(Player& player)
```
Returns the type of the given player if it is an AI.

### `Player_GetAllEntities`
```lua
Player_GetAllEntities(Player& player)
```
Returns an sim::EntityGroupObs containing all the players entities including ones in squad.

### `Player_GetCurrentPopulation`
```lua
Player_GetCurrentPopulation(Player& player, CapType capType)
```
Use capType CT_Personnel to get current squad cap, CT_Vehicle to get current vehicle cap, CT_Medic to get current medic cap

### `Player_GetCurrentPopulationCap`
```lua
Player_GetCurrentPopulationCap(Player& player, CapType capType)
```
Get current popcap. Use capType CT_Personnel to get current squad cap or CT_VehicleCap to get current vehicle cap.

### `Player_GetDisplayName`
```lua
Player_GetDisplayName(Player& player)
```
Returns the players UI name.

### `Player_GetEntities`
```lua
Player_GetEntities(Player& player)
```
Returns an sim::EntityGroupObs containing all the players entities excluding ones in squad.

### `Player_GetEntitiesEGroup`
```lua
Player_GetEntitiesEGroup(Player& player, EGroupID group)
```
Gets all the player's current entities and loads them into the specified egroup.

### `Player_GetEntityBPCost`
```lua
Player_GetEntityBPCost(PlayerID player, PropertyBagGroup pbg)
```
Returns the modified cost of the given entity including all modifications added by the given player

### `Player_GetEntityCount`
```lua
Player_GetEntityCount(Player& player)
```
Returns the number of entities a player currently owns

### `Player_GetEntityCountByUnitType`
```lua
Player_GetEntityCountByUnitType(Player& player, String unitTypeString)
```
Returns the number of entities of a certain unit type

### `Player_GetEntityName`
```lua
Player_GetEntityName(Player& player, Integer index)
```
Returns the name of an entity a player currently owns

### `Player_GetID`
```lua
Player_GetID(Player& player)
```
Returns the id of the player

### `Player_GetMaxPopulationCap`
```lua
Player_GetMaxPopulationCap(Player& player, CapType capType)
```
Get maximum popcap. Use capType CT_Personnel to get max squad cap or CT_VehicleCap to get max vehicle cap.

### `Player_GetMaxPopulationCapOverride`
```lua
Player_GetMaxPopulationCapOverride(Player& player, CapType capType)
```
Get maximum popcap including any overrides. Use capType CT_Personnel to get max squad cap or CT_VehicleCap to get max vehicle cap. If there are no overrides, the default max pop cap is returned.

### `Player_GetNumGatheringSquads`
```lua
Player_GetNumGatheringSquads(Player& player, Integer type)
```
Returns the number of squads currently gathering resources of a given type

### `Player_GetNumStrategicPoints`
```lua
Player_GetNumStrategicPoints(Player& p)
```
Returns the number of strategic points (not objectives) this player owns

### `Player_GetNumVictoryPoints`
```lua
Player_GetNumVictoryPoints(Player& p)
```
Returns the number of strategic objectives this player owns

### `Player_GetRace`
```lua
Player_GetRace(Player& player)
```
Returns the race for the given player.

### `Player_GetRaceName`
```lua
Player_GetRaceName(Player& player)
```
Returns the name of the race for a given player (always in english)

### `Player_GetRelationship`
```lua
Player_GetRelationship(PlayerID player1, PlayerID player2)
```
DEPRECATED, use Player_ObserveRelationship instead.

### `Player_GetResource`
```lua
Player_GetResource(Player& player, Integer type)
```
Returns the amount of resources a given player has.

### `Player_GetResourceRate`
```lua
Player_GetResourceRate(Player& player, Integer type)
```
Returns the amount of resources a given player is getting per second.

### `Player_GetResources`
```lua
Player_GetResources(Player& player)
```
Returns the list of all the resources a given player has.

### `Player_GetSlotIndex`
```lua
Player_GetSlotIndex(Player& player)
```
Returns the lobby slot index for this player, starting at one

### `Player_GetSquadBPCost`
```lua
Player_GetSquadBPCost(PlayerID pPlayer, PropertyBagGroup pbg)
```
Returns the modified cost of the given unit including all modifications added by the given player

### `Player_GetSquadCount`
```lua
Player_GetSquadCount(Player& player)
```
Returns the number of squads a player currently owns

### `Player_GetSquads`
```lua
Player_GetSquads(Player& player)
```
Returns a SquadGroupObs containing all the players units.

### `Player_GetStartingPosition`
```lua
Player_GetStartingPosition(Player& player)
```
Returns the starting position for this player

### `Player_GetState`
```lua
Player_GetState(PlayerID pPlayer)
```
Returns the current game state of the player.

### `Player_GetStateModelBool`
```lua
Player_GetStateModelBool(Player& player, String key)
```
Returns a boolean value from the Player's state model corresponding to the given key.

### `Player_GetStateModelEntityTarget`
```lua
Player_GetStateModelEntityTarget(Player& player, String key)
```
Returns an Entity value from the Player's state model corresponding to the given key.

### `Player_GetStateModelEnumTableBool`
```lua
Player_GetStateModelEnumTableBool(Player& player, String key, Integer tableRowIndex)
```
Returns a boolean value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTableEntityTarget`
```lua
Player_GetStateModelEnumTableEntityTarget(Player& player, String key, Integer tableRowIndex)
```
Returns an Entity value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTableFloat`
```lua
Player_GetStateModelEnumTableFloat(Player& player, String key, Integer tableRowIndex)
```
Returns a float value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTableInt`
```lua
Player_GetStateModelEnumTableInt(Player& player, String key, Integer tableRowIndex)
```
Returns an integer value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTablePlayerTarget`
```lua
Player_GetStateModelEnumTablePlayerTarget(Player& player, String key, Integer tableRowIndex)
```
Returns a Player value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTableSquadTarget`
```lua
Player_GetStateModelEnumTableSquadTarget(Player& player, String key, Integer tableRowIndex)
```
Returns a Squad value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelEnumTableVector3f`
```lua
Player_GetStateModelEnumTableVector3f(Player& player, String key, Integer tableRowIndex)
```
Returns a Vector3f value from the player's state model corresponding to the given key and table row index (0 based).

### `Player_GetStateModelFloat`
```lua
Player_GetStateModelFloat(Player& player, String key)
```
Returns a float value from the Player's state model corresponding to the given key.

### `Player_GetStateModelInt`
```lua
Player_GetStateModelInt(Player& player, String key)
```
Returns an integer value from the Player's state model corresponding to the given key.

### `Player_GetStateModelPlayerTarget`
```lua
Player_GetStateModelPlayerTarget(Player& player, String key)
```
Returns a Player value from the Player's state model corresponding to the given key.

### `Player_GetStateModelSquadTarget`
```lua
Player_GetStateModelSquadTarget(Player& player, String key)
```
Returns a Squad value from the Player's state model corresponding to the given key.

### `Player_GetStateModelVector3f`
```lua
Player_GetStateModelVector3f(Player& player, String key)
```
Returns a Vector3f value from the Player's state model corresponding to the given key.

### `Player_GetStrategicPointCaptureProgress`
```lua
Player_GetStrategicPointCaptureProgress(PlayerID player, EntityID strategicPoint)
```
Returns a value (-1.0 to 1.0) of how close a point is to being controlled by the team of the player provided

### `Player_GetTeam`
```lua
Player_GetTeam(Player& p)
```
Get the team a player is on

### `Player_GetTributeIncrementModifier`
```lua
Player_GetTributeIncrementModifier()
```
Returns the current game state of the player.

### `Player_GetUIColour`
```lua
Player_GetUIColour(Player& player)
```
Returns the UI colour of a player with respect to the local machine. Access with .r .g .b .a. Values are in the range 0-255.

### `Player_GetUnitCount`
```lua
Player_GetUnitCount(Player& player)
```
Returns the current number of units the player has.

### `Player_GetUpgradeBPCost`
```lua
Player_GetUpgradeBPCost(PlayerID player, ScarUpgradePBG upgradePBG)
```
Returns the cost of an upgrade.

### `Player_GetUpgradeBPCostByResource`
```lua
Player_GetUpgradeBPCostByResource(PlayerID player, ScarUpgradePBG upgradePBG, Integer type)
```
Returns the cost of an upgrade in a specific resource.

### `Player_GetUpgradeTimeCost`
```lua
Player_GetUpgradeTimeCost(ScarUpgradePBG upgradePBG)
```
Returns the unmodified time cost of an upgrade in seconds.

### `Player_GiftResource`
```lua
Player_GiftResource(Player& player, Integer type, Real amount)
```
Set the gifted resource amount for a given player A positive resource amount means the player receives the resources A negative resource amount means the player sends the resources Ignores income cap and resource sharing.

### `Player_HasAbility`
```lua
Player_HasAbility(Player& player, ScarAbilityPBG pAbilityPBG)
```
Tests to see if a player has an ability

### `Player_HasCapturingSquadNearStrategicPoint`
```lua
Player_HasCapturingSquadNearStrategicPoint(PlayerID player, EntityID strategicPoint)
```
Returns true if the given player has units that are able to capture in the capturable area of the given strategic point

### `Player_HasEntity`
```lua
Player_HasEntity(Player& player, ScarEntityPBG entity)
```
Tests to see if the player has any entities with the specified PBG

### `Player_HasMapEntryPosition`
```lua
Player_HasMapEntryPosition(PlayerID player)
```
Returns whether a player has a map entry position

### `Player_HasUpgrade`
```lua
Player_HasUpgrade(PlayerID pPlayer, ScarUpgradePBG upgradePBG)
```
Return true if the squad has purchased the specified upgrade.

### `Player_IsAbilityActive`
```lua
Player_IsAbilityActive(Player& player, ScarAbilityPBG abilityPBG)
```
Returns true or false, depending on whether the passed in player ability is active on the player

### `Player_IsAlive`
```lua
Player_IsAlive(Player& player)
```
Returns true if player is still alive and false if player is dead.  Will error if playerIdx is an invalid index.

### `Player_IsHuman`
```lua
Player_IsHuman(Player& player)
```
Returns whether a player is human controlled (local or remote), not dead, and not replaced by an AI

### `Player_IsSurrendered`
```lua
Player_IsSurrendered(Player& player)
```
Returns true if player has surrendered and false if not.  Will error if playerIdx is an invalid index.

### `Player_IsValid`
```lua
Player_IsValid(Integer id)
```
Check if id corresponds to a player

### `Player_NumUpgradeComplete`
```lua
Player_NumUpgradeComplete(Player& player, ScarUpgradePBG upgradePBG)
```
Returns the number of upgrades that this player has.

### `Player_ObserveRelationship`
```lua
Player_ObserveRelationship(PlayerID observer, PlayerID target)
```
Get the relationship that observer has to target.

### `Player_ObserveReputation`
```lua
Player_ObserveReputation(PlayerID observer, PlayerID target)
```
Get the reputation that observer has to target.

### `Player_RemoveAbilityLockoutZone`
```lua
Player_RemoveAbilityLockoutZone(Player& player, ScarAbilityPBG abilityPBG, MarkerID marker)
```
Removes a marker that was previously a lockout zone.

### `Player_RemoveAllUpgrades`
```lua
Player_RemoveAllUpgrades(Player& player)
```
Removes all upgrade from a player

### `Player_RemoveUpgrade`
```lua
Player_RemoveUpgrade(Player& player, ScarUpgradePBG upgrade)
```
Removes an upgrade from a player

### `Player_ResetAbilityCooldowns`
```lua
Player_ResetAbilityCooldowns(Player& player, ScarAbilityPBG ability)
```
Reset the cooldown of an ability on every unit a player has, and the player itself.

### `Player_ResetResource`
```lua
Player_ResetResource(Player& player, Integer type)
```
Reset the resource amount for a given player to zero.

### `Player_SetAllCommandAvailabilityInternal`
```lua
Player_SetAllCommandAvailabilityInternal(Player& player, Availability availability, String reason)
```
Sets availability of ALL entity, squad and player commands.

### `Player_SetDefaultSquadMoodMode`
```lua
Player_SetDefaultSquadMoodMode(Player& player, SquadCombatBehaviourMoodMode mood)
```
Set default squad mood mode which can be overrided by squad level mood mode settings

### `Player_SetPopCapOverride`
```lua
Player_SetPopCapOverride(Player& player, Real personnel)
```
Sets a pop cap override that ignores any modifiers.

### `Player_SetRelationship`
```lua
Player_SetRelationship(PlayerID observer, PlayerID target, Relation relationship)
```
Set the relationship that observer has to target. If the relationship does not match the current reputation, the reputation will be changed to match it.

### `Player_SetReputation`
```lua
Player_SetReputation(PlayerID observer, PlayerID target, BaseType reputation)
```
Set the reputation that observer has to target. If the reputation does not match the current relationship, the relationship will be changed to match it.

### `Player_SetResource`
```lua
Player_SetResource(Player& player, Integer type, Real amt)
```
Set the resource amount for a given player.  Ignores income cap and resource sharing.

### `Player_SetResourceInternal`
```lua
Player_SetResourceInternal(Player& player, Integer type, Real amt, AddResourceReason reason)
```
Set the resource amount for a given player.  Ignores income cap and resource sharing.

### `Player_SetResources`
```lua
Player_SetResources(Player& player, ResourceAmount resourceAmount)
```
Set all the resource amount for a given player.  Ignores income cap and resource sharing.

### `Player_SetStateModelBool`
```lua
Player_SetStateModelBool(Player& player, String key, Boolean value)
```
Sets a boolean value in the Player's state model corresponding to the given key.

### `Player_SetStateModelEntityTarget`
```lua
Player_SetStateModelEntityTarget(Player& player, String key, EntityID value)
```
Sets an Entity TargetHandle value in the Player's state model corresponding to the given key.

### `Player_SetStateModelEnumTableBool`
```lua
Player_SetStateModelEnumTableBool(Player& player, String key, Integer tableRowIndex, Boolean value)
```
Sets a boolean value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTableEntityTarget`
```lua
Player_SetStateModelEnumTableEntityTarget(Player& player, String key, Integer tableRowIndex, EntityID value)
```
Sets an Entity TargetHandle value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTableFloat`
```lua
Player_SetStateModelEnumTableFloat(Player& player, String key, Integer tableRowIndex, Real value)
```
Sets a float value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTableInt`
```lua
Player_SetStateModelEnumTableInt(Player& player, String key, Integer tableRowIndex, Integer value)
```
Sets an integer value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTablePlayerTarget`
```lua
Player_SetStateModelEnumTablePlayerTarget(Player& player, String key, Integer tableRowIndex, PlayerID value)
```
Sets a Player TargetHandle value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTableSquadTarget`
```lua
Player_SetStateModelEnumTableSquadTarget(Player& player, String key, Integer tableRowIndex, SquadID value)
```
Sets a Squad TargetHandle value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelEnumTableVector3f`
```lua
Player_SetStateModelEnumTableVector3f(Player& player, String key, Integer tableRowIndex, Position value)
```
Sets a Vector3f value in the player's state model corresponding to the given key and table row index (0 based).

### `Player_SetStateModelFloat`
```lua
Player_SetStateModelFloat(Player& player, String key, Real value)
```
Sets a float value in the Player's state model corresponding to the given key.

### `Player_SetStateModelInt`
```lua
Player_SetStateModelInt(Player& player, String key, Integer value)
```
Sets an integer value in the Player's state model corresponding to the given key.

### `Player_SetStateModelPlayerTarget`
```lua
Player_SetStateModelPlayerTarget(Player& player, String key, PlayerID value)
```
Sets a Player TargetHandle value in the Player's state model corresponding to the given key.

### `Player_SetStateModelSquadTarget`
```lua
Player_SetStateModelSquadTarget(Player& player, String key, SquadID value)
```
Sets a Squad TargetHandle value in the Player's state model corresponding to the given key.

### `Player_SetStateModelVector3f`
```lua
Player_SetStateModelVector3f(Player& player, String key, Position value)
```
Sets a Vector3f value in the Player's state model corresponding to the given key.

### `Player_StopAbility`
```lua
Player_StopAbility(PlayerID player, ScarAbilityPBG ability, Boolean bIsEarlyExit)
```
Abruptly stops an active ability

## PlayerColour (4 functions)

### `PlayerColour_ClearConfigChangedCallback`
```lua
PlayerColour_ClearConfigChangedCallback()
```
Clears the config changed callback

### `PlayerColour_Disable`
```lua
PlayerColour_Disable()
```
Clear player color overriding and use the "PlayerColour" setting instead.

### `PlayerColour_Enable`
```lua
PlayerColour_Enable()
```
Force enable player color that overrides the current "PlayerColour" setting.

### `PlayerColour_SetConfigChangedCallback`
```lua
PlayerColour_SetConfigChangedCallback(LuaFunction function)
```
Sets a callback firing when user changes the config for player colour

## render (1 functions)

### `render_viewport_toggle`
```lua
render_viewport_toggle()
```
Disable rendering and render update

## RenderStats (9 functions)

### `RenderStats_Disable`
```lua
RenderStats_Disable()
```
Disable collecting and displaying render stats

### `RenderStats_DumpToLogFile`
```lua
RenderStats_DumpToLogFile()
```
Output the render stats to a CSV LogFile for viewing

### `RenderStats_Enable`
```lua
RenderStats_Enable()
```
Enable collecting and displaying render stats

### `RenderStats_SetUpdateTime`
```lua
RenderStats_SetUpdateTime(Real time)
```
Set the render stats refresh update interval (seconds)

### `RenderStats_SortInstances`
```lua
RenderStats_SortInstances()
```
Sort render stats by model instances (descending sort)

### `RenderStats_SortRenderCalls`
```lua
RenderStats_SortRenderCalls()
```
Sort render stats by render calls (descending sort)

### `RenderStats_SortShaderChanges`
```lua
RenderStats_SortShaderChanges()
```
Sort render stats by shader changes (descending sort)

### `RenderStats_SortTris`
```lua
RenderStats_SortTris()
```
Sort render stats by mesh triangles (descending sort)

### `RenderStats_Toggle`
```lua
RenderStats_Toggle()
```
Toggle collecting and displaying render stats

## ResourceContainer (3 functions)

### `ResourceContainer_ClearCache`
```lua
ResourceContainer_ClearCache(String cacheName)
```
Cleanup resources in cache. Only for debug purposes, not in RTM.

### `ResourceContainer_CreateCache`
```lua
ResourceContainer_CreateCache(String cacheName, Integer cacheSize)
```
Create a cache to load resources into giving its name and number of resources to hold

### `ResourceContainer_LogRefs`
```lua
ResourceContainer_LogRefs()
```
Log resource references to log. Only for debug purposes, not in RTM.

## RulesProfiler (5 functions)

### `RulesProfiler_Activate`
```lua
RulesProfiler_Activate(Boolean on)
```
Activate the scar RulesProfiler

### `RulesProfiler_Enable`
```lua
RulesProfiler_Enable(Boolean on)
```
Enable the scar RulesProfiler so it runs in the background. Call this before RulesProfiler_Activate

### `RulesProfiler_IsActive`
```lua
RulesProfiler_IsActive()
```
Returns true if the scar RulesProfiler is active

### `RulesProfiler_ResetTypeFilter`
```lua
RulesProfiler_ResetTypeFilter()
```
Don't filter the RulesProfiler displayed rules.

### `RulesProfiler_SetTypeFilter`
```lua
RulesProfiler_SetTypeFilter(String filter)
```
Filter the RulesProfiler to filter displayed rules to given type. E.g., "SCAR", "AI"

## SBP (3 functions)

### `SBP_Exists`
```lua
SBP_Exists(String pbgShortname)
```
Returns true if a squad blueprint exists with the given name.

### `SBP_GetFirstEBP`
```lua
SBP_GetFirstEBP(ScarSquadPBG sbp)
```
Get the first entity blueprint property bag in a provided squad blueprint property bag.

### `SBP_IsOfRace`
```lua
SBP_IsOfRace(String pbgShortname, ScarRacePBG race)
```
Returns whether the squad blueprint is of specified race

## Scar (10 functions)

### `Scar_AddInit`
```lua
Scar_AddInit(LuaFunction f)
```
Register an init function with the scar system.

### `Scar_DebugCheatMenuExecute`
```lua
Scar_DebugCheatMenuExecute(String command)
```
execute command string in cheat menu domain. Will only work if dev mode is enabled! (it's OFF by default in RTM builds)

### `Scar_DebugConsoleExecute`
```lua
Scar_DebugConsoleExecute(String command)
```
execute console command string. Will only work if dev mode is enabled! (it's OFF by default in RTM builds)

### `Scar_DrawMarkers`
```lua
Scar_DrawMarkers()
```
Toggle drawing debug info for scar markers

### `Scar_GroupInfo`
```lua
Scar_GroupInfo()
```
Toggle mouse over debug info on which group the entity belongs to

### `Scar_GroupList`
```lua
Scar_GroupList()
```
Toggle a list of all egroups and sgroups in the game

### `Scar_InitComplete`
```lua
Scar_InitComplete()
```
Lets lua tell the game when it has finished initializing

### `Scar_InitExists`
```lua
Scar_InitExists(LuaFunction f)
```
Returns true if an init function exists

### `Scar_Reload`
```lua
Scar_Reload()
```
Reload all scar scripts

### `Scar_RemoveInit`
```lua
Scar_RemoveInit(LuaFunction f)
```
Unregister an init function that was registered from Scar_AddInit

## scartype (2 functions)

### `scartype_enum_tostring`
```lua
scartype_enum_tostring(StackVar v)
```
Returns a string representing the scartype when passed a scartype enum value

### `scartype_tostring`
```lua
scartype_tostring(StackVar v)
```
Returns a string representing the scartype

## Setup (6 functions)

### `Setup_GetSlotOptions`
```lua
Setup_GetSlotOptions(StackVarTable outOptions, Integer playerIndex)
```
Fill table with slot options for the specified player - schema is loaded from .win file

### `Setup_GetWinConditionOptions`
```lua
Setup_GetWinConditionOptions(StackVarTable outOptions)
```
Fill table with win condition options - schema is loaded from .win file

### `Setup_SetPlayerName`
```lua
Setup_SetPlayerName(PlayerID player, String name)
```
Set the UI name of a given player.

### `Setup_SetPlayerRace`
```lua
Setup_SetPlayerRace(PlayerID player, ScarRacePBG racePBG)
```
Set the race for a given player.  Use World_GetRaceBlueprint() to get the race id from the ME name.

### `Setup_SetPlayerStartingPosition`
```lua
Setup_SetPlayerStartingPosition(PlayerID player, Position pos)
```
Set the starting position of a given player.

### `Setup_SetPlayerTeam`
```lua
Setup_SetPlayerTeam(PlayerID p, Integer team_id)
```
Put a player in a team. Use TEAM_NEUTRAL as the team_id to set the player as neutral

## SGroup (33 functions)

### `SGroup_Add`
```lua
SGroup_Add(SGroupID group, SquadID squadron)
```
Adds an squadron to the end of a group if the group doesn't already have it.

### `SGroup_AddGroup`
```lua
SGroup_AddGroup(SGroupID group, SGroupID grouptoadd)
```
Same as EGroup_AddGroup.  Note: You cannot mix squad groups and entity groups.

### `SGroup_CalculateClusterSeparation`
```lua
SGroup_CalculateClusterSeparation(SGroupID sgroup, Boolean spawnedOnly, Integer numClusters)
```
Try group the given list of squads into clusters and returns the average distance between these clusters.  Returns -1 if any error occurs.

### `SGroup_Clear`
```lua
SGroup_Clear(SGroupID sgroup)
```
Removes all entities from a group.

### `SGroup_ClearPostureSuggestion`
```lua
SGroup_ClearPostureSuggestion(SGroupID sgroup)
```
Clears any previous posture suggestions made to a squad

### `SGroup_Compare`
```lua
SGroup_Compare(SGroupID group1, SGroupID group2)
```
Returns true if the contents of the two groups are equal. Order of the entities does not matter.

### `SGroup_ContainsSGroup`
```lua
SGroup_ContainsSGroup(SGroupID group1, SGroupID group2, Boolean all)
```
Returns true if SGroup1 contains ANY or ALL of SGroup2

### `SGroup_ContainsSquad`
```lua
SGroup_ContainsSquad(SGroupID group, Integer SquadID, Boolean includeDespawned)
```
Returns true if SGroup contains a particular SquadID

### `SGroup_Count`
```lua
SGroup_Count(SGroupID sgroup)
```
Returns the total number of spawned and despawned squads in a group.

### `SGroup_CountAlliedSquads`
```lua
SGroup_CountAlliedSquads(SGroupID group, PlayerID player)
```
Returns the number of squads within an Sgroup that match an alliance with the player passed in

### `SGroup_CountDeSpawned`
```lua
SGroup_CountDeSpawned(SGroupID sgroup)
```
Returns the number of despawned squads in a group.

### `SGroup_CountEnemySquads`
```lua
SGroup_CountEnemySquads(SGroupID group, PlayerID player)
```
Returns the number of squads within an Sgroup that match an alliance with the player passed in

### `SGroup_CountSpawned`
```lua
SGroup_CountSpawned(SGroupID sgroup)
```
Returns the number of spawned squads in a group.

### `SGroup_Create`
```lua
SGroup_Create(String name)
```
Returns a new squadron group with the given name.

### `SGroup_CreateUniqueWithPrefix`
```lua
SGroup_CreateUniqueWithPrefix(String prefix)
```
Returns a new squad group with an autogenerated unique name, optionally prefixed by the string passed in.

### `SGroup_Destroy`
```lua
SGroup_Destroy(SGroupID sgroup)
```
Manually destroy a group that you don't need anymore.

### `SGroup_Exists`
```lua
SGroup_Exists(String name)
```
Returns true if the squad group with the given name exists

### `SGroup_FacePosition`
```lua
SGroup_FacePosition(SGroupID sgroup, Position pos)
```
Works like Squad_FacePosition.  All Squads will face the same direction, with the squad the closest to the center determining the direction.

### `SGroup_ForEach`
```lua
SGroup_ForEach(SGroupID sgroup, StackVarFunction f)
```
Call a lua function for each item in a group. Function will recieve (groupid, itemindex, itemid) and should return true to break or false to continue.

### `SGroup_ForEachAllOrAny`
```lua
SGroup_ForEachAllOrAny(SGroupID sgroup, Boolean all, StackVarFunction f)
```
Call a lua function for each item in a group. Function will receive (groupid, itemindex, itemid) and should return a bool.

### `SGroup_ForEachAllOrAnyEx`
```lua
SGroup_ForEachAllOrAnyEx(SGroupID sgroup, Boolean all, StackVarFunction f, Boolean spawned, Boolean despawned)
```
Same as SGroup_ForEachAllOrAny except you have a choice to iterate over spawned squads, despawned squads, or both.

### `SGroup_ForEachEx`
```lua
SGroup_ForEachEx(SGroupID sgroup, StackVarFunction f, Boolean spawned, Boolean despawned)
```
Same as SGroup_ForEach except you have a choice to iterate over spawned squads, despawned squads, or both.

### `SGroup_FromName`
```lua
SGroup_FromName(String name)
```
Find an squadron group with a given name.

### `SGroup_GetDeSpawnedSquadAt`
```lua
SGroup_GetDeSpawnedSquadAt(SGroupID group, Integer int)
```
Returns the despawned squad at a certain position in the group.

### `SGroup_GetName`
```lua
SGroup_GetName(SGroupID sgroup)
```
Returns the name of a given squad group.

### `SGroup_GetPosition`
```lua
SGroup_GetPosition(SGroupID group)
```
Returns the center position of a squad group.

### `SGroup_GetSpawnedSquadAt`
```lua
SGroup_GetSpawnedSquadAt(SGroupID group, Integer int)
```
Returns the spawned squad at a certain position in the group.

### `SGroup_GetSquadAt`
```lua
SGroup_GetSquadAt(SGroupID group, Integer int)
```
Returns the squad at a certain position in the group.

### `SGroup_Intersection`
```lua
SGroup_Intersection(SGroupID group, SGroupID grouptointersect)
```
Same as EGroup_Intersection. Note: You cannot mix squad groups and entity groups.

### `SGroup_IsValid`
```lua
SGroup_IsValid(Integer sgroupID)
```
Check to see if an sgroup still exists without needing the name.

### `SGroup_Remove`
```lua
SGroup_Remove(SGroupID group, SquadID squadron)
```
Removes an squadron from a group.

### `SGroup_SnapFacePosition`
```lua
SGroup_SnapFacePosition(SGroupID sgroup, Position pos)
```
Works like SGroup_FacePosition except with no interpolation.  All Squads will face the same direction, with the squad the closest to the center determining the direction.

### `SGroup_SuggestPosture`
```lua
SGroup_SuggestPosture(SGroupID sgroup, Integer posture, Real duration)
```
Suggests a posture to an SGroup, lasting the passed duration

## ShaderStats (7 functions)

### `ShaderStats_Disable`
```lua
ShaderStats_Disable()
```
Disable collecting and displaying render stats

### `ShaderStats_DumpToLogFile`
```lua
ShaderStats_DumpToLogFile()
```
Output the render stats to a CSV LogFile for viewing

### `ShaderStats_Enable`
```lua
ShaderStats_Enable()
```
Enable collecting and displaying render stats

### `ShaderStats_SetUpdateTime`
```lua
ShaderStats_SetUpdateTime(Real time)
```
Set the render stats refresh update interval (seconds)

### `ShaderStats_SortPixelCount`
```lua
ShaderStats_SortPixelCount()
```
Sort render stats by model instances (descending sort)

### `ShaderStats_SortShaderNames`
```lua
ShaderStats_SortShaderNames()
```
Sort render stats by model instances (descending sort)

### `ShaderStats_Toggle`
```lua
ShaderStats_Toggle()
```
Toggle collecting and displaying render stats

## Sim (24 functions)

### `Sim_CheckRequirements`
```lua
Sim_CheckRequirements()
```
Toggle check requirements information

### `Sim_DebugDrawSimTick`
```lua
Sim_DebugDrawSimTick()
```
Draw the current sim tick

### `Sim_DrawAttention`
```lua
Sim_DrawAttention()
```
Toggle drawing debug info for the attention system

### `Sim_DrawEntityCrusherOBB`
```lua
Sim_DrawEntityCrusherOBB()
```
Toggle the crush OBB

### `Sim_DrawEntityExtensions`
```lua
Sim_DrawEntityExtensions()
```
Toggle entity information

### `Sim_DrawEntityStateMove`
```lua
Sim_DrawEntityStateMove()
```
Toggle entity move state debug drawing

### `Sim_EntityAbility`
```lua
Sim_EntityAbility()
```
Toggle a list of all active abilities on the entity

### `Sim_EntityDelay`
```lua
Sim_EntityDelay()
```
Draw the per-entity decision delay if there is one

### `Sim_EntityDrawPosture`
```lua
Sim_EntityDrawPosture()
```
Toggle posture info text for selected entities

### `Sim_EntityHistory`
```lua
Sim_EntityHistory()
```
Toggle a list of all active modifiers on the entity

### `Sim_EntityInfo`
```lua
Sim_EntityInfo()
```
Toggle entity information

### `Sim_EntityModifier`
```lua
Sim_EntityModifier()
```
Toggle a list of all active modifiers on the entity

### `Sim_EntityOBB`
```lua
Sim_EntityOBB()
```
Draw the OBBs for the entity

### `Sim_EntityOOCTarget`
```lua
Sim_EntityOOCTarget()
```
Draw OOC target debug info

### `Sim_EntityStateTreeCommands`
```lua
Sim_EntityStateTreeCommands()
```
Toggle visualization of entity state tree commands

### `Sim_EntityUpgrades`
```lua
Sim_EntityUpgrades()
```
Toggle a list of all completed upgrades on the entity.

### `Sim_GetDrawMarketInfo`
```lua
Sim_GetDrawMarketInfo()
```
Is the Market info currently being drawn?

### `Sim_PlayerInfo`
```lua
Sim_PlayerInfo()
```
Toggle a list of all active player abilities

### `Sim_PlayerModifiers`
```lua
Sim_PlayerModifiers()
```
Toggle a list of all active player modifiers

### `Sim_SetDrawMarketInfo`
```lua
Sim_SetDrawMarketInfo(Boolean bEnable)
```
Set/clear drawing of the market info.

### `Sim_ShotBlockers`
```lua
Sim_ShotBlockers()
```
Toggle simulation boxes for shot blockers only

### `Sim_SimBox`
```lua
Sim_SimBox()
```
Toggle simulation boxes for entities

### `Sim_SquadHistory`
```lua
Sim_SquadHistory()
```
Toggle a list of all active modifiers on the entity

### `Sim_SquadInfo`
```lua
Sim_SquadInfo()
```
Toggle squad information

## SitRep (2 functions)

### `SitRep_PlayMovie`
```lua
SitRep_PlayMovie(String url)
```
Play the specified movie.

### `SitRep_StopMovie`
```lua
SitRep_StopMovie()
```
Stop the currently playing movie.

## Sound (19 functions)

### `Sound_Debug_ShowAudioRegions`
```lua
Sound_Debug_ShowAudioRegions(Boolean enable)
```
Toggles the display of the terrain audio environment zones on/off.

### `Sound_ForceMusicEnabled`
```lua
Sound_ForceMusicEnabled()
```
for the cheat menu

### `Sound_ForceSetMinimumMusicCombatIntensity`
```lua
Sound_ForceSetMinimumMusicCombatIntensity(Real combatIntensity, Real durationSeconds)
```
Force set the combat intensity to be at least combatIntensity for a duration.

### `Sound_ForceSilenceEnabled`
```lua
Sound_ForceSilenceEnabled()
```
for the cheat menu

### `Sound_IsPlaying`
```lua
Sound_IsPlaying(Integer handle)
```
Returns true if the sound associated with the handle is currently playing.

### `Sound_MusicStop`
```lua
Sound_MusicStop()
```
stops the music immediately and go into silence.

### `Sound_Play2D`
```lua
Sound_Play2D(String eventName)
```
Plays a 2D sound. Returns a handle to the sound event.

### `Sound_Play3D`
```lua
Sound_Play3D(String eventName, EntityID actor)
```
Plays a 3D sound on the entity. Returns a handle to the sound event.

### `Sound_PlaySpeech`
```lua
Sound_PlaySpeech(String eventName, Integer eventArgs)
```
Play a speech event based on the local player's race.

### `Sound_PlaySpeechForPlayer`
```lua
Sound_PlaySpeechForPlayer(PlayerID player, String eventName, Integer eventArgs)
```
Play a speech event based on a player's race.

### `Sound_PostEvent`
```lua
Sound_PostEvent(String eventName, Integer handle)
```
Posts an event on an already playing sound. Returns a handle to the new sound event.

### `Sound_SetForceMusic`
```lua
Sound_SetForceMusic(Boolean value)
```
tells the music system if it should be trying to enter/stay in the playing music state

### `Sound_SetForceSilence`
```lua
Sound_SetForceSilence(Boolean value)
```
tells the music system if it should be trying to enter/stay in the silent state

### `Sound_SetMinimumMusicCombatIntensity`
```lua
Sound_SetMinimumMusicCombatIntensity(Real combatIntensity, Real durationSeconds)
```
Set the target combat intensity to at least the value of value combatIntensity for a duration.

### `Sound_SetMusicIntensityScaling`
```lua
Sound_SetMusicIntensityScaling(Real scale)
```
sets the scaling multiplier for the music intensity value

### `Sound_SetMusicRaceCode`
```lua
Sound_SetMusicRaceCode(String raceCode)
```
sets the race rtpc for controlling what race's music gets played

### `Sound_SetScriptedMusicDuration`
```lua
Sound_SetScriptedMusicDuration(Real durationSecs)
```
Prevents the music system from automatically switching between layers and stopping for the duration.

### `Sound_StartMusicOutro`
```lua
Sound_StartMusicOutro(String outroEvent)
```
stops the music immediately and go into silence.

### `Sound_Stop`
```lua
Sound_Stop(Integer handle)
```
Stops sound associated with the handle.

## Splat (3 functions)

### `Splat_Create`
```lua
Splat_Create(String splatName, Position position, Real xScale, Real zScale, Real rotationDegrees, Integer r, Integer g, Integer b, Integer a, Boolean mirrorX, Boolean mirrorZ)
```
Add a splat to the terrain. Returns a unique decal id allow for future removal via Splat_Destroy

### `Splat_Destroy`
```lua
Splat_Destroy(TerrainSplatObject* handle)
```
Destroy a splat by unique id

### `Splat_GetInvalidID`
```lua
Splat_GetInvalidID()
```
Get the Splat ID that represents an invalid splat (useful to check if creation failed)

## Squad (201 functions)

### `Squad_AddAbility`
```lua
Squad_AddAbility(SquadID squad, ScarAbilityPBG ability)
```
Allows the squad to use this ability

### `Squad_AddAllResources`
```lua
Squad_AddAllResources(SquadID squad, Real amount)
```
Add resources of all types to the specified squad by the specified amount, specifically to the SquadResourceExt.

### `Squad_AddSlotItemToDropOnDeath`
```lua
Squad_AddSlotItemToDropOnDeath(SquadID squad, ScarSlotItemPBG pbg, Real dropChance, Boolean exclusive)
```
Add to the list of slot items to drop when this squad is wiped out

### `Squad_AdjustAbilityCooldown`
```lua
Squad_AdjustAbilityCooldown(SquadID squad, Integer tickAmount)
```
Advance ability cooldown

### `Squad_CanAttackEntity`
```lua
Squad_CanAttackEntity(SquadID attacker, EntityID target, Boolean checkFOW, Boolean checkVis)
```
Check if squad can attack target

### `Squad_CanCaptureStrategicPoint`
```lua
Squad_CanCaptureStrategicPoint(SquadID squad, EntityID entity)
```
Returns true if squad can capture stategic point

### `Squad_CanCaptureTeamWeapon`
```lua
Squad_CanCaptureTeamWeapon(SquadID pSquad, EntityID pEntity)
```
True if the squad can capture the entity sync weapon

### `Squad_CanCastAbilityOnEntity`
```lua
Squad_CanCastAbilityOnEntity(SquadID castingSquad, ScarAbilityPBG abilityPBG, EntityID targetEntity)
```
Test whether a squad can be ordered to do this ability on the target squad

### `Squad_CanCastAbilityOnPosition`
```lua
Squad_CanCastAbilityOnPosition(SquadID castingSquad, ScarAbilityPBG abilityPBG, Position targetPos)
```
Test whether a squad can be ordered to do this ability on the target squad

### `Squad_CanCastAbilityOnSquad`
```lua
Squad_CanCastAbilityOnSquad(SquadID castingSquad, ScarAbilityPBG abilityPBG, SquadID targetSquad)
```
Test whether a squad can be ordered to do this ability on the target squad

### `Squad_CancelProductionQueueItem`
```lua
Squad_CancelProductionQueueItem(SquadID squad, Integer index)
```
Cancels an item in a production queue.  Index 0 is the currently producing item.

### `Squad_CanHold`
```lua
Squad_CanHold(SquadID squad)
```
Checks whether a squad can hold any squad

### `Squad_CanInstantReinforceNow`
```lua
Squad_CanInstantReinforceNow(SquadID squad)
```
Returns true if the squad is available to be reinforced

### `Squad_CanLoadSquad`
```lua
Squad_CanLoadSquad(SquadID squad, SquadID loadthis, Boolean assumeEmpty, Boolean assumeVisible)
```
Checks whether a squad can load another squad

### `Squad_CanPickupSlotItem`
```lua
Squad_CanPickupSlotItem(SquadID pSquad, EntityID pEntity)
```
True if the squad can pickup the entity slot item

### `Squad_CanRecrew`
```lua
Squad_CanRecrew(SquadID pSquad, EntityID pEntity)
```
True if the squad can recrew the entity

### `Squad_CanSeeEntity`
```lua
Squad_CanSeeEntity(SquadID squad, EntityID entity)
```
Returns true if the distance between a target entity and the source squad is less than it squad's sight distance.  There is no LOS or FOW check.

### `Squad_CanSeeSquad`
```lua
Squad_CanSeeSquad(SquadID squad, SquadID target)
```
Returns true if the distance between a target squad and the source squad is less than it squad's sight distance.  There is no LOS or FOW check.

### `Squad_CanTargetEntity`
```lua
Squad_CanTargetEntity(Squad& squad, Entity& target, Boolean checkFOW)
```
Check if a squad can target and attack a given entity.

### `Squad_CanTargetSquad`
```lua
Squad_CanTargetSquad(Squad& squad, Squad& target, Boolean checkFOW)
```
Check if a squad can target and attack at least one entity in the given target squad.

### `Squad_ClearPostureSuggestion`
```lua
Squad_ClearPostureSuggestion(SquadID squad)
```
Clears any previous posture suggestions made to a squad

### `Squad_ClearStateModelEnumTableTarget`
```lua
Squad_ClearStateModelEnumTableTarget(SquadID squad, String key, Integer tableRowIndex)
```
Clears a TargetHandle value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_ClearStateModelTarget`
```lua
Squad_ClearStateModelTarget(SquadID squad, String key)
```
Clears a TargetHandle value in the squad's state model corresponding to the given key.

### `Squad_CompleteUpgrade`
```lua
Squad_CompleteUpgrade(SquadID pSquad, ScarUpgradePBG upgradePBG)
```
Instantly adds an upgrade to a given squad

### `Squad_Count`
```lua
Squad_Count(SquadID squad)
```
Returns the number of units currently in a squad (spawned AND despawned!!)

### `Squad_CreateAndSpawnToward`
```lua
Squad_CreateAndSpawnToward(ScarSquadPBG sbp, PlayerID player, Integer loadoutCount, Position pos, Position toward)
```
Create a squad, spawn it and assign it to a player.

### `Squad_DeSpawn`
```lua
Squad_DeSpawn(SquadID squad)
```
Despawn the entire squad at its current position.

### `Squad_Destroy`
```lua
Squad_Destroy(SquadID squad)
```
Remove an squad from the world and destroy it.

### `Squad_EnableProductionQueue`
```lua
Squad_EnableProductionQueue(SquadID squad, Boolean enable)
```
Sets whether a squad can produce anything (including upgrades)

### `Squad_EnableSurprise`
```lua
Squad_EnableSurprise(SquadID squad, Boolean enable)
```
Enables or disables the surprise feature on thie given squad

### `Squad_ExtensionCount`
```lua
Squad_ExtensionCount()
```
Returns total squad extension count.

### `Squad_ExtensionEnabled`
```lua
Squad_ExtensionEnabled(SquadID pSquad, ComponentDependencyIndex extID)
```
Returns true if the squad has the specific extension enabled.

### `Squad_ExtensionName`
```lua
Squad_ExtensionName(SquadID pSquad, ComponentDependencyIndex extID)
```
Returns a string name of the given extension on the squad.

### `Squad_FacePosition`
```lua
Squad_FacePosition(SquadID squad, Position pos)
```
Set the rotation of all units in a squad to face the position.

### `Squad_FaceSquad`
```lua
Squad_FaceSquad(SquadID squad1, SquadID squad2)
```
Get 2 squads to face each other. This function works on spawned squads only.

### `Squad_FindCover`
```lua
Squad_FindCover(SquadID squad, Position pos, Real coverSearchRadius)
```
Tries to find cover within a certain radius of a position. If no cover is found, it returns the position used for the search.

### `Squad_FindCoverCompareCurrent`
```lua
Squad_FindCoverCompareCurrent(SquadID squad, Position pos, Real coverSearchRadius, Real maxPathDistanceFromGoal, Boolean compareToCurrentCover)
```
Tries to find cover within a certain radius of a position, traveling a max distance to get there, and possibly comparing against current position's cover. If no cover is found, it returns the position used for the search.

### `Squad_FromID`
```lua
Squad_FromID(Integer id)
```
Get a squad from a mission editor ID.

### `Squad_GetActiveUpgrades`
```lua
Squad_GetActiveUpgrades(Squad& squad)
```
Returns all active upgrades this squad has.

### `Squad_GetAttackTargets`
```lua
Squad_GetAttackTargets(SquadID squad, SGroupID sgroup)
```
Find the squad member current or forced targets. The sgroup is cleared, and any attack target squads found are added to the sgroup. Entity targets like buildings are ignored.

### `Squad_GetBlueprint`
```lua
Squad_GetBlueprint(SquadID squad)
```
Returns the squad blueprint of the squad (from the attribute editor)

### `Squad_GetDestination`
```lua
Squad_GetDestination(SquadID squad)
```
Returns the squad's destination, if it's moving. IMPORTANT: you must only call this function if Squad_HasDestination has returned true.

### `Squad_GetFirstEntity`
```lua
Squad_GetFirstEntity(SquadID squad)
```
Get the first entity (at index 0) in a squad.

### `Squad_GetHeading`
```lua
Squad_GetHeading(SquadID squad)
```
Returns the average heading of the spawned units in the squad. The heading is currently a lua table with three entries (x, y, z)

### `Squad_GetHealth`
```lua
Squad_GetHealth(SquadID squad)
```
Returns the current health of a squad.

### `Squad_GetHealthMax`
```lua
Squad_GetHealthMax(SquadID squad)
```
Returns the max health of the squad.

### `Squad_GetHealthPercentage`
```lua
Squad_GetHealthPercentage(SquadID squad, Boolean bIncludeBonuses)
```
Returns how much of an original squad's health is left, accounting for deaths (ex: a squad of 3 riflemen would be at 50% health, since they started with 6 members) Note: This is the same percentage that the UI uses.

### `Squad_GetHealthPercentageWithShields`
```lua
Squad_GetHealthPercentageWithShields(SquadID squad, Boolean includeBonuses)
```
Returns how much of the squad's health is left as a percentage.

### `Squad_GetHoldEntity`
```lua
Squad_GetHoldEntity(SquadID squad)
```
Get which building (entity) is the squad garrisoned

### `Squad_GetHoldSquad`
```lua
Squad_GetHoldSquad(SquadID squad)
```
Get which vehicle (squad) is the squad garrisoned

### `Squad_GetID`
```lua
Squad_GetID(SquadID squad)
```
Returns an integer containing the unqiue squad ID for this squad.

### `Squad_GetInternalAIEncounterPtr`
```lua
Squad_GetInternalAIEncounterPtr(SquadID squad)
```
returns the Encounter that controls the Squad

### `Squad_GetInvulnerableEntityCount`
```lua
Squad_GetInvulnerableEntityCount(SquadID squad)
```
Returns the number of invulnerable member

### `Squad_GetInvulnerableMinCap`
```lua
Squad_GetInvulnerableMinCap(SquadID squad)
```
Returns squad health min cap or the highest invulnerable min cap percentage from members of the squad.

### `Squad_GetLastAttacker`
```lua
Squad_GetLastAttacker(SquadID squad, SGroupID sgroup)
```
Find the last squad attacker on this squad. If found, the squad is added to the sgroup

### `Squad_GetLastAttackers`
```lua
Squad_GetLastAttackers(SquadID squad, SGroupID group, Real timeSeconds)
```
Find the squad attackers on this squad from the last seconds specified. The sgroup is cleared, then any squads found are added to the sgroup. Building attackers are ignored.

### `Squad_GetLastEntityAttacker`
```lua
Squad_GetLastEntityAttacker(SquadID squad, EGroupID egroup)
```
Find the last entity attacker on this squad. If found, the entity added to egroup

### `Squad_GetMax`
```lua
Squad_GetMax(SquadID squad)
```
Returns the max number of units allowed in the squad

### `Squad_GetMaxEntityDropOffDistance`
```lua
Squad_GetMaxEntityDropOffDistance(SquadID targetSquad)
```
Returns the sum of all entities in a squad's resourceDropOffDistance state model value if it exists and the entities have a state model ext.  Otherwise it will return 0.0f

### `Squad_GetMinArmor`
```lua
Squad_GetMinArmor(SquadID squad)
```
Returns the current minimum armor of a squad.

### `Squad_GetNumSlotItem`
```lua
Squad_GetNumSlotItem(SquadID squad, ScarSlotItemPBG pbg)
```
Get the number of slot items with the same ID that the squad has

### `Squad_GetPlayerOwner`
```lua
Squad_GetPlayerOwner(SquadID squad)
```
Returns the Player owner of the given squad. Squad MUST NOT be owned by the world.

### `Squad_GetPosition`
```lua
Squad_GetPosition(SquadID squad)
```
Returns the average position of the spawned units in the squad. The position is currently a lua table with three entries (x, y, z)

### `Squad_GetPositionDeSpawned`
```lua
Squad_GetPositionDeSpawned(SquadID squad)
```
Returns the average position of the despawned AND spawned units in the squad.

### `Squad_GetProductionQueueItem`
```lua
Squad_GetProductionQueueItem(SquadID squad, Integer index)
```
Returns the blueprint for a production queue item with index.

### `Squad_GetProductionQueueItemType`
```lua
Squad_GetProductionQueueItemType(SquadID squad, Integer index)
```
Returns the production type (PITEM_Upgrade, PITEM_Spawn, PITEM_SquadUpgrade, PITEM_SquadReinforce, PITEM_PlayerUpgrade) for a production queue item with index.

### `Squad_GetProductionQueueSize`
```lua
Squad_GetProductionQueueSize(SquadID squad)
```
Returns the number of items in the squad's production queue.

### `Squad_GetRace`
```lua
Squad_GetRace(SquadID squad)
```
Returns the race property bag group for the given squad

### `Squad_GetShieldPercentage`
```lua
Squad_GetShieldPercentage(SquadID squad)
```
Returns how much of the squad's shield is left as a percentage.

### `Squad_GetSlotItemAt`
```lua
Squad_GetSlotItemAt(SquadID squad, Integer index)
```
Returns the ID of the slot item. Use Squad_GetSlotItemCount to determine how many slot items the squad has. The first index is 1

### `Squad_GetSlotItemCount`
```lua
Squad_GetSlotItemCount(SquadID squad)
```
Returns how many slot items this squad has

### `Squad_GetSquadDoingDisableOnSquad`
```lua
Squad_GetSquadDoingDisableOnSquad(SquadID pSquad)
```
returns the Squad that sent the passed squad in a disable state

### `Squad_GetSquadsHeld`
```lua
Squad_GetSquadsHeld(SquadID squad, SGroupID sgroup)
```
Clear the sgroup, then add all squads held by 'squad' to it

### `Squad_GetStateModelBool`
```lua
Squad_GetStateModelBool(SquadID squad, String key)
```
Returns a boolean value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelEntityTarget`
```lua
Squad_GetStateModelEntityTarget(SquadID squad, String key)
```
Returns an Entity value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelEnumTableBool`
```lua
Squad_GetStateModelEnumTableBool(SquadID squad, String key, Integer tableRowIndex)
```
Returns a boolean value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTableEntityTarget`
```lua
Squad_GetStateModelEnumTableEntityTarget(SquadID squad, String key, Integer tableRowIndex)
```
Returns an Entity value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTableFloat`
```lua
Squad_GetStateModelEnumTableFloat(SquadID squad, String key, Integer tableRowIndex)
```
Returns a float value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTableInt`
```lua
Squad_GetStateModelEnumTableInt(SquadID squad, String key, Integer tableRowIndex)
```
Returns an integer value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTablePlayerTarget`
```lua
Squad_GetStateModelEnumTablePlayerTarget(SquadID squad, String key, Integer tableRowIndex)
```
Returns a Player value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTableSquadTarget`
```lua
Squad_GetStateModelEnumTableSquadTarget(SquadID squad, String key, Integer tableRowIndex)
```
Returns a Squad value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelEnumTableVector3f`
```lua
Squad_GetStateModelEnumTableVector3f(SquadID squad, String key, Integer tableRowIndex)
```
Returns a Vector3f value from the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_GetStateModelFloat`
```lua
Squad_GetStateModelFloat(SquadID squad, String key)
```
Returns a float value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelInt`
```lua
Squad_GetStateModelInt(SquadID squad, String key)
```
Returns an integer value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelPlayerTarget`
```lua
Squad_GetStateModelPlayerTarget(SquadID squad, String key)
```
Returns a Player value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelSquadTarget`
```lua
Squad_GetStateModelSquadTarget(SquadID squad, String key)
```
Returns a Squad value from the squad's state model corresponding to the given key.

### `Squad_GetStateModelVector3f`
```lua
Squad_GetStateModelVector3f(SquadID squad, String key)
```
Returns a Vector3f value from the squad's state model corresponding to the given key.

### `Squad_GetVehicleMobileDriverSquad`
```lua
Squad_GetVehicleMobileDriverSquad(SquadID pSquad)
```
Gets the mobile driver squad from a vehicle squad

### `Squad_GetVeterancy`
```lua
Squad_GetVeterancy(SquadID squad)
```
Get current squad veterancy

### `Squad_GetVeterancyRank`
```lua
Squad_GetVeterancyRank(SquadID squad)
```
Get current squad veterancy rank.

### `Squad_GiveSlotItem`
```lua
Squad_GiveSlotItem(SquadID squad, ScarSlotItemPBG pbg)
```
Gives a slot item to the squad. Can fail due to not enough slots left

### `Squad_HasAbility`
```lua
Squad_HasAbility(SquadID squad, ScarAbilityPBG ability)
```
Tests to see if a squad has an ability

### `Squad_HasAcceptedCommands`
```lua
Squad_HasAcceptedCommands(SquadID squad)
```
Returns true if the squad has an accepted command that it will try to perform next

### `Squad_HasActiveCommand`
```lua
Squad_HasActiveCommand(SquadID squad)
```
Returns true if there's an active command currently for the squad

### `Squad_HasBuilding`
```lua
Squad_HasBuilding(SquadID pSquad)
```
Returns true if the given squad has a building in it (includes team weapons)

### `Squad_HasDestination`
```lua
Squad_HasDestination(SquadID squad)
```
Returns whether this squad is moving and has a destination, it will not return true on the same tick that the move request is issued

### `Squad_HasEntityWithNInteractors`
```lua
Squad_HasEntityWithNInteractors(SquadID targetSquad, String interactionTypeName, Integer minAttachedCount)
```
Returns if squad contains an entity with at least minAttachedCount attached interactibles of interactionTypeName type

### `Squad_HasHeavyWeapon`
```lua
Squad_HasHeavyWeapon(SquadID pSquad)
```
Returns true if the given squad has a heavy weapon (non moving setup weapon)

### `Squad_HasInfantry`
```lua
Squad_HasInfantry(SquadID pSquad)
```
Returns true if the given squad has at least one infantry unit in it (includes team weapons)

### `Squad_HasProductionQueue`
```lua
Squad_HasProductionQueue(SquadID squad)
```
Returns true if a squad has a production queue.

### `Squad_HasSetupTeamWeapon`
```lua
Squad_HasSetupTeamWeapon(SquadID pSquad)
```
Returns true if the given squad has team weapon setup for attack

### `Squad_HasTeamWeapon`
```lua
Squad_HasTeamWeapon(SquadID pSquad)
```
Returns true if the given squad has a team weapon

### `Squad_HasUpgrade`
```lua
Squad_HasUpgrade(SquadID squad, ScarUpgradePBG pbg)
```
Return true if the squad has purchased the specified upgrade.

### `Squad_HasVehicle`
```lua
Squad_HasVehicle(SquadID pSquad)
```
Returns true if the given squad has a vehicle in it (includes team weapons)

### `Squad_HasWeaponHardpoint`
```lua
Squad_HasWeaponHardpoint(SquadID pSquad, String hardPointName)
```
Returns true if the given squad has at least one Entity who has the specified weapon hardpoint.

### `Squad_IncreaseVeterancy`
```lua
Squad_IncreaseVeterancy(SquadID squad, Real veterancy, Boolean silent, Boolean applyModifiers)
```
Increase current squad veterancy

### `Squad_IncreaseVeterancyRank`
```lua
Squad_IncreaseVeterancyRank(SquadID squad, Integer numranks, Boolean silent)
```
Increase current squad veterancy rank

### `Squad_InstantSetupTeamWeapon`
```lua
Squad_InstantSetupTeamWeapon(SquadID squad)
```
Stops current squads activity and instant setup the team weapon if they have one

### `Squad_IsAbilityActive_CS`
```lua
Squad_IsAbilityActive_CS(SquadID squad, ScarAbilityPBG pbg)
```
True if the ability is active

### `Squad_IsAlive`
```lua
Squad_IsAlive(SquadID squad)
```
Check if the squad is alive

### `Squad_IsAttacking`
```lua
Squad_IsAttacking(SquadID squad, Real time)
```
Returns true if any unit in the squad is attacking within the time

### `Squad_IsAttackMoving`
```lua
Squad_IsAttackMoving(SquadID squad)
```
Returns true if the squad is currently attack-moving.

### `Squad_IsCapturing`
```lua
Squad_IsCapturing(SquadID squad)
```
Returns true if the squad is currently capturing.

### `Squad_IsCasualty`
```lua
Squad_IsCasualty(SquadID squad)
```
Returns true if any spawned entity in the squad is a casualty

### `Squad_IsConstructing`
```lua
Squad_IsConstructing(SquadID squad)
```
Returns true if the squad is currently constructing.

### `Squad_IsDoingAbility`
```lua
Squad_IsDoingAbility(SquadID squad, ScarAbilityPBG pbg)
```
True if squad is currently performing the given ability

### `Squad_IsFemale`
```lua
Squad_IsFemale(SquadID squad)
```
Returns whether the passed in squad is female

### `Squad_IsGatheringResourceType`
```lua
Squad_IsGatheringResourceType(SquadID targetSquad, Integer type)
```
Returns if squad contains an entity that is performing a specific unit role

### `Squad_IsHoldingAny`
```lua
Squad_IsHoldingAny(SquadID squad)
```
Check if the squad has a hold on anything (use this on vehicles)

### `Squad_IsHoldingPosition`
```lua
Squad_IsHoldingPosition(SquadID squad)
```
Returns true if Squad is holding position.

### `Squad_IsIdle`
```lua
Squad_IsIdle(SquadID squad)
```
Returns true if the squad is idling

### `Squad_IsInAIEncounter`
```lua
Squad_IsInAIEncounter(SquadID squad)
```
returns true if the Squad is in an Encounter

### `Squad_IsInBackground`
```lua
Squad_IsInBackground(SquadID pSquad)
```
Returns whether or not the squad is in the background. Default returns false (if the squad is empty)

### `Squad_IsInHoldEntity`
```lua
Squad_IsInHoldEntity(SquadID squad)
```
Check if the squad is garrisoned in entity (building)

### `Squad_IsInHoldSquad`
```lua
Squad_IsInHoldSquad(SquadID squad)
```
Check if the squad is loaded in squad (vehicle

### `Squad_IsInMeleeCombat`
```lua
Squad_IsInMeleeCombat(SquadID pSquad)
```
Returns true if the squad is in melee combat

### `Squad_IsKnockedBack`
```lua
Squad_IsKnockedBack(SquadID squad)
```
True if the squad is currently being knocked back

### `Squad_IsMoving`
```lua
Squad_IsMoving(SquadID squad)
```
Returns true if any unit in the squad is currently moving

### `Squad_IsOfType`
```lua
Squad_IsOfType(SquadID squad, String type)
```
Determines if this squad is of the given type. Types are defined in squad_type_ext/squad_type_list

### `Squad_IsOnWalkableWall`
```lua
Squad_IsOnWalkableWall(SquadID squad, Boolean all)
```
Returns true if any entity of a squad (all=false) or the whole (all=true) squad is on walkable wall.

### `Squad_IsOwnedByPlayer`
```lua
Squad_IsOwnedByPlayer(SquadID squad, PlayerID player)
```
Returns true if the given squad is owned by the given player

### `Squad_IsReinforcing`
```lua
Squad_IsReinforcing(SquadID squad)
```
Returns true if the squad is currently reinforcing.  This function will return false if the squad does not have a reinforce ext.

### `Squad_IsRetreating`
```lua
Squad_IsRetreating(SquadID squad)
```
Returns true if the squad is retreating

### `Squad_IsSBPOfType`
```lua
Squad_IsSBPOfType(ScarSquadPBG sbp, String type)
```
Returns true if the given blueprint is of the given type. Types are defined in squad_type_ext/squad_type_list

### `Squad_IsSettingDemolitions`
```lua
Squad_IsSettingDemolitions(SquadID squad)
```
Returns true if the squad is currently placing charges.

### `Squad_IsSiege`
```lua
Squad_IsSiege(ScarSquadPBG pbg)
```
Returns true if the supplied squad pbg is a siege unit

### `Squad_IsStunned`
```lua
Squad_IsStunned(SquadID squad)
```
True if the squad is currently stunned

### `Squad_IsUnderAttack`
```lua
Squad_IsUnderAttack(SquadID squad, Real time)
```
Returns true if any unit in the squad is under attack within the time

### `Squad_IsUnderAttackByPlayer`
```lua
Squad_IsUnderAttackByPlayer(SquadID squad, PlayerID pAttackerOwner, Real time)
```
Returns true if squad is under attack by enemy from a particular player

### `Squad_IsUnderAttackFromDirection`
```lua
Squad_IsUnderAttackFromDirection(SquadID squad, Integer offset, Real timeSeconds)
```
Returns true if the squad was under attack from a certain direction (8 offset types, see ScarUtil.scar)

### `Squad_IsUpgrading`
```lua
Squad_IsUpgrading(SquadID squad, ScarUpgradePBG upgrade)
```
Returns true if the squad is currently upgrading something specific.

### `Squad_IsUpgradingAny`
```lua
Squad_IsUpgradingAny(SquadID squad)
```
Returns true if the squad is currently upgrading anything.

### `Squad_IsValid`
```lua
Squad_IsValid(Integer id)
```
Check if a squad with the given ID can be found in the world

### `Squad_Kill`
```lua
Squad_Kill(SquadID squad)
```
Kill whole squad.  Sets health to 0, and triggers death effects.

### `Squad_NumUpgradeComplete`
```lua
Squad_NumUpgradeComplete(SquadID squad, ScarUpgradePBG upgradePBG)
```
Returns the number of upgrades that this squad has.

### `Squad_Population`
```lua
Squad_Population(SquadID squad, CapType type)
```
get squad pop cost, use CT_Personnel, CT_Vehicle, CT_Medic for captype

### `Squad_Precache`
```lua
Squad_Precache(ScarSquadPBG sbp, Integer skinItemDefinitionID, PlayerID player, String resourceContainerCacheName, String source, String id)
```
Precache squad resources and listen for event GE_EntityPrecached that it is done

### `Squad_RemoveAbility`
```lua
Squad_RemoveAbility(SquadID squad, ScarAbilityPBG ability)
```
Removes an ability that was previously added by Squad_AddAbility. You cannot remove static abilities (from AE: squad_ability_ext)

### `Squad_RemoveSlotItemAt`
```lua
Squad_RemoveSlotItemAt(SquadID squad, Integer index, Boolean bInstantWeaponChange)
```
Removes a slot item from the squad.

### `Squad_RemoveStateModelListBool`
```lua
Squad_RemoveStateModelListBool(SquadID squad, String key, Boolean value)
```
Removes a boolean value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListEntityTarget`
```lua
Squad_RemoveStateModelListEntityTarget(SquadID squad, String key, EntityID value)
```
Removes an Entity TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListFloat`
```lua
Squad_RemoveStateModelListFloat(SquadID squad, String key, Real value)
```
Removes a float value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListInt`
```lua
Squad_RemoveStateModelListInt(SquadID squad, String key, Integer value)
```
Removes an integer value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListPlayerTarget`
```lua
Squad_RemoveStateModelListPlayerTarget(SquadID squad, String key, PlayerID value)
```
Removes a Player TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListSquadTarget`
```lua
Squad_RemoveStateModelListSquadTarget(SquadID squad, String key, SquadID value)
```
Removes a Squad TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_RemoveStateModelListVector3f`
```lua
Squad_RemoveStateModelListVector3f(SquadID squad, String key, Position value)
```
Removes a Vector3f value in the squad's state model list corresponding to the given key.

### `Squad_RemoveUpgrade`
```lua
Squad_RemoveUpgrade(SquadID squad, ScarUpgradePBG upgrade)
```
Removes an upgrade from a squad

### `Squad_RewardActionPoints`
```lua
Squad_RewardActionPoints(SquadID squad, Real actionPoint)
```
Give squad action points

### `Squad_SBPEntityAt`
```lua
Squad_SBPEntityAt(ScarSquadPBG sbp, Integer index)
```
ZERO-BASED get of entity blueprints out of squad blueprint

### `Squad_SBPGetMax`
```lua
Squad_SBPGetMax(ScarSquadPBG sbp)
```
Returns the max number of units allowed in the squad blueprint

### `Squad_SetBackground`
```lua
Squad_SetBackground(SquadID pSquad, Boolean isInBackground)
```
Sets the squad to be in the background or foreground. By default, all squads are in the foreground

### `Squad_SetExtEnabled`
```lua
Squad_SetExtEnabled(SquadID pSquad, String extID, Boolean enabled)
```
Enables or disables the squad's UI extension (which controls all UI elements related to the squad)

### `Squad_SetHealth`
```lua
Squad_SetHealth(SquadID squad, Real healthPercent)
```
Set the health of all units in a squad.  Health must be in range [0.0, 1.0]

### `Squad_SetInvulnerableEntityCount`
```lua
Squad_SetInvulnerableEntityCount(SquadID squad, Integer invEntityCount, Real resetTime)
```
Make a squad invulnerable to physical damage when number of members drop to or below specified count.

### `Squad_SetInvulnerableMinCap`
```lua
Squad_SetInvulnerableMinCap(SquadID squad, Real minHealthPercentage, Real resetTime)
```
Make a squad invulnerable to physical damage.

### `Squad_SetMoodMode`
```lua
Squad_SetMoodMode(SquadID squad, SquadCombatBehaviourMoodMode mood)
```
Set soldier mood mode.

### `Squad_SetMoveType`
```lua
Squad_SetMoveType(SquadID squad, ScarMoveTypePBG movetypePBG)
```
Sets the squad's move type

### `Squad_SetPlayerOwner`
```lua
Squad_SetPlayerOwner(SquadID squad, PlayerID owner)
```
Changes the owner of the given squad.

### `Squad_SetPosition`
```lua
Squad_SetPosition(SquadID squad, Position pos, Position positionFacingToward)
```
Moves the squad to a new position and snaps squad members onto grid cell centres.

### `Squad_SetPosition3D`
```lua
Squad_SetPosition3D(SquadID squad, Position pos, Position toward)
```
Moves the squad to an arbitrary new 3D position.

### `Squad_SetRecrewable`
```lua
Squad_SetRecrewable(SquadID squad, Boolean capturable)
```
Set entity inside the squad to be recrewable or not when it becomes abandoned

### `Squad_SetResource`
```lua
Squad_SetResource(SquadID squad, Integer resourceType, Real newAmount)
```
This function uses squad resources rather than entity resources. For awarding resources to units, it's best to use Entity_AddResource instead (located in luaentity.cpp).

### `Squad_SetStateModelBool`
```lua
Squad_SetStateModelBool(SquadID squad, String key, Boolean value)
```
Sets a boolean value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelEntityTarget`
```lua
Squad_SetStateModelEntityTarget(SquadID squad, String key, EntityID value)
```
Sets an Entity TargetHandle value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelEnumTableBool`
```lua
Squad_SetStateModelEnumTableBool(SquadID squad, String key, Integer tableRowIndex, Boolean value)
```
Sets a boolean value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTableEntityTarget`
```lua
Squad_SetStateModelEnumTableEntityTarget(SquadID squad, String key, Integer tableRowIndex, EntityID value)
```
Sets an Entity TargetHandle value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTableFloat`
```lua
Squad_SetStateModelEnumTableFloat(SquadID squad, String key, Integer tableRowIndex, Real value)
```
Sets a float value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTableInt`
```lua
Squad_SetStateModelEnumTableInt(SquadID squad, String key, Integer tableRowIndex, Integer value)
```
Sets an integer value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTablePlayerTarget`
```lua
Squad_SetStateModelEnumTablePlayerTarget(SquadID squad, String key, Integer tableRowIndex, PlayerID value)
```
Sets a Player TargetHandle value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTableSquadTarget`
```lua
Squad_SetStateModelEnumTableSquadTarget(SquadID squad, String key, Integer tableRowIndex, SquadID value)
```
Sets a Squad TargetHandle value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelEnumTableVector3f`
```lua
Squad_SetStateModelEnumTableVector3f(SquadID squad, String key, Integer tableRowIndex, Position value)
```
Sets a Vector3f value in the squad's state model corresponding to the given key and table row index (0 based).

### `Squad_SetStateModelFloat`
```lua
Squad_SetStateModelFloat(SquadID squad, String key, Real value)
```
Sets a float value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelInt`
```lua
Squad_SetStateModelInt(SquadID squad, String key, Integer value)
```
Sets an integer value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelListBool`
```lua
Squad_SetStateModelListBool(SquadID squad, String key, Boolean value, Boolean allowDuplicates)
```
Sets a boolean value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListEntityTarget`
```lua
Squad_SetStateModelListEntityTarget(SquadID squad, String key, EntityID value, Boolean allowDuplicates)
```
Sets an Entity TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListFloat`
```lua
Squad_SetStateModelListFloat(SquadID squad, String key, Real value, Boolean allowDuplicates)
```
Sets a float value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListInt`
```lua
Squad_SetStateModelListInt(SquadID squad, String key, Integer value, Boolean allowDuplicates)
```
Sets an integer value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListPlayerTarget`
```lua
Squad_SetStateModelListPlayerTarget(SquadID squad, String key, PlayerID value, Boolean allowDuplicates)
```
Sets a Player TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListSquadTarget`
```lua
Squad_SetStateModelListSquadTarget(SquadID squad, String key, SquadID value, Boolean allowDuplicates)
```
Sets a Squad TargetHandle value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelListVector3f`
```lua
Squad_SetStateModelListVector3f(SquadID squad, String key, Position value, Boolean allowDuplicates)
```
Sets a Vector3f value in the squad's state model list corresponding to the given key.

### `Squad_SetStateModelPlayerTarget`
```lua
Squad_SetStateModelPlayerTarget(SquadID squad, String key, PlayerID value)
```
Sets a Player TargetHandle value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelSquadTarget`
```lua
Squad_SetStateModelSquadTarget(SquadID squad, String key, SquadID value)
```
Sets a Squad TargetHandle value in the squad's state model corresponding to the given key.

### `Squad_SetStateModelVector3f`
```lua
Squad_SetStateModelVector3f(SquadID squad, String key, Position value)
```
Sets a Vector3f value in the squad's state model corresponding to the given key.

### `Squad_SetVeterancyDisplayVisibility`
```lua
Squad_SetVeterancyDisplayVisibility(SquadID squad, Boolean visible)
```
Turn on/off display of the unit portrait veterancy stars

### `Squad_SetWorldOwned`
```lua
Squad_SetWorldOwned(SquadID squad)
```
Makes a squad neutral

### `Squad_Spawn`
```lua
Squad_Spawn(SquadID squad, Position pos, String spawnType)
```
Spawn the entire squad at a give  n position

### `Squad_SpawnToward`
```lua
Squad_SpawnToward(SquadID squad, Position pos, Position toward, String spawnType)
```
Spawn the entire squad at a given position

### `Squad_Split`
```lua
Squad_Split(SquadID squad, Integer int)
```
Split the squad into 2. The new squad size is specified by the number passed in

### `Squad_StopAbility`
```lua
Squad_StopAbility(SquadID squad, ScarAbilityPBG ability, Boolean bIsEarlyExit)
```
Abruptly stops an active ability

### `Squad_SuggestPosture`
```lua
Squad_SuggestPosture(SquadID squad, Integer posture, Real duration)
```
Suggests a posture to a squad, lasting the passed duration

### `Squad_TryFindClosestFreePosition`
```lua
Squad_TryFindClosestFreePosition(SquadID squad, Position targetPosition)
```
Returns the closest free position to the target position for the squad

## SquadGroup (1 functions)

### `SquadGroup_CountSpawnedAndStatsInitialized`
```lua
SquadGroup_CountSpawnedAndStatsInitialized(SGroupID sgroup, PlayerID player)
```
iterates through an sgroup, returns count with AIStatsSquad

## StateTree (3 functions)

### `StateTree_QueueGlobalStateTreeEntity`
```lua
StateTree_QueueGlobalStateTreeEntity(Boolean keepAlive, String openingBranchName, EntityID entity)
```
Run a global state tree on an entity

### `StateTree_QueueGlobalStateTreePlayer`
```lua
StateTree_QueueGlobalStateTreePlayer(Boolean keepAlive, String openingBranchName, PlayerID player)
```
Run a global state tree on a player

### `StateTree_QueueGlobalStateTreeSquad`
```lua
StateTree_QueueGlobalStateTreeSquad(Boolean keepAlive, String openingBranchName, SquadID squad)
```
Run a global state tree on a squad

## statgraph (1 functions)

### `statgraph_save`
```lua
statgraph_save(Boolean begin)
```
Save the statgraph output to a file

## Subtitle (8 functions)

### `Subtitle_EndAllSpeech`
```lua
Subtitle_EndAllSpeech()
```
Prematurely finish all queued speech

### `Subtitle_EndCurrentSpeech`
```lua
Subtitle_EndCurrentSpeech()
```
Prematurely finish currently playing speech and advance the next one in queue

### `Subtitle_PlayCharacterSpeech`
```lua
Subtitle_PlayCharacterSpeech(String name, String text, String icon, String audioCtrlEvent)
```
Plays a global speech with subtitle and character icon and name in the overlay

### `Subtitle_PlayNarrativeEvent`
```lua
Subtitle_PlayNarrativeEvent(String str)
```
Plays a narrative event as a series of subtitled speech transitions when given the event's reflect ID.

### `Subtitle_PlayNarrativeLine`
```lua
Subtitle_PlayNarrativeLine(String str)
```
Plays a global speech with subtitle and actor icon specified in the narrative line with given ID.

### `Subtitle_PlaySpeechForSquadFromLocString`
```lua
Subtitle_PlaySpeechForSquadFromLocString(ScarBriefingActorPBG briefingActorPBG, String loc, Boolean disableIconSubtitle, String audioCtrlEvent, SquadID squad, Boolean is3D)
```
Plays a global speech with subtitle and actor icon in the overlay with speech bubbles on squad decorators.

### `Subtitle_PlaySpeechInternal`
```lua
Subtitle_PlaySpeechInternal(ScarBriefingActorPBG briefingActorPBG, String loc, Boolean disableIconSubtitle, String audioCtrlEvent, SquadID squad, Boolean is3D)
```
Plays a global speech with subtitle

### `Subtitle_UnstickCurrentSpeech`
```lua
Subtitle_UnstickCurrentSpeech()
```
Removes "sticky" state from currently playing speech (if any)

## SynchronizedCommand (3 functions)

### `SynchronizedCommand_PlayerAbility`
```lua
SynchronizedCommand_PlayerAbility(PlayerID player, PlayerID dest, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a player ability command (PCMD_Ability) to a player.

### `SynchronizedCommand_PlayerPosAbility`
```lua
SynchronizedCommand_PlayerPosAbility(PlayerID player, PlayerID dest, Position pos, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a positional ability command (PCMD_Ability) to a player

### `SynchronizedCommand_PlayerPosDirAbility`
```lua
SynchronizedCommand_PlayerPosDirAbility(PlayerID player, PlayerID dest, Position pos, Position dir, ScarAbilityPBG abilityPBG, Boolean skipCostAndPrereq)
```
Send a positional/directional ability command (PCMD_Ability) to a player

## Taskbar (2 functions)

### `Taskbar_IsVisible`
```lua
Taskbar_IsVisible()
```
Returns true if the taskbar is visible. (not deterministic)

### `Taskbar_SetVisibility`
```lua
Taskbar_SetVisibility(Boolean visible)
```
Sets taskbar visibility.

## Team (1 functions)

### `Team_GetRelationship`
```lua
Team_GetRelationship(Integer team1, Integer team2)
```
Returns the relationship between 2 teams.

## Terrain (8 functions)

### `Terrain_CreateSplat`
```lua
Terrain_CreateSplat(String _name, Real xpos, Real zpos, Real scale)
```
Create a splat on the terrain

### `Terrain_DrawGrid`
```lua
Terrain_DrawGrid(Integer increment)
```
Draw a grid on the terrain with tunable increment

### `Terrain_DrawGridLines`
```lua
Terrain_DrawGridLines(Integer spacing)
```
Draw lines on a grid on the terrain with tunable spacing

### `Terrain_DrawMaterialMap`
```lua
Terrain_DrawMaterialMap(Boolean onoff)
```
Draw terrain material map cells

### `Terrain_GetCoverType_AsNumber`
```lua
Terrain_GetCoverType_AsNumber(Position pos)
```
Takes a ScarPosition and returns a number representing the cover type at this position

### `Terrain_GetCoverType_AsString`
```lua
Terrain_GetCoverType_AsString(Position pos)
```
Takes a ScarPosition and returns a string representing the cover type at this position

### `Terrain_LoadHeightMap`
```lua
Terrain_LoadHeightMap()
```
Load the saved terrain height map. This will restore the state of the terrain height map to

### `Terrain_SaveHeightMap`
```lua
Terrain_SaveHeightMap()
```
Save the current terrain height map. It can be restored to that state by using Terrain_LoadHeightMap.

## TerrainHighlight (2 functions)

### `TerrainHighlight_Hide`
```lua
TerrainHighlight_Hide()
```
Hide metadata layer overlay on terrain

### `TerrainHighlight_Show`
```lua
TerrainHighlight_Show(String metadataLayerName, Real opacity)
```
Display metadata layer on terrain. Replaces previously displayed terrain highlight

## Territory (9 functions)

### `Territory_ContainsSectorID`
```lua
Territory_ContainsSectorID(SectorID sectorID)
```
Returns true if the Territory contains the given SectorID.

### `Territory_FindClosestSectorToPoint`
```lua
Territory_FindClosestSectorToPoint(Position pos3D)
```
Returns the SectorID of the closest Sector Generator point to the given ScarPosition.

### `Territory_GetAdjacentSectors`
```lua
Territory_GetAdjacentSectors(SectorID sectorID)
```
Returns a table of SectorIDs that are adjacent to the given SectorID.

### `Territory_GetPrimaryEntityInSector`
```lua
Territory_GetPrimaryEntityInSector(SectorID sectorID)
```
Returns the primary entity in the given sector, if one exists, and nil otherwise.

### `Territory_GetSectorContainingPoint`
```lua
Territory_GetSectorContainingPoint(Position pos3D)
```
Returns the sector containing the given ScarPosition.

### `Territory_GetSectorCreatorEntity`
```lua
Territory_GetSectorCreatorEntity(SectorID sectorID)
```
Get the creator entity of the sector by sectorID

### `Territory_GetSectorGeneratorPointOnTerrain`
```lua
Territory_GetSectorGeneratorPointOnTerrain(SectorID sectorID)
```
Returns the generator point of the given sector, snapped to the surface of the terrain.

### `Territory_GetSectorOwnerID`
```lua
Territory_GetSectorOwnerID(SectorID sectorID)
```
Get the ID of the owner of the sector

### `Territory_IsHexagonTerritory`
```lua
Territory_IsHexagonTerritory()
```
Returns true if the territory is a HexagonTerritory.

## Toggle (1 functions)

### `Toggle_Scanning_Info`
```lua
Toggle_Scanning_Info()
```
Toggles the scanning info from the ScanForTarget track for the debug entity

## UI (125 functions)

### `UI_AddChild`
```lua
UI_AddChild(String elementName, String typeName, String childName, StackVarTable propertyTable)
```
Add a new child named childName and of type typeName to elementName.

### `UI_AddCommandBinding`
```lua
UI_AddCommandBinding(String groupName, String bindingName, String callbackName)
```
Adds a command binding for groupName.bindingName to global function callbackName.

### `UI_AddEventHandler`
```lua
UI_AddEventHandler(String elementName, String eventName, String callbackName)
```
Adds the event handler on elementName for event eventName to global function callbackName(elementName, eventName).

### `UI_AddText`
```lua
UI_AddText(String elementName, String text)
```
Add text to elementName.

### `UI_AllTerritoryHide`
```lua
UI_AllTerritoryHide()
```
Toggle off all territory lines. Each call to UI_AllTerritoryHide must be matched by a call to UI_AllTerritoryShow

### `UI_AllTerritoryShow`
```lua
UI_AllTerritoryShow()
```
Toggle on all territory lines. Each call to UI_AllTerritoryShow must be matched by a call to UI_AllTerritoryHide

### `UI_AutosaveMessageHide`
```lua
UI_AutosaveMessageHide()
```
DEPRECATED! Removes a message added by UI_AutosaveMessageShow.

### `UI_AutosaveMessageShow`
```lua
UI_AutosaveMessageShow()
```
DEPRECATED! Shows a message indicating that the game is autosaving.

### `UI_CameraOptionsPopup`
```lua
UI_CameraOptionsPopup()
```
Opens a pop-up which takes the user directly to the camera settings

### `UI_CapturePointLinesHide`
```lua
UI_CapturePointLinesHide()
```
Toggle off capture-point boundary lines. Each call to UI_CapturePointLinesHide must be matched by a call to UI_CapturePointLinesShow

### `UI_CapturePointLinesShow`
```lua
UI_CapturePointLinesShow()
```
Toggle on capture-point boundary lines. Each call to UI_CapturePointLinesShow must be matched by a call to UI_CapturePointLinesHide

### `UI_Clear`
```lua
UI_Clear(String elementName)
```
Clear the contents of elementName.

### `UI_ClearEventCueFromID`
```lua
UI_ClearEventCueFromID(Integer id)
```
Clears an event cue with a specific ID. The ID is obtained as a return value from either UI_CreateEventCueClickable or UI_CreateEventCueClickableByType.

### `UI_ClearEventCues`
```lua
UI_ClearEventCues()
```
Clears all active event cues

### `UI_ClearModalAbilityPhaseCallback`
```lua
UI_ClearModalAbilityPhaseCallback()
```
Clears the ability phase callback.

### `UI_ClearModalConstructionPhaseCallback`
```lua
UI_ClearModalConstructionPhaseCallback()
```
Clears the construction phase callback.

### `UI_ClearModalHoverCallback`
```lua
UI_ClearModalHoverCallback()
```
Clears the construction phase callback.

### `UI_ClearSkipNISCallback`
```lua
UI_ClearSkipNISCallback()
```
Clears the try-to-skip-NIS callback

### `UI_CommandCardSetColumns`
```lua
UI_CommandCardSetColumns(Integer columns)
```
Set the numner of columns in the command card.

### `UI_CommandCardSetRows`
```lua
UI_CommandCardSetRows(Integer rows)
```
Set the numner of rows in the command card.

### `UI_CoverPreviewHide`
```lua
UI_CoverPreviewHide()
```
Toggle off cover preview. Each call to UI_CoverPreviewHide must be matched by a call to UI_CoverPreviewShow

### `UI_CoverPreviewShow`
```lua
UI_CoverPreviewShow()
```
Toggle on cover preview. Each call to UI_CoverPreviewShow must be matched by a call to UI_CoverPreviewHide

### `UI_CreateCustomEventCueFrom`
```lua
UI_CreateCustomEventCueFrom(sender player. Can be null. Used for retrieving player information. E.g. team color., event type id, visible duration of the event cue., enable repeat filtering if > 0. Make the event cue alive but not visible beyond its lifetime., when repeatTime > 0) how many times a event cue with the same customEventType can be repeated during repeatTime, when repeatTime > 0) filter out a event cue if it's within the range of a existing one with the same customEventType, title text if any, description text if any, ui data template of the event cue., path to the custom icon if any., color red channel., color green channel., color blue channel., color red alpha., event cue visibility flags. ECV_None: not visible ECV_Queue: visible in the queue ECV_Title: visible as title ECV_Queue | ECV_Title : both, Control event cue visibility in action ECAV_Global ECAV_ExecuterIsOwnOrAlly ECAV_ExecuterIsEnemy ECAV_CanSeeExecutor ECAV_CanSeeTarget ECAV_CanEnemySeeExecutor ECAV_TargetIsOwn ECAV_TargetIsAlly ECAV_OwnsTargetAndExecuterIsEnemy ECAV_AlliedToTargetAndExecuterIsEnemy ECAV_ExecuterIsOwn ECAV_ExecuterIsAlly ECAV_CanSeeTargetAndExecutorIsOwnOrAlly ECAV_CanSeeTargetAndExecutorIsOwn, function callback function.)
```
Create a event cue from a sender.

### `UI_CreateEntityKickerMessage`
```lua
UI_CreateEntityKickerMessage(target entity, localized message to display., relative path to the icon. Displayed before the message. Empty string ("") to not use an icon., relative path to the symbol. Displayed after the message. Empty string ("") to not use a symbol., offset on the x axis., offset on the y axis.)
```
Create a custom kicker message on the given entity.

### `UI_CreateEventCueClickable`
```lua
UI_CreateEventCueClickable(Integer customEventType, Real lifetime, Integer repeatCount, Real repeatTime, String title, String description, String dataTemplate, String iconPath, String soundPath, Integer red, Integer green, Integer blue, Integer alpha, EventCueVisibility visibility, LuaFunction function)
```
Creates a custom event cue. The Lua function callback passed in takes an ID as an argument which can be used to clear the event cue with UI_ClearEventCueFromID.

### `UI_CreateEventCueClickableByType`
```lua
UI_CreateEventCueClickableByType(UIEventType eventType, Real lifetime, String title, String description, String dataTemplate, String iconPath, String soundPath, Integer red, Integer green, Integer blue, Integer alpha, EventCueVisibility visibility, LuaFunction function)
```
Creates a named event cue. Returns the ID associated to the created event cue item. This ID can be used to clear the event cue item with UI_ClearEventCueFromID. The Lua function callback passed in takes an ID as an argument which can be used to clear the event cue with UI_ClearEventCueFromID.

### `UI_CreateEventCueClickableCanQueue`
```lua
UI_CreateEventCueClickableCanQueue(Integer customEventType, Real lifetime, Integer repeatCount, Real repeatTime, String title, String description, String dataTemplate, String iconPath, String soundPath, Integer red, Integer green, Integer blue, Integer alpha, EventCueVisibility visibility, LuaFunction function)
```
Creates a custom event cue. The Lua function callback passed in takes an ID as an argument which can be used to clear the event cue with UI_ClearEventCueFromID. Enables optional parameter that allows the event to only tick its duration whilst it is at the front of the stack to ensure it will always be visible in the high-priority stack.

### `UI_CreateMinimapBlipOnMarkerFrom`
```lua
UI_CreateMinimapBlipOnMarkerFrom(PlayerID sender, MarkerID marker, Real lifeTime, String dataTemplate)
```
Create a blips on a ScarMarker from a sender. sender is used for retrieving player information like team color

### `UI_CreateMinimapBlipOnPosFrom`
```lua
UI_CreateMinimapBlipOnPosFrom(PlayerID sender, Position position, Real lifeTime, String dataTemplate)
```
Create a blips on a position from a sender. sender is used for retrieving player information like team color

### `UI_CreatePositionKickerMessage`
```lua
UI_CreatePositionKickerMessage(target position, localized message to display, relative path to the icon. Displayed before the message., relative path to the symbol. Displayed after the message., number of seconds the kicker should be displayed for. 0 to use default value., offset on the x axis., offset on the y axis.)
```
Create a custom kicker message on the given position.

### `UI_CreateSimpleEntityKickerMessage`
```lua
UI_CreateSimpleEntityKickerMessage(target entity, localized message to display.)
```
Create a simple text only kicker message on the given entity.

### `UI_CreateSimplePositionKickerMessage`
```lua
UI_CreateSimplePositionKickerMessage(target position, localized message to display)
```
Create a simple text only kicker message on the given position.

### `UI_CreateSimpleSquadKickerMessage`
```lua
UI_CreateSimpleSquadKickerMessage(target squad, localized message to display)
```
Create a simple text only kicker message on the given squad.

### `UI_CreateSquadKickerMessage`
```lua
UI_CreateSquadKickerMessage(target squad, localized message to display, relative path to the icon. Displayed before the message., relative path to the symbol. Displayed after the message., number of seconds the kicker should be displayed for. 0 to use default value., offset on the x axis., offset on the y axis.)
```
Create a custom kicker message on the given squad.

### `UI_CreateTagForPosition`
```lua
UI_CreateTagForPosition(a scar position. Won't accept a position extremely close (std::numeric_limits<float>::min()) to the existing ones.)
```
Create a position tag.

### `UI_CursorHide`
```lua
UI_CursorHide()
```
Hides the mouse cursor

### `UI_CursorShow`
```lua
UI_CursorShow()
```
Shows the mouse cursor if it has been hidden

### `UI_DestroyTagForPosition`
```lua
UI_DestroyTagForPosition(same of or extremely close (std::numeric_limits<float>::min()) to an existing position. If there are multiple candidates, delete the closest.)
```
Destroy a position tag

### `UI_EnableEntityDecorator`
```lua
UI_EnableEntityDecorator(EntityID entity, Boolean enabled)
```
Enable or disable entity decorator. The default is decorator enabled.

### `UI_EnableEntityMinimapIndicator`
```lua
UI_EnableEntityMinimapIndicator(EntityID entity, Boolean enabled)
```
Enable or disable entity minimap indicator. The default is enabled.

### `UI_EnableEntitySelectionVisuals`
```lua
UI_EnableEntitySelectionVisuals(EntityID entity, Boolean enabled)
```
Enable or disable entity selection visuals. The default is visuals enabled.

### `UI_EnableGameEventCueType`
```lua
UI_EnableGameEventCueType(GameEventID gameEventType, Boolean enable)
```
Enables or disables event cues.

### `UI_EnableResourceTypeKicker`
```lua
UI_EnableResourceTypeKicker(ResourceType resourceType, Boolean enable)
```
Enables or disables resource kickers.

### `UI_EnableSquadDecorator`
```lua
UI_EnableSquadDecorator(SquadID squad, Boolean enabled)
```
Enable or disable the squad decorator. The default is decorator enabled.

### `UI_EnableSquadMinimapIndicator`
```lua
UI_EnableSquadMinimapIndicator(SquadID squad, Boolean enabled)
```
Enable or disable squad minimap indicator. The default is enabled.

### `UI_EnableUIEventCueType`
```lua
UI_EnableUIEventCueType(UIEventType uiEventType, Boolean enable)
```
Enables or disables event cues.

### `UI_FadeOutEventCueFromID`
```lua
UI_FadeOutEventCueFromID(Integer id)
```
Triggers an event cue to start its fadeout animation. The animation is determined in XAML.

### `UI_FlashAbilityButton`
```lua
UI_FlashAbilityButton(ScarAbilityPBG ability, Boolean stopOnClick)
```
Flash an ability command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashConstructionButton`
```lua
UI_FlashConstructionButton(ScarEntityPBG ebp, Boolean stopOnClick)
```
Flash a construction item command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashEntity`
```lua
UI_FlashEntity(EntityID entity, String actionOnName)
```
Flashes the entity using attributes from [tuning][ui]

### `UI_FlashEntityCommandButton`
```lua
UI_FlashEntityCommandButton(EntityCommandType command, Boolean stopOnClick)
```
Flash an entity order command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashEventCue`
```lua
UI_FlashEventCue(Integer eventCueID, Boolean stopOnClick)
```
Flash an event cue item.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashMenu`
```lua
UI_FlashMenu(String menuName, Boolean stopOnClick)
```
Flash a menu command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashObjectiveCounter`
```lua
UI_FlashObjectiveCounter(Integer objectiveID)
```
Flash an objective counter.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashObjectiveIcon`
```lua
UI_FlashObjectiveIcon(Integer objectiveID, Boolean stopOnClick)
```
Flash an objective.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashProductionBuildingButton`
```lua
UI_FlashProductionBuildingButton(String type, Boolean stopOnClick)
```
Flash a production building button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashProductionButton`
```lua
UI_FlashProductionButton(ProductionItemType type, PropertyBagGroup pbg, Boolean stopOnClick)
```
Flash a production item command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashSquadCommandButton`
```lua
UI_FlashSquadCommandButton(SquadCommandType command, Boolean stopOnClick)
```
Flash a squad order command button.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashUSSEntityButton`
```lua
UI_FlashUSSEntityButton(EntityID entity, Boolean stopOnClick)
```
Flash a button on the USS for this entity.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_FlashUSSSquadButton`
```lua
UI_FlashUSSSquadButton(SquadID squad, Boolean stopOnClick)
```
Flash a button on the USS for this squad.  Pass the return value to UI_StopFlashing to stop flashing the button.

### `UI_GetAbilityIconName`
```lua
UI_GetAbilityIconName(ScarAbilityPBG abilityBag)
```
Returns the icon name for a given ability

### `UI_GetActiveRadialMenuType`
```lua
UI_GetActiveRadialMenuType()
```
Returns the type of the menu which is currently open. These types are: RMT_Invalid (returned as the default value if no radial is open), RMT_ContextualRadialMenu, RMT_RegimentsMenu, RMT_FindMenu

### `UI_GetDecoratorsEnabled`
```lua
UI_GetDecoratorsEnabled()
```
Returns whether all decorators are enabled or not

### `UI_GetDecoratorVisibilityEntity`
```lua
UI_GetDecoratorVisibilityEntity(Entity entity)
```
Gets an enum value indicating the visibility of decorators for an entity.

### `UI_GetDecoratorVisibilitySquad`
```lua
UI_GetDecoratorVisibilitySquad(Squad squad)
```
Gets an enum value indicating the visibility of decorators for a squad.

### `UI_GetGovernmentRadialWeights`
```lua
UI_GetGovernmentRadialWeights()
```
Returns a resource amount representing the current weights the government/vilager automation system is using

### `UI_GetMarqueeRadius`
```lua
UI_GetMarqueeRadius()
```
Returns the current size of the selection marquee as a float.

### `UI_GetUICommandPBG`
```lua
UI_GetUICommandPBG(String pbgShortname)
```
Returns an ui command property bag group.

### `UI_GetXboxCommandCardTab`
```lua
UI_GetXboxCommandCardTab()
```
Returns the active command card tab in kbm (XCCT_Commands, XCCT_Economic, XCCT_Military, XCCT_Invalid)

### `UI_HighlightSquad`
```lua
UI_HighlightSquad(SquadID squad, Real duration)
```
Turn on squad highlight UI feature for the specified duration.

### `UI_IsCivSpecificMenuOpen`
```lua
UI_IsCivSpecificMenuOpen()
```
Check if the civ specific menu is currently open (e.g. the Abbasid Golden Age menu)

### `UI_IsLayerContentLoaded`
```lua
UI_IsLayerContentLoaded(FrontEnd_Layer layer, String contentPath)
```
Check if content is loaded for a specific layer

### `UI_IsMinimapFocusActive`
```lua
UI_IsMinimapFocusActive()
```
Check if Salisbury Minimap focus mode is active (expanded Minimap with pings available to the controller)

### `UI_IsQueueModifierDown`
```lua
UI_IsQueueModifierDown()
```
Check if the player currently has the 'queue modifier' key down (shift on PC, LT on controller)

### `UI_IsReplay`
```lua
UI_IsReplay()
```
Is a replay match currently.

### `UI_IsXboxControllerUI`
```lua
UI_IsXboxControllerUI()
```
Returns true when the user has a controller as their preferred input type

### `UI_IsXboxKBMUI`
```lua
UI_IsXboxKBMUI()
```
Check if we are running xbox ui and in kbm mode

### `UI_IsXboxUI`
```lua
UI_IsXboxUI()
```
Returns true when running on a console or PC with with the -showXboxUI or -showPS5UI arguments

### `UI_LetterboxFade`
```lua
UI_LetterboxFade(Real r, Real g, Real b, Real a, Real duration, Real aspectRatio, Boolean persistent)
```
Fades the letterbox to a given RGBA colour over a number of seconds by a given aspect ratio.

### `UI_MessageBoxHide`
```lua
UI_MessageBoxHide(DialogResult dialogResult)
```
If the message box is activated, close it.  The callback will receive the button parameter given.

### `UI_MessageBoxReset`
```lua
UI_MessageBoxReset()
```
Reset message box data set by previous calls (to display a new message box).

### `UI_MessageBoxSetButton`
```lua
UI_MessageBoxSetButton(DialogResult dialogResult, String text, String tooltip, String icon, Boolean isEnabled)
```
Set the text/tooltip/enabled state of a button on the dialog.

### `UI_MessageBoxSetText`
```lua
UI_MessageBoxSetText(String title, String message)
```
Set the title and message body of the dialog.

### `UI_ModalVisual_CreateReticule`
```lua
UI_ModalVisual_CreateReticule(ScarReticulePBG reticulePbg, Real radius)
```
Create a reticule

### `UI_ModalVisual_Destroy`
```lua
UI_ModalVisual_Destroy(Integer id)
```
Destroy a modal visual

### `UI_NewHUDFeature`
```lua
UI_NewHUDFeature(HUDFeatureType newHUDFeature, String featureText, String featureIcon, Real duration)
```
Brings up a message and arrow pointing to a HUD feature.

### `UI_OutOfBoundsLinesHide`
```lua
UI_OutOfBoundsLinesHide()
```
Toggle off terrain out of bounds lines. Each call to UI_OutOfBoundsLinesHide must be matched by a call to UI_OutOfBoundsLinesShow

### `UI_OutOfBoundsLinesShow`
```lua
UI_OutOfBoundsLinesShow()
```
Toggle on terrain out of bounds lines. Each call to UI_OutOfBoundsLinesShow must be matched by a call to UI_OutOfBoundsLinesShowHide

### `UI_OverrideUIProperty`
```lua
UI_OverrideUIProperty(PropertyBagGroup pbgHoldingUIInfo, String propertyName, String overrideValue)
```
modifies certain UI properties of ebp and sbp. Must be called at the script loading time. Currently supports overriding "screen_name" and "flag_icon"

### `UI_PickIDForInputMode`
```lua
UI_PickIDForInputMode(Integer kbmID, Integer gamepadID)
```
Will select the correct locID based on the preferred input mode.

### `UI_Remove`
```lua
UI_Remove(String elementName)
```
Remove elementName from its parent.

### `UI_RemoveCommandBinding`
```lua
UI_RemoveCommandBinding(String groupName, String bindingName)
```
Removes a command binding for groupName.bindingName.

### `UI_RemoveEventHandler`
```lua
UI_RemoveEventHandler(String elementName, String eventName, String callbackName)
```
Removes the event handler on elementName for event eventName to global function callbackName(elementName, eventName).

### `UI_RestrictBuildingPlacement`
```lua
UI_RestrictBuildingPlacement(MarkerID marker)
```
Only allow buildings to be placed inside a marker.

### `UI_ScreenFade`
```lua
UI_ScreenFade(Real r, Real g, Real b, Real a, Real duration, Boolean persistent)
```
Fades the screen to a given RGBA colour over a number of seconds. mouse input is blocked during the fade, and you can control whether the input keeps being blocked after the fade has ended (be careful!)

### `UI_SectorsHide`
```lua
UI_SectorsHide()
```
Toggle off sector lines. Each call to UI_SectorsHide must be matched by a call to UI_SectorsShow

### `UI_SectorsShow`
```lua
UI_SectorsShow()
```
Toggle on sector lines. Each call to UI_SectorsShow must be matched by a call to UI_SectorsHide

### `UI_SetAlliedBandBoxSelection`
```lua
UI_SetAlliedBandBoxSelection(Boolean allow)
```
Sets the game to allow allied squads to be selected at the same time as your own squads

### `UI_SetAllowLoadAndSave`
```lua
UI_SetAllowLoadAndSave(Boolean allowLoadAndSave)
```
Enables or disable load and save features at the pause menu

### `UI_SetControlGroupSelectedCallback`
```lua
UI_SetControlGroupSelectedCallback(in the format of function(controlGroupIndex))
```
Sets a callback firing when user select a control group either by hotkey or by control group button

### `UI_SetCPMeterVisibility`
```lua
UI_SetCPMeterVisibility(Boolean visible)
```
Sets the visibility of the Command Point meter.

### `UI_SetDataContext`
```lua
UI_SetDataContext(String elementName, StackVarTable table)
```
Converts table to a data context for bindings of elementName.

### `UI_SetDecoratorsEnabled`
```lua
UI_SetDecoratorsEnabled(Boolean enabled)
```
Enables or disables all decorators

### `UI_SetEnablePauseMenu`
```lua
UI_SetEnablePauseMenu(Boolean isEnable)
```
Enable/Disable pause menu showing up when the pause menu hot key is pressed.

### `UI_SetEntityDataContext`
```lua
UI_SetEntityDataContext(EntityID entity, StackVarTable table)
```
Converts table to a data context exposed through entity models.

### `UI_SetEntityDecorator`
```lua
UI_SetEntityDecorator(EntityID entity, String decorator)
```
Explicitly set the decorator a squad should use.

### `UI_SetEntityGhostSpottedStaggered`
```lua
UI_SetEntityGhostSpottedStaggered(EntityID entity)
```
Sets the game to show the entity ghost in a spotted state

### `UI_SetForceShowSubtitles`
```lua
UI_SetForceShowSubtitles(Boolean forceShowSubtitles)
```
Sets the game to force show subtitles even if the player has them turned off.

### `UI_SetMinimapTrueNorth`
```lua
UI_SetMinimapTrueNorth(Real trueNorthAngleDeg)
```
Sets the angle of True North for the minimap in degrees

### `UI_SetModalAbilityPhaseCallback`
```lua
UI_SetModalAbilityPhaseCallback(LuaFunction function)
```
Sets a function to be called when the player clicks an ability and gets a targeting UI. Your function will have 2 arguments: [Blueprint] ability blueprint, [integer] phase: TP_Position, TP_Facing (only if ability requires facing), TP_Issued (not deterministic) or TP_Cancelled (for all issuables)

### `UI_SetModalConstructionPhaseCallback`
```lua
UI_SetModalConstructionPhaseCallback(LuaFunction function)
```
Sets a function to be called when the player clicks a construction item and gets a targeting UI. Your function will have 2 arguments: [Blueprint] ability blueprint, [integer] phase: TP_Position, TP_Facing (only if ability requires facing), TP_Issued (not strict) or TP_Cancelled (for all issuables)

### `UI_SetModalHoverCallback`
```lua
UI_SetModalHoverCallback(LuaFunction function)
```
Sets a function to be called when the player clicks a construction item and gets a targeting UI. Your function will have 2 arguments: [Blueprint] ability blueprint, [integer] phase: TP_Position, TP_Facing (only if ability requires facing), TP_Issued (not strict) or TP_Cancelled (for all issuables)

### `UI_SetPlayerDataContext`
```lua
UI_SetPlayerDataContext(PlayerID player, StackVarTable table)
```
Converts table to a data context exposed through player models.

### `UI_SetPropertyValue`
```lua
UI_SetPropertyValue(String elementName, String propertyName, StackVar stackVar)
```
Sets the property propertyName on elementName to value stackVar.

### `UI_SetPropertyValues`
```lua
UI_SetPropertyValues(String elementName, StackVarTable propertyTable)
```
Sets the properties on elementName to the key/value pairs in propertyTable.

### `UI_SetSkipNISCallback`
```lua
UI_SetSkipNISCallback(LuaFunction function)
```
Sets a callback firing when user try to skip the NIS

### `UI_SetSquadDataContext`
```lua
UI_SetSquadDataContext(SquadID squad, StackVarTable table)
```
Converts table to a data context exposed through squad models.

### `UI_SetSquadDecorator`
```lua
UI_SetSquadDecorator(SquadID squad, String decorator)
```
Explicitly set the decorator a squad should use.

### `UI_SetSquadDecoratorAlwaysVisible`
```lua
UI_SetSquadDecoratorAlwaysVisible(SquadID squad, Boolean alwaysVisible)
```
Turn on of off the squad decorator being always visible. The default is decorator not always visible.

### `UI_SetTutorializedWidgetsRequired`
```lua
UI_SetTutorializedWidgetsRequired(Boolean isRequired)
```
Set whether settings to toggle HUD widgets that are required in the tutorial should be ignored

### `UI_SystemMessageHide`
```lua
UI_SystemMessageHide(String message)
```
Removes a message added by Game_ShowSystemMessage.

### `UI_SystemMessageShow`
```lua
UI_SystemMessageShow(String message)
```
Shows a system message in the area where Game Paused text appears.

### `UI_ToggleDecorators`
```lua
UI_ToggleDecorators()
```
Toggles all decorators on or off.

### `UI_UnrestrictBuildingPlacement`
```lua
UI_UnrestrictBuildingPlacement()
```
Removes the restriction on building placement.

### `UI_XboxIsLandmarkRadialOpen`
```lua
UI_XboxIsLandmarkRadialOpen()
```
Check if the landmark menu is currently open (from within the radial menu)

## UIWarning (1 functions)

### `UIWarning_Show`
```lua
UIWarning_Show(String text)
```
Displays a brief UI warning in the critical alert message area.

## Vaulting (1 functions)

### `Vaulting_DrawDebug`
```lua
Vaulting_DrawDebug()
```
Toggles on or off vaulting debug drawing

## Vector (3 functions)

### `Vector_Length`
```lua
Vector_Length(Position pos)
```
Calculates the length of the provided vector

### `Vector_Lerp`
```lua
Vector_Lerp(Real factor, Position pos1, Position pos2)
```
Linearly interpolates between the two provided vectors based on the provided factor

### `Vector_Normalize`
```lua
Vector_Normalize(Position pos)
```
Returns the normalized version of the provided vector

## Weapon (12 functions)

### `Weapon_AllWeaponAttackGround`
```lua
Weapon_AllWeaponAttackGround()
```
Toggle enabling all weapon gound attack

### `Weapon_AnimInfo`
```lua
Weapon_AnimInfo()
```
Toggle weapon animation information

### `Weapon_AttackRadii`
```lua
Weapon_AttackRadii()
```
Toggle weapon attack radii around the entities

### `Weapon_Firing`
```lua
Weapon_Firing()
```
Toggle weapon firing lines

### `Weapon_HardPointInfo`
```lua
Weapon_HardPointInfo()
```
Toggle weapon hard point information

### `Weapon_Info`
```lua
Weapon_Info()
```
Toggle weapon state and calculation information

### `Weapon_PrintBestTarget`
```lua
Weapon_PrintBestTarget()
```
Toggle weapon best target result

### `Weapon_PriorityInfo`
```lua
Weapon_PriorityInfo()
```
Toggle weapon priority information (must TAG entity you want info about)

### `Weapon_ProjectileDetonateTimer`
```lua
Weapon_ProjectileDetonateTimer()
```
Toggle weapon projectile denotation timer

### `Weapon_ProjectileInfo`
```lua
Weapon_ProjectileInfo()
```
Toggle weapon projectile information

### `Weapon_ScatterInfo`
```lua
Weapon_ScatterInfo()
```
Toggle weapon scatter target information

### `Weapon_Tracking`
```lua
Weapon_Tracking()
```
Toggle weapon tracking lines and maximum angles

## WinWarning (2 functions)

### `WinWarning_PublishLoseReminder`
```lua
WinWarning_PublishLoseReminder(PlayerID player, Integer warningLevel)
```
Triggers a UI event cue and an audio cue that the player is about to lose the game.

### `WinWarning_ShowLoseWarning`
```lua
WinWarning_ShowLoseWarning(String text, Real fadeIn, Real duration, Real fadeOut)
```
Call UI_TitleDestroy to remove.

## World (84 functions)

### `World_CalculateEntitiesAveragePositionInArea`
```lua
World_CalculateEntitiesAveragePositionInArea(PlayerID player, Position pos, Real radius, OwnerType ownerType, Boolean onlyEntitiesInSquads)
```
Returns the average positions of the entities in the area

### `World_ChangeZoneInteractivity`
```lua
World_ChangeZoneInteractivity(Integer targetInteractivity, Integer adjustedInteractivity)
```
Changes target interactivity zones to adjusted interactivity (255 max), probably only safe to use post NIS

### `World_DestroyWallsNearMarker`
```lua
World_DestroyWallsNearMarker(MarkerID marker)
```
Destroys walls (entities with a wall_ext) near a marker

### `World_DistanceEGroupToPoint`
```lua
World_DistanceEGroupToPoint(EGroupID egroup, Position p1, Boolean closest)
```
Get the distance between a squad group and a point.

### `World_DistancePointToPoint`
```lua
World_DistancePointToPoint(Position p1, Position p2)
```
Get the distance between two points.

### `World_DistanceSGroupToPoint`
```lua
World_DistanceSGroupToPoint(SGroupID sgroup, Position p1, Boolean closest)
```
Get the distance between a squad group and a point.

### `World_DistanceSquaredPointToPoint`
```lua
World_DistanceSquaredPointToPoint(Position p1, Position p2)
```
Get the distance squared between two points.

### `World_EnableReplacementObjectForEmptyPlayers`
```lua
World_EnableReplacementObjectForEmptyPlayers(Boolean enable)
```
Determines whether empty players get converted to null resource points.

### `World_EnableSharedLineOfSight`
```lua
World_EnableSharedLineOfSight(PlayerID p0, PlayerID p1, Boolean enableSharedVision)
```
Enables or disables shared line of sight between these two players

### `World_EndSP`
```lua
World_EndSP(Boolean localPlayerWon, WinReason winReason)
```
Wins/loses a single team mission for the local teams, with given win reason

### `World_GetAllEntities`
```lua
World_GetAllEntities(EGroupID egroup)
```
Clears the egroup, then finds and adds all entities to it

### `World_GetAllEntitiesOfType`
```lua
World_GetAllEntitiesOfType(EGroupID egroup, String type)
```
Clears the egroup, then finds and adds all entities of the given type to it

### `World_GetAllNeutralEntities`
```lua
World_GetAllNeutralEntities(EGroupID egroup)
```
Clears the egroup, then finds and adds all neutral entities to it

### `World_GetAllNeutralSquads`
```lua
World_GetAllNeutralSquads(SGroupID sgroup)
```
Clears the sgroup, then finds and adds all neutral squads to it

### `World_GetAllSquads`
```lua
World_GetAllSquads(SGroupID sgroup)
```
Clears the sgroup, then finds and adds all squads to it

### `World_GetAllSquadsOfType`
```lua
World_GetAllSquadsOfType(SGroupID sgroup, String type)
```
Clears the sgroup, then finds and adds all squads of the given type to it

### `World_GetBlueprintEntities`
```lua
World_GetBlueprintEntities(ScarEntityPBG pbg, EGroupID outEntities)
```
Returns all entities with this blueprint - warning this function iterates over all entities so it is slow

### `World_GetCoverPoints`
```lua
World_GetCoverPoints(EGroupID group)
```
Appends all cover points to an egroup.

### `World_GetEntitiesNearMarker`
```lua
World_GetEntitiesNearMarker(PlayerID player, EGroupID egroup, MarkerID marker, OwnerType ownerType)
```
Clears the egroup, then finds and adds entities near the marker to the egroup

### `World_GetEntitiesNearPoint`
```lua
World_GetEntitiesNearPoint(PlayerID player, EGroupID egroup, Position pos, Real radius, OwnerType ownerType)
```
Clears the egroup, then finds and adds entities near the point to the egroup

### `World_GetEntitiesWithinTerritorySector`
```lua
World_GetEntitiesWithinTerritorySector(PlayerID player, EGroupID egroup, Integer inSectorID, OwnerType ownerType)
```
Clears the egroup, then finds and adds entities within the territory sector to the egroup

### `World_GetGameTicks`
```lua
World_GetGameTicks()
```
Return the total number of game (simulation) ticks elapsed.

### `World_GetGameTime`
```lua
World_GetGameTime()
```
Return the total game time in seconds.

### `World_GetHeightAt`
```lua
World_GetHeightAt(Real x, Real y)
```
returns the height of ground at 2D pos x,y

### `World_GetInteractionStageAtPoint`
```lua
World_GetInteractionStageAtPoint(Position position)
```
Returns the interaction stage of the cell in the provided position

### `World_GetLength`
```lua
World_GetLength()
```
Returns the total playable length of the game world (z coordinate)

### `World_GetMetadataBiomePBGName`
```lua
World_GetMetadataBiomePBGName(String layerName, Real x, Real y)
```
Get the Biome PBG's name of the specified terrain metadata layer and the specified coordinates.

### `World_GetMetadataLayerBoolean`
```lua
World_GetMetadataLayerBoolean(String layerName, Real x, Real y)
```
Get the boolean value of the specified terrain metadata layer and the specified coordinates.

### `World_GetMetadataLayerInteger`
```lua
World_GetMetadataLayerInteger(String layerName, Real x, Real y)
```
Get the integer value of the specified terrain metadata layer and the specified coordinates.

### `World_GetMetadataLayerNumber`
```lua
World_GetMetadataLayerNumber(String layerName, Real x, Real y)
```
Get the numeric value of the specified terrain metadata layer and the specified coordinates.

### `World_GetMetadataLayerPBG`
```lua
World_GetMetadataLayerPBG(String layerName, Real x, Real y)
```
Get the PBG of the specified terrain metadata layer and the specified coordinates.

### `World_GetMetadataLayerString`
```lua
World_GetMetadataLayerString(String layerName, Real x, Real y)
```
Get the PBG of the specified terrain metadata layer and the specified coordinates.

### `World_GetNearestInteractablePoint`
```lua
World_GetNearestInteractablePoint(Position position)
```
returns the nearest intractable position to the supplied position

### `World_GetNeutralEntitiesNearMarker`
```lua
World_GetNeutralEntitiesNearMarker(EGroupID egroup, MarkerID marker)
```
Find and add neutral entities near the marker to the egroup

### `World_GetNeutralEntitiesNearPoint`
```lua
World_GetNeutralEntitiesNearPoint(EGroupID egroup, Position pos, Real radius)
```
Find and add neutral entities near the point to the egroup

### `World_GetNeutralEntitiesWithinTerritorySector`
```lua
World_GetNeutralEntitiesWithinTerritorySector(EGroupID egroup, Integer sectorID)
```
Find and add neutral entities within the territory sector to the egroup

### `World_GetNumEntitiesNearPoint`
```lua
World_GetNumEntitiesNearPoint(ScarEntityPBG ebp, Position pos, Real radius)
```
Return the number of entities of the same ebp in the sphere volume

### `World_GetNumStrategicPoints`
```lua
World_GetNumStrategicPoints()
```
Returns the number of strategic points on this map (does not count strat. objectives)

### `World_GetOffsetPosition`
```lua
World_GetOffsetPosition(Position position, Position heading, Integer offset, Real distance)
```
Returns a position that is offset a certain distance from the position/heading passed in. see ScarUtil.scar for explanation of 'offset' parameter.

### `World_GetOffsetPositionRelativeToFacingTarget`
```lua
World_GetOffsetPositionRelativeToFacingTarget(Position position, Position facingTarget, Real offset)
```
Offsets the input position relative to the facing target

### `World_GetOffsetVectorPosition`
```lua
World_GetOffsetVectorPosition(Position position, Position heading, Position offset)
```
Returns a position that is offset from the input position by the offset vector rotated by the direction supplied

### `World_GetPlayerAt`
```lua
World_GetPlayerAt(Integer index)
```
Returns the player at a given index, numbers start at one

### `World_GetPlayerCount`
```lua
World_GetPlayerCount()
```
Return the total number of players in the world

### `World_GetPlayerIndex`
```lua
World_GetPlayerIndex(PlayerID player)
```
Returns the player index given the Player*

### `World_GetPossibleSquadsBlueprint`
```lua
World_GetPossibleSquadsBlueprint(ScarRacePBG racePBG, Integer index)
```
Returns the blueprint of a chosen squad for a race

### `World_GetPossibleSquadsCount`
```lua
World_GetPossibleSquadsCount(ScarRacePBG racePBG)
```
Returns the number of types of squads a race can build

### `World_GetRaceBlueprint`
```lua
World_GetRaceBlueprint(String racename)
```
Returns the race index of a race, given its name (from the ME).

### `World_GetRand`
```lua
World_GetRand(Integer min, Integer max)
```
Returns a random integer with range [min, max]

### `World_GetScenarioMaxPlayers`
```lua
World_GetScenarioMaxPlayers()
```
Returns maximum number of players in this match

### `World_GetSpawnablePosition`
```lua
World_GetSpawnablePosition(Position around, EntityID entity)
```
Given any position in the world, this function will return position safe for spawning a given entity

### `World_GetSquadsNearMarker`
```lua
World_GetSquadsNearMarker(PlayerID player, SGroupID sgroup, MarkerID marker, OwnerType ownerType)
```
Clears the sgroup, then finds and adds squads near the marker to the sgroup

### `World_GetSquadsNearPoint`
```lua
World_GetSquadsNearPoint(PlayerID player, SGroupID sgroup, Position pos, Real radius, OwnerType ownerType)
```
Clears the sgroup, then finds and adds squads near the point to the sgroup

### `World_GetSquadsWithinTerritorySector`
```lua
World_GetSquadsWithinTerritorySector(PlayerID player, SGroupID sgroup, Integer inSectorID, OwnerType ownerType)
```
Clears the sgroup, then finds and adds squads within territory sector identified by sector ID

### `World_GetStrategyPoints`
```lua
World_GetStrategyPoints(EGroupID group, Boolean bIncludeVP)
```
Appends all the strategic resource points to an egroup.

### `World_GetTeamTerritoryGaps`
```lua
World_GetTeamTerritoryGaps(Integer sectorID1, Integer sectorID2, StackVarTable results)
```
Returns one or more sector IDs that would connect two unconnected pieces of territory. return value is through a table (since there can be more than one way to connect territory) - each entry in this table is a table of sector IDs.

### `World_GetTerrainCellType`
```lua
World_GetTerrainCellType(Real x, Real y)
```
returns the cell type of the cell in the specified coordinates. 0 = Sky, 1 = Land, 2 = Water.

### `World_GetTerritorySectorID`
```lua
World_GetTerritorySectorID(Position pos)
```
Return the sector ID from the position

### `World_GetTerritorySectorPosition`
```lua
World_GetTerritorySectorPosition(Integer inSectorID)
```
Returns the position of a sectors generator point.

### `World_GetWidth`
```lua
World_GetWidth()
```
Returns the total playable width of the game world (x coordinate)

### `World_IsCurrentInteractionStageActive`
```lua
World_IsCurrentInteractionStageActive(Integer stage)
```
Returns whether the interaction stage is currently active

### `World_IsGameOver`
```lua
World_IsGameOver()
```
Is the game over?

### `World_IsInSupply`
```lua
World_IsInSupply(PlayerID player, Position pos)
```
Returns true if position is in-supply for the given player

### `World_IsMultiplayerGame`
```lua
World_IsMultiplayerGame()
```
Returns whether or not the game type of this world is multiplayer

### `World_IsPointInPlayerTerritory`
```lua
World_IsPointInPlayerTerritory(PlayerID player, Position position)
```
Returns true if position if part of the entity territory

### `World_IsPosOnWalkableWall`
```lua
World_IsPosOnWalkableWall(Position p)
```
Returns if a position is on walkable wall

### `World_IsReplay`
```lua
World_IsReplay()
```
Returns TRUE if the game is currently in a replay state.

### `World_IsTerritorySectorOwnedByPlayer`
```lua
World_IsTerritorySectorOwnedByPlayer(PlayerID player, Integer inSectorID)
```
Find if player has ownership to this territory sector.

### `World_KillPlayer`
```lua
World_KillPlayer(PlayerID player, KillPlayerReason reason)
```
Kills the player with a reason.

### `World_LeaveGameMatch`
```lua
World_LeaveGameMatch()
```
Quit the game without declaring it over and return to frontend.

### `World_OwnsEntity`
```lua
World_OwnsEntity(EntityID entity)
```
Returns true if the squad is owned by the world

### `World_OwnsSquad`
```lua
World_OwnsSquad(SquadID squad)
```
Returns true if the squad is owned by the world

### `World_PointPointProx`
```lua
World_PointPointProx(Position p1, Position p2, Real prox)
```
Returns true if two world positions are in proximity to each other

### `World_Pos`
```lua
World_Pos(Real x, Real y, Real z)
```
Creates a new Position object.

### `World_PosInBounds`
```lua
World_PosInBounds(Position pos)
```
Returns if given position is in playable area.

### `World_Reset`
```lua
World_Reset()
```
DO NOT CALL UNLESS YOU DO AUTOMATED TESTING

### `World_SetAllInteractiveStagesVisibility`
```lua
World_SetAllInteractiveStagesVisibility(Boolean visibilityStatus)
```
Unlocks all the interaction stages

### `World_SetDesignerSupply`
```lua
World_SetDesignerSupply(Position point, Boolean bSupply)
```
Sets a particular sector in the world as a supply provider (or not)

### `World_SetInteractionStage`
```lua
World_SetInteractionStage(Integer stage)
```
Set current interaction stage to value supplied, must be >= 0

### `World_SetPlayerLose`
```lua
World_SetPlayerLose(PlayerID player)
```
Sets the player to a lose state, with a reason for losing, and kills the player

### `World_SetPlayerWin`
```lua
World_SetPlayerWin(PlayerID player)
```
Sets the player to a win state.

### `World_SetSharedLineOfSightEnabledAndMergeExploredMaps`
```lua
World_SetSharedLineOfSightEnabledAndMergeExploredMaps(PlayerID p0, PlayerID p1, Boolean enableSharedVision)
```
Enables or disables shared line of sight between these two players, and merges explored maps when needed

### `World_SetTeamWin`
```lua
World_SetTeamWin(Integer winningTeam, WinReason winReason)
```
Sets every player on a team to a win state, with a reason for winning. Also sets all other players to a lose state, and kills them (if they're not already dead)

### `World_SpawnDemolitionCharge`
```lua
World_SpawnDemolitionCharge(PlayerID player, Position pos)
```
spawn a demolitions charge at a position, 'player' is the one that owns the demolitions and can detonate them.

### `World_TeamTerritoryPointsConnected`
```lua
World_TeamTerritoryPointsConnected(Integer team_index, Position p1, Position p2)
```
Returns true if the two points are in the same territory region, and owned by the specified territory team, Returns false otherwise.

