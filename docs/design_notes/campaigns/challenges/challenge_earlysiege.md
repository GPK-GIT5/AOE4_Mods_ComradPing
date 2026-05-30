# Challenge Mission: Early Siege

## OVERVIEW

Challenge Mission: Early Siege is a timed Mongol vs Rus scenario where the player must destroy the enemy Town Center and Kremlin Landmark as fast as possible to earn medal rankings (Gold ≤6min, Silver ≤10min, Bronze ≤20min). The player starts in Castle Age with 16 archers, 16 spearmen, 3 scouts, and resources (1700 wood, 800 gold, 600 stone) plus access to siege construction via the Siege Engineers upgrade. The Rus enemy defends a walled fortress with archers, men-at-arms, spearmen, mangonels, springalds, and wall garrisons deployed across multiple defense zones managed by MissionOMatic Defend modules. A 5-shot cinematic pre-intro showcases siege unit types (rams, springalds, mangonels) before gameplay begins. If the player loses all units and cannot produce more, reinforcements spawn but medals are forfeited.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_earlysiege.scar` | core | Main mission logic: objectives, victory/defeat, medal system, enemy AI defense, unit spawning, restrictions, and MissionOMatic recipe |
| `challenge_mission_earlysiege_preintro.scar` | other (cinematic) | 5-shot pre-intro cinematic spawning demonstration armies showcasing rams, springalds, mangonels, and full army formations |
| `challenge_mission_earlysiege_training.scar` | training | Tutorial hint system guiding players through building rams, springalds, mangonels, and siege towers with goal sequences |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnInit` | earlysiege | Configures objectives, benchmarks, minimap blips, annihilation costs |
| `Mission_OnGameSetup` | earlysiege | Sets player references, disables landmark rebuild |
| `Mission_Preset` | earlysiege | Calls player setup and restriction functions |
| `Mission_PreStart` | earlysiege | Spawns units, upgrades, starts patrols, holds for cinematic |
| `Mission_Start` | earlysiege | Initializes objectives, registers events, starts update loops |
| `Mission_PreStart_IntroNISFinished` | earlysiege | Releases mission hold when cinematic ends |
| `ChallengeMission_SetupChallengePlayers` | earlysiege | Sets both players to Castle Age, names them |
| `GetRecipe` | earlysiege | Defines MissionOMatic recipe with Defend and TownLife modules |
| `ChallengeMission_SetupChallenge` | earlysiege | Creates per-player challenge state, reveals objectives, sets 10x production |
| `ChallengeMission_InitStartingUnits` | earlysiege | Spawns player army and all enemy garrison units |
| `ChallengeMission_InitStartingUpgrades` | earlysiege | Grants arrow slits, siege engineers, unit upgrades |
| `ChallengeMission_SetRestrictions` | earlysiege | Removes Age 4 units/techs, enemy economy upgrades |
| `ChallengeMission_FindAllResources` | earlysiege | Catalogs all neutral wood, stone, gold on map |
| `ChallengeMission_InitTownLifeModules` | earlysiege | Assigns enemy villagers to TownLife economic modules |
| `ChallengeMission_InitFisherman` | earlysiege | Workaround to assign fishermen to shore fish deposits |
| `ChallengeMission_InitCombatModules` | earlysiege | Assigns enemy squads to Defend zone modules |
| `ChallengeMission_RallyMilitary` | earlysiege | Moves all enemy military to their rally positions |
| `ChallengeMission_RallySpearmen` | earlysiege | Positions enemy spearmen and springalds at waypoints |
| `ChallengeMission_RallyWallArchers` | earlysiege | Positions wall archers in arc formations behind walls |
| `ChallengeMission_InitializeObjectives` | earlysiege | Registers primary, secondary, and medal objectives |
| `ChallengeMission_Update` | earlysiege | Main loop: checks victory, manages medal timer transitions |
| `ChallengeMission_OnDestruction` | earlysiege | GE_EntityKilled handler: tracks objectives, wall breach, annihilation |
| `ChallengeMission_CheckVictory` | earlysiege | Completes mission when both key buildings destroyed |
| `ChallengeMission_CheckAnnihilation` | earlysiege | Checks if player lost all non-scout/gaia squads |
| `CheckEarlySiegeAnnihiliation` | earlysiege | Interval check: evaluates if player can still produce units |
| `EarlySiegeReinforcements` | earlysiege | Respawns full starting army, resets resources, forfeits medals |
| `ChallengeMission_MusicCheck` | earlysiege | Adjusts music intensity based on player proximity to zones |
| `ChallengeMission_MissedGold` | earlysiege | Plays narration when gold medal time expires |
| `ChallengeMission_MissedSilver` | earlysiege | Plays narration when silver medal time expires |
| `ChallengeMission_MissedBronze` | earlysiege | Plays narration when bronze medal time expires |
| `WallArchersReset` | earlysiege | Repositions wall archers in arc after losing 2 units |
| `WallArchersRetreat` | earlysiege | Retreats wall archers to Town Center after wall breach |
| `DefendWithArchers` | earlysiege | Archers prioritize ranged siege, then any attackers near gate |
| `DefendWithMenAtArms` | earlysiege | Men-at-arms prioritize rams, then any attackers in outer zone |
| `DefendWithSpearmen` | earlysiege | Spearmen prioritize rams, then any attackers in inner zone |
| `DefendWithSpringalds` | earlysiege | Springalds prioritize siege, then any attackers in inner zone |
| `PositionEnemySpearmen` | earlysiege | Moves spearmen to block inner zone entrance on detection |
| `MenAtArmsPatrolLeft` | earlysiege | Patrol waypoint handler: right → center |
| `MenAtArmsPatrolCenter` | earlysiege | Patrol waypoint handler: center → left or right |
| `MenAtArmsPatrolRight` | earlysiege | Patrol waypoint handler: left → center |
| `EnemyPatrolDetectedPlayer` | earlysiege | Reveals ford zone and plays narration on player proximity |
| `EnemyPatrolAttackPlayer` | earlysiege | Ends patrol, attacks player when within 40 range |
| `EnemyGarrisonWoodFort` | earlysiege | Garrisons nearby villagers into wooden fortress on attack |
| `SetVillagersToHunt` | earlysiege | Assigns enemy hunters to nearest deer deposits |
| `ChallengeMission_InitializeOutro` | earlysiege | Makes player units invulnerable, sets buildings on fire |
| `ChallengeMission_CheckCheer` | earlysiege | Triggers victory cheering when no enemies remain nearby |
| `ChallengeMission_SetBuildingsOnFire` | earlysiege | Randomly damages and ignites enemy buildings for outro |
| `ChallengeMission_EndChallenge` | earlysiege | Sets player victorious, slows sim rate |
| `ArcFormation` | earlysiege | Arranges squad in curved line between two positions |
| `ScriptScatterUnits` | earlysiege | Scatters units away from center point by distance |
| `EarlySiegeTrainingHelper` | earlysiege | Resets construction phase when infantry deselected |
| `EarlySiege_PreIntro_Shot01_Units` | preintro | Shot 1: spawns enemy archers, spearmen, horsemen in formations |
| `EarlySiege_PreIntro_Shot02_Units` | preintro | Shot 2: spawns player spearmen, initiates ram construction |
| `EarlySiege_PreIntro_Shot02_Build_Ram` | preintro | Orders spearmen to construct ram with 0.5x build time |
| `EarlySiege_PreIntro_Shot02_Delayed_Scatter` | preintro | Scatters spearmen away from completed ram |
| `EarlySiege_PreIntro_Shot02_RamComplete` | preintro | Detects ram completion, triggers move and garrison |
| `EarlySiege_PreIntro_Shot02_Move_Ram` | preintro | Moves ram toward enemy at reduced speed |
| `EarlySiege_PreIntro_Shot02_Garrison` | preintro | Orders spearmen to garrison completed ram |
| `EarlySiege_PreIntro_Shot03_Units` | preintro | Shot 3: spawns player springalds vs enemy MAA |
| `EarlySiege_PreIntro_Shot03_Attack` | preintro | Springalds attack MAA then attack-move |
| `EarlySiege_PreIntro_Shot04_Units` | preintro | Shot 4: spawns player mangonels vs enemy archers |
| `EarlySiege_PreIntro_Shot05_Units` | preintro | Shot 5: full army with rams, mangonels, horsemen, infantry |
| `EarlySiegeCheer` | preintro | Garrisons infantry into rams, moves rams toward gates |
| `EarlySiegeFinalPositions` | preintro | Positions archers and horsemen for final cinematic shot |
| `EarlySiege_PreIntro_CleanUpAll` | preintro | Destroys all cinematic units/buildings, resets fog/resources |
| `EarlySiegeTrainingGoals_OnInit` | training | Registers all siege training goal sequences |
| `EarlySiegeTrainingGoals_InitRamHint` | training | Creates PC ram-building tutorial goal sequence |
| `EarlySiegeTrainingGoals_InitRamHint_Xbox` | training | Creates Xbox ram-building tutorial with radial menu step |
| `TrainingGoal_EnableEarlySiegeGoals` | training | Enables all 5 siege training goal sequences |
| `TrainingGoal_DisableEarlySiegeGoals` | training | Disables all 5 siege training goal sequences |
| `UserHasIdleSiegeEngineers` | training | Predicate: checks for idle infantry after 15s delay |
| `UserHasIdleSiegeEngineers_Xbox` | training | Xbox predicate: checks for idle infantry with radial context |
| `UserHasSelectedSiegeEngineer` | training | Goal: validates infantry selected for ram construction |
| `UserIsBuildingBatteringRam` | training | Goal: detects ram placement phase active |
| `UserHasBuiltBatteringRam` | training | Goal: confirms ram construction started |
| `RamStartedIgnorePredicate` | training | Ignore predicate: suppresses hint if ram already exists |
| `RamBuiltPredicate` | training | Predicate: detects completed ram for garrison hint |
| `UserHasSelectedBatteringRam` | training | Goal: confirms player selected a built ram |
| `SpringaldBuiltPredicate` | training | Predicate: detects player-built springald |
| `UserHasSelectedSpringald` | training | Goal: confirms player selected a springald |
| `MangonelBuiltPredicate` | training | Predicate: detects player-built mangonel |
| `UserHasSelectedMangonelIntro` | training | Goal: confirms player selected a mangonel |
| `SiegeTowerBuiltPredicate` | training | Predicate: detects siege tower construction attempt |
| `UserHasSelectedSiegeTower` | training | Goal: dismisses warning when construction cancelled |

## KEY SYSTEMS

### Objectives

| Constant/Variable | Purpose |
|---|---|
| `_challenge.victory.objectiveVictory` | Primary: "Defeat the Rus" — completes mission on fulfillment |
| `_challenge.victory.objectiveSub1` | Secondary: "Destroy the Rus Town Center" — tracked via `enemy_capital` EGroup |
| `_challenge.victory.objectiveSub2` | Secondary: "Destroy the Kremlin Landmark" — tracked via `enemy_landmark` EGroup |
| `_challenge.benchmarks.gold.objective` | Bonus: Gold medal — complete within 6 min (7 min Xbox) |
| `_challenge.benchmarks.silver.objective` | Bonus: Silver medal — complete within 10 min (12 min Xbox) |
| `_challenge.benchmarks.bronze.objective` | Bonus: Bronze medal — complete within 20 min (both platforms) |
| `_challenge.benchmarks.unplaced.objective` | Bonus: Time elapsed display — no medal tier |
| `_challenge.victory.failedMedals` | Information: shown when medals forfeited due to reinforcements |
| `_challenge.victory.completionRequirement` | Integer `2` — both sub-objectives required for victory |
| `_challenge.victory.hasBreachedWall` | Boolean — tracks first wall segment destroyed |

### Difficulty

No `Util_DifVar` calls are present. This is a single-difficulty challenge mission. Medal thresholds serve as effective difficulty scaling:

| Parameter | PC Value | Xbox Value |
|-----------|----------|------------|
| Gold time | 6 min | 7 min |
| Silver time | 10 min | 12 min |
| Bronze time | 20 min | 20 min |

Production speed is set to 10x for the player. Ram build time is modified to 0.1x (10x faster). Siege Engineers upgrade is pre-completed for the player.

### Spawns

**Player Starting Army:**
- 16× Mongol Archers (Age 3) at `mkr_player_spearmen1_spawn`
- 16× Mongol Spearmen (Age 3) at `mkr_player_spearmen2_spawn`
- 3× Mongol Scouts at `mkr_player_scout_spawn`

**Enemy Static Garrison:**
- 2× Rus Springalds at `mkr_inner_springald_spawn`
- 1× Rus Mangonel at `mkr_enemy_mangonel_spawn`
- 6× Rus Men-at-Arms at `mkr_enemy_menatarms_spawn`
- 5× Rus Men-at-Arms (patrol group) at `mkr_menatarms_patrol_right`
- 10× Rus Archers at `mkr_enemy_archers_spawn`
- 10× Rus Spearmen at `mkr_enemy_spearmen_spawn`
- 8× Rus Archers (wall group 1) at `mkr_enemy_wall_archers_spawn01`
- 7× Rus Archers (wall group 2) at `mkr_enemy_wall_archers_spawn01`
- 2× Rus Villagers (fishermen group 0) at `mkr_enemy_fisherman0_spawn`
- 1× Rus Villager (fisherman group 1) at `mkr_enemy_fisherman1_spawn`
- 2× Rus Villagers (hunters) at `mkr_enemy_hunter_spawn`

**Reinforcements (on annihilation):** Full starting army re-deployed at original spawn markers, resources reset to starting values. Medals are permanently forfeited.

**Cinematic Units (pre-intro, destroyed on cleanup):**
- Shot 1: 16 enemy archers, 5 enemy spearmen, 10 enemy horsemen
- Shot 2: 12 player spearmen + constructed ram
- Shot 3: 4 player springalds, 2 enemy mangonels, 12 enemy MAA
- Shot 4: 2 player mangonels, 13 enemy archers
- Shot 5: Full player army (2 rams, 3 mangonels, 1 horseman, 26 spearmen, 10 archers) + 5 enemy spearmen

### AI

**No `AI_Enable` calls.** Enemy behavior is entirely scripted via rules:

- **MissionOMatic Defend Modules:** 4 zones — DefendOuter (men-at-arms), DefendInner (spearmen + springalds), DefendGate (archers), DefendFord (mangonels)
- **MissionOMatic TownLife Modules:** 4 zones — FarmingEcon (12 food villagers), WoodEcon (4 wood), FishingEcon (2 food), HuntingEcon (2 food). All `maxVillagers = 0`, `canBuild = false`
- **Patrol System:** 5 men-at-arms patrol left↔center↔right waypoints. On player proximity (<70): reveals ford zone + narration. On proximity (<40): attack-moves to player, garrisons nearby villagers in wooden fortress, removes patrol rules
- **Reactive Defense (post-wall-breach):** `DefendWithArchers` targets ranged siege first, then any units near gate zone. `DefendWithMenAtArms` targets rams first, then any units in outer zone. `DefendWithSpearmen` targets rams first, then any units in inner zone. `DefendWithSpringalds` targets siege first, then any units in inner zone
- **Wall Archers:** Reset to arc formation behind walls every time 2 are lost. On wall breach, retreat to Town Center area
- **Spearmen Repositioning:** `PositionEnemySpearmen` moves spearmen to block inner zone entrance when player detected within 40 range

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `ChallengeMission_Update` | `Rule_AddInterval`, 0.125s | Main objective/medal update loop |
| `ChallengeMission_MusicCheck` | `Rule_AddInterval`, 1s | Updates music intensity by player position |
| `CheckEarlySiegeAnnihiliation` | `Rule_AddInterval`, 0.5s | Monitors player unit count for reinforcement trigger |
| `EnemyPatrolDetectedPlayer` | `Rule_AddInterval`, 0.5s | Checks proximity for patrol detection narration |
| `EnemyPatrolAttackPlayer` | `Rule_AddInterval`, 0.5s | Checks proximity for patrol attack trigger |
| `MenAtArmsPatrolLeft/Center/Right` | `Rule_AddInterval`, 1s | Patrol waypoint navigation |
| `PositionEnemySpearmen` | `Rule_AddInterval`, 1s | Moves spearmen to block inner zone on detection |
| `WallArchersReset` | `Rule_AddInterval`, 0.5s | Repositions wall archers after losses |
| `DefendWithArchers` | `Rule_AddInterval`, 3.5s | Post-breach: archers target attackers near gate |
| `DefendWithMenAtArms` | `Rule_AddInterval`, 3.5s | Post-breach: MAA target attackers in outer zone |
| `DefendWithSpearmen` | `Rule_AddInterval`, 3.5s | Post-breach: spearmen target attackers in inner zone |
| `DefendWithSpringalds` | `Rule_AddInterval`, 5s | Post-breach: springalds target siege in inner zone |
| `EarlySiegeTrainingHelper` | `Rule_AddInterval`, 0.125s | Resets construction phase on infantry deselection |
| `ChallengeMission_RallyMilitary` | `Rule_AddOneShot`, 10s | Positions all enemy military after mission start |
| `ChallengeMission_InitFisherman` | `Rule_AddOneShot`, 2s | Deferred fisherman assignment workaround |
| `Mission_PreStart_IntroNISFinished` | `Rule_AddInterval`, 0.125s | Polls for cinematic end to release mission hold |
| Reinforcement grace timer | 10s (via `World_GetGameTime`) | Waits 10s after units lost before granting reinforcements |

### Starting Resources

| Resource | Amount |
|----------|--------|
| Food | 0 |
| Wood | 1,700 |
| Gold | 800 |
| Stone | 600 |

### Starting Upgrades

**Player (Mongol):** Siege Engineers, Siege Weapon Speed, Raid Bounty
**Enemy (Rus):** Arrow Slits (outposts), Boiling Oil, Spearman 2 & 3, Archer 3

### Unit/Tech Restrictions

**Player:** Age 4 siege (trebuchet, bombard) removed. Trade cart removed. Advanced field constructs removed. Multiple Ovoo/Mongol-specific techs removed. Pack building ability removed.
**Enemy:** MAA/Archer/Spearman Age 3 upgrades removed. Horseman 3, Knight 4, Crossbowman 4 removed. All economy upgrades removed. Villager and fishing boat production removed. Outpost cannon/springald/stone upgrades removed.

## CROSS-REFERENCES

### Imports

| Import | File |
|--------|------|
| `Cardinal.scar` | earlysiege |
| `training/coretraininggoals.scar` | earlysiege, training |
| `training/coretrainingconditions.scar` | training |
| `MissionOMatic/MissionOMatic.scar` | earlysiege |
| `MissionOMatic/MissionOMatic_utility.scar` | earlysiege |
| `challenge_mission_earlysiege_training.scar` | earlysiege |
| `challenge_mission_earlysiege_preintro.scar` | earlysiege |

### Inter-File Function Calls

- `earlysiege.scar` → `EarlySiegeTrainingGoals_OnInit()` (defined in training file)
- `earlysiege.scar` → `TrainingGoal_EnableEarlySiegeGoals()` (defined in training file)
- `earlysiege.scar` → `EarlySiege_PreIntro_CleanUpAll()` (defined in preintro file)
- `earlysiege.scar` → `EarlySiegeTrainingHelper()` interval calls training file state variables (`selectSiegeEngineersCount`, `placingRamPhaseActive`)
- preintro file reads globals: `localPlayer`, `enemyPlayer`, `cinematicFinished`, `_challenge.startingResources`
- training file reads globals: `localPlayer`, `training_currentConstructionPhase`

### Shared Globals

- `localPlayer` / `enemyPlayer` — player references used across all 3 files
- `cinematicFinished` — boolean flag checked by preintro shots, set in earlysiege
- `_challenge` — main data table (resources, benchmarks, victory state) used by earlysiege and preintro cleanup
- `playerGotReinforcements` — annihilation flag affecting medal logic
- `sg_single` / `eg_single` — shared temporary SGroup/EGroup for single-unit operations

### MissionOMatic Integration

Uses `GetRecipe()` pattern with 4 Defend modules and 4 TownLife modules. Modules are populated post-spawn via `Prefab_DoAction` and `MissionOMatic_FindModule`. Intro/outro NIS events referenced as `EVENTS.EarlySiege_PreIntro` and `EVENTS.EarlySiege_Outro`.

### Event Cues / Narration Events

- `EVENTS.NarrationAtStart` — start dialogue
- `EVENTS.NarrRamIntro` — ram introduction narration
- `EVENTS.NarrEnemyPatrols` — patrol detection narration
- `EVENTS.NarrEnteredWalls` — wall breach narration
- `EVENTS.NarrTargetPriority` — non-critical building destroyed hint
- `EVENTS.NarrDestroyTC` — Town Center destroyed narration
- `EVENTS.NarrDestroyKremlin` — Kremlin destroyed narration
- `EVENTS.NarrGoldFailed` / `NarrSilverFailed` / `NarrBronzeFailed` — medal expiry narration
