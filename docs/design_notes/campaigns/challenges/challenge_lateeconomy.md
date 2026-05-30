# Challenge Mission: Late Economy

## OVERVIEW

The Late Economy challenge tasks the player (as Rus, starting in Castle Age) with building a booming economy and advancing to the Imperial Age under time pressure. The player must train 80 villagers, 30 traders, and construct an Imperial Age landmark to win. A medal system (Gold/Silver/Bronze) tracks completion time against benchmarks. Military buildings, defenses, and naval units are restricted — the focus is purely economic. A training hint system provides ongoing guidance for idle Town Centers, Markets, villagers, traders, and scouts.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_lateeconomy.scar` | core | Main mission logic: objectives, victory/defeat, medal benchmarks, restrictions, unit spawning, narrative hints, and annihilation check. |
| `challenge_mission_lateeconomy_preintro.scar` | other | Sets up animated pre-intro cinematic shots showing villagers farming, trading, building, and forestry. |
| `challenge_mission_lateeconomy_training.scar` | training | Registers and manages dynamic training goal sequences for idle TC/Market/Villager/Trader/Scout prompts. |

---

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | lateeconomy | Configures data tables, objectives, benchmarks, and Xbox overrides |
| `Mission_Preset` | lateeconomy | Calls game setup, player config, and restrictions |
| `Mission_PreStart` | lateeconomy | Runs pre-intro cinematic, holds mission start |
| `Mission_Start` | lateeconomy | Initializes objectives, registers events, starts rules |
| `Mission_PreStart_IntroNISFinished` | lateeconomy | Releases mission hold after intro, sets starting resources |
| `ChallengeMission_OnGameSetup` | lateeconomy | Creates localPlayer reference |
| `ChallengeMission_SetupPlayer` | lateeconomy | Sets Rus identity, Castle Age start, enables wonders |
| `ChallengeMission_SetRestrictions` | lateeconomy | Removes military/defense/naval buildings, units, and upgrades |
| `ChallengeMission_InitStartingUpgrades` | lateeconomy | Grants hunting gear upgrade at start |
| `ChallengeMission_FindAllResources` | lateeconomy | Caches all neutral wood/stone/gold resource egroups |
| `ChallengeMission_InitStartingUnits` | lateeconomy | Spawns farmers, foresters, miners, hunters, traders, scout |
| `ChallengeMission_AssignUnitsToResources` | lateeconomy | Auto-tasks each worker group to nearest resource |
| `ChallengeMission_PositionStartingUnits` | lateeconomy | Warps starting units to spawn markers for intro |
| `ChallengeMission_RallyStartingUnits` | lateeconomy | Formation-moves units to rally points after intro |
| `ChallengeMission_AssignTrader` | lateeconomy | Assigns starting traders to south settlement |
| `ChallengeMission_SetupChallenge` | lateeconomy | Creates per-player `_challenge` state table with timer |
| `ChallengeMission_InitializeObjectives` | lateeconomy | Registers and starts all primary/secondary/medal objectives |
| `ChallengeMission_Update` | lateeconomy | Polls villager/trader counts, updates counters and medals |
| `ChallengeMission_OnUpgradeComplete` | lateeconomy | Detects Imperial Age upgrade completion and econ techs |
| `ChallengeMission_OnConstructionComplete` | lateeconomy | Tracks TC/market/house/farm construction for secondaries |
| `ChallengeMission_OnDestruction` | lateeconomy | Triggers annihilation check on entity death |
| `ChallengeMission_CheckAnnihilation` | lateeconomy | Evaluates if player has no squads and cannot produce more |
| `ChallengeMission_CheckAgingUp` | lateeconomy | Warns player if aging up before meeting unit requirements |
| `ChallengeMission_CheckUnitCount` | lateeconomy | Triggers narration when villager+trader goals both met |
| `ChallengeMission_NarrativeHintSecondTownCenter` | lateeconomy | Plays hint when player can afford second TC |
| `ChallengeMission_NarrativeHintMarkets` | lateeconomy | Plays hint to build markets at pop ≥ 35 or wood > 550 |
| `ChallengeMission_NarrativeHintHouses` | lateeconomy | Plays hint when pop cap usage ≥ 85% |
| `ChallengeMission_NarrativeHintFarms` | lateeconomy | Plays hint at ≥ 25 villagers and food < 500 |
| `ChallengeMission_NarrativeHintTechnologies` | lateeconomy | Plays hint at pop ≥ 35 or gold > 500 |
| `ChallengeMission_MissedGold` | lateeconomy | Plays narration for missing gold medal time |
| `ChallengeMission_MissedSilver` | lateeconomy | Plays narration for missing silver medal time |
| `ChallengeMission_MissedBronze` | lateeconomy | Plays narration for missing bronze medal time |
| `ChallengeMission_OnComplete` | lateeconomy | Starts camera outro on victory objective completion |
| `ChallengeMission_EndChallenge` | lateeconomy | Sets player victorious, slows sim rate |
| `ChallengeMission_DefeatPresentation` | lateeconomy | Shows defeat message and stinger video |
| `EarlyEconomy_PreIntro_Setup_Scenes` | preintro | Gets blueprints, creates all preintro SGroups |
| `EarlyEconomy_PreIntro_Shot01_Units` | preintro | Spawns farmers/foresters/hunters, assigns to resources |
| `EarlyEconomy_PreIntro_Shot02_Units` | preintro | Spawns second farmers, queues farm builder and trader |
| `EarlyEconomy_PreIntro_Shot02_SpawnFarmerAtTownCenter` | preintro | Spawns villager to build a farm (delayed 4s) |
| `EarlyEconomy_PreIntro_Shot02_SpawnTraderAtMarket` | preintro | Spawns trader and moves to rally (delayed 11s) |
| `EarlyEconomy_PreIntro_Shot03_Units` | preintro | Spawns 8 builders, constructs Town Center |
| `EarlyEconomy_PreIntro_Shot03_ConstructTownCenter` | preintro | Issues TC construction command with 0.5x build time |
| `EarlyEconomy_PreIntro_Shot04_Units` | preintro | Spawns 5 foresters, assigns to nearest trees |
| `EarlyEconomy_PreIntro_Shot05_Units` | preintro | Spawns traders and cheering villagers |
| `EarlyEconomy_PreIntro_Clean_Scenes` | preintro | Destroys all preintro units/buildings, resets build time |
| `DespawnCarcasses` | preintro | Destroys all neutral carriable entities |
| `LateEconomyTrainingGoals_OnInit` | training | Registers all goal sequences (platform-aware) |
| `LateEconomyTrainingGoals_InitVillagerTraining` | training | Creates select-TC → train-villager goal sequence (PC) |
| `LateEconomyTrainingGoals_InitVillagerTraining_Xbox` | training | Same with radial menu step for Xbox |
| `LateEconomyTrainingGoals_InitTraderTraining` | training | Creates select-Market → train-trader goal sequence (PC) |
| `LateEconomyTrainingGoals_InitTraderTraining_Xbox` | training | Same with radial menu step for Xbox |
| `TrainingGoal_EnableLateEconomyGoals` | training | Enables all 5 late economy goal sequences |
| `TrainingGoal_DisableLateEconomyGoals` | training | Disables all 5 late economy goal sequences |
| `UserHasIdleTownCenter` | training | Predicate: checks for idle TC with resources to train |
| `UserHasIdleTownCenter_Xbox` | training | Xbox variant with 3-step radial goal |
| `UserHasIdleMarket` | training | Predicate: checks for idle Market with resources |
| `UserHasIdleMarket_Xbox` | training | Xbox variant with 3-step radial goal |
| `UserHasIdleScout` | training | Predicate: checks for idle Scout unit |
| `SelectNextIdleIfVillagersIdle` | training | Predicate: prompts idle villager selection via pop button |
| `SelectNextIdleIfTradersIdle` | training | Predicate: prompts idle trader selection via pop button |
| `EnoughMarkersExplored` | training | Ignore condition: stops scout hints after 3 areas explored |
| `UserHasSelectedTownCenter` | training | IsComplete: checks if TC is selected |
| `TCHasStartedToTrainAVillager` | training | IsComplete: checks if selected TC is producing villager |
| `UserHasSelectedMarket` | training | IsComplete: checks if Market is selected |
| `MarketHasStartedToTrainATrader` | training | IsComplete: checks if selected Market is producing trader |
| `UserHasNoMeansMarket` | training | Ignore: player lacks resources or pop for trader |
| `UserHasNoMeansTownCenter` | training | Ignore: player lacks food or pop for villager |

---

## KEY SYSTEMS

### Objectives

**Primary (`_challenge.victory`)**
| Objective | Purpose |
|-----------|---------|
| `objectiveVictory` | OT_Primary — "Build a booming economy"; completes when all sub-objectives done |
| `objectiveVillagers` | OT_Secondary — Train 80 villagers (counter tracked, reverts if count drops) |
| `objectiveTraders` | OT_Secondary — Train 30 traders (counter tracked, reverts if count drops) |
| `objectiveLandmark` | OT_Secondary — Build Imperial Age landmark |

**Secondary (`_challenge.secondary`)**
| Objective | Purpose |
|-----------|---------|
| `objectiveVictory` | OT_Secondary — "Expand your base"; completes when all secondaries done |
| `objectiveSecondTownCenter` | Build a second Town Center |
| `objectiveAddTownCenters` | Build 4 total Town Centers |
| `objectiveAddMarkets` | Build 4 total Markets |
| `objectiveAddHouses` | Build houses until pop usage < 85% |
| `objectiveAddFarms` | Build 20 total farms |
| `objectiveResearchTechs` | Research 3 economic technologies |

**Benchmarks (OT_Bonus medals)**
| Medal | PC Time | Xbox Time |
|-------|---------|-----------|
| Gold | 10m 30s | 10m 45s |
| Silver | 15m 30s | 16m 00s |
| Bronze | 19m 30s | 20m 00s |
| Unplaced | No limit | No limit |

### Difficulty

No `Util_DifVar` calls are present. The challenge is single-difficulty with fixed thresholds. Xbox gets slightly relaxed medal times via `UI_IsXboxUI()` check.

### Spawns

**Starting Units (Castle Age Rus):**
- 2 + 2 farmers (at two farm clusters)
- 1 fisherman
- 7 foresters
- 2 gold miners
- 2 stone miners
- 4 hunters (+ 1 deer spawned)
- 2 + 2 traders (assigned to south settlement)
- 1 scout

**Starting Resources:** 400 food, 560 wood, 100 gold, 400 stone

**Starting Upgrades:** `upgrade_econ_villager_hunting_gear_1`

**Pre-Intro Cinematic Units (temporary):**
- Shot 1: 3 farmers, 4 foresters, 2 hunters
- Shot 2: 2 farmers, 1 farm builder (delayed 4s), 1 trader (delayed 11s)
- Shot 3: 8 TC builders (0.5x build time modifier)
- Shot 4: 5 foresters
- Shot 5: 2 traders, 4 cheering villagers
- All despawned via `EarlyEconomy_PreIntro_Clean_Scenes` before gameplay begins

### AI

No AI players. Single-player challenge; `localPlayer` is the only participant.

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `ChallengeMission_Update` | 0.125s | Polls villager/trader counts, updates medal brackets |
| `ChallengeMission_NarrativeHintSecondTownCenter` | 0.5s | Checks if player can afford 2nd TC |
| `ChallengeMission_NarrativeHintMarkets` | 0.5s | Checks if player should build markets |
| `ChallengeMission_NarrativeHintHouses` | 3s (→ 35s) | Checks pop cap usage ≥ 85%; interval increases after triggering |
| `ChallengeMission_NarrativeHintFarms` | 0.5s | Checks if farms needed |
| `ChallengeMission_NarrativeHintTechnologies` | 0.5s | Checks if research should begin |
| `ChallengeMission_CheckAgingUp` | 0.5s | Warns if aging up prematurely |
| `ChallengeMission_CheckUnitCount` | 0.5s | Narrates when both unit goals met |
| `Mission_PreStart_IntroNISFinished` | 0.125s | Waits for intro event to finish |
| `EarlyEconomy_PreIntro_Shot02_SpawnFarmerAtTownCenter` | OneShot 4s | Delayed farmer spawn in pre-intro |
| `EarlyEconomy_PreIntro_Shot02_SpawnTraderAtMarket` | OneShot 11s | Delayed trader spawn in pre-intro |
| `EarlyEconomy_PreIntro_Shot03_ConstructTownCenter` | OneShot 0.1s | Immediate TC build command |
| `ChallengeMission_MissedGold` | OneShot 1.2s | Plays missed-gold narration |
| `ChallengeMission_MissedSilver` | OneShot 1.2s | Plays missed-silver narration |
| `ChallengeMission_MissedBronze` | OneShot 1.2s | Plays missed-bronze narration |
| Per-player `challengeTimer_N` | Medal-based | Tracks elapsed time against current medal goal |

**Training Hint Timing Variables:**
| Variable | Value | Purpose |
|----------|-------|---------|
| `__t_challengeStartIdleTC` | 15s | Delay before first idle TC hint |
| `__t_challengeIntervalIdleTC` | 5s | Repeat interval for idle TC hint |
| `__t_challengeStartIdleMarket` | 20s | Delay before first idle Market hint |
| `__t_challengeIntervalIdleMarket` | 5s | Repeat interval for idle Market hint |
| `__t_challengeStartIdleVillager` | 10s | Delay before first idle villager hint |
| `__t_challengeIntervalIdleVillager` | 5s | Repeat interval for idle villager hint |
| `__t_challengeStartIdleTrader` | 15s | Delay before first idle trader hint |
| `__t_challengeIntervalIdleTrader` | 10s | Repeat interval for idle trader hint |
| `__t_challengeStartIdleScout` | 30s | Delay before first idle scout hint |
| `__t_challengeIntervalIdleScout` | 20s | Repeat interval for idle scout hint |
| `__n_challengeScoutAreasToExplore` | 3 | Areas to explore before scout hints stop |

---

## CROSS-REFERENCES

### Imports
| File | Imports |
|------|---------|
| `challenge_mission_lateeconomy.scar` | `Cardinal.scar`, `training/coretraininggoals.scar`, `challenge_mission_lateeconomy_training.scar`, `challenge_mission_lateeconomy_preintro.scar` |
| `challenge_mission_lateeconomy_preintro.scar` | `Cardinal.scar` |
| `challenge_mission_lateeconomy_training.scar` | `training/coretrainingconditions.scar`, `training/coretraininggoals.scar` |

### Module Registration
- `challenge_mission_lateeconomy_training.scar` registers `"LateEconomyTrainingGoals"` via `Core_RegisterModule`, exposing `LateEconomyTrainingGoals_OnInit` as a lifecycle callback.

### Shared Globals
- `localPlayer` — created in core, used across all three files
- `_challenge` — main data table defined in core, read by training predicates (e.g., `_challenge.victory.objectiveVillagers`)
- `eg_allWoodResources` — created in core's `FindAllResources`, referenced by preintro for tree assignment
- `eg_farms` — shared between preintro (Shot01/02 farm assignment) and core (post-intro farmer assignment)
- `sg_single`, `eg_single` — reusable scratch groups used throughout all files
- `sg_player_startingscouts` — created in core, referenced in preintro cleanup

### Inter-File Function Calls
- Core calls `EarlyEconomy_PreIntro_Setup_Scenes()` and the preintro clean-up functions from `Mission_PreStart`
- Core references `EVENTS.LateEconomy_PreIntro` for the intro Intel sequence
- Training predicates reference `_challenge.victory.objectiveVillagers` and `_challenge.victory.objectiveTraders` to stop prompting after objectives are complete

### Blueprint References (Rus)
- Buildings: `building_town_center_rus`, `building_resource_farm_control_rus`, plus 15+ removed military/defense buildings
- Units: `unit_villager_1_rus`, `unit_trade_cart_rus`, `unit_scout_1_rus`, `gaia_huntable_deer`
- Upgrades: `upgrade_econ_villager_hunting_gear_1`, `imperial_age`, plus 10+ removed military/naval upgrades
- Annihilation type map: town_center→villager, barracks→spearman, archery_range→archer, stable→horseman, siege_workshop→springald, monastery→monk

### Event/Intel Keys
`EVENTS.LateEconomy_PreIntro`, `EVENTS.Narr_Start`, `EVENTS.Narr_BuildTownCenter`, `EVENTS.Narr_TownCenterComplete`, `EVENTS.Narr_BuildMarkets`, `EVENTS.Narr_BuildHouses`, `EVENTS.Narr_BuildFarms`, `EVENTS.Narr_Research`, `EVENTS.Narr_ConstructingLandmark`, `EVENTS.Narr_EnoughUnits`, `EVENTS.Narr_MissedGold`, `EVENTS.Narr_MissedSilver`, `EVENTS.Narr_MissedBronze`, `EVENTS.Camera_Outro`
