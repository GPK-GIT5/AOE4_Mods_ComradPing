# Gameplay: MissionOMatic Framework

## OVERVIEW

MissionOMatic is the core mission runtime framework used by ALL Age of Empires IV campaign missions. It consumes a declarative **recipe** (a Lua table returned by `GetRecipe()`) and initializes all locations, AI behaviour modules, battalions, objectives, and metrics. The framework is built around a modular architecture: **Conditions** evaluate boolean state, **Actions** execute game logic, **Playbills** sequence condition/action blocks, and **Objectives** bridge these systems to the player-facing HUD. Behaviour **Modules** (TownLife, Defend, Attack, RovingArmy, UnitSpawner) manage AI unit groups through Encounter-based goals, with a reinforcement/unit-request pipeline connecting producers to consumers. Supporting subsystems handle waves (timed unit spawning from buildings), raiding (autonomous roaming attacks), leaders (hero downed/recovery state), upgrades (per-civ age-gated unlock tables), and mission reporting.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| missionomatic.scar | core | Main entry point; imports all subsystems, processes recipe, initializes players/locations/modules/objectives |
| missionomatic_actionlist.scar | core | Runs ordered lists of named actions with async support via `WAIT_FOR_ACTION_TO_FINISH` |
| missionomatic_conditionlist.scar | core | Evaluates boolean condition lists (ALL/ANY/NONE) for objectives and playbills |
| missionomatic_objectives.scar | objectives | Registers, starts, and monitors player-facing objectives from recipe data |
| missionomatic_playbills.scar | core | Manages sequenced condition→action stages with parallel sequence support |
| missionomatic_wave.scar | spawns | Spawns units from buildings with per-type build-time cooldowns, staging/assault flow |
| missionomatic_utility.scar | core | UnitTable helpers, formation constants, spawn resolution, module dissolve, villager assignment |
| missionomatic_upgrades.scar | data | Per-civilization, per-age tables of unit upgrades, research, and squad production unlocks |
| missionomatic_custommetrics.scar | other | Plugin system for recipe-defined end-of-mission metrics |
| missionomatic_leader.scar | core | Hero/leader unit surrender-and-recovery lifecycle with neutral holder transfer |
| missionomatic_raiding.scar | spawns | Autonomous raid party management with probe scouts, exclusion timers, target cycling |
| missionomatic_reporting.scar | other | Generates post-mission report (battalions, objectives, metrics) for metagame |
| missionomatic_allybanners.scar | other | Allied banner-controlled armies with auto-reinforcement monitoring |
| missionomatic_artofwar.scar | other | Art of War / Challenge mission timer and medal benchmark system |
| module_attack.scar | automated | Attack module — units assault a target position via Encounter goals |
| module_defend.scar | automated | Defend module — units hold a position with optional withdrawal conditions |
| module_rovingarmy.scar | automated | RovingArmy module — mobile force cycling through target waypoints |
| module_townlife.scar | automated | TownLife module — AI economy, building, and unit production via skirmish AI |
| module_unitspawner.scar | spawns | UnitSpawner module — off-map or on-map unit spawning as a unit provider |
| module_common.scar | core | Shared AI module helpers: combat area resolution, module lookup from encounter |

---

## FUNCTION INDEX

### Core Framework (missionomatic.scar)

| Function | File | Purpose |
|----------|------|---------|
| MissionOMatic_OnInit | missionomatic.scar | Top-level init: global SGroups, resources, subsystems |
| MissionOMatic_Preset | missionomatic.scar | Processes recipe: locations, modules, battalions, objectives |
| MissionOMatic_PreStart | missionomatic.scar | Runs preStart actions and introNIS from recipe |
| MissionOMatic_Start | missionomatic.scar | Fades in, runs onStart actions, triggers objectives |
| MissionOMatic_SetupPlayer | missionomatic.scar | Creates player from recipe with age/civ settings |
| MissionOMatic_InitializeModule | missionomatic.scar | Dispatches module init by type (Defend, Attack, etc.) |
| MissionOMatic_FindModule | missionomatic.scar | Looks up a module by descriptor string |
| MissionOMatic_EndMission | missionomatic.scar | Triggers win/loss with optional custom debrief |

### Action System (missionomatic_actionlist.scar)

| Function | File | Purpose |
|----------|------|---------|
| ActionList_Init | actionlist | Imports action scripts by name, resolves functions |
| ActionList_PlayActions | actionlist | Queues an action list with context and callback |
| ActionList_Manager | actionlist | Per-frame rule processing queued action lists |
| Action_Do | actionlist | Dispatches a single action to its `Action_<name>_Do` |
| Action_Finish | actionlist | Callback signaling an async action completed |
| Action_StartObjective_Do | actionlist | Starts an objective with optional sub-objectives |
| Action_CompleteObjective_Do | actionlist | Completes an objective |
| Action_FailObjective_Do | actionlist | Fails an objective |
| Action_Wait_Do | actionlist | Delays action list for N seconds |
| Action_CallScarFunction_Do | actionlist | Calls arbitrary SCAR function by name |
| Action_PlaySpeechEvent_Do | actionlist | Plays intel speech event, waits for completion |
| Action_SpawnUnits_Do | actionlist | Spawns units at a location |
| Action_SpawnUnitsToModule_Do | actionlist | Spawns units into a behaviour module |
| Action_DissolveModuleIntoModule_Do | actionlist | Transfers units between modules |
| Action_MissionComplete_Do | actionlist | Triggers mission victory |
| Action_MissionFail_Do | actionlist | Triggers mission failure |
| Action_SetMusicIntensity_Do | actionlist | Locks/unlocks music intensity |
| Action_Loop_Do | actionlist | Loops a playbill back to a given stage |
| Action_BookmarkTime_Do | actionlist | Creates a named game-time timestamp |
| Action_ExpositionCamera_Do | actionlist | Plays exposition camera sequence |
| Action_NotifyPlayer_Do | actionlist | Creates event cue, minimap blip, FOW reveal |

### Condition System (missionomatic_conditionlist.scar)

| Function | File | Purpose |
|----------|------|---------|
| ConditionList_CheckList | conditionlist | Evaluates a list of conditions (wraps in ALL) |
| ConditionList_CheckItem | conditionlist | Evaluates a single condition item |
| Condition_Boolean_Check | conditionlist | ALL/ANY/NONE boolean combinator |
| Condition_GameTime_Check | conditionlist | Checks elapsed game time against threshold |
| Condition_HasUnits_Check | conditionlist | Checks player unit count, optionally by type/tag |
| Condition_HasBuildings_Check | conditionlist | Checks player building count by type |
| Condition_UnitAtLocation_Check | conditionlist | Checks if units are near a marker/location |
| Condition_ModuleDefeated_Check | conditionlist | Checks if a module's units are all dead |
| Condition_ObjectiveIsComplete_Check | conditionlist | Checks objective completion status |
| Condition_SubobjectivesAreComplete_Check | conditionlist | Checks if child objectives are complete |
| Condition_UnitsSpotted_Check | conditionlist | Checks if player can see tagged/module units |
| Condition_UnitsKilled_Check | conditionlist | Checks if tagged/module units are all dead |
| Condition_AskScarFunction_Check | conditionlist | Calls arbitrary function as condition |
| Condition_LocationCaptured_Check | conditionlist | Checks if a location has been captured |

### Objective System (missionomatic_objectives.scar)

| Function | File | Purpose |
|----------|------|---------|
| MissionOMatic_InitializeObjective | objectives | Creates and registers an objective from recipe data |
| MissionOMatic_TriggerStartingObjectives | objectives | Starts objectives marked `isStartingObjective` |
| MissionOMatic_FindObjective | objectives | Looks up objective by ID, table, or descriptor |
| Recipe_AddObjectives | objectives | Dynamically adds objectives to a recipe |
| Objective_TransitionTo | objectives | Plays VO/CTAs then starts a new objective |
| MissionOMatic_ObjectiveCallback_OnStart | objectives | Runs start actions, kicks off playbill/timer/counter |
| MissionOMatic_ObjectiveCallback_CheckForComplete | objectives | Evaluates complete.conditions every second |
| MissionOMatic_ObjectiveCallback_OnComplete | objectives | Runs complete actions, stops playbill |
| MissionOMatic_Objective_SetupHintpoints | objectives | Adds UI elements (blips, arrows, reticules) |

### Playbill System (missionomatic_playbills.scar)

| Function | File | Purpose |
|----------|------|---------|
| Playbill_Start | playbills | Starts parallel condition/action sequences |
| Playbill_Stop | playbills | Stops all sequences with a given ID |
| Playbill_Manager | playbills | Per-second rule checking conditions/running actions |

### Wave System (missionomatic_wave.scar)

| Function | File | Purpose |
|----------|------|---------|
| Wave_New | wave | Creates a new wave with unit table and spawn config |
| Wave_Prepare | wave | Begins spawning units into staging/assault modules |
| Wave_Launch | wave | Transfers staged units into assault module |
| Wave_SetUnits | wave | Updates wave unit composition |
| Wave_Monitor | wave | Per-second build monitoring across all waves |
| Wave_SpawnUnits | wave | Spawns units at available spawn buildings |
| Wave_FilterUnitsByDifficulty | wave | Removes units not matching current difficulty |

### Module: Attack (module_attack.scar)

| Function | File | Purpose |
|----------|------|---------|
| Attack_Init | module_attack | Spawns units, creates Attack encounter |
| Attack_Monitor | module_attack | Checks reinforcement needs every 5s |
| Attack_Disband | module_attack | Stops module, returns units to SGroup |
| Attack_UpdateTargetLocation | module_attack | Changes encounter target dynamically |
| Attack_UnitRequest_Start | module_attack | Provides units to other modules on request |

### Module: Defend (module_defend.scar)

| Function | File | Purpose |
|----------|------|---------|
| Defend_Init | module_defend | Spawns units, creates Defend encounter |
| Defend_Monitor | module_defend | Checks flee conditions & reinforcement needs |
| Defend_CreateEncounter | module_defend | Sets encounter goal with combat/leash ranges |
| Defend_Disband | module_defend | Stops module and cleans up |
| Defend_UpdateTargetLocation | module_defend | Relocates defend position |
| Defend_UnitRequest_Start | module_defend | Provides units, then back-fills from TownLife |

### Module: RovingArmy (module_rovingarmy.scar)

| Function | File | Purpose |
|----------|------|---------|
| RovingArmy_Init | module_rovingarmy | Creates mobile army with target list |
| RovingArmy_SetTarget | module_rovingarmy | Sets single target, clears previous |
| RovingArmy_AddTarget | module_rovingarmy | Appends target to target list |
| RovingArmy_Disband | module_rovingarmy | Stops encounters, returns units |
| RovingArmy_Pause / RovingArmy_Start | module_rovingarmy | Pauses/resumes target cycling |
| _RovingArmy_Monitor | module_rovingarmy | Checks withdraw threshold, reinforcements |
| _RovingArmy_AttackTarget | module_rovingarmy | Creates attack encounter for current target |
| _RovingArmy_BelowThreshold | module_rovingarmy | Withdraws to fallback when losses exceed threshold |

### Module: TownLife (module_townlife.scar)

| Function | File | Purpose |
|----------|------|---------|
| TownLife_Init | module_townlife | Sets up AI economy with homebase, villagers |
| TownLife_Monitor | module_townlife | Checks reinforcement needs every 5s |
| TownLife_UnitRequest_Start | module_townlife | Spawns requested units via wave manager |
| TownLife_Disband | module_townlife | Stops module, removes homebase bindings |

### Module: UnitSpawner (module_unitspawner.scar)

| Function | File | Purpose |
|----------|------|---------|
| UnitSpawner_Init | module_unitspawner | Spawns initial units with options |
| UnitSpawner_UnitRequest_Start | module_unitspawner | Off-map unit spawner with time estimate |

### Other Systems

| Function | File | Purpose |
|----------|------|---------|
| Raiding_Init | raiding | Initializes raid system with spawn/timing params |
| Raiding_TriggerRaid | raiding | Assigns or creates raid party for position |
| Missionomatic_InitializeLeader | leader | Sets up leader hero unit with surrender logic |
| Missionomatic_LeaderSurrender | leader | Transfers leader to neutral, starts recovery obj |
| Missionomatic_LeaderRecovery | leader | Returns leader to player, restores modifiers |
| Init_AlliedBanner | allybanners | Creates banner-controlled allied army |
| Missionomatic_ChallengeInit | artofwar | Sets up Art of War medal benchmarks |

---

## KEY SYSTEMS

### Recipe Architecture

The recipe is a Lua table returned by a mission's `GetRecipe()` function containing:

- **players** — Player definitions (civ, age, displayName); processed by `MissionOMatic_SetupPlayer`
- **playAs** — Descriptor of the human player
- **locations** — Location definitions (position, egroup, range); initialized as Location prefabs
- **modules** — Behaviour module definitions with `type` field dispatching to `<Type>_Init`; supports `difficulty` filtering
- **battalions** — Unit group definitions sourced from metagame for reporting
- **objectives** — Objective definitions with start/complete/fail conditions, actions, playbills, hintpoints
- **metrics** — Custom metric definitions for post-mission reporting
- **preStart.actions** — Actions run before mission starts (holds mission start)
- **onStart.actions** — Actions run when mission begins
- **introNIS** — Intro NIS event function
- **audioSettings** — Campaign/mission name for audio system
- **cameraStartMarker** — Initial camera position

### Module System

All modules share a common pattern:
1. `<Type>_Init(data)` — Spawns units, creates Encounter, registers in `t_allModules` and type-specific list
2. `<Type>_Monitor` — Interval rule (typically 5s) for reinforcement, state checks
3. `<Type>_GetSGroup` / `<Type>_AddSGroup` / `<Type>_RemoveSGroup` — Unit management
4. `<Type>_Disband` — Full teardown, returns units
5. `<Type>_IsDefeated` — Returns true if SGroup is empty
6. `<Type>_UnitRequest_ProvideEstimate` / `<Type>_UnitRequest_Start` — Unit provider interface

**Module types:**
- **TownLife** — AI economy (villagers, gathering, building). Uses skirmish AI via `AIPlayer_GetOrCreateHomebase`. Produces units via internal Wave manager.
- **Defend** — Holds position. Supports `withdrawData` (flee on spotted/units-left/custom-condition). Creates `plan = "Defend"` encounters.
- **Attack** — Assaults target. Creates `plan = "Attack"` encounters. Monitors reinforcement needs.
- **RovingArmy** — Mobile force with target list. Targeting types: `Discard`, `Cycle`, `Reverse`, `Proximity`, `Random`, `RandomMeandering`. State machine: `ARMY_STATUS_EMPTY | ATTACKING | DEFENDING | DISSOLVED | DISSOLVING_INTO_MODULE`. Supports `withdrawThreshold` for automatic fallback.
- **UnitSpawner** — Barebones spawner, acts as off-map unit provider with configurable `spawnRate`.

### Unit Request Pipeline

Modules request reinforcements via `MissionOMatic_RequestUnits(requestingModule, requestData, unitSources)`. Unit sources are other modules implementing the provider interface. Flow:
1. Requesting module calls `Reinforcement_AreReinforcementsNeeded` (compares current vs ideal composition)
2. `MissionOMatic_RequestUnits` solicits estimates from potential providers
3. Best provider starts production (`UnitRequest_Start`)
4. On completion, `MissionOMatic_RequestComplete` delivers units to the requester's `AddSGroup`

### Objective Lifecycle

Objectives follow: **Register → Start → [Monitor conditions] → Complete/Fail**

Recipe objective fields:
- `descriptor` — String identifier
- `title`, `description`, `type` (OT_Primary/OT_Secondary)
- `isStartingObjective` — Auto-starts on mission begin
- `parent` — Links as sub-objective
- `start.actions` / `start.preactions` / `start.intelEvent` — On-start hooks
- `complete.conditions` — ConditionList checked every second
- `complete.actions` / `complete.preactions` — On-complete hooks
- `fail.conditions` / `fail.actions` — Failure hooks
- `playbill` — Attached playbill started/stopped with objective
- `countDown` / `counterGoal` — Timer/counter display
- `hintpoints` — UI elements (blips, arrows, reticules)

### Playbill System

Playbills are sequences of `{conditions, actions}` stages. Multiple sequences can run in parallel (same ID). The `Playbill_Manager` rule checks conditions every second; when met, runs the actions via `ActionList_PlayActions`, then advances to the next stage. Supports looping via `Action_Loop_Do`.

### Action System

Actions are named Lua functions following `Action_<name>_Do(action, context)`. They can:
- Return nothing (immediate)
- Return `WAIT_FOR_ACTION_TO_FINISH` and later call `Action_Finish(context)` (async)

Built-in actions: StartObjective, CompleteObjective, FailObjective, Wait, CallScarFunction, PlaySpeechEvent, NotifyPlayer, SpawnUnits, SpawnUnitsToModule, DissolveModuleIntoModule, MissionComplete, MissionFail, SetMusicIntensity, Loop, ExpositionCamera, SnapCamera, BookmarkTime, SetInvulnerable, MoveUnits, AddResources, and more.

### Condition System

Conditions follow `Condition_<name>_Check(condition, context) → bool`. Combinators: `CONDITION_LIST_ALL`, `CONDITION_LIST_ANY`, `CONDITION_LIST_NONE`. Built-in conditions: GameTime, HasUnits, HasBuildings, HasResources, HasReachedAge, UnitAtLocation, TaggedUnitAtLocation, UnitsSpotted, UnitsKilled, ModuleDefeated, LocationCaptured, LocationRazed, ObjectiveIsComplete, SubobjectivesAreComplete, ObjectiveCounter, ObjectiveTimer, AskScarFunction, and more.

### Wave System

Waves spawn units from production buildings with per-unit-type build-time cooldowns. Architecture:
- `Wave_New(data)` — Creates wave with player, spawn (egroup/marker), units, staging/assault modules
- `Wave_Prepare` — Begins spawning; units go into staging module first
- `Wave_Launch` — Transfers staged units to assault module
- `Wave_Monitor` — Checks available spawns, spawns units when cooldowns expire
- Supports `auto_launch` (automatic launch when all units spawned), `use_separate_spawns` (per-building spawn points), difficulty filtering

Unit type categories: infantry, ranged, cavalry, siege, town_center, religious. Building types map to categories (barracks→infantry, archery_range→ranged, etc.).

### Raiding System

Autonomous AI raiding via `Raiding_Init`. Creates RovingArmy-based raid parties with:
- Exclusion radius/timer to prevent target overlap
- Party limit and size controls
- Scout probes for map awareness
- Proximity-based target assignment to existing parties
- Configurable `raiderComposition` with ratio-based unit generation
- `Util_DifVar`-scaled timing: `{120, 120, 90, 60}` for raid cooldown, `{80, 80, 70, 60}` for scout timing

### Leader System

Hero/leader units use a downed/recovery mechanic:
- On low health: leader transfers to `neutralHolder` player, becomes immobile, loses LoS
- Recovery objective `OBJ_RecoverDownedLeader` shown with UI hintpoints
- On recovery: returns to owner, health restored to `Util_DifVar({1.0, 0.5, 0.4, 0.3})`
- Handles control group preservation, selection clearing, music stingers

### Upgrade System

Per-civilization tables (`unit_upgrades`, `research_upgrades`, `squad_production`) organized by age (AGE_DARK/FEUDAL/CASTLE/IMPERIAL) plus `ALWAYS_REMOVE`. Supported civs: english, normans, french, rus, mongol (with improved/double variants), hre, chinese. Mongol entries use dual sub-tables for standard/improved tiers.

### Difficulty Scaling

- `Util_DifVar({easy, normal, hard, expert})` used throughout for timing, unit counts, thresholds
- Wave units support `difficulty` field for per-difficulty filtering
- Modules support `difficulty` field in recipe for conditional initialization
- Leader revival health scaled by difficulty

### Timers

| Timer | Interval | Purpose |
|-------|----------|---------|
| ActionList_Manager | every frame | Processes running action lists |
| Playbill_Manager | 1s | Checks playbill conditions per stage |
| Wave_MonitorAllWaves | 1s | Spawns units when build times expire |
| Attack_Monitor | 5s | Reinforcement requests for attack modules |
| Defend_Monitor | 1s | Flee conditions and reinforcement checks |
| _RovingArmy_Monitor | 1s | Withdraw threshold and reinforcement checks |
| TownLife_Monitor | 5s | Reinforcement requests for town modules |
| Missionomatic_CheckLeader | 0.125s | Leader surrender/recovery state check |
| _Raiding_Monitor | 1s | Raid timer, scout spawning, idle party check |
| _MonitorAllyArmy | 15s | Allied banner army reinforcement |

---

## CROSS-REFERENCES

### Imports
- `cardinal.scar` — Core engine API
- `training.scar`, `training/coretrainingconditions.scar`, `training/coretraininggoals.scar` — Tutorial/training system
- `scarutil.scar` — General SCAR utilities
- `gathering_utility.scar` — Resource gathering assignment helpers
- `core_encounter.scar` — Encounter system (AI goal management)
- `ai/wave_generator.scar` — Wave generator system
- `ai/army.scar` — Army system (used by raiding, allied banners)
- `gameplay/currentageui.scar` — Age display UI
- `GroupCallers.scar` — SGroup/EGroup utilities
- `formation.scar` — Formation system
- `unit_trainer.scar` — Unit training system

### Shared Globals

| Global | Type | Purpose |
|--------|------|---------|
| `MissionRecipe` | Table | The active mission recipe |
| `t_allModules` | Table | All initialized behaviour modules |
| `t_attackModules` | Table | Attack module instances |
| `t_defendModules` | Table | Defend module instances |
| `t_rovingArmyModules` | Table | RovingArmy module instances |
| `t_townLifeModules` | Table | TownLife module instances |
| `t_unitSpawnerModules` | Table | UnitSpawner module instances |
| `g_missionObjectives` | Table | All registered mission objectives |
| `__t_Objectives` | Table | SCAR objective system internal table |
| `g_waves` | Table | All active wave definitions |
| `g_raidSystem` | Table | Active raid system state |
| `t_allLeaders` | Table | All leader unit instances |
| `g_allied_banner_armies` | Table | Allied banner-controlled armies |
| `sg_startingUnits` | SGroup | Units present at mission start |
| `eg_startingBuildings` | EGroup | Buildings present at mission start |
| `sg_scriptSpawnedUnits` | SGroup | Script-spawned units |
| `sg_waveManagerStagedUnits` | SGroup | Units currently in wave staging |
| `sg_ignoreForUnitComposition` | SGroup | Units excluded from ideal composition |
| `t_allUnitTypes` | Table | Unit type→display name→value mapping |
| `PLAYERS` | Table | Player data table |
| `EVENTS` | Table | Speech/intel event functions |
| `g_timeStamps` | Table | Named time bookmarks |
| `b_missionIsTriggering` | Boolean | Suppresses conditions during save |
| `content_pack` | Number | Campaign content identifier (1=Vanilla, 2=AoW, 3=Abbasid, 4=Rogue) |

### Inter-file Function Calls

- `MissionOMatic_FindModule` — Called by actions, conditions, wave spawning, dissolve utilities
- `MissionOMatic_FindObjective` — Called by objective actions and conditions
- `MissionOMatic_RequestUnits` / `MissionOMatic_RequestComplete` — Called by all module monitors and unit providers
- `Reinforcement_AreReinforcementsNeeded` / `Reinforcement_UpdateIdealComposition` — Called by all module monitors
- `Prefab_DoAction(module, "ActionName")` — Universal module dispatch used across all files
- `ActionList_PlayActions` — Called by objectives, playbills, utility wrappers (`PlayECAM`, `PlaySpeech`)
- `ConditionList_CheckList` — Called by objectives and playbill manager
- `Encounter_Create` / `Encounter_SetGoalData` / `Encounter_Stop` — Called by all combat modules
- `ResolveSpawnLocation` — Called by modules, waves, raiding, utility functions
- `UnitEntry_DeploySquads` — Called by all modules, waves, raiding, utility spawners
- `DissolveModuleIntoModule` — Called by actions, RovingArmy fallbacks, defend withdrawal
- `AI_Module_ResolveCombatArea` — Called by Defend, RovingArmy, Attack for target resolution
