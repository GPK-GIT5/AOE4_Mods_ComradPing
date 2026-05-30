# Gameplay: Prefabs & Replay

## OVERVIEW

The prefabs system provides a WorldBuilder-integrated, schema-driven framework for placing reusable gameplay components (triggers, exclusion zones, pickups, objectives, villager life simulations) directly in the map editor. Each prefab consists of a `_schema.scar` file defining editor-exposed parameters (using typed fields like `ST_MARKER`, `ST_PLAYER`, `ST_SGROUP`, `ST_PBG`) and a companion `.scar` implementation file containing `_Init`, `_Activate`, `_Trigger`, and `_Stop` lifecycle functions. Prefabs communicate via `Prefab_DoAction` dispatching and an external-interest registration pattern that allows cross-prefab triggering with optional delays. The replay system is a separate, lightweight module (`ReplayStatViewer`) that populates XAML-bound data contexts with per-player stats during replay playback, updated on a 5-second interval. The configuration file `prefabs_config.scar` is an empty table placeholder for future prefab-level configuration.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| prefabs_config.scar | data | Empty configuration table — placeholder for prefab system settings |
| canseetrigger_schema.scar | schema | Schema for CanSeeTrigger: player visibility check against marker/SGroup/EGroup |
| canseetrigger.scar | core | Fires trigger actions when a player can see a target location or group |
| exclusionarea_schema.scar | schema | Schema for ExclusionArea: AI no-path/no-target radius around a marker |
| exclusionarea.scar | core | Adds/removes AI exclusion areas via `AI_PlayerAddExclusionArea` / `AI_PlayerRemoveExclusionArea` |
| healthtrigger_schema.scar | schema | Schema for HealthTrigger: fires when SGroup/EGroup health crosses a threshold |
| healthtrigger.scar | core | Monitors group average health with configurable comparison operators |
| momobjective_schema.scar | schema | Schema for Mission-o-Matic objectives with conditions, hintpoints, and start/complete/fail intel events |
| momobjective.scar | core | Stub initializer for MoM objectives (logic delegated to MoM system) |
| pickups_schema.scar | schema | Schema for difficulty-filtered entity pickups at marker locations |
| pickups.scar | core | Spawns pickup entities filtered by SP difficulty (Easy/Normal/Hard) |
| playertrigger_schema.scar | schema | Schema for PlayerTrigger: proximity-based trigger zone with blueprint filtering |
| playertrigger.scar | core | Fires trigger actions when player units enter a marker radius; supports repeat/re-enter |
| villagerlife_schema.scar | schema | Schema for VillagerLife: ambient villager spawning with resource jobs and flee/attack responses |
| villagerlife.scar | core | Spawns villagers, assigns resource gathering jobs, manages flee/attack AI responses |
| replaystatviewer.scar | core | Populates replay HUD stat tabs with per-player data via XAML data contexts |

## FUNCTION INDEX

### Trigger Prefabs

| Function | File | Purpose |
|----------|------|---------|
| `canseetrigger_Init` | canseetrigger.scar | Initializes data, starts check rule if immediate |
| `canseetrigger_Activate` | canseetrigger.scar | Manually starts the visibility check interval |
| `canseetrigger_Stop` | canseetrigger.scar | Force-stops trigger by setting count to limit |
| `canseetrigger_Test` | canseetrigger.scar | Tests Player_CanSee against marker/SGroup/EGroup |
| `canseetrigger_Check` | canseetrigger.scar | Interval rule: triggers and self-removes on success |
| `canseetrigger_Trigger` | canseetrigger.scar | Dispatches prefab/SCAR/intel actions with delays |
| `canseetrigger_GetTriggerCount` | canseetrigger.scar | Returns number of times instance has triggered |
| `canseetrigger_RegisterExternalInterest` | canseetrigger.scar | Registers external prefab action for cross-triggering |
| `playertrigger_Init` | playertrigger.scar | Initializes data, calls StandardTriggerSystem if immediate |
| `playertrigger_Activate` | playertrigger.scar | Manually activates proximity trigger system |
| `playertrigger_Stop` | playertrigger.scar | Force-stops trigger by setting count to limit |
| `playertrigger_Trigger` | playertrigger.scar | Dispatches actions; handles repeat/re-enter logic |
| `playertrigger_GetTriggerCount` | playertrigger.scar | Returns number of activations |
| `playertrigger_TriggerExited` | playertrigger.scar | Checks if player units left zone; re-arms trigger |
| `playertrigger_RegisterExternalInterest` | playertrigger.scar | Registers external prefab for cross-triggering |
| `healthtrigger_Init` | healthtrigger.scar | Initializes health check; adds rule if immediate |
| `healthtrigger_Activate` | healthtrigger.scar | Manually starts health monitoring rule |
| `healthtrigger_check` | healthtrigger.scar | Per-frame rule: compares avg health to threshold |
| `healthtrigger_Trigger` | healthtrigger.scar | Dispatches prefab/SCAR/intel-table actions on fire |
| `healthtrigger_RegisterExternalInterest` | healthtrigger.scar | Registers external interest for cross-triggering |

### AI & Environment Prefabs

| Function | File | Purpose |
|----------|------|---------|
| `exclusionarea_Init` | exclusionarea.scar | Reads marker radii; enables if `start_enabled` |
| `exclusionarea_Enable` | exclusionarea.scar | Calls `AI_PlayerAddExclusionArea` for target player |
| `exclusionarea_Disable` | exclusionarea.scar | Calls `AI_PlayerRemoveExclusionArea` for target player |
| `pickups_Init` | pickups.scar | Spawns all pickups via `pickups_SpawnAllPickups` |
| `pickups_SpawnAllPickups` | pickups.scar | Iterates pickup list, filters by SP difficulty, creates entities |

### VillagerLife

| Function | File | Purpose |
|----------|------|---------|
| `VillagerLife_Create` | villagerlife.scar | Runtime constructor: builds instance with SGroups per job |
| `villagerlife_Init` | villagerlife.scar | Prefab/runtime init: deploys villagers, starts monitor rule |
| `VillagerLife_Find` | villagerlife.scar | Looks up VillagerLife instance by name |
| `VillagerLife_AddSGroup` | villagerlife.scar | Adds villagers to a specific job (roaming/wood/food/stone/gold) |
| `VillagerLife_GoToWork` | villagerlife.scar | Assigns all job groups to resource gathering |
| `VillagerLife_Monitor` | villagerlife.scar | Main loop: checks enemies, triggers flee or attack |
| `VillagerLife_Attack` | villagerlife.scar | Creates Encounter with attack plan against enemies |
| `VillagerLife_Wander` | villagerlife.scar | Sends idle villager to random building or position |
| `VillagerLife_GarrisonIsNearby` | villagerlife.scar | Checks for garrisonable buildings near flee marker |
| `VillagerLife_DestroyIfNearPosition` | villagerlife.scar | Despawns fleeing villagers that reached destination |
| `VillagerLife_OnFail` | villagerlife.scar | Encounter callback: resets attacking flag |
| `VillagerLife_OnSuccess` | villagerlife.scar | Encounter callback: returns villagers to work |

### MoM Objective

| Function | File | Purpose |
|----------|------|---------|
| `momobjective_Init` | momobjective.scar | Stub initializer (logic in MoM system) |
| `PrefabSchema_ConditionList` | momobjective_schema.scar | Builds reusable condition sub-schema table |
| `PrefabSchema_ComparisonOptions` | momobjective_schema.scar | Returns comparison operator option strings |

### Replay

| Function | File | Purpose |
|----------|------|---------|
| `ReplayStatViewer_PopulateReplayStatTabs` | replaystatviewer.scar | Registers XAML data templates for stat tabs |
| `ReplayStatViewer_RegisterDataContextUpdater` | replaystatviewer.scar | Registers global data context update callback |
| `ReplayStatViewer_RegisterPlayerDataContextUpdater` | replaystatviewer.scar | Registers per-player data context update callback |
| `ReplayStatViewer_OnInit` | replaystatviewer.scar | Module init (template population placeholder) |
| `ReplayStatViewer_Start` | replaystatviewer.scar | Sets initial data context; starts 5s update rule |
| `ReplayStatViewer_OnGameOver` | replaystatviewer.scar | Clears updaters and removes interval rule |
| `ReplayStatViewer_UpdatePlayerDataContexts` | replaystatviewer.scar | Iterates all players, runs updaters, sets UI contexts |

## KEY SYSTEMS

### Prefab Schema Types

All schemas use a standard set of typed fields for WorldBuilder integration:

| Schema Type | Purpose |
|-------------|---------|
| `ST_STRING` | Text/enum with optional `options` list |
| `ST_NUMBER` | Numeric value (float or `integer = true`) |
| `ST_BOOLEAN` | True/false toggle |
| `ST_PLAYER` | Player reference (e.g. "Player1") |
| `ST_MARKER` | Map marker with optional `hasRange`/`hasDirection` |
| `ST_SGROUP` | Squad group reference |
| `ST_EGROUP` | Entity group reference |
| `ST_PREFAB` | Reference to another prefab instance with `compatibility` filter |
| `ST_PBG` | Property bag group (blueprint reference with `blueprintType`) |
| `ST_TABLE` | Nested sub-table with its own `itemSchema` and `multiplicity` |

Schemas support `requirement` fields for conditional visibility (e.g., `requirement = {"trigger_type", "Marker"}`) and `compatibility` tags for prefab-to-prefab linking.

### Trigger Architecture

All trigger prefabs (PlayerTrigger, CanSeeTrigger, HealthTrigger) share a common pattern:

1. **Activation**: `"Immediately"` (auto-start at init) or `"Manually"` (via `_Activate` call)
2. **Monitoring**: `Rule_AddInterval` polls condition every 1 second (health: every frame via `Rule_Add`)
3. **Firing**: On condition met, iterates `things_to_trigger` list and dispatches via `Rule_AddOneShot` with configurable delay
4. **Action types**: `"Prefab"` → `Prefab_DoAction(target, "Trigger")`, `"Scar Function"` → `_G[name](instance)`, `"Speech Event"/"Call Intel Table"` → `Util_StartIntel(EVENTS[name])`
5. **Repeatability**: Optional `repeatable` flag with `repeat_count` (0 = infinite) and `repeat_type` (`"Timed Delay"` or `"Leave and Re-enter"/"Leave and Come Back"`)
6. **External interest**: Other prefabs register callbacks via `_RegisterExternalInterest`, dispatched alongside built-in actions

**PlayerTrigger** uses `PrefabHelper_StandardTriggerSystem` for proximity detection with `Player_GetAllSquadsNearMarker`, supports aircraft filtering (`ignore_planes`), camouflage filtering (`ignore_camouflage`), and custom blueprint include/exclude lists.

**CanSeeTrigger** uses `Player_CanSeePosition` / `Player_CanSeeSGroup` / `Player_CanSeeEGroup` for line-of-sight checks.

**HealthTrigger** uses `EGroup_GetAvgHealth` / `SGroup_GetAvgHealth` with configurable comparison operators (`<`, `<=`, `==`, `>=`, `>`). Non-repeatable by design.

### VillagerLife System

Ambient civilian simulation with five job types:

- **Jobs**: `roaming` (wander randomly), `wood`, `food`, `stone`, `gold` (gather resources)
- **Spawning**: Uses `UnitEntry_DeploySquads` with `scar_villager` blueprint; roaming villagers get 0.7 speed modifier
- **Response modes**: `"none"` (passive), `"flee"` (move to flee marker with 1.15x speed, despawn on arrival), `"attack"` (create `Encounter` with attack plan)
- **Flee logic**: Checks `VillagerLife_GarrisonIsNearby` for TC/outpost/castle within 6 range of flee marker; falls back to backup marker if no garrison
- **Monitor loop**: 1-second interval checks for visible enemies, transitions to flee or attack state, handles idle villager wandering to random buildings
- **Runtime creation**: `VillagerLife_Create()` allows spawning from script (not just WorldBuilder)
- **Global registry**: All instances stored in `t_villagerLifePrefabs` table, queryable via `VillagerLife_Find(name)`
- **Mongol special case**: Mongol villagers assigned to sheep instead of farms for food gathering

### Pickups System

- Spawns pickup entities at marker locations filtered by single-player difficulty
- Difficulty options: `"All"`, `"Easy"`, `"Normal"`, `"Hard"`, `"Easy / Normal"`, `"Normal / Hard"`
- Uses `Game_GetSPDifficulty()` returning 0 (Easy), 1 (Normal), 2 (Hard)
- Tagged `"triggerable"` compatibility — can be activated by other trigger prefabs

### MoM Objective Schema

Defines WorldBuilder-configurable objectives for the Mission-o-Matic system:

- **Types**: `"Primary"`, `"Bonus"`, `"Warning"`, `"Sub-objective"` (requires parent prefab)
- **Lifecycle**: `start` (intel event), `complete` (conditions + intel), `fail` (conditions + intel)
- **Conditions**: `Boolean` (Any/All/None), `AskScarFunction`, `GameTime` (with comparison and bookmark), `HasReachedAge`, `HasResources`, `HasBuildings`, `HasUnits`
- **Hintpoints**: Attached to Marker, SGroup, Location (prefab), or Module (prefab) with optional minimap blip
- Implementation is a stub (`momobjective_Init` does nothing); actual logic lives in the MoM runtime

### Exclusion Areas

- Defines AI no-go zones with separate no-target and no-path radii
- Both radii attached to the same position via `lockedTo` marker linkage
- Can be toggled at runtime via `exclusionarea_Enable` / `exclusionarea_Disable`
- `start_enabled` controls whether active on init

### Replay Stat Viewer

- Registered as two Core modules: `"ReplayStatViewer"` and `"XboxReplayStatViewer"`
- Only active when `UI_IsReplay()` returns true
- **Data templates**: `PlayerScoreTemplate`, `CurrentResourcesTemplate`, `IncomeTemplate`, `MilitaryTemplate`, `ConquestTrackerTemplate`, `ReligiousTrackerTemplate`, `WonderTrackerTemplate`
- **Update loop**: `Rule_AddInterval` at 5.0 seconds calls all registered updaters, then `UI_SetPlayerDataContext` per player
- **Extensibility**: Game modes register custom updaters via `ReplayStatViewer_RegisterDataContextUpdater` (global) and `ReplayStatViewer_RegisterPlayerDataContextUpdater` (per-player with `player, scarModel` args)
- **ScarModel fields**: `Age`, `PlayerScore_Target/Current`, `Conquest_Target/Current`, `Relics_Target/Current`, `Wonder_Target/Current`
- Cleans up updaters and removes interval rule on `OnGameOver`

### Timers

| Timer | File | Interval | Purpose |
|-------|------|----------|---------|
| `canseetrigger_Check` | canseetrigger.scar | 1s | Polls Player_CanSee visibility condition |
| `healthtrigger_check` | healthtrigger.scar | every frame | Polls group average health vs threshold |
| `canseetrigger_TriggerExited` | canseetrigger.scar | 1s | Checks if units left trigger area for re-arm |
| `playertrigger_TriggerExited` | playertrigger.scar | 0.1s | Rapid poll for units leaving trigger zone |
| `VillagerLife_Monitor` | villagerlife.scar | 1s | Main villager behavior loop |
| `ReplayStatViewer_UpdatePlayerDataContexts` | replaystatviewer.scar | 5s | Refreshes replay stat UI data contexts |

## CROSS-REFERENCES

### Imports
- `pickups.scar` imports `Prefabs/Schemas/Pickups.scar` (its own schema)

### Core API Dependencies
- **Prefab system**: `Prefab_GetInstance`, `Prefab_DoAction` — central dispatch used by all prefab files
- **PrefabHelper**: `PrefabHelper_StandardTriggerSystem` — shared proximity trigger logic (used by PlayerTrigger)
- **Core module system**: `Core_RegisterModule` — used by ReplayStatViewer for lifecycle hooks (`OnInit`, `Start`, `OnGameOver`)
- **UI system**: `UI_SetDataContext`, `UI_SetPlayerDataContext`, `UI_IsReplay` — XAML data binding for replay
- **AI system**: `AI_PlayerAddExclusionArea`, `AI_PlayerRemoveExclusionArea` — used by ExclusionArea
- **Encounter system**: `Encounter_Create` — used by VillagerLife for attack behavior
- **Gathering utilities**: `AssignVillagersToWood`, `AssignVillagersToStone`, `AssignVillagersToGold`, `AssignVillagersToFarms`, `AssignVillagersToSheep` — from `gathering_utility.scar` (core)
- **UnitEntry**: `UnitEntry_DeploySquads` — squad spawning used by VillagerLife
- **Intel system**: `Util_StartIntel`, `EVENTS` table — used by trigger prefabs for speech/intel events

### Shared Globals
- `PLAYERS` — player table iterated by ReplayStatViewer
- `t_villagerLifePrefabs` — global registry of all VillagerLife instances
- `G_encounter_villagerLife_table` — maps encounter IDs to VillagerLife instances for callbacks
- `sg_temp`, `eg_temp`, `sg_single` — shared scratch groups used by VillagerLife
- `UPG.COMMON.UPGRADE_UNIT_TOWN_CENTER_WHEELBARROW_1` — wheelbarrow upgrade removed from AI villagers

### Inter-File Function Calls
- All trigger prefabs call `Prefab_DoAction(target, "Trigger")` to chain-activate other prefabs
- Trigger prefabs resolve SCAR function names from `_G` global table at runtime
- VillagerLife uses `Player_GetRaceName` to branch Mongol-specific food gathering logic
- MoM objective schema references `PrefabSchema_ConditionList` and `PrefabSchema_ComparisonOptions` helper functions defined in the same file
