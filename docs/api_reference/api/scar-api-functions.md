# SCAR API Functions — Complete Reference

Last Updated: 2026-03-18

All 4,435 functions extracted from the AoE4 Lua runtime, organized by category.

> **Typed signatures**: For full typed parameter signatures of 1,976 engine API functions, see
> [scar-engine-api-signatures.md](scar-engine-api-signatures.md) (source: official scardocs, API date 2026-05-07).

---

## Squad_ (254 functions)
Entity group member management, state checks, commands, veterancy, production.

### Creation & Destruction
- `Squad_CreateAndSpawnToward` / `Squad_CreateToward` — Create squads at positions
- `Squad_Spawn` / `Squad_DeSpawn` — Spawn/despawn squad
- `Squad_Destroy` — Destroy squad
- `Squad_Kill` — Kill squad with combat effects
- `Squad_Split` — Split squad members

### State Queries
- `Squad_IsAlive` / `Squad_IsDead` — Life state
- `Squad_IsIdle` / `Squad_IsMoving` / `Squad_IsAttacking` — Activity state
- `Squad_IsInHoldEntity` / `Squad_IsInHoldSquad` — Garrison state
- `Squad_IsRetreating` / `Squad_IsReinforcing` — Movement state
- `Squad_IsUnderAttack` — Combat state
- `Squad_IsOfType` — Blueprint type check
- `Squad_IsInCover` / `Squad_IsDugIn` — Position state
- `Squad_IsGathering` / `Squad_IsCapturing` — Task state
- `Squad_IsInvulnerable` / `Squad_IsSelectable` — Modifier state
- `Squad_IsTraining` / `Squad_IsUpgrading` — Production state

### Getters
- `Squad_GetHealth` / `Squad_GetHealthMax` / `Squad_GetHealthPercentage` — Health
- `Squad_GetPosition` / `Squad_GetHeading` — Position/direction
- `Squad_GetBlueprint` / `Squad_GetPlayerOwner` — Identity
- `Squad_GetMinArmor` / `Squad_GetMaxArmor` — Armor values
- `Squad_GetVeterancyRank` / `Squad_GetVeterancyExperience` — Veterancy
- `Squad_GetProductionQueueCount` / `Squad_GetProductionQueueItem` — Queue
- `Squad_GetActiveCommand` — Current command
- `Squad_GetStateModelFloat/Int/Bool/Enum` — State model access
- `Squad_GetSquadCount` / `Squad_EntityAt` — Composition

### Setters
- `Squad_SetHealth` / `Squad_SetHealthMin` — Health
- `Squad_SetInvulnerable` / `Squad_SetInvulnerableMinCap` — Invulnerability
- `Squad_SetSelectable` / `Squad_SetWorldOwned` — Selection/ownership
- `Squad_SetStateModelFloat/Int/Bool/Enum` — State model
- `Squad_SetMoveType` / `Squad_SetMoveSpeedScaling` — Movement
- `Squad_SetVeterancyDisplayLevel` — Veterancy display

### Combat & Abilities
- `Squad_CanAttackEntity` / `Squad_CanAttackNow` — Attack checks
- `Squad_CanCastAbilityOnPosition/Entity/Squad/EGroup/SGroup` — Ability checks
- `Squad_CanTargetEntity` / `Squad_CanTargetSquad` — Targeting
- `Squad_HasAbility` / `Squad_AddAbility` / `Squad_RemoveAbility` — Abilities
- `Squad_HasWeapon` / `Squad_HasTeamWeapon` — Weapons
- `Squad_StopAbility` / `Squad_AdjustAbilityCooldown` — Ability management

### Upgrades & Production
- `Squad_CompleteUpgrade` / `Squad_RemoveUpgrade` / `Squad_NumUpgradeComplete` — Upgrades
- `Squad_HasUpgrade` / `Squad_IsUpgrading` — Upgrade checks
- `Squad_EnableProductionQueue` — Production control
- `Squad_CancelProductionQueueItem` — Queue management

### Movement & Position
- `Squad_WarpToPos` / `Squad_FacePosition` / `Squad_FaceSquad` — Teleport/face
- `Squad_TryFindClosestFreePosition` — Pathfinding helper
- `Squad_ForceFormationUpdate` / `Squad_ForceIdleFormationFacing` — Formation

---

## Entity_ (237 functions)
Individual entity management — buildings, units, resources.

### Creation & Destruction
- `Entity_Create` / `Entity_CreateENV` — Create entities
- `Entity_Spawn` / `Entity_DeSpawn` — Spawn control
- `Entity_Destroy` / `Entity_DestroyStrategicPoint` — Destruction
- `Entity_Kill` — Kill with effects

### State Queries
- `Entity_IsAlive` / `Entity_IsDead` — Life
- `Entity_IsBuilding` / `Entity_IsBurnable` — Type
- `Entity_IsStrategicPoint` / `Entity_IsStrategicPointCapturedBy` — Strategic points
- `Entity_IsOfType` — Blueprint type check
- `Entity_IsInvulnerable` / `Entity_IsSelectable` — Modifier state
- `Entity_IsProducing` / `Entity_IsUpgrading` — Production
- `Entity_IsPartOfSquad` — Composition
- `Entity_IsConstructionComplete` / `Entity_IsConstructionInProgress` — Building state

### Getters
- `Entity_GetHealth` / `Entity_GetHealthMax` / `Entity_GetHealthPercentage` — Health
- `Entity_GetPosition` / `Entity_GetHeading` — Position
- `Entity_GetBlueprint` / `Entity_GetPlayerOwner` — Identity
- `Entity_GetRadius` — Size
- `Entity_GetMaxHoldSquadSlots` — Garrison capacity
- `Entity_GetStateModelFloat/Int/Bool/Enum` — State model
- `Entity_GetSquad` — Owning squad

### Setters
- `Entity_SetHealth` / `Entity_ApplyHealthChange` — Health
- `Entity_SetInvulnerable` / `Entity_SetSelectable` — Modifier state
- `Entity_SetStateModelFloat/Int/Bool/Enum` — State model
- `Entity_SetHeading` / `Entity_WarpToPos` — Position
- `Entity_SetAnimatorState` / `Entity_SetAnimatorEvent` — Animation

### Building Functions
- `Entity_BuildImmediate` — Instant construction
- `Entity_ConvertBlueprint` — Change blueprint
- `Entity_SnapToGridAndGround` — Placement
- `Entity_HasAbility` / `Entity_CanAttackNow` — Capability checks

---

## SGroup_ (176 functions)
Squad group management — selections, filters, commands.

### Core Operations
- `SGroup_Create` / `SGroup_CreateIfNotFound` — Create groups
- `SGroup_Add` / `SGroup_AddGroup` / `SGroup_AddLeaders` — Add members
- `SGroup_Remove` / `SGroup_Clear` — Remove/clear
- `SGroup_Destroy` — Destroy group
- `SGroup_Exists` / `SGroup_FromName` — Lookup

### Targeting & Filtering
- `SGroup_Filter` / `SGroup_FilterCount` — Blueprint filtering
- `SGroup_FilterOnScreen` — Screen filter
- `SGroup_Intersection` — Set intersection
- `SGroup_ContainsBlueprint` / `SGroup_ContainsSquad` — Membership

### State Queries
- `SGroup_IsAlive` / `SGroup_IsEmpty` — Group state
- `SGroup_IsAttackMoving` / `SGroup_IsMoving` — Movement
- `SGroup_IsDugIn` / `SGroup_IsInHoldEntity` — Position
- `SGroup_IsFemale` / `SGroup_IsUnderAttack` — State checks
- `SGroup_CanCastAbilityOnPosition/Entity/Squad` — Ability checks

### Getters
- `SGroup_GetPosition` / `SGroup_GetAvgHealth` — Aggregate data
- `SGroup_GetSquadAt` / `SGroup_Count` / `SGroup_CountSpawned` — Members
- `SGroup_GetSpawnedSquadAt` — Spawned members
- `SGroup_TotalMembersCount` — Total entity count

### Setters
- `SGroup_SetSelectable` / `SGroup_SetInvulnerable` — Group properties
- `SGroup_SetPlayerOwner` — Ownership
- `SGroup_EnableSurprise` / `SGroup_EnableUIDecorator` — Visual state

### Combat & Movement
- `SGroup_Kill` / `SGroup_DeSpawn` — Destruction
- `SGroup_WarpToMarker` / `SGroup_WarpToPos` — Teleport
- `SGroup_FacePosition` — Orientation
- `SGroup_CompleteUpgrade` / `SGroup_IncreaseVeterancy` — Progression

---

## Player_ (166 functions)
Player state, resources, diplomacy, production capabilities.

### Resources
- `Player_AddResource` / `Player_SetResource` / `Player_GetResource` — Resource management
- `Player_GiftResource` — Tribute
- `Player_GetResourceRate` / `Player_GetResourceRateGathered` — Income rates
- `Player_ResetResource` — Reset

### Units & Buildings
- `Player_GetSquads` / `Player_GetEntities` / `Player_GetSquadsOnscreen` — Query
- `Player_GetSquadCount` / `Player_GetEntityCount` — Counts
- `Player_FindFirstOwnedEntityOfType` — Search
- `Player_OwnsEntity` / `Player_OwnsSquad` — Ownership
- `Player_CanConstruct` / `Player_CanSeeEntity` / `Player_CanSeeSquad` — Capability

### State & Identity
- `Player_IsAlive` / `Player_IsDead` — Life state
- `Player_IsHuman` — Human/AI check
- `Player_FromId` / `Player_GetID` — Identity
- `Player_GetRaceName` / `Player_GetDisplayName` — Info
- `Player_GetCurrentAge` — Age/era

### Production & Upgrades
- `Player_SetEntityProductionAvailability` / `Player_SetSquadProductionAvailability` — Lock/unlock production
- `Player_SetConstructionMenuAvailability` — Building menu
- `Player_SetUpgradeAvailability` — Upgrades
- `Player_CompleteUpgrade` / `Player_RemoveUpgrade` — Direct upgrade control

### Diplomacy
- `Player_ObserveRelationship` — Set relationship
- `Player_GetRelationship` — Query relationship

### Population
- `Player_GetPopCapCurrent` / `Player_GetPopCapMax` — Capacity
- `Player_SetPopCapOverride` / `Player_ClearPopCapOverride` — Override
- `Player_SetMaxPopulation` — Max pop

---

## UI_ (149 functions)
HUD, minimap, screen effects, event cues, decorators.

### Minimap
- `UI_CreateMinimapBlipOnSGroup` / `UI_CreateMinimapBlipOnEGroup` — Blips
- `UI_SetMinimapTrueNorth` — Orientation

### Event Cues & Messages
- `UI_CreateEventCueClickable` / `UI_CreateEventCueClickableByPlayer` — Event cues
- `UI_SystemMessage` / `UI_SystemMessageLarge` — System messages
- `UI_CreateKickerMessage` / `UI_CreateSpeechBubble` — Floating text

### Screen Effects
- `UI_ScreenFade` / `UI_LetterboxFade` — Fades
- `UI_TitleDestroy` / `UI_TitleStart` — Title cards

### Flash/Highlight
- `UI_FlashAbilityButton` / `UI_FlashEntity` / `UI_FlashMinimap` — Flash elements
- `UI_StopFlashingEntity` — Stop flash

### HUD Control
- `UI_SetForceShowSubtitles` / `UI_NewHUDFeature` — Display
- `UI_EnableSquadDecorator` / `UI_EnableEntityDecorator` — Decorators
- `UI_SetSkipNISCallback` — NIS control

### Tags
- `UI_CreateTagForPosition` / `UI_CreateTagForUID` — Create tags
- `UI_DestroyTagForPosition` — Remove tags

---

## EGroup_ (114 functions)
Entity group management — buildings, resources, strategic points.

Same pattern as SGroup_ but for entities: `Create`, `Add`, `Remove`, `Filter`, `ForEach`, `Count`, `GetEntityAt`, `ContainsEntity`, state checks, position queries, etc.

Key unique functions:
- `EGroup_SetBurnExtEnabled` — Enable/disable burning
- `EGroup_SortBasedOnHealth` — Health sorting
- `EGroup_InstantCaptureStrategicPoint` — Instant strategic point capture

---

## AI_ (139 functions)
Core AI system control.

- `AI_Enable` / `AI_DisableAll` / `AI_IsEnabled` — AI toggle
- `AI_SetDifficulty` / `AI_GetDifficulty` — Difficulty
- `AI_SetPersonality` / `AI_GetPersonality` — AI behavior profiles
- `AI_LockAll` / `AI_UnlockAll` — Lock AI actions
- `AI_AddPrefab` / `AI_SetPrefabCanReassign` — Prefab management
- `AI_ConvertToSimPlayer` — Convert AI player
- `AI_SetCaptureImportance` — Strategic priorities
- `AI_CombatFitness*` — Squad combat evaluation
- `AI_SquadDataDictionary*` — AI squad data storage

---

## AIEncounter_ (123 functions)
AI encounter configuration — combat, formation, targeting, fallback behaviors.

### Combat Guidance
- `AIEncounter_CombatGuidance_SetCombatRange` / `SetLeashRange` — Ranges
- `AIEncounter_CombatGuidance_SetIdleAttack` — Idle behavior

### Engagement
- `AIEncounter_EngagementGuidance_Set*` — 20+ engagement settings

### Fallback 
- `AIEncounter_FallbackGuidance_Set*` — 20+ fallback settings including retreat, reinforce

### Formation Phase
- `AIEncounter_FormationPhase_*` — Formation battle management

### Target
- `AIEncounter_TargetGuidance_SetSquadPatrolPathByName` — Patrol paths
- `AIEncounter_TargetGuidance_SetSquadPatrolWander` — Wander behavior

### Tactics
- `AIEncounter_TacticFilter_SetAbilityPriority` — Ability priority
- `AIEncounter_TacticFilter_Set*` — Tactic filtering

---

## World_ (99 functions)
World queries — proximity, entities, terrain, game state.

- `World_GetNeutralEntitiesNearMarker` — Neutral entity queries
- `World_GetEntitiesNearPoint/Marker` — Proximity searches
- `World_GetPlayerAt` / `World_GetPlayerCount` — Player queries
- `World_DistancePointToPoint` / `World_DistanceSquadToPoint` — Distance
- `World_GetHeightAt` / `World_IsTerrainPassable` — Terrain
- `World_OwnsEntity` / `World_OwnsSquad` — Ownership
- `World_Pos` — Position creation
- `World_KillPlayer` — Kill player
- `World_EndSP` — End single-player game

---

## AIPlayer_ (96 functions)
AI player management — scouting, pathing, resource management.

- `AIPlayer_UpdateSkirmishScoutingTasks` — Scouting
- `AIPlayer_CachedPathCrossesEnemyTerritory` — Path analysis
- `AIPlayer_GetClumpCentreSquad` — Cluster queries
- `AIPlayer_DebugClearIslandDecisionOverride` — Debug island AI

---

## Cmd_ (42 functions)
Issue commands to units/buildings.

- `Cmd_Move` / `Cmd_AttackMove` — Movement commands
- `Cmd_Attack` / `Cmd_AttackTarget` — Attack commands
- `Cmd_Garrison` / `Cmd_Unload` — Garrison commands
- `Cmd_Ability` / `Cmd_InstantUpgrade` — Production commands
- `Cmd_Stop` / `Cmd_Retreat` — Control commands
- `Cmd_BuildStructure` — Construction

---

## Camera_ (72 functions)
Camera control for cinematics and gameplay.

- `Camera_MoveToIfClose` / `Camera_MoveTo` — Movement
- `Camera_SetInputEnabled` — Player camera control
- `Camera_SetPitchRelative` — Angle
- `Camera_QueueRelativeSplinePanPos` — Spline animations
- `Camera_ResetRotation` — Reset

---

## Modify_ (80 functions)
Apply modifiers to entities/squads/players.

- `Modify_TargetPriority` — Targeting
- `Modify_PlayerExperienceReceived` — XP rates
- `Modify_WoodGatherRate` — Gather rates (per resource type)

---

## Game_ (71 functions)
Game state, settings, save/load.

- `Game_GetLocalPlayer` — Local player reference
- `Game_GetSPDifficulty` — Difficulty query
- `Game_SetVisibility` — Fog of war
- `Game_EndSP` — End game
- `Game_GetSaveGameFileSizeDev` — Dev utilities

---

## Sound_ / Music_ (66 functions)
Audio control.

- `Sound_SetMusicCombatMaxDistance` — Combat music range
- `Music_LockIntensity` — Lock music state

---

## Marker_ (26 functions)
Map marker queries.

- `Marker_GetPosition` / `Marker_GetDirection` — Position/direction
- `Marker_GetProximityRadiusOrDefault` — Radius
- `Marker_Exists` — Existence check

---

## Rule_ / Event_ (63 functions)
Rule system — intervals, one-shots, global events.

- `Rule_AddInterval` / `Rule_AddOneShot` — Timed rules
- `Rule_AddGlobalEvent` — Event listeners
- `Rule_Remove` / `Rule_RemoveAll` / `Rule_RemoveWithID` — Cleanup
- `Rule_RemoveGlobalEvent` — Remove event listeners
- `Event_IsFunctionQueuedOrRunning` — Check state
- `Event_GroupLeftAlive` — Group event hooks

---

## Timer_ (17 functions)
Timer management.

- `Timer_Start` / `Timer_End` — Create/destroy
- `Timer_GetElapsed` / `Timer_GetRemaining` — Query
- `Timer_Pause` / `Timer_Resume` — Control

---

## Objective_ (56 functions)
Objective management.

- `Objective_Start` / `Objective_Complete` / `Objective_Fail` — Lifecycle
- `Objective_IsStarted` / `Objective_IsComplete` — State
- `Objective_SetTitle` / `Objective_SetDescription` — Display
- `Objective_AddTimerBar` — Timer bars
- `Objective_AddGroundReticule` / `Objective_RemoveGroundReticule` — Map markers
- `Objective_StopTimer` / `Objective_ResumeTimer` — Timer control
- `Objective_TriggerTitleCard` — Title card display

---

## FOW_ (35 functions)
Fog of War control.

- `FOW_EnableTint` — Tint control
- `FOW_RevealArea` / `FOW_RevealAll` — Reveal
- `FOW_PlayerRevealEntity/Squad` — Per-unit reveal

---

## Util_ (90 functions)
General-purpose utilities.

- `Util_Comparison` — Value comparison helper
- `Util_ClearSquadsForCine` — Cinematic prep
- `Util_CreateSquads` — Squad creation helper

---

## Misc_ (78 functions)
Miscellaneous queries and utilities.

- `Misc_IsEGroupSelected` / `Misc_IsSGroupSelected` — Selection checks
- `Misc_IsEntityOnScreen` / `Misc_IsSquadOnScreen` — Screen checks
- `Misc_GetMouseOverSquad` — Mouse hover
- `Misc_AbortToFE` — Return to frontend

---

## BP_ (57 functions)
Blueprint operations.

- `BP_GetName` — Get blueprint name string
- `BP_GetSquadBlueprint` / `BP_GetEntityBlueprint` / `BP_GetUpgradeBlueprint` — Get specific BPs
- `BP_GetAIFormationTargetPriorityBlueprint` — AI priority

---

## Other Categories

| Category | Count | Purpose |
|----------|-------|---------|
| `Prox_` | 23 | Proximity checks between groups/positions |
| `Training_` | 22 | Training/tutorial system |
| `Location_` | 22 | MissionOMatic location modules |
| `Army_` | 20+ | Army system (see army.scar) |
| `HintPoint_` | 17 | Hint point creation/management |
| `Modifier_` | 16 | Modifier application/removal |
| `SyncWeapon_` | 9 | Sync weapon (team weapon) management |
| `Territory_` | 9 | Territory/sector control |
| `NIS_` | 8 | Non-interactive sequence (cutscene) |
| `Network_` | 5 | Network events/callbacks |
| `Decal_` | 5 | Ground decal management |
| `Table_` | 12 | Lua table utilities |
| `Formation_` | 3 | Formation management |
| `Team_` | 3 | Team operations |
| `StateTree_` | 3 | State tree management |
