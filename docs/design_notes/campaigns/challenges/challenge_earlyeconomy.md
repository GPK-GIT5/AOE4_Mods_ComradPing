# Challenge Mission: Early Economy

## OVERVIEW

The Early Economy challenge mission teaches players fundamental economic mechanics as the English civilization. The player starts with a Town Center and must train villagers, gather food and gold, build economic infrastructure (house, mill, lumber camp, mining camp), and ultimately begin construction of a Dark Age Landmark to advance to the Feudal Age. Performance is scored by a timed medal system (gold ≤5:10, silver ≤6:00, bronze ≤7:30) that downgrades as thresholds are exceeded. A 6-shot pre-intro cinematic demonstrates sheep gathering, scouting, building construction, deer hunting, and landmark construction before gameplay begins. The training system provides dynamic hints for idle Town Centers, idle villagers, and idle scouts.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_earlyeconomy.scar` | core | Main mission logic: objectives, resource tracking, medal system, building/upgrade callbacks, hint triggers, victory flow |
| `challenge_mission_earlyeconomy_preintro.scar` | other (cinematic) | Pre-intro cinematic with 6 scripted economy vignettes: sheep gathering, scouting, building construction, deer hunting, landmark building, cheering |
| `challenge_mission_earlyeconomy_training.scar` | training | Dynamic training goal system: idle TC villager production prompts, idle villager selection prompts, idle scout exploration prompts |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | core | Defines objectives, benchmarks, medal thresholds; Xbox adjustments |
| `Mission_Preset` | core | Calls game setup, player setup, and restrictions |
| `Mission_PreStart` | core | Launches pre-intro, spawns scenes, holds mission start |
| `Mission_PreStart_PreIntroNISFinished` | core | Polls pre-intro completion, cleans scenes, spawns starting units |
| `Mission_PreStart_IntroNISFinished` | core | Polls intro completion, sets resources, releases mission hold |
| `Mission_Start` | core | Initializes objectives, rules, events, disables core training |
| `ChallengeMission_OnGameSetup` | core | Creates localPlayer reference from world slot 1 |
| `ChallengeMission_SetupPlayer` | core | Sets player name to English, age to Dark, max Feudal |
| `ChallengeMission_SetRestrictions` | core | Removes military buildings, upgrades, death/scuttle abilities |
| `ChallengeMission_SetupChallenge` | core | Initializes player challenge table, hides barracks/dock/outpost/walls |
| `ChallengeMission_FindAllResources` | core | Collects all neutral tree, stone, gold entities into EGroups |
| `ChallengeMission_InitStartingUnits` | core | Spawns 6 villagers, 1 scout, 1 sheep, 7 west deer |
| `ChallengeMission_SpawnDeer` | core | Delayed spawn of 7 south deer (3s after start) |
| `ChallengeMission_PositionStartingUnits` | core | Warps starting units to spawn markers for cinematic |
| `ChallengeMission_RallyStartingScout` | core | Moves scout through waypoints at 0.6× speed |
| `ChallengeMission_InitializeObjectives` | core | Registers all objectives, starts timer, sets food/gold from landmark cost |
| `ChallengeMission_Update` | core | Polls villager/food/gold counts, completes sub-objectives, manages medals |
| `ChallengeMission_TrackScore` | core | Stores completion time to Data Store on victory |
| `ChallengeMission_OnConstructionStart` | core | GE_ConstructionStart: detects landmark/mill construction |
| `ChallengeMission_OnConstructionComplete` | core | GE_ConstructionComplete: completes house/mill/mining/lumber objectives |
| `ChallengeMission_OnBuildItemComplete` | core | GE_BuildItemComplete: triggers build hints based on population thresholds |
| `ChallengeMission_OnUpgradeComplete` | core | GE_UpgradeComplete: completes eco tech objective on Survival Techniques |
| `ChallengeMission_OnDestruction` | core | GE_EntityKilled: re-starts landmark objective if landmark destroyed |
| `ChallengeMission_CheckVillagers` | core | Fires intel when villager goal met but resources still needed |
| `ChallengeMission_HintWhenMiningStone` | core | Warns player not to mine stone (fires once) |
| `ChallengeMission_ConstructLandmark` | core | Prompts landmark construction when food+gold objectives complete |
| `ChallengeMission_ExploredSouth` | core | Cancels deer hint if player explored west deer or east |
| `ChallengeMission_DeerExplored` | core | Fires explore hint with minimap blip after 55s |
| `ChallengeMission_GatherSheep` | core | Prompts sheep gathering if idle after 20s |
| `ChallengeMission_IdleScout` | core | Prompts scout usage if idle after 60s |
| `ChallengeMission_IdleTC` | core | Prompts villager production if TC idle >5s after 15s |
| `ChallengeMission_RemindMill` | core | Prompts mill construction when all sheep consumed (40s+) |
| `ChallengeMission_MissedGold` | core | Plays narration when gold medal time exceeded |
| `ChallengeMission_MissedSilver` | core | Plays narration when silver medal time exceeded |
| `ChallengeMission_MissedBronze` | core | Plays narration when bronze medal time exceeded |
| `ChallengeMission_OnComplete` | core | Triggers celebration walla, outro camera, mission complete |
| `ChallengeMission_EndChallenge` | core | Sets player victorious, slows sim rate to 0.5 |
| `Outro_Landmark_Construct` | core | Spawns villagers building/cheering around outro landmark |
| `EarlyEconomy_PreIntro_Setup_Scenes` | preintro | Creates all SGroups/EGroups, sets English building BPs |
| `EarlyEconomy_PreIntro_Shot01_Units` | preintro | Shot 1: villagers gather sheep near TC |
| `EarlyEconomy_PreIntro_Shot01_ButcherSheep` | preintro | Commands villagers to gather from sheep |
| `EarlyEconomy_PreIntro_Shot01_TrainVillager` | preintro | Spawns extra villager after 11s to join gathering |
| `EarlyEconomy_PreIntro_Shot02_Units` | preintro | Shot 2: scout finds sheep, herds toward TC |
| `EarlyEconomy_PreIntro_Shot02_ScoutMoves` | preintro | Scout waypoints toward deer spawn area |
| `EarlyEconomy_PreIntro_Shot02_HaltSheep` | preintro | Stops sheep at rally when scout passes waypoint |
| `EarlyEconomy_PreIntro_Shot03_Units` | preintro | Shot 3: villagers build house, mill, lumber camp |
| `EarlyEconomy_PreIntro_Shot04_Units` | preintro | Shot 4: hunters kill and gather deer |
| `EarlyEconomy_PreIntro_Shot05_Units` | preintro | Shot 5: 7 villagers build landmark (0.25× build time) |
| `EarlyEconomy_PreIntro_Shot06_Units` | preintro | Shot 6: villagers cheer at completed landmark |
| `EarlyEconomy_PreIntro_Clean_Scenes` | preintro | Removes all rules, destroys units/buildings, resets build times |
| `DespawnCarcasses` | preintro | Destroys all neutral carriable entities (carcasses) |
| `EarlyEconomyTrainingGoals_OnInit` | training | Registers villager, idle villager, idle scout goal sequences |
| `EarlyEconomyTrainingGoals_InitVillagerTraining` | training | PC: TC select → queue villager 2-step training goal |
| `EarlyEconomyTrainingGoals_InitVillagerTraining_Xbox` | training | Xbox: TC select → RT radial → queue villager 3-step goal |
| `TrainingGoal_EnableEarlyEconomyGoals` | training | Enables all early economy training goal sequences |
| `TrainingGoal_DisableEarlyEconomyGoals` | training | Disables all early economy training goal sequences |
| `UserHasIdleTownCenter` | training | Predicate: TC not producing, player has food + pop space |
| `UserHasIdleTownCenter_Xbox` | training | Xbox predicate: same as above with radial menu step |
| `UserIsTrainingVillager` | training | Checks if TC is currently producing a villager |
| `UserHasSelectedTownCenter` | training | Completion: player selected the specific TC entity |
| `TCHasStartedToTrainAVillager` | training | Completion: selected TC is now producing a villager |
| `SelectNextIdleIfVillagersIdle` | training | Predicate: any villager idle for interval duration |
| `UserHasIdleScout` | training | Predicate: scout idle for interval, capped at 5 repeats |
| `EnoughMarkersExplored` | training | Ignore: suppresses scout hint after 3+ markers explored |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `_challenge.victory.objectiveVictory` | OT_Primary | Prepare to advance to the Feudal Age (parent; complete when all subs done) |
| `_challenge.victory.objectiveVillagers` | OT_Primary (sub) | Train additional villagers (counter: 0/21) |
| `_challenge.victory.objectiveFood` | OT_Primary (sub) | Gather food (counter: 0/landmark food cost, dynamically set) |
| `_challenge.victory.objectiveGold` | OT_Primary (sub) | Gather gold (counter: 0/landmark gold cost, dynamically set) |
| `_challenge.victory.objectiveLandmark` | OT_Primary (sub) | Begin construction of a Landmark (starts when food+gold met) |
| `_challenge.secondary.objectiveVictory` | OT_Secondary | Build up a base (parent for secondary sub-objectives) |
| `_challenge.secondary.objectiveFirstHouse` | OT_Secondary (sub) | Build a House (triggered at 8+ population) |
| `_challenge.secondary.objectiveMill` | OT_Secondary (sub) | Build a Mill (triggered at 12+ villagers) |
| `_challenge.secondary.objectiveEcoTech` | OT_Secondary (sub) | Research Survival Techniques (triggered after first mill) |
| `_challenge.secondary.objectiveMiningCamp` | OT_Secondary (sub) | Build a Mining Camp (triggered at 9+ villagers) |
| `_challenge.secondary.objectiveLumberCamp` | OT_Secondary (sub) | Build a Lumber Camp (triggered at 10+ pop or wood < 100) |
| `_challenge.benchmarks.gold.objective` | OT_Bonus | Gold medal: complete within 5m10s (5m20s Xbox) |
| `_challenge.benchmarks.silver.objective` | OT_Bonus | Silver medal: complete within 6m00s (6m30s Xbox) |
| `_challenge.benchmarks.bronze.objective` | OT_Bonus | Bronze medal: complete within 7m30s (8m00s Xbox) |
| `_challenge.benchmarks.unplaced.objective` | OT_Bonus | No medal — time elapsed display only |

### Difficulty

No `Util_DifVar` usage. Difficulty is implicit through the timed medal system:

| Medal | Time Limit (PC) | Time Limit (Xbox) |
|-------|-----------------|-------------------|
| Gold | 5m 10s | 5m 20s |
| Silver | 6m 00s | 6m 30s |
| Bronze | 7m 30s | 8m 00s |

Xbox thresholds are relaxed in `Mission_OnInit` via `UI_IsXboxUI()` check. Player is locked to `AGE_DARK` with max age `AGE_FEUDAL`.

### Spawns

**Starting Units** (deployed in `ChallengeMission_InitStartingUnits`):

| Unit Type | Blueprint | Count | Location |
|-----------|-----------|-------|----------|
| Villagers | `scar_villager` | 6 | `mkr_player_startingvillager_spawn` |
| Scout | `scar_scout` | 1 | `mkr_player_startingscout_spawn` |
| Sheep | `gaia_herdable_sheep` | 1 | `mkr_player_startingsheep_spawn` (set world-owned) |
| Deer (west) | `gaia_huntable_deer` | 7 | `mkr_deer_west_spawn` through `mkr_deer_west_spawn07` |
| Deer (south) | `gaia_huntable_deer` | 7 | `mkr_deer_south_spawn` through `mkr_deer_south_spawn07` (delayed 3s) |

- Deer are set world-owned after spawning. Minimap icons (`gaia_deer_dummy_minimap_icon`) are placed at each deer cluster.
- South deer are spawned via `Rule_AddOneShot(ChallengeMission_SpawnDeer, 3)` to stagger loading.
- No enemy units exist in this mission.

### AI

No AI players, no `AI_Enable`, no encounter plans, no patrol logic. This is a purely single-player economy tutorial with no combat.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Rule_AddInterval(ChallengeMission_Update, 0.125)` | 0.125s | Polls villager/food/gold counts and medal transitions |
| `Rule_AddInterval(ChallengeMission_TrackScore, 0.125)` | 0.125s | Checks victory and stores completion time |
| `Rule_AddInterval(ChallengeMission_CheckVillagers, 0.5)` | 0.5s | Fires intel when villager goal met |
| `Rule_AddInterval(ChallengeMission_ConstructLandmark, 0.125)` | 0.125s | Prompts landmark build when food+gold complete |
| `Rule_AddInterval(ChallengeMission_HintWhenMiningStone, 1)` | 1s | Warns player not to mine stone |
| `Rule_AddInterval(ChallengeMission_ExploredSouth, 0.25)` | 0.25s | Cancels deer hint if explored |
| `Rule_AddOneShot(ChallengeMission_DeerExplored, 55)` | 55s | Fires explore hint with minimap blip |
| `Rule_AddInterval(ChallengeMission_GatherSheep, 0.25)` | 0.25s | Prompts sheep gathering after 20s idle |
| `Rule_AddInterval(ChallengeMission_IdleScout, 0.25)` | 0.25s | Prompts scout usage after 60s idle |
| `Rule_AddInterval(ChallengeMission_IdleTC, 0.25)` | 0.25s | Prompts villager training if TC idle >5s |
| `Rule_AddInterval(ChallengeMission_RemindMill, 0.25)` | 0.25s | Prompts mill build when sheep exhausted (40s+) |
| `Rule_AddOneShot(ChallengeMission_SpawnDeer, 3)` | 3s | Delayed spawn of south deer cluster |
| `Rule_AddOneShot(ChallengeMission_MissedGold, 1.2)` | 1.2s | Plays medal downgrade narration |
| `Rule_AddOneShot(ChallengeMission_MissedSilver, 1.2)` | 1.2s | Plays medal downgrade narration |
| `Rule_AddOneShot(ChallengeMission_MissedBronze, 1.2)` | 1.2s | Plays medal downgrade narration |
| `Rule_AddInterval(Mission_PreStart_PreIntroNISFinished, 0.125)` | 0.125s | Polls pre-intro cinematic completion |
| `Rule_AddInterval(Mission_PreStart_IntroNISFinished, 0.125)` | 0.125s | Polls intro cinematic completion |

### Pre-Intro Cinematic System

The pre-intro consists of 6 scripted economy vignettes using English units and buildings:

| Shot | Theme | Units & Actions |
|------|-------|-----------------|
| 1 | Sheep gathering | 2 villagers + 1 sheep near TC; villagers butcher sheep; 3rd villager trained after 11s |
| 2 | Scouting | 1 scout + 1 sheep; scout moves through waypoints, sheep halted at rally point |
| 3 | Building construction | 1 villager builds house, 2 build mill, 1 builds lumber camp (English BPs) |
| 4 | Deer hunting | 3 deer spawned; 3 villagers hunt and gather from deer |
| 5 | Landmark building | 7 villagers (3 east + 4 west) build Westminster Hall at 0.25× build time |
| 6 | Celebration | Villagers cheer at completed landmark (staggered 2.5s) |

- Each shot has a corresponding cleanup function. `EarlyEconomy_PreIntro_Clean_Scenes` is the master cleanup that removes all rules, destroys all player squads/entities (except TC), despawns carcasses, and resets build times.
- Building blueprints used: `BUILDING_HOUSE_CONTROL_ENG`, `BUILDING_ECON_FOOD_CONTROL_ENG`, `BUILDING_ECON_WOOD_CONTROL_ENG`, `BUILDING_LANDMARK_AGE1_WESTMINSTER_HALL_ENG`.

### Training System

Three goal sequences registered via `coretraininggoals.scar`:

| Goal Sequence ID | Trigger Predicate | Ignore Condition | Message |
|------------------|-------------------|------------------|---------|
| `train_villager` | `UserHasIdleTownCenter` — TC not producing, player has food + pop cap space, villager obj incomplete | None | "Select your Town Center to train Villagers" → "Click here to queue up additional Villagers" |
| `idle_villager` | `SelectNextIdleIfVillagersIdle` — any villager idle for `__t_challengeIntervalIdleVillager` (5s) | `NoIdleVillagers` | "Select the next idle Villager and assign it to a job" |
| `idle_scout` | `UserHasIdleScout` — scout idle for `__t_challengeIntervalIdleScout` (10s), max 5 repeats/session | `EnoughMarkersExplored` — 3+ of 5 exploration markers seen | "Do not forget about your Scout. You must explore to find more resources." |

**Training timing variables:**

| Variable | Value | Purpose |
|----------|-------|---------|
| `__t_challengeStartIdleTC` | 15s | Grace period before TC idle hints start |
| `__t_challengeIntervalIdleTC` | 5s | Interval between TC idle checks |
| `__t_challengeStartIdleVillager` | 10s | Grace period before villager idle hints |
| `__t_challengeIntervalIdleVillager` | 5s | Idle duration before villager hint fires |
| `__t_challengeStartIdleScout` | 20s | Grace period before scout idle hints |
| `__t_challengeIntervalIdleScout` | 10s | Idle duration before scout hint fires |
| `__n_challengeScoutAreasToExplore` | 3 | Number of markers to suppress scout hints |

- Xbox variant adds an extra radial menu step (`UserHasOpenedContextualRadial`) between TC selection and villager queue.
- Timer-based predicates use `Timer_Pause`/`Timer_Resume` — timer only advances while the relevant unit is actually idle.

### Exploration Markers

Five exploration markers tracked by `EnoughMarkersExplored`:
- `mkr_exploration_west`
- `mkr_exploration_east`
- `mkr_exploration_northwest`
- `mkr_exploration_north`
- `mkr_exploration_south`

Once 3 of 5 are revealed via `Player_CanSeePosition`, scout training hints are suppressed.

## CROSS-REFERENCES

### Imports

**core (`challenge_mission_earlyeconomy.scar`)**:
- `Cardinal.scar` — standard Cardinal framework
- `training/coretraininggoals.scar` — shared training goal framework
- `MissionOMatic/MissionOMatic_utility.scar` — Mission-o-Matic utility functions
- `challenge_mission_earlyeconomy_training.scar` — training goals specific to this mission
- `challenge_mission_earlyeconomy_preintro.scar` — pre-intro cinematic
- `cardinal_narrative.scar` — narrative/intel event system

**preintro (`challenge_mission_earlyeconomy_preintro.scar`)**:
- `Cardinal.scar`

**training (`challenge_mission_earlyeconomy_training.scar`)**:
- `training/coretrainingconditions.scar` — shared training condition predicates
- `training/coretraininggoals.scar` — shared training goal framework
- Registers module via `Core_RegisterModule("EarlyEconomyTrainingGoals")`

### Shared Globals

- `_challenge` — central data table shared across files; holds objectives, benchmarks, starting resources, icons, timer name, victory requirements
- `localPlayer` — player handle (World slot 1), used across all files
- `preintroFinished` / `cinematicFinished` — boolean flags set externally (by event system) to signal cinematic completion
- `EVENTS` — event table from `.events` import, referenced for narration (`Narr_Start`, `Narr_BuildMill`, `Narr_MissedGold`, `Camera_Outro`, etc.)
- `PLAYERS` — global player table iterated in most functions
- `townCenterLastIdleTime` — tracks last time TC was producing (for idle TC hint)
- `sg_preintro_*` — SGroups shared between preintro setup and cleanup functions
- `eg_minimap` — EGroup for minimap deer icons
- `houseBP`, `millBP`, `lumberCampBP`, `landmarkBP` — English building blueprints set in preintro, used in cleanup
- `landmarkEntity` — stores entity reference when landmark construction starts

### Inter-File Function Calls

- Core → Preintro: `EarlyEconomy_PreIntro_Setup_Scenes()` called from `Mission_PreStart`; `EarlyEconomy_PreIntro_Clean_Scenes()` called from `Mission_PreStart_PreIntroNISFinished`
- Core → Training: training module auto-initialized via `Core_RegisterModule("EarlyEconomyTrainingGoals")` calling `EarlyEconomyTrainingGoals_OnInit`
- Core disables default training in `Mission_Start`: `TrainingGoal_DisableAgeUpGoals()`, `TrainingGoal_DisableCoreControlGoals()`, `TrainingGoal_DisableCoreEconGoals()`
- Training reads `_challenge.victory.objectiveVillagers` completion state to suppress TC training hints once villager goal is met
- Training reads `player._challenge.startTime` to enforce grace periods before hints activate

### Building Restrictions

The following are removed from player production via `ITEM_REMOVED`:
- Military: barracks, archery range, cavalry stable, siege works, dock, outpost, keep
- Defensive: palisade wall/gate, stone wall/gate/bastion, tower
- Economic: market, additional town centers
- Units: `unit_archer_2_eng`
- Upgrades: all tier-2 harvest rate upgrades, Professional Scouts, Improved Enclosures, villager health
- Abilities: `core_unit_death` (delete units), `core_building_scuttle` (delete buildings)

### Notable Implementation Details

- Food and gold requirements for objectives are dynamically derived from `Player_GetEntityBPCost(localPlayer, landmarkBP)` rather than hardcoded, adapting to balance changes.
- The `_challenge.victory.objectiveVillagers` objective can be re-opened if the villager count drops below 21 after being completed (e.g., villager death).
- Similarly, food/gold objectives revert to incomplete if resources fall below thresholds before landmark construction starts.
- Medal objective timer uses `COUNT_UP` display but tracks thresholds internally — when a threshold is exceeded, the current medal objective is failed and the next tier is registered.
- The `ChallengeMission_RemindMill` function checks for both live sheep (`gaia_herdable_sheep` squads) and sheep carcasses (`carriable` entities) before determining sheep are exhausted.
- Secondary objectives are triggered by population/building thresholds in `ChallengeMission_OnBuildItemComplete` rather than being started at mission init.
- Scout intro rally uses `Modify_UnitSpeed` at 0.6× to slow the scout for cinematic pacing.
