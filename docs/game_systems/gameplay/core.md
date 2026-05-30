# Gameplay: Core Systems

## OVERVIEW

The core gameplay library provides the foundational SCAR scripting infrastructure for Age of Empires IV campaigns and game modes. It encompasses the initialization pipeline (`gamesetup.scar` → `cardinal.scar` → `Core.scar`), the objective lifecycle system, AI encounter management with plan-based phases, campaign UI panels (tribute/reinforcement), narrative cinematic tooling, unit spawning/despawning, formation systems, resource gathering utilities, team management, and type-to-blueprint resolution. These files are imported by every campaign mission and many multiplayer game modes; they define the public API surface that mission scripts call into.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| autotest.scar | other | Autotest helpers for spawning units from blueprint tables at random spawn points |
| campaignpanel.scar | core | Campaign tribute & reinforcement panel UI — resource trading and purchasable items |
| cardinal.scar | core | Project-level setup: age/color/music/audio constants, objective type definitions, player age management, cinematic mode, type-to-blueprint resolver, UnitEntry delegates |
| cardinal_encounter.scar | core | Mid-layer between script encounters and AI encounters; splits large groups into sub-encounter families |
| cardinal_narrative.scar | core | Narrative utilities: cheering, leader crowns, speech playback, corpse fields, camera splines, cinematic mode toggles |
| core_encounter.scar | core | SCAR encounter framework: creation, phase transitions, plan registration, AI notification routing |
| designerlib.scar | core | Designer-facing helpers: random table items, table utilities, resource enable/disable, production queue counting |
| gamesetup.scar | core | Legacy mission initialization pipeline: player setup → variables → difficulty → restrictions → preset → objectives → NIS → start |
| gathering_utility.scar | core | Villager resource gathering assignment: find resources, assign to gold/stone/wood/berries/sheep/deer/fish/farms |
| markerpaths.scar | core | Minimap path rendering and marker-based squad movement along spline-defined paths |
| mission.scar | core | Mission completion/failure flow with NIS, stinger, splash screen, and Game_EndSP calls |
| network.scar | core | Deterministic network event broadcast for MP-safe callbacks; string.split utility |
| objectives.scar | objectives | Full objective lifecycle: register, start, complete, fail, stop, timers, counters, UI elements, pings, health bars, ground reticules |
| shieldwall.scar | core | Shield wall formation: multi-row positioning with backfill, damage modifiers, auto-replacement on kill |
| team.scar | core | Team management: player sorting into ALLIES/ENEMIES, team resource/building queries |
| unitexit.scar | core | Unit exit/despawn system: move-to-and-despawn, staggered removal, exit type registration |

## FUNCTION INDEX

### Cardinal & Setup

| Function | File | Purpose |
|----------|------|---------|
| `Player_GetCurrentAge` | cardinal.scar | Returns player age (1-4) via upgrade checks |
| `Player_SetCurrentAge` | cardinal.scar | Grants/removes age upgrades to set player age |
| `Player_SetMaximumAge` | cardinal.scar | Locks construction menus to cap age progression |
| `Player_GetMaximumAge` | cardinal.scar | Returns max allowed age from state model |
| `Player_SetMutualRelationships` | cardinal.scar | Sets all player-pairs to same relationship |
| `Cardinal_ConvertTypeToSquadBlueprint` | cardinal.scar | Resolves unit type strings to squad blueprints |
| `Cardinal_ConvertTypeToEntityBlueprint` | cardinal.scar | Resolves type strings to entity blueprints |
| `Cmd_FormationMove` | cardinal.scar | Formation move with optional delete-on-arrival |
| `Cmd_FormationAttackMove` | cardinal.scar | Formation attack-move with optional cleanup |
| `Cmd_FormationMoveToAndDestroy` | cardinal.scar | Formation move then destroy on arrival |
| `Cmd_FormationStop` | cardinal.scar | Stops formation movement |
| `SGroup_FormationWarpToMarker` | cardinal.scar | Instant teleport in formation to marker |
| `SGroup_FormationWarpToPos` | cardinal.scar | Instant teleport in formation to position |
| `Project_UnitEntry_PreprocessDeployment` | cardinal.scar | Filters units by difficulty, resolves type→SBP |
| `Project_UnitEntry_EndDeployment` | cardinal.scar | Groups units by destination for formation moves |

### Game Setup & Mission Flow

| Function | File | Purpose |
|----------|------|---------|
| `OnGameSetup` | gamesetup.scar | Frame-1 entry: calls Mission_SetupPlayers |
| `OnInit` | gamesetup.scar | Main init: variables → difficulty → prefabs → objectives → NIS |
| `Mission_Complete` | mission.scar | Triggers victory flow with NIS/movie/stinger/splash |
| `Mission_Fail` | mission.scar | Triggers failure flow with splash/stinger |
| `Mission_CompleteSkipOutro` | mission.scar | Victory without outro NIS |
| `Mission_PreFail` | mission.scar / gamesetup.scar | Camera pan + fullscreen before fail |
| `_gameOver_message` | cardinal.scar | Displays victory/defeat stinger UI |
| `CheatMenu_RegisterCheatFunction` | gamesetup.scar | Adds debug cheat to mission restart menu |
| `CheatMenu_AddMenuItem` | gamesetup.scar | Registers cheat menu item in debug console |

### Encounter System

| Function | File | Purpose |
|----------|------|---------|
| `Encounter_Create` | core_encounter.scar | Creates SCAR encounter with plan and units |
| `Encounter_SetGoalData` | core_encounter.scar | Updates goal data, restarts encounter |
| `Encounter_GetGoalData` | core_encounter.scar | Returns original goal data table |
| `Encounter_Stop` | core_encounter.scar | Stops an active encounter |
| `Encounter_Start` | core_encounter.scar | Resumes a stopped encounter |
| `Encounter_Restart` | core_encounter.scar | Forces full encounter restart |
| `Encounter_IsActive` | core_encounter.scar | Returns whether encounter is running |
| `Encounter_AddSGroup` | core_encounter.scar | Adds squads to encounter, restarts phase |
| `Encounter_RemoveSGroup` | core_encounter.scar | Removes squads, ends phase if empty |
| `Encounter_GetSGroup` | core_encounter.scar | Returns encounter's SGroup |
| `Encounter_GetAIEncounter` | core_encounter.scar | Returns underlying AI encounter |
| `Encounter_RegisterPlan` | core_encounter.scar | Registers an encounter plan type |
| `Encounter_BeginNewPhase` | core_encounter.scar | Starts a new encounter phase |
| `Encounter_FindAssociatedEncounter` | core_encounter.scar | Finds encounter by squad/sgroup/ID |
| `Cardinal_CreateAIEncounterWithStateModelTunings` | cardinal_encounter.scar | Creates AI encounter, splits large groups into families |
| `Cardinal_CleanupAIEncounter` | cardinal_encounter.scar | Tears down encounter families and children |
| `AIEncounter_TargetGuidance_SetTarget` | core_encounter.scar | Sets encounter target from various types |

### Objectives

| Function | File | Purpose |
|----------|------|---------|
| `Objective_Register` | objectives.scar | Registers objective with Obj_Create and callbacks |
| `Objective_Start` | objectives.scar | Activates objective with optional titlecard/intel |
| `Objective_Complete` | objectives.scar | Completes objective with presentation queue |
| `Objective_Fail` | objectives.scar | Fails objective with presentation queue |
| `Objective_Stop` | objectives.scar | Returns objective to waiting-to-start state |
| `Objective_UpdateText` | objectives.scar | Updates title/description with optional titlecard |
| `Objective_Show` | objectives.scar | Shows/hides objective from UI |
| `Objective_IsComplete` | objectives.scar | Checks completion status |
| `Objective_IsFailed` | objectives.scar | Checks failure status |
| `Objective_IsStarted` | objectives.scar | Checks if objective has been started |
| `Objective_AreAllPrimaryObjectivesComplete` | objectives.scar | Returns true when all primaries done |
| `Objective_GetSubObjectives` | objectives.scar | Returns table of child objectives |
| `Objective_AreSubObjectivesComplete` | objectives.scar | Checks ALL/ANY sub-objective completion |
| `Objective_AddUIElements` | objectives.scar | Adds pings/hintpoints/arrows to objective |
| `Objective_RemoveUIElements` | objectives.scar | Removes UI elements by element ID |
| `Objective_BlinkUIElements` | objectives.scar | Blinks hintpoint/arrows for attention |
| `Objective_AddPing` | objectives.scar | Adds minimap blip to objective |
| `Objective_RemovePing` | objectives.scar | Removes minimap blip by ping ID |
| `Objective_AddAreaHighlight` | objectives.scar | Adds circle/square map highlight |
| `Objective_AddGroundReticule` | objectives.scar | Adds visual ground splat |
| `Objective_RemoveGroundReticule` | objectives.scar | Removes ground reticule by ID |
| `Objective_AddHealthBar` | objectives.scar | Adds health bar tied to unit |
| `Objective_AddTimerBar` | objectives.scar | Adds timer bar for objective countdown |
| `Objective_StartTimer` | objectives.scar | Starts COUNT_UP or COUNT_DOWN timer |
| `Objective_TriggerTitleCard` | objectives.scar | Manual titlecard placement in intel events |
| `Objective_TogglePings` | objectives.scar | Toggles minimap blips on/off |

### Campaign Panel (Tribute & Reinforcement)

| Function | File | Purpose |
|----------|------|---------|
| `CampaignPanel_Init` | campaignpanel.scar | Initializes shared panel state and XAML UI |
| `TributePanel_Init` | campaignpanel.scar | Sets callback for tribute sends |
| `TributePanel_Create` | campaignpanel.scar | Creates tribute panel for owner→recipients |
| `TributePanel_Enable` / `_Disable` | campaignpanel.scar | Shows/hides tribute panel |
| `TributePanel_AddRecipient` | campaignpanel.scar | Adds player to tribute recipient list |
| `TributePanel_RemoveRecipient` | campaignpanel.scar | Removes player from recipient list |
| `TributePanel_EnableResourceType` | campaignpanel.scar | Enables specific resource type for sending |
| `TributePanel_DisableResourceType` | campaignpanel.scar | Disables resource type with optional reason |
| `ReinforcementPanel_Init` | campaignpanel.scar | Sets callback for item purchases |
| `ReinforcementPanel_Create` | campaignpanel.scar | Creates reinforcement panel with item list |
| `ReinforcementPanel_Enable` / `_Disable` | campaignpanel.scar | Shows/hides reinforcement panel |
| `ReinforcementPanel_AddItem` | campaignpanel.scar | Adds purchasable item to panel |
| `ReinforcementPanel_RemoveItem` | campaignpanel.scar | Removes item from panel |
| `ReinforcementPanel_UpdateItem` | campaignpanel.scar | Updates item data (cost, text, etc.) |
| `ReinforcementPanel_DisableItem` | campaignpanel.scar | Disables item with reason text |
| `ReinforcementPanel_EnableItem` | campaignpanel.scar | Re-enables disabled item |

### Narrative & Cinematic

| Function | File | Purpose |
|----------|------|---------|
| `SGroup_EnableCheering` | cardinal_narrative.scar | Triggers cheer animation/walla with duration |
| `SGroup_EnableLeaderCrown` | cardinal_narrative.scar | Shows/hides crown on leader units |
| `SGroup_PlaySpeech` | cardinal_narrative.scar | Plays speech audio on first squad |
| `Util_EnableCardinalCinematicMode` | cardinal_narrative.scar | Enters/exits intro/outro camera mode with FOW/UI |
| `Util_PlayCameras` | cardinal_narrative.scar | Runs series of camera splines with speech/functions |
| `Util_ClearSquadsForCine` | cardinal_narrative.scar | Destroys all squads for outro cinematics |
| `Util_CorpseField` | cardinal_narrative.scar | Spawns and kills units to create corpse fields |
| `Util_UnitParade` | cardinal_narrative.scar | Spawns units moving along path in parade formation |
| `Util_UnitParadeGrid` | cardinal_narrative.scar | Spawns units in grid formation along waypoints |
| `Mission_EnableAbilities` | cardinal_narrative.scar | Enables/disables ability groups for players |
| `MissionOMatic_ShowTitleCard` | cardinal_narrative.scar | Shows mission title card from recipe data |

### Unit Exit & Spawning

| Function | File | Purpose |
|----------|------|---------|
| `Util_ExitSquads` | unitexit.scar | High-level squad despawn with exit type |
| `UnitExit_CompleteAllImmediately` | unitexit.scar | Forces all in-progress exits to finish |
| `Autotest_SpawnFromTable` | autotest.scar | Spawns units from structured blueprint table |

### Designer Library

| Function | File | Purpose |
|----------|------|---------|
| `Table_GetRandomItem` | designerlib.scar | Returns random item(s) from table |
| `Table_GetRandomItemWeighted` | designerlib.scar | Weighted random selection from table |
| `Table_Contains` | designerlib.scar | Checks if table contains item |
| `Table_Copy` | designerlib.scar | Deep copies a table |
| `Table_MakeReadOnly` | designerlib.scar | Makes table read-only with error on write |
| `Resources_Disable` / `Resources_Enable` | designerlib.scar | Toggles resource income via modifiers |
| `Player_GetSquadsOnscreen` | designerlib.scar | Fills sgroup with on-screen squads |
| `Player_GetProductionQueueSize` | designerlib.scar | Counts total units in production |

### Gathering Utility

| Function | File | Purpose |
|----------|------|---------|
| `Gathering_FindAllResources` | gathering_utility.scar | Populates egroups with all map resources by type |
| `Gathering_AssignVillagersToGather` | gathering_utility.scar | Generic villager→resource assignment |
| `Gathering_AssignVillagersToGold` | gathering_utility.scar | Assigns villagers to gold deposits |
| `Gathering_AssignVillagersToWood` | gathering_utility.scar | Assigns villagers to wood deposits |
| `Gathering_AssignVillagersToStone` | gathering_utility.scar | Assigns villagers to stone deposits |
| `Gathering_AssignVillagersToBerries` | gathering_utility.scar | Assigns villagers to berry bushes |
| `Gathering_AssignVillagersToFarms` | gathering_utility.scar | Assigns villagers to farms |
| `Gathering_AssignVillagersToSheep` | gathering_utility.scar | Assigns villagers to sheep |

### Shield Wall

| Function | File | Purpose |
|----------|------|---------|
| `ShieldWall_Create` | shieldwall.scar | Creates multi-row shield wall between two positions |
| `ShieldWall_Release` | shieldwall.scar | Releases units from wall formation |
| `ShieldWall_AddSGroup` | shieldwall.scar | Adds reinforcements to wall backfill |

### Team

| Function | File | Purpose |
|----------|------|---------|
| `Team_DefineAllies` | team.scar | Returns up to 4 ally player IDs |
| `Team_DefineEnemies` | team.scar | Returns up to 4 enemy player IDs |
| `Team_IsAlive` | team.scar | Returns if any team member is alive |
| `Team_HasBuilding` | team.scar | Checks if team owns specific buildings |
| `Team_GetAll` | team.scar | Fills sgroup/egroup with team's units |
| `Team_AddResource` | team.scar | Adds resources to all team members |

### Network

| Function | File | Purpose |
|----------|------|---------|
| `Network_RegisterEvent` | network.scar | Registers callback for broadcast messages |
| `Network_CallEvent` | network.scar | Broadcasts MP-safe event with message string |
| `Network_Callback` | network.scar | GE_BroadcastMessage handler that dispatches events |

### Marker Paths

| Function | File | Purpose |
|----------|------|---------|
| `MarkerPaths_MoveSGroupAlongPath` | markerpaths.scar | Queued formation moves along named markers |
| `MarkerPaths_AttackMoveSGroupAlongPath` | markerpaths.scar | Queued attack-moves along named markers |
| `MarkerPaths_GenerateIcons` | markerpaths.scar | Creates directional minimap path icons |
| `MarkerPaths_ClearIcons` | markerpaths.scar | Removes minimap path display |
| `MarkerPaths_AnimateArrowPath` | markerpaths.scar | Animates directional arrows along path |

## KEY SYSTEMS

### Objective Types
- `OT_Primary` — Main mission objectives (default style)
- `OT_Secondary` — Sub-objectives (auto-assigned when Parent is set)
- `OT_Bonus` / `ObjectiveType_Bonus` — Optional bonus objectives
- `OT_Information` / `OT_Warning` — Informational/warning notifications
- `ObjectiveType_Battle` — Battle-specific UI template
- `ObjectiveType_Build` — Construction-specific UI template
- `ObjectiveType_Capture` — Capture-specific UI template
- `ObjectiveType_Optional` — Optional objective template
- `ObjectiveType_Tip` — Tutorial tip objectives
- `ObjectiveType_LeaderInjured` — Leader health warning
- `ObjectiveType_TugOfWar` — Strength tug-of-war bar display
- `ObjectiveType_Unrest` — Unrest meter display

### Objective Lifecycle
1. `Objective_Register()` — Creates objective with Obj_Create, sets up callbacks
2. `Objective_Start()` — Queues start presentation (titlecard + intel event)
3. Active phase — timers, counters, health bars, UI elements managed by `Objective_Manager` (1s interval)
4. `Objective_Complete()` / `Objective_Fail()` — Queued end presentation with stinger
5. Presentation lock (`__Objective_PresentationLock`) ensures sequential processing

### Encounter Plan System
- Plans are registered via `Encounter_RegisterPlan()` with name, start function, phases table, and optional defaults
- Built-in plans imported: `Plan_Attack`, `Plan_Defend`, `Plan_TownLife`, `Plan_Move`, `Plan_DoNothing`
- Each plan defines phases with `startFunction`, `endFunction`, and `aiNotificationFunction`
- Encounters transition between phases via `_Encounter_TransitionToPhase()`
- Cardinal layer (`cardinal_encounter.scar`) handles splitting large encounters into families of sub-encounters (cluster limit: 50 units per sub-encounter)
- Siege tower special case: forces encounter family creation for squad release handling

### Age System
- Constants: `AGE_DARK=1`, `AGE_FEUDAL=2`, `AGE_CASTLE=3`, `AGE_IMPERIAL=4`
- Age checked via upgrade presence (`feudal_age`, `castle_age`, `imperial_age`)
- `Player_SetMaximumAge()` removes construction menus and landmark options per civ prefix
- Special handling for Abbasid wing upgrades (ages via research not landmarks)

### Music & Audio
- Combat intensity mapping: thresholds at 0/575/2000/3500/8200 control music state
- Objective stingers: separate audio for start/complete/fail per objective type
- Walla events: small/medium/large variants for celebrate/engage/fear/spearwall/charge
- Cinematic audio: `MIX_START_INTRO_CAM`, `MIX_RETURN_TO_GAME`, `MIX_START_OUTRO_CAM`

### Campaign Panel
- Single XAML-based UI serves both tribute and reinforcement features
- Tribute: network-safe via `Network_CallEvent` → `_TributePanel_Send_ReceieveNetworkMessage`
- Reinforcement: items have costs (food/wood/gold/stone/population), auto-disable when insufficient
- Message format: pipe-separated player tributes, comma-separated resource values
- Manager rule continuously checks resource sufficiency and updates dirty UI state

### Initialization Pipeline (gamesetup.scar)
1. `OnGameSetup()` → `Mission_SetupPlayers()`
2. `PreInit()` / `OnInit()` → Variables → Difficulty → Prefabs → Restrictions → Preset → Objectives → NIS
3. `_StartMission()` → Camera position → `Mission_Start()` (1s delay) → Title cards
4. Cheat system: persistent values via debug console, mission restart with cheat function

### Type-to-Blueprint Resolver
- `Cardinal_ConvertTypeToSquadBlueprint(typeList, player)`: resolves string type lists (e.g. `"cavalry_light"`) to SBPs
- Caches results by civ × age × type combination for performance
- Auto-detects civilization from player, age from type tags (`scar_age1`–`scar_age4`)
- Campaign proxy races mapped to underlying races (e.g., Lithuania → HRE, Il-Khanate → Mongol)

### Unit Exit System
- `EXIT.No_Type` — Immediate despawn
- `EXIT.MoveToAndDespawn` — Move to location, despawn within range
- Manager rule (0.5s interval) handles staggered despawns and stuck-unit re-orders
- `UnitExit_CompleteAllImmediately()` for cinematic cleanup

### Shield Wall
- Multi-row formation between two points with configurable spacing (1.2 unit, 1.0 row)
- Front-row units get 3x damage, 0.75x received damage, max block rates
- Auto-replacement: killed wall units replaced from row behind, then backfill pool
- `ShieldWall_Release()` removes all modifiers and hold-position commands

### Network Events
- `Network_RegisterEvent()` assigns integer IDs to callback function names
- `Network_CallEvent()` broadcasts via `Command_PlayerBroadcastMessage` for MP determinism
- `Network_Callback()` dispatches `GE_BroadcastMessage` to matching registered functions
- Used by campaign panel for tribute sends and reinforcement purchases

## CROSS-REFERENCES

### Import Chain
```
cardinal.scar
  ├── import("Core.scar")
  ├── import("GameScarUtil.scar")
  ├── import("Prefabs.scar")
  ├── import("replay/replaystatviewer.scar")
  └── import("ui/vizierui.scar")

gamesetup.scar
  ├── import("GameScarUtil.scar")
  ├── import("Prefabs.scar")
  └── import("GameFunctions.scar")

core_encounter.scar
  ├── import("EncounterPlans/Plan_Attack.scar")
  ├── import("EncounterPlans/Plan_Defend.scar")
  ├── import("EncounterPlans/Plan_TownLife.scar")
  ├── import("EncounterPlans/Plan_Move.scar")
  └── import("EncounterPlans/Plan_DoNothing.scar")

campaignpanel.scar
  └── import("Cardinal.scar")

gathering_utility.scar
  └── import("scarutil.scar")
```

### Key Globals
- `g_missionData` — Mission configuration (objectives, NIS, title cards, start camera, difficulty)
- `__t_Objectives` — Registry of all objective tables
- `t_coreEncounter_allEncounters` — All active SCAR encounters
- `t_coreEncounter_allPlans` — All registered encounter plans
- `t_cardinalEncounters_allFamilies` — Active encounter families (split encounters)
- `_t_campaignPanel` — Campaign panel state (tribute + reinforcement UI data)
- `PLAYERS` — Player table used by broadcast system
- `TEAM_ALLIES` / `TEAM_ENEMIES` / `TEAM_HUMANS` — Sorted team lists
- `RACE` — Pre-populated race ID table (used by type-to-blueprint)
- `content_pack` — Content pack identifier for conditional logic

### Inter-File Function Calls
- `cardinal.scar` calls `Core_CallDelegateFunctions("RegisterEncounterPlans")` → triggers `Project_RegisterEncounterPlans()`
- `core_encounter.scar` calls `_Encounter_AINotificationCallback` which `cardinal_encounter.scar` intercepts via `_CardinalEncounter_AINotificationCallback`
- `gamesetup.scar` calls `Objective_Register()` from `objectives.scar` during `_InitializeObjectives()`
- `campaignpanel.scar` calls `Network_RegisterEvent` / `Network_CallEvent` from `network.scar`
- `cardinal_narrative.scar` calls `Util_EnableCardinalCinematicMode` which uses `Util_FullscreenMode` / `Util_EnterCinematicMode` from `GameScarUtil.scar`
- `mission.scar` calls `_gameOver_message` defined in `cardinal.scar`
- `cardinal.scar` `Project_UnitEntry_*` delegates are called by the UnitEntry system in `Core.scar`
- `gathering_utility.scar` uses `sg_single`, `eg_single`, `eg_temp` temp groups from `scarutil.scar`
