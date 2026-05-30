# Angevin Chapter 2: Bremule

## OVERVIEW

Brémule (1119) is the second chapter of the Angevin campaign — a multi-phase defensive mission where the Norman/English player must hold off a massive French invasion led by King Louis. The mission flows through distinct phases: an initial French advance on player-held villages (Fleury, Grainville, Cressenville), King Henry's arrival with reinforcements once the French are thinned, optional recapture of any lost villages, and a final push to defeat King Louis's army at Brémule. Core mechanics include multiple AI roving army modules (main army, scouts, hunting parties, ram siege waves), a camp/patrol system for Louis at Brémule, escalating wave generation tied to game time and difficulty, and location ownership transfers with building reconstruction by French AI villagers. The player starts in Feudal Age (max Castle) with English units spread across three villages and must manage economy and defense against difficulty-scaled French attacks.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp2_bremule.scar` | core | Main mission setup: players, variables, difficulty, restrictions, recipe, all French army modules, ram/hunting/scout systems, cinematic spawns, utility functions, game-over logic |
| `obj_frenchadvance.scar` | objectives | Phase 1 objective: hold Fleury against French advance, trigger King Henry reinforcements, transition to Phase 2 |
| `obj_defeatthefrench.scar` | objectives | Phase 2 primary objective: defeat King Louis's rallied army at Brémule to win the mission |
| `obj_recaptures.scar` | objectives | Optional parent objective wrapper for village recapture tasks |
| `obj_retakecressenville.scar` | objectives | Capture-style objective for retaking Cressenville from French control |
| `obj_retakegrainville.scar` | objectives | Capture-style objective for retaking Grainville from French control |
| `obj_funckeys.scar` | objectives | Optional tutorial objective teaching F1–F4 building quick-select (PC and Xbox variants) |
| `training_bremule.scar` | training | Training goal sequences for blacksmith upgrades and unit upgrades at barracks |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | ang_chp2_bremule | Configure 3 players, ages, relationships, pop cap |
| `Mission_SetupVariables` | ang_chp2_bremule | Create SGroups/EGroups, init leaders, set flags |
| `Mission_SetDifficulty` | ang_chp2_bremule | Define difficulty table with Util_DifVar scaling |
| `Mission_SetRestrictions` | ang_chp2_bremule | Lock trade cart, unlock French ranged building |
| `Mission_Preset` | ang_chp2_bremule | Init objectives, outpost upgrades, invulnerable barns, AI paths |
| `Mission_Start` | ang_chp2_bremule | Start villager setup, OBJ_FrenchAdvance, grant AI resources |
| `GetRecipe` | ang_chp2_bremule | Define MissionOMatic recipe with locations and modules |
| `Init_FrenchAssault` | ang_chp2_bremule | Spawn all French armies, scouts, start advance rules |
| `Init_FrenchBackfill` | ang_chp2_bremule | Spawn scaled reinforcements into LouisReUp module |
| `Init_Hunting_RovingArmy` | ang_chp2_bremule | Create hunting roving army targeting visible player units |
| `Init_FrenchWaves` | ang_chp2_bremule | Prepare first hunting wave with horsemen/knights |
| `Init_Ram_RovingArmy` | ang_chp2_bremule | Create ram siege roving army with time-scaled composition |
| `ConstructWave` | ang_chp2_bremule | Generate ram wave units scaling with game time |
| `Reset_RamWave` | ang_chp2_bremule | Respawn ram wave units on death timer |
| `Siege_LaunchPoint` | ang_chp2_bremule | Pick spawn point: ambush hill, captured town, or base |
| `Siege_Targets` | ang_chp2_bremule | Build target list based on town ownership |
| `UpdateWaveTarget` | ang_chp2_bremule | Retarget hunting army toward nearest visible player units |
| `Set_HuntingReinforcements` | ang_chp2_bremule | Schedule hunting army respawn after death |
| `Spawn_HuntingReinforcements` | ang_chp2_bremule | Spawn scaled hunting wave into module |
| `NewScoutGroup` | ang_chp2_bremule | Create scout camps and roving scout modules |
| `NewSingleScout` | ang_chp2_bremule | Respawn individual scout on previous scout death |
| `AmbushSpawn` | ang_chp2_bremule | Place ambush force at switchback hill |
| `AmbushCamp` | ang_chp2_bremule | Build tent props at ambush location |
| `SetUpTent` | ang_chp2_bremule | Arrange Louis's army in camp formation at Brémule |
| `PatrolCamp` | ang_chp2_bremule | Move camp patrol groups between random markers |
| `CombatWatch` | ang_chp2_bremule | Detect player near Brémule, trigger camp defense |
| `CampShutDown` | ang_chp2_bremule | Dissolve camp patrols, init defense encounter |
| `Init_Camp_Defense_Encounter` | ang_chp2_bremule | Create Encounter plan defending Brémule with Louis army |
| `LiquidateLouisArmy` | ang_chp2_bremule | Merge Louis armies, disband modules, set up camp |
| `Transfer_Defenders` | ang_chp2_bremule | Move percentage of units between army modules |
| `VillagerSetup` | ang_chp2_bremule | Assign starting villagers to gold, food, wood, farms |
| `Rebuild_Location` | ang_chp2_bremule | French AI rebuilds captured town buildings |
| `Build_LocationTable` | ang_chp2_bremule | Snapshot entity positions/blueprints for rebuild |
| `PlayerDeath` | ang_chp2_bremule | Fail mission if no town center remains |
| `Louis_Weakened` | ang_chp2_bremule | Nerf Louis when health drops below 15% |
| `Bremule_Intro_Parade` | ang_chp2_bremule | Spawn and parade English intro units |
| `French_IntroSpawn` | ang_chp2_bremule | Spawn full French intro army with formations |
| `SpinUp_CounterAttack` | obj_frenchadvance | Create counter-attack roving army from Louis forces |
| `KingHenry_Reinforcements` | obj_frenchadvance | Deploy Henry + 30 reinforcements, check Fleury clear |
| `FrenchAdvance_OnStart` | obj_frenchadvance | Start intro parade, event cues, hint points |
| `FrenchAdvance_OnComplete` | obj_frenchadvance | Transition to Phase 2, start hunting/ram/scout systems |
| `FrenchArrival` | obj_frenchadvance | Handle French capture of Grainville or Cressenville |
| `CheckCaptures` | obj_frenchadvance | Start recapture objectives for lost villages |
| `RecaptureEvent` | obj_frenchadvance | Play intel and switch music on first recapture |
| `OnCapture_CancelProductionQueue` | obj_frenchadvance | Cancel all production in captured town buildings |
| `DeafeattheFrench_Start` | obj_defeatthefrench | Init tutorials, auto-save, add Louis banner UI |
| `DeafeattheFrench_IsComplete` | obj_defeatthefrench | True when Louis army + reserves ≤ 20 |
| `CountFrench` | obj_defeatthefrench | Update progress bar for defeat objective |
| `CaptureCressenville_Start` | obj_retakecressenville | Enable Cressenville capturable, spawn French villagers |
| `CaptureCressenville_Complete` | obj_retakecressenville | Clear flag, spawn monk/villagers, schedule counterattack |
| `CaptureGrainville_Start` | obj_retakegrainville | Enable Grainville capturable, spawn French villagers |
| `CaptureGrainville_Complete` | obj_retakegrainville | Clear flag, send challenge event, schedule counterattack |
| `Bremule_Tutorials_Init` | training_bremule | Register blacksmith and unit upgrade training goals |
| `FuncKeys_InitObjectives` | obj_funckeys | Register F1–F4 quick-select tutorial objectives |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_FrenchAdvance` | Primary/Battle | Phase 1: Hold off the French advance |
| `SOBJ_HoldingFleury` | Sub/Battle | Hold Fleury until King Henry arrives |
| `SOBJ_ClearFleury` | Sub/Battle | Push remaining French out of Fleury |
| `OBJ_DefeatTheFrench` | Primary/Battle | Phase 2: Stop King Louis rallying troops (win when ≤20 remain) |
| `SOBJ_BurningBarn` | Secondary | Investigate the smoke |
| `SOBJ_KingLouis_Title` | Secret/Battle | King Louis banner UI container |
| `OBJ_Recapture` | Optional | Parent wrapper for village recapture |
| `SOBJ_CaptureCressenville` | Capture | Retake Cressenville from French |
| `SOBJ_DefeatCressenvilleRebels` | Sub/Capture | Push French out of Cressenville |
| `SOBJ_LocationCressenville` | Sub/Capture | Cressenville location marker |
| `SOBJ_CaptureGrainville` | Capture | Retake Grainville from French |
| `SOBJ_DefeatGrainvilleRebels` | Sub/Capture | Push French out of Grainville |
| `SOBJ_LocationGrainville` | Sub/Capture | Grainville location marker |
| `OBJ_FuncKeys` | Optional | Teach F1–F4 quick-select (Normal or below) |
| `SOBJ_F1`–`SOBJ_F4` | Sub/Optional | Select military/economy/research/landmark buildings |
| `OBJ_DebugComplete_Min/Mid/Max` | Debug | Cheat objectives to skip to victory with varying defender counts |

**Flow:** `OBJ_FrenchAdvance` → (recaptures if villages lost) → `OBJ_DefeatTheFrench` → Mission_Complete.

### Difficulty

| Parameter | Story | Easy | Normal | Hard | Effect |
|-----------|-------|------|--------|------|--------|
| `scoutsAmount` | 4 | 4 | 8 | 12 | Number of French scout waypoints active |
| `invasionScale` | 0.18 | 0.5 | 0.75 | 1.0 | Multiplier on backfill/ambush army sizes |
| `attackWaveScale` | 0 | 0 | 1 | 2 | Hunting wave power scaling factor |
| `attackWaveFrequency` | 15 | 15 | 10 | 5 | Minutes between hunting army respawns |
| `ramWaveFrequency` | 10 | 10 | 5 | 5 | Minutes between ram wave respawns |
| `storyStartingVillagers` | 2 | 0 | 0 | 0 | Extra villagers at Fleury (gold + food) |
| `matchUpSimplify.ranged` | 0 | 0 | 1 | 1 | Ranged unit multiplier in ambush |
| `matchUpSimplify.infantry` | 2 | 2 | 1 | 1 | Infantry multiplier in ambush |
| `enemyStartsMaxed` | false | false | false | true | French start at max composition |
| `t_frenchScoutCamps` | 4 | 4 | 6 | 8 | Number of scout camp waypoints |

Additional difficulty gates:
- Hunting army, ram waves, and scouts only spawn on Normal+ (`Game_GetSPDifficulty() >= GD_NORMAL`)
- `OBJ_FuncKeys` only starts on Normal or below
- Counter-attack targeting uses `ARMY_TARGETING_CYCLE` on Easy, `ARMY_TARGETING_DISCARD` otherwise
- Siege targets exclude Fleury on Easy difficulty

### Spawns

**Phase 1 — French Advance:**
- **French Intro Army:** ~200 spearmen fill + horsemen (5+5+10+20+20), knights (5+5+10 parading), archers (40), spearmen (5×4 groups), King Louis + 9 knights as retinue
- **FrenchArmy_Scout1/2/3:** 1 scout + 2 horsemen each, targeting Cressenville/Grainville/Fleury
- **t_FrenchDefenders:** 6 spearmen, 3 men-at-arms, 6 archers (template for captured town garrisons)

**Phase 1 → 2 Transition:**
- **King Henry Reinforcements:** 9 knights + King Henry hero, 14 archers, 10 spearmen, 6 men-at-arms (deploy at `mkr_english_reinforcments`)
- **French Backfill (LouisReUp):** 30×invasionScale knights, 50×invasionScale horsemen, 45×invasionScale spearmen, 45×invasionScale archers

**Phase 2 — Ongoing Waves (Normal+ only):**
- **Hunting Army:** Initial 10 horsemen + 5 knights + 1 scout; respawns scale with `huntingScale` counter
- **Ram Waves:** Spearmen (12+waveDiffModded), men-at-arms (waveDiffModded/2), rams (1+waveDiffModded/5), plus random bonus units; `waveDiffModded` computed from game time via polynomial curve (capped at 50)
- **Ambush Force:** Archers (12×invasionScale×ranged) + spearmen (12×invasionScale×infantry) at switchback hill
- **Counterattacks:** 25% of Louis army split off as roving army targeting siege targets, triggered 60s after village recapture

**Villager Life:**
- Captured Cressenville/Grainville get 3 roaming + 3 food (+ 3 wood for Grainville) French villagers via `VillagerLife_Create`
- French AI villagers rebuild destroyed town buildings using snapshotted `Build_LocationTable`

### AI

| System | Details |
|--------|---------|
| `AI_Enable(player3, false)` | Player 3 (neutral Norman holder) AI disabled |
| `FrenchArmy1` | Main roving army; targets Brémule → Cressenville → Grainville → Fleury (DISCARD); withdrawThreshold 0.05 |
| `FrenchArmy_Scout1/2/3` | 3 scout groups attack-moving to each village (DISCARD) |
| `Louis_Retinue` | Roving army leashed to Brémule (combatRange 80, leashRange 500); receives transferred units |
| `LouisReUp` | Roving army ferrying backfill troops to Brémule (DISCARD) |
| `FrenchArmy_Hunting` | Hunting roving army; retargets to nearest visible player units outside safe zone; `UpdateWaveTarget` runs recursively via `Rule_AddOneShot` |
| `FrenchArmy_Ram` | Siege roving army; `attackMoveStyle_attackEverything`; spawn point adapts to captured territory |
| `French_Scout_N` | N scout modules with `ARMY_TARGETING_RANDOM` across 8 waypoints; respawn on death via `Delay_ScoutSpawn` |
| `French_HillAmbush` | One-shot roving army at switchback hill; `onDeathDissolve = true` |
| `Camp_Defense_Encounter` | Encounter plan: Attack at Brémule, combatRange 90, leashRange 160, `attackMoveStyle_attackEverything`; resets to camp patrol when threat clears |
| `PatrolCamp` (interval 10s) | Louis army patrols between camp markers at 0.35× speed; dissolves into combat encounter when player approaches |
| Counter-attacks | `SpinUp_CounterAttack` creates disposable roving armies from 25% of Louis army, `onDeathDissolve = true` |
| `FOW_PlayerRevealArea` | Player 2 gets permanent reveal of Grainville; temporary reveals on recapture |

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `PlayerDeath` | 1s interval | Check town center loss condition |
| `FleuryObjective_InitialUpdate` | 1s interval | Track French count at Fleury, trigger Henry arrival when ≤20 |
| `FrenchArrival` (×2) | 1s interval | Check French capture of Cressenville and Grainville |
| `FrenchNotify` | 1s interval | Lock tense combat music when French reach arrival marker |
| `RovingLastPosition` | 1.5s interval | Cache hunting army position for walla audio |
| `ThreatArrow_SpottedHuntingArmy` | 1s interval | Show/hide threat arrows on hunting army |
| `Init_FrenchWaves` | 120s one-shot | Initialize first hunting wave (post-advance) |
| `Init_Ram_RovingArmy` | 150s one-shot | Initialize first ram siege wave (post-advance) |
| `UpdateWaveTarget` | 1–10s self-rescheduling | Retarget hunting army to visible player units |
| `Spawn_HuntingReinforcements` | attackWaveFrequency×60s one-shot | Respawn hunting army after death |
| `StartRamTimer → Reset_RamWave` | ramWaveFrequency×60×SiegeCamp_TimerMod() | Respawn ram wave (0.3× timer if ambush camp alive) |
| `Bremule_Tutorials_Init` | 15s one-shot | Start blacksmith/unit upgrade training goals |
| `Bremule_ChangeBurningFarmsteadOwnership` | 10s one-shot | Move burning farmstead to world-owned |
| `Cressenville_Delayed_Counterattack` | 60s one-shot | Launch 25% counterattack after Cressenville recaptured |
| `Grainville_Delayed_Counterattack` | 60s one-shot | Launch 25% counterattack after Grainville recaptured |
| `CountFrench` | 1s interval | Update OBJ_DefeatTheFrench progress bar |
| `EnglishPushBack` | 3s interval | Trigger intel when player recaptures first village |
| `Check_GroupsArrived` | 5s interval | Wait for Louis army + reup to reach Brémule, then liquidate |
| `EnsureCampArrival` | 20s interval | Periodically re-issue move commands to Brémule |
| `PatrolCamp` | 10s interval | Random patrol movement for camped Louis army |
| `CombatWatch` | 2s interval | Detect player near Brémule, shut down camp |
| `RestartCamp` | 5s interval | Re-establish camp after combat if no threats |
| `Delay_ScoutSpawn → NewSingleScout` | 8s one-shot | Respawn scout after death |
| `RecapturesComplete` | 1s interval | Check both villages recaptured, set b_endGame |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (recipe, locations, modules, objectives)
- `obj_frenchadvance.scar` — Phase 1 objectives
- `obj_retakegrainville.scar` — Grainville recapture objective
- `obj_retakecressenville.scar` — Cressenville recapture objective
- `obj_defeatthefrench.scar` — Phase 2 win objective
- `obj_recaptures.scar` — Optional recapture parent objective
- `obj_funckeys.scar` — F-key tutorial objective
- `prefabs/schemas/villagerlife.scar` — VillagerLife_Create system for French villager simulation
- `training_bremule.scar` — Mission training/tutorial goals
- `training/campaigntraininggoals.scar` — Shared campaign training framework

### Shared Globals
- `player1` (English/Norman), `player2` (French), `player3` (neutral Norman holder)
- `g_leaderHenry`, `g_leaderLouis` — initialized via `Missionomatic_InitializeLeader`
- `b_GrainvilleFrench`, `b_CressenvilleFrench` — ownership flags read across all objective files
- `b_endGame` — set in `RecapturesComplete`, checked by wave/scout respawn systems to stop spawning
- `b_RecaptureIntelPlayed`, `b_frenchHuntersLaunched`, `b_hunterArrow_On` — one-shot event flags
- `t_difficulty` — difficulty table referenced by army init, wave, and spawn functions
- `sg_french_rovingarmy`, `sg_louis_army`, `sg_french_huntingarmy`, `sg_french_ram` — shared SGroups across modules
- `eg_village_fleury/grainville/cressenville/bremule` — EGroups for location buildings
- `sg_louisholdingarmy` — merged Louis army used by `CountFrench` for progress tracking
- `cressenville_EntityTable`, `grainville_EntityTable` — building snapshots for rebuild system
- `hint_grainville`, `hint_cressenville`, `hint_fleury` — HintPoint handles toggled across files

### Inter-File Function Calls
- `ang_chp2_bremule.scar` calls `*_InitObjectives()` from all objective files in `Mission_Preset`
- `obj_frenchadvance.scar` calls `CheckCaptures()`, `AmbushSpawn()`, `Init_Hunting_RovingArmy()`, `Init_FrenchWaves()`, `Init_Ram_RovingArmy()`, `NewScoutGroup()`, `UpdateWaveTarget()` (all in core)
- `obj_frenchadvance.scar` calls `SpinUp_CounterAttack()` (defined in same file), `Rebuild_Location()`, `OnCapture_CancelProductionQueue()` (core)
- `obj_defeatthefrench.scar` calls `Bremule_Tutorials_Init()` from `training_bremule.scar`
- `obj_retakecressenville/grainville.scar` call `RecaptureEvent()`, `VillagersReinforce()`, `SpinUp_CounterAttack()` from obj_frenchadvance
- `obj_retakecressenville/grainville.scar` call `Init_VillagerLife_Cressenville/Grainville()` from core
- `training_bremule.scar` uses `CampaignTraining_TimeoutIgnorePredicate` from shared `campaigntraininggoals.scar`
- MissionOMatic framework calls: `RovingArmy_Init`, `RovingArmy_SetTarget`, `RovingArmy_AddSGroup`, `RovingArmy_SetTargets`, `Wave_New`, `Wave_Prepare`, `Wave_SetUnits`, `Encounter_Create`, `Location_SetCapturable`, `Location_SetPlayerOwner`, `Prefab_DoAction`, `SpawnUnitsToModule`, `UnitEntry_DeploySquads`
