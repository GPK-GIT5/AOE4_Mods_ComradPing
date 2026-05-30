# Challenge Mission: Late Siege

## OVERVIEW

Challenge Mission: Late Siege is a timed scenario where the player controls a Delhi Sultanate (Imperial Age) army besieging a Holy Roman Empire (Castle Age) walled city. The player must destroy all three key enemy buildings — the Town Center, Aachen Chapel landmark, and Regnitz Cathedral landmark — as fast as possible to earn medals (Gold ≤6min, Silver ≤9min, Bronze ≤15min; Xbox: 7/10/16min). The mission features a multi-shot cinematic pre-intro showing siege weapons being built and walls being attacked, followed by gameplay with proximity-triggered enemy responses, knight patrols, gate sally-forth logic, and landmark defense AI. If the player loses all units, reinforcements are spawned (but medals are forfeited). Starting resources are dynamically calculated to afford 2 trebuchets, 1 bombard, 1 ram, and 1 siege tower.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_latesiege.scar` | core | Main mission script: setup, objectives, victory/medal tracking, AI defense logic, annihilation/reinforcement, outro |
| `challenge_mission_latesiege_preintro.scar` | other (cinematic) | Multi-shot pre-intro cinematic deploying units, siege construction, wall attacks, building fires, and cleanup |
| `challenge_mission_latesiege_training.scar` | training | Tutorial goal sequences teaching siege tower, ram, springald, mangonel, trebuchet, and bombard usage |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `LateSiege_PreIntro_Shot01_Units` | preintro | Deploy enemy archers/spearmen/MAA on walls in arc formation |
| `LateSiege_PreIntro_Shot01_Face_Archers` | preintro | Nudge gate archers forward to wall edge |
| `LateSiege_PreIntro_Shot01_Face_Archers2` | preintro | Nudge long-wall archers forward to wall edge |
| `LateSiege_PreIntro_Shot02_Units` | preintro | Spawn player MAA and order ram/siege tower construction |
| `LateSiege_PreIntro_Shot02_Delayed_Scatter` | preintro | Scatter MAA away from siege tower build sites |
| `LateSiege_PreIntro_Shot02_Delayed_Scatter2` | preintro | Scatter MAA away from ram build site |
| `LateSiege_PreIntro_Shot02_SiegeTower_Halt` | preintro | Freeze completed siege tower in place |
| `LateSiege_PreIntro_Shot02_Ram_Halt` | preintro | Freeze completed ram in place |
| `LateSiege_PreIntro_Shot03_Units` | preintro | Deploy siege towers and ram; garrison and attack |
| `LateSiege_PreIntro_Shot03_SiegeTower_Unload` | preintro | Unload siege tower 1 onto nearest wall segment |
| `LateSiege_PreIntro_Shot03_SiegeTower_Unload2` | preintro | Unload siege tower 2 onto nearest wall segment |
| `LateSiege_PreIntro_Shot03_SiegeTower_AttackArchers` | preintro | Attack-move unloaded infantry toward enemy archers |
| `LateSiege_PreIntro_Shot04_Units` | preintro | Deploy trebuchet/bombard; damage/set fire to buildings |
| `LateSiege_PreIntro_Shot04_AttackWall` | preintro | Order trebuchet and bombard to attack closest wall |
| `LateSiege_PreIntro_Shot04_ClearWallSection` | preintro | Move archers away from wall under bombardment |
| `LateSiege_PreIntro_Shot05_Units` | preintro | Spawn hidden gate-holder unit; damage remaining buildings |
| `LateSiege_PreIntro_CleanUpAll` | preintro | Master cleanup calling all shot cleanup functions |
| `LateSiege_PreIntro_CleanUp05_Unreveal_Map` | preintro | Reset FOW after cinematic; unhide naval buildings |
| `LateSiege_PreIntro_CleanUp_ResetResources` | preintro | Reset player resources after cinematic cancellation |
| `ArcFormation` | preintro | Position SGroup units in curved line formation |
| `ScriptScatterUnits` | preintro | Scatter SGroup units away from a center point |
| `Mission_OnInit` | latesiege | Initialize challenge data, objectives, medal benchmarks |
| `Mission_OnGameSetup` | latesiege | Disable landmark rebuild for both players |
| `Mission_Preset` | latesiege | Setup players and apply restrictions |
| `Mission_PreStart` | latesiege | Spawn starting units/upgrades; hold for cinematic |
| `Mission_Start` | latesiege | Setup challenge, objectives, register event callbacks |
| `GetRecipe` | latesiege | Define MissionOMatic recipe with zones and TownLife |
| `ChallengeMission_SetupChallengePlayers` | latesiege | Set player ages (Imperial vs Castle) and names |
| `ChallengeMission_SetRestrictions` | latesiege | Remove madrasa/outpost upgrades and wall construction |
| `ChallengeMission_SetupChallenge` | latesiege | Configure pop cap, production speed 10x, FOW reveals |
| `ChallengeMission_InitStartingUnits` | latesiege | Spawn player and enemy armies at designated markers |
| `ChallengeMission_InitStartingUpgrades` | latesiege | Grant siege engineers, archer 3, boiling oil upgrades |
| `ChallengeMission_InitCombatModules` | latesiege | Assign enemy units to MissionOMatic defend modules |
| `ChallengeMission_RallyEnemyArchers` | latesiege | Position 18 archer groups on walls in arc formations |
| `ChallengeMission_RallyEnemyMilitary` | latesiege | Move spearmen, MAA, and knights to rally points |
| `ChallengeMission_RallyPlayerMilitary` | latesiege | Face and position all player starting units |
| `ChallengeMission_PatrolEnemyKnights` | latesiege | Start 3-point knight patrol system with attack triggers |
| `ChallengeMission_PatrolEnemyKnights1` | latesiege | Handle knight patrol at point 1 with proximity attack |
| `ChallengeMission_PatrolEnemyKnights2` | latesiege | Handle knight patrol at point 2 with direction toggle |
| `ChallengeMission_PatrolEnemyKnights3` | latesiege | Handle knight patrol at point 3 with proximity attack |
| `ChallengeMission_InitializeObjectives` | latesiege | Register primary/secondary/medal objectives with UI elements |
| `ChallengeMission_Update` | latesiege | Tick medal timer; transition gold→silver→bronze→unplaced |
| `ChallengeMission_GateUnderAttack` | latesiege | Send spearmen to defend gate when attacked |
| `ChallengeMission_DefendAfterSallyForth` | latesiege | Continue targeting siege outside gate; retreat if clear |
| `ChallengeMission_ProximityInner` | latesiege | Activate inner defense when player nears inner trigger |
| `ChallengeMission_ProximityGate` | latesiege | Sally forth spearmen when player nears gate |
| `ChallengeMission_ProximityWest` | latesiege | Send knights to defend west zone on proximity |
| `ChallengeMission_ProximityFlank` | latesiege | Send knights to defend flank on proximity |
| `ChallengeMission_DefendFlank` | latesiege | Continue knight flank defense; retreat when clear |
| `ChallengeMission_AttackRams` | latesiege | Send MAA to attack rams near inner zone |
| `ChallengeMission_OnDestruction` | latesiege | Handle landmark/TC/wall destruction; update objectives |
| `ChallengeMission_CheckAnnihilation` | latesiege | Detect if player lost all units; trigger reinforcements |
| `CheckLateSiegeAnnihiliation` | latesiege | Verify annihilation conditions with production queue check |
| `CalculateLateSiegeStartingResources` | latesiege | Compute resources for 2 treb + 1 bombard + 1 ram + 1 ST |
| `LateSiegeReinforcements` | latesiege | Respawn full army and resources; forfeit medals |
| `ChallengeMission_CheckVictory` | latesiege | Check conquest progress ≥3; complete or fail objective |
| `DefendAgainstSiege` | latesiege | Send defenders when landmarks/TC are under attack |
| `RetreatArchers` | latesiege | Move gate archers back when gate is destroyed |
| `EnemyGarrisonTownCenter` | latesiege | Garrison nearby villagers in TC on wall breach |
| `ChallengeMission_SetBuildingsOnFire` | latesiege | Randomly damage/ignite enemy buildings during outro |
| `ChallengeMission_CheckCheer` | latesiege | Make player units cheer when enemies cleared |
| `CheckIfSiegeBuildingsSelected` | latesiege | Remove siege workshop/madrasa hint points on selection |
| `UserHasUnloadedSiegeTowerNarration` | latesiege | Trigger narration when siege tower unloads on wall |
| `LateSiegeTrainingGoals_OnInit` | training | Initialize all 9 siege training goal sequences |
| `TrainingGoal_EnableLateSiegeGoals` | training | Enable all late siege training goal sequences |
| `TrainingGoal_DisableLateSiegeGoals` | training | Disable all late siege training goal sequences |
| `CanBuildSiegeTowerPredicate` | training | Check if player can build siege tower (PC) |
| `CanBuildSiegeTowerPredicate_Xbox` | training | Check if player can build siege tower (Xbox) |
| `UserHasSelectedSiegeEngineer` | training | Detect player selecting infantry for construction |
| `UserIsBuildingSiegeTower` | training | Detect player placing siege tower blueprint |
| `UserHasBuiltSiegeTower` | training | Detect siege tower construction started |
| `HasSiegeTowerPredicateForGarrison` | training | Check if built siege tower has nearby infantry |
| `UserHasGarrisonedSiegeTower` | training | Detect units garrisoned inside siege tower |
| `HasGarrisonedSiegeTowerNearWallPredicate` | training | Check garrisoned siege tower near enemy walls |
| `UserHasUnloadedSiegeTower` | training | Detect siege tower unload-on-wall ability used |
| `RamBuiltPredicate` | training | Check if player has built a battering ram |
| `SpringaldBuiltPredicate` | training | Check if player has built a springald |
| `MangonelBuiltPredicate` | training | Check if player has built a mangonel |
| `TrebuchetBuiltPredicate` | training | Check if player has built a trebuchet |
| `BombardBuiltPredicate` | training | Check if player has built a bombard |

## KEY SYSTEMS

### Objectives

| Constant/Key | Type | Purpose |
|--------------|------|---------|
| `objectiveVictory` | Primary | "Defeat the Holy Roman Empire" — complete when all 3 buildings destroyed |
| `objectiveSub1` | Secondary | Destroy HRE Town Center |
| `objectiveSub2` | Secondary | Destroy Aachen Chapel Landmark |
| `objectiveSub3` | Secondary | Destroy Regnitz Cathedral Landmark |
| `benchmarks.gold.objective` | Bonus | Gold medal — complete within 6 min (7 Xbox) |
| `benchmarks.silver.objective` | Bonus | Silver medal — complete within 9 min (10 Xbox) |
| `benchmarks.bronze.objective` | Bonus | Bronze medal — complete within 15 min (16 Xbox) |
| `benchmarks.unplaced.objective` | Bonus | "Time Elapsed" — no medal, count-up timer |
| `failedMedals` | Information | Shown after reinforcements forfeit all medals |

### Difficulty

No `Util_DifVar` scaling is used. Difficulty is effectively fixed:
- **Player**: Delhi Sultanate, Imperial Age, pop cap 100, 10x production speed
- **Enemy**: Holy Roman Empire, Castle Age, static defenders
- **Xbox adjustments**: Medal thresholds relaxed by +1 minute each tier
- **Starting resources**: Dynamically calculated via `CalculateLateSiegeStartingResources()` to guarantee 2 trebuchets + 1 bombard + 1 ram + 1 siege tower

### Spawns

**Player starting army** (spawned at `Mission_PreStart`):
- 20× Men-at-Arms (Sultanate tier 3)
- 10× Spearmen (Sultanate tier 3)
- 10× Archers (Sultanate tier 3)
- 3× Scouts (Sultanate tier 1)
- 2× War Elephants (Sultanate tier 3)
- 2× Monks (Sultanate tier 2, garrisoned in Madrasa)

**Enemy static defenders**:
- 8× Men-at-Arms (HRE tier 3) — inner defense
- 14× Spearmen group 1 (HRE tier 3) — gate sally-forth
- 18× Spearmen group 2 (HRE tier 3) — east/TC defense
- 8× Knights (HRE tier 3) — 3-point patrol
- 18× Archer groups (01–18, 1–7 squads each) — positioned on walls in arc formations

**Pre-intro cinematic units** (temporary, cleaned up after):
- Shot 1: 7+6+12 enemy archers, 10 spearmen, 10 MAA on walls
- Shot 2: 10+10+8 player MAA constructing ram and 2 siege towers
- Shot 3: 8+16+8 player MAA, 2 siege towers, 1 ram — garrison and assault
- Shot 4: 1 trebuchet, 1 bombard, 20 MAA — bombard walls
- Shot 5: 1 hidden gate-holder unit

**Reinforcements** (on total player army loss):
- Identical to starting army minus monks; resources reset; medals forfeited

### AI

- **No `AI_Enable` calls** — enemy AI is entirely scripted via proximity triggers and rule intervals
- **Knight patrol**: 3-waypoint patrol loop (`mkr_enemy_knights_patrol1/2/3`) with 5-second pause at endpoints; direction toggles; attacks player units within 18 range; removed on proximity trigger
- **Gate defense**: Spearmen1 sally forth when player enters gate proximity (35 range) or gate is attacked; prefer targeting rams and long-range siege
- **Inner defense**: Spearmen1 assigned to DefendGate module when player nears inner trigger (20 range)
- **Landmark defense** (`DefendAgainstSiege`, 2s interval): MAA defend Aachen Chapel; knights defend Regnitz Cathedral; spearmen2 defend Town Center — all triggered on `Entity_IsUnderAttack` within 5s
- **Flank defense**: Knights sally forth on flank proximity; attack nearby units; retreat if area clears
- **Gate destruction**: Archers retreat via `RetreatArchers()`; MAA begin targeting rams; villagers garrison TC on wall breach
- **MissionOMatic modules**: DefendInner (MAA), DefendEast (spearmen2), DefendGate (spearmen1), DefendWest (knights); TownLife modules for farming and town zones (no villager production)

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `ChallengeMission_Update` | 0.125s | Medal/objective state machine tick |
| `CheckLateSiegeAnnihiliation` | 0.5s | Monitor player annihilation state |
| `ChallengeMission_ProximityWest` | 1s | Detect player near west zone |
| `ChallengeMission_ProximityGate` | 1s | Detect player near gate |
| `ChallengeMission_GateUnderAttack` | 1s | Detect gate under attack |
| `ChallengeMission_ProximityInner` | 1s | Detect player near inner zone |
| `ChallengeMission_ProximityFlank` | 1s | Detect player near flank |
| `DefendAgainstSiege` | 2s | Check if landmarks/TC are under attack |
| `CheckIfSiegeBuildingsSelected` | 1s | Remove hint points on workshop/madrasa selection |
| `ChallengeMission_DefendAfterSallyForth` | 5s | Continue gate siege defense after sally |
| `ChallengeMission_DefendFlank` | 2.5s | Continue flank defense after knight sally |
| `ChallengeMission_PatrolEnemyKnights1/2/3` | 1s | Knight patrol waypoint checks |
| `ChallengeMission_AttackRams` | 1s | MAA target rams after gate destroyed |
| `ChallengeMission_CheckCheer` | 1s | Check for victory cheer state (outro) |
| `Mission_PreStart_IntroNISFinished` | 0.125s | Wait for cinematic to finish before starting |
| `reinforcementTime + 10` | — | Delay before ignoring remaining resources for annihilation check |
| Pre-intro `Shot01_Face_Archers` | OneShot 1s | Nudge archer positions |
| Pre-intro `Shot01_Face_Archers2` | OneShot 4s | Nudge second archer group |
| Pre-intro `Shot02_Delayed_Scatter` | OneShot 6s | Scatter MAA from siege tower sites |
| Pre-intro `Shot02_Delayed_Scatter2` | OneShot 10s | Scatter MAA from ram site |
| Pre-intro `Shot04_AttackWall` | OneShot 1.7s | Begin trebuchet/bombard wall attack |
| Pre-intro `Shot04_ClearWallSection` | OneShot 16s | Move archers from targeted wall section |
| Medal failure narration | OneShot 1.2s | Play missed gold/silver/bronze dialogue |

## CROSS-REFERENCES

### Imports
- `Cardinal.scar` — core game framework
- `MissionOMatic/MissionOMatic.scar` — modular mission system (defend modules, TownLife)
- `MissionOMatic/MissionOMatic_utility.scar` — MissionOMatic utility functions
- `training/coretraininggoals.scar` — base training system (`TrainingGoal_DisableCoreControlGoals`, `TrainingGoal_DisableCoreEconGoals`)
- `training/coretrainingconditions.scar` — training condition helpers (`UserIsGoingToBuildBuildingType`, `UserHasStartedToBuildABuilding`, etc.)
- `challenge_mission_latesiege_preintro.scar` — imported by core file for cinematic
- `challenge_mission_latesiege_training.scar` — imported by core file for tutorial hints

### Shared Globals
- `localPlayer` / `enemyPlayer` — shared across all 3 files
- `cinematicFinished` — flag set in core, checked throughout preintro to short-circuit cinematic logic
- `_challenge` — master config table (resources, benchmarks, victory, annihilation, icons)
- `PLAYERS` — global player iteration table from Cardinal
- `EVENTS` — narration events (NarrIntro, NarrEnemySally, NarrWallDestroyed, NarrWallsClimbed, NarrDestroyTC, NarrDestroyFirst/Second, NarrGoldFailed, NarrSilverFailed, NarrBronzeFailed, LateSiege_PreIntro, LateSiege_Outro)
- `sg_single` / `eg_single` — reusable single-element groups
- `hasUnloadedSiegeTower` — narration trigger flag
- `playerGotReinforcements` — medal forfeiture flag
- `minimapBlips` — tracked minimap blip entries for cleanup
- `enemy_capital`, `enemy_landmark1`, `enemy_landmark2` — EGroups (prefab-defined)
- `eg_player_siegeworkshop1/2`, `eg_player_madrasa` — player building EGroups (prefab-defined)

### Inter-File Function Calls
- Core → training: `LateSiegeTrainingGoals_OnInit()`, `TrainingGoal_EnableLateSiegeGoals()`
- Core → preintro: `LateSiege_PreIntro_CleanUpAll()` (commented out but referenced)
- Training → core training: `Training_AddGoalSequence()`, `Training_GoalSequence()`, `Training_Goal()`, `Training_EnableGoalSequenceByID()`
- Preintro → core: reads `cinematicFinished`, `_challenge.startingResources`; calls `CalculateLateSiegeStartingResources()`

### Blueprint References
- **Player (Sultanate)**: `unit_manatarms_3_sul`, `unit_archer_3_sul`, `unit_spearman_3_sul`, `unit_scout_1_sul`, `unit_war_elephant_3_sul`, `unit_monk_2_sul`, `unit_siege_tower_3_sul`, `unit_ram_3_sul`, `unit_trebuchet_4_cw_sul`, `unit_bombard_4_sul`
- **Enemy (HRE)**: `unit_manatarms_3_hre`, `unit_spearman_3_hre`, `unit_knight_3_hre`, `unit_archer_3_hre`, `unit_villager_1_hre`
- **Upgrades**: `upgrade_siege_engineers_sul`, `upgrade_tech_university_murder_holes_4`, `upgrade_unit_archer_3`, `upgrade_transport_construction_speed_sul`, `UPGRADE_TOWER_SPRINGALD`
- **Abilities**: `siege_tower_unload_on_wall`, `core_building_scuttle`, `toggle_spawn_hold_sul`
