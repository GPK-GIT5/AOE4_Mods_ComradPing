# Russia Chapter 3: Ugra

## OVERVIEW

Russia Chapter 3 is a defensive mission where the player controls Ivan III's Rus forces against Akmet Khan's Mongol army across a river with two fordable crossings. The mission flows through three major phases: a timed preparation period to build forces and position them at the north and south fords, a 15-minute hold phase where the player must maintain force superiority at both fords while repelling escalating Mongol attacks, and a final assault phase where the player crosses the river to destroy the Mongol town center. A dynamic force-ratio system (tug-of-war) continuously evaluates unit strength at each ford — if Rus superiority drops below a threshold, Mongol defenders launch attacks across the river. An optional objective tasks the player with intercepting a southern Mongol reinforcement column before it reaches the fords.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp3_ugra.scar` | core | Main mission script: player/enemy setup, recipe, variables, intro cinematics, mission flow |
| `obj_mongolwaves.scar` | objectives | Preparation timer, ford movement objectives, vanguard scout repel waves |
| `obj_holdfords.scar` | objectives | Hold fords superiority timer, ford force evaluation, reinforcement phases, southern intercept |
| `obj_attackmongols.scar` | objectives | Final attack phase: destroy Mongol TC, building pack-up, defender retreat, outro |
| `training_ugra.scar` | training | Tutorial goal sequences for Ivan III's leader production ability |
| `ugra_combatvalue.scar` | data | Unit type list with blueprint references; resource-weighted combat value calculation |
| `gdm_chp3_ugra_automated.scar` | automated | Automated testing: checkpoint registration, AI-driven army management, wall construction |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | gdm_chp3_ugra | Init SGroups, timers, difficulty vars, register objectives |
| `Mission_SetupPlayers` | gdm_chp3_ugra | Configure players, ages, relationships, tower upgrades |
| `Mission_Preset` | gdm_chp3_ugra | Colors, AI paths, init units, launch autotest |
| `Mission_Start` | gdm_chp3_ugra | Set resources, start OBJ_FindMongols, begin sheep gather |
| `GetRecipe` | gdm_chp3_ugra | Return MissionOMatic recipe with locations/modules/playbill |
| `Ugra_InitEnemyUnits` | gdm_chp3_ugra | Deploy Mongol intro units and send along paths |
| `Ugra_InitPlayerUnits` | gdm_chp3_ugra | Deploy Rus intro army, Ivan, assign villagers to resources |
| `Ugra_AssignStartingMonUnits` | gdm_chp3_ugra | Transfer intro Mongol units into Defend modules |
| `Ugra_SendIntroUnits` | gdm_chp3_ugra | Queue delayed formation-move waypoints for intro |
| `Ugra_SkipIntro` | gdm_chp3_ugra | Warp intro units to final positions on skip |
| `Ugra_CheckMissionEndCondition` | gdm_chp3_ugra | Fail if Rus TC destroyed; win if Mongol TC destroyed |
| `Ugra_GatherSheep` | gdm_chp3_ugra | Move nearby sheep toward gather marker |
| `Achievement_OnEntityKilled` | gdm_chp3_ugra | Track outpost kills for achievement (50 threshold) |
| `MongolWaves_InitObjectives` | obj_mongolwaves | Register prepare, move-to-fords, repel wave objectives |
| `MongolWaves_CheckPrepareCompletion` | obj_mongolwaves | Complete prepare objective when timer expires |
| `MongolWaves_CheckMoveUnitStart` | obj_mongolwaves | Start move-to-fords if timer ≤120s or pop ≥130 |
| `Ugra_PrepareTimerComplete` | obj_mongolwaves | Set prepareTimerComplete flag at 66% of timer |
| `HoldFords_InitObjectives` | obj_holdfords | Register hold-ford objectives, start force count loop |
| `Ugra_UpdateForceCount` | obj_holdfords | Calculate force ratios at both fords, update UI |
| `Ugra_NorthFordDelayedLaunch` | obj_holdfords | Transfer north ford defenders to AttackNorth if ratio low |
| `Ugra_SouthFordDelayedLaunch` | obj_holdfords | Transfer south ford defenders to AttackSouth if ratio low |
| `Ugra_EvaluateForceValue` | obj_holdfords | Sum weighted combat values for an SGroup |
| `Ugra_Phase2` | obj_holdfords | Add MAA/crossbow to waves, reduce build times |
| `Ugra_Phase3` | obj_holdfords | Add spear/horseman/archer to waves, further reduce times |
| `Ugra_Phase4` | obj_holdfords | Add MAA/knight/crossbow to waves, fastest build times |
| `Ugra_ProbeFord` | obj_holdfords | Spawn cavalry probe wave at alternating fords |
| `Ugra_ReinforceFords` | obj_holdfords | Trigger Wave_Prepare for both ford waves |
| `Ugra_ReinforcementTrain` | obj_holdfords | Spawn southern reinforcement column with mobile buildings |
| `Ugra_SouthernReinforcementsCheck` | obj_holdfords | Complete optional obj when all reinforcements dead |
| `Ugra_ReleaseReinforcements` | obj_holdfords | Release surviving reinforcements to south ford defense |
| `Ugra_UnpackSouthernReinforcements` | obj_holdfords | Unpack mobile Mongol buildings at south positions |
| `Ugra_SplitAndFallback` | obj_holdfords | Split ford modules by unit type into fort defense |
| `Ugra_SplitModule` | obj_holdfords | Distribute reinforcements into sub-defend modules by type |
| `Ugra_TimerComplete` | obj_holdfords | Complete OBJ_MaintainSuperiority when timer ends |
| `Ugra_WarnPlayerIfTheyCrossTheFords` | obj_holdfords | Trigger warning intel if player crosses to far side |
| `Ugra_OnSquadKilled` | obj_holdfords | Track southern reinforcement kill count for sub-objective |
| `AttackMongols_InitObjectives` | obj_attackmongols | Register attack/destroy TC objectives |
| `Ugra_CheckTownCenterDestroyed` | obj_attackmongols | Complete attack obj when Mongol TC EGroup empty |
| `Ugra_PackUpBuildings` | obj_attackmongols | Convert packable Mongol buildings to mobile units |
| `Ugra_ConvoyRetreat` | obj_attackmongols | Retreat packed buildings when player spots them |
| `Ugra_DefendersRetreatOnEngage` | obj_attackmongols | Retreat fraction of defenders when under attack |
| `Ugra_InitOutro` | obj_attackmongols | Spawn outro units, retreat Mongols, fire cannons |
| `Ugra_InitializeUnitValues` | ugra_combatvalue | Calculate resource-weighted value for each unit type |
| `MissionTutorial_IvanLeaderAura` | training_ugra | Training sequence for Ivan's production ability (PC) |
| `MissionTutorial_IvanLeaderAura_XBox` | training_ugra | Training sequence for Ivan's production ability (Xbox) |
| `AutoTest_OnInit` | automated | Initialize autotest if CampaignAutoTest arg present |
| `AutomatedUgra_RegisterCheckpoints` | automated | Register 5 test checkpoints with timeouts |
| `AutomatedMission_Start` | automated | Reveal FOW, begin phase-0 checkpoint checks |
| `AutomatedUgra_Phase1_SetUpPhase1` | automated | Create two roving armies for north/south fords |
| `_AutomatedUgra_UnitReplenish` | automated | Replenish army module when below 50% strength |
| `AutomatedUgra_VillagerWalls_Init` | automated | Spawn villagers to build walls/towers at both fords |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_FindMongols` | Primary | Timed preparation phase — build forces before Mongols attack |
| `OBJ_PrepareForMongols` | Primary | Completes when prepare timer expires, triggers repel phase |
| `OBJ_MoveUnitsToFords` | Primary | Move units to fords (starts at ≤120s remaining or pop ≥130) |
| `SOBJ_MoveToNorthFord` | Sub (TugOfWar) | North ford force ratio progress indicator |
| `SOBJ_MoveToSouthFord` | Sub (TugOfWar) | South ford force ratio progress indicator |
| `OBJ_RepelMongols` | Battle | Repel two vanguard scout waves |
| `SOBJ_RepelWave1` | Sub (Battle) | Repel 6 horsemen at south ford |
| `SOBJ_RepelWave2` | Sub (Battle) | Repel 6 horsemen at north ford |
| `OBJ_MaintainSuperiority` | Information | Hold fords for 900s countdown timer |
| `SOBJ_NorthFordRus` | Sub (TugOfWar) | North ford force ratio during hold phase |
| `SOBJ_SouthFordRus` | Sub (TugOfWar) | South ford force ratio during hold phase |
| `OBJ_SouthernReinforcements` | Optional | Intercept southern Mongol reinforcement column |
| `SOBJ_DestroyUnits` | Sub (Optional) | Kill count tracker for reinforcement column |
| `OBJ_AttackMongols` | Battle | Destroy Mongol encampment (final phase) |
| `SOBJ_DestroyTownCenter` | Sub (Battle) | Destroy Mongol Town Center to win |
| `OBJ_DebugComplete` | Debug | Cheat objective to skip to victory |

### Difficulty

| Parameter | Easy | Standard | Hard | Hardest |
|-----------|------|----------|------|---------|
| `prepareTimer` | 520 | 520 | 400 | 280 |
| `monReinforcePeriod` | 85 | 54 | 48 | 42 |
| `monReinforcePhase2Delay` | 450 (50%) | 450 (50%) | 297 (33%) | 225 (25%) |
| `monReinforcePhase3Delay` | 9999 (never) | 9999 (never) | 594 (66%) | 450 (50%) |
| `monReinforcePhase4Delay` | 9999 (never) | 9999 (never) | 9999 (never) | 675 (75%) |
| `monWaveTimer` | 60 | 60 | 60 | 60 |
| Villager count (sg_rus_villagers2) | 8 | 6 | 6 | 6 |
| Villager count (sg_rus_villagers3/4) | 4 | 3 | 3 | 3 |
| Ford1 spearman | 4 | 6 | 6 | 6 |
| Ford1 archer | 8 | 10 | 10 | 10 |
| Ford1 crossbow | 3 | 5 | 5 | 5 |
| Probe horseman (Ph1) | 4 | 4 | 6 | 6 |
| Probe horsearcher (Ph1) | 2 | 2 | 2 | 4 |
| Probe knight (Ph1) | 0 | 0 | 0 | 2 |
| Southern reinforce horseman | 6 | 6 | 6 | 8 |
| Southern reinforce horsearcher | 4 | 6 | 8 | 10 |
| Southern reinforce MAA | 0 | 2 | 4 | 4 |
| Southern reinforce archer | 4 | 6 | 8 | 10 |
| Southern reinforce mangonel | 0 | 1 | 2 | 2 |
| Southern reinforce ram | 1 | 1 | 1 | 2 |

### Spawns

- **Vanguard Scouts**: Two waves of 6 horsemen each — wave 1 at south ford, wave 2 at north ford. Triggered sequentially after prepare timer.
- **Ford Defenders**: Initial Mongol garrison at each ford (spearman, MAA, archer, crossbow). Split into 4 sub-modules per ford for formation positioning.
- **Wave System**: `Wave_New` creates continuous reinforcement waves for both fords. Initial composition: 1 spearman + 1 archer. Phases 2–4 add MAA, crossbow, horseman, knight and reduce build times (from 12–17s down to 6–8s).
- **Probe Waves**: Cavalry raids (`Ugra_ProbeFord`) at alternating fords on `monWaveTimer` interval. Composition scales by phase (1–4) and difficulty. Rams added if player has walls.
- **Southern Reinforcements**: Single reinforcement column spawned at `monReinforceWaveDelay` (530s). Includes horseman, horsearcher, MAA, archer, mangonel, ram + 3 mobile Mongol buildings. Move at 50% speed along 5 waypoints toward south ford. If not destroyed, released to south ford defense.
- **Backup Forces**: Two large backup groups at `mkr_monbackup1` (archers, knights, horse archers, horsemen) and `mkr_monbackup2` with auto-reinforcement from MonVillagers.
- **Fort Staging**: `DefendMonFortRanged` at Mongol fort serves as staging area for Wave system before deployment.
- **Attack Phase**: On hold completion, ford defenders split by type (cav → DefendNorthCav/DefendSouthCav, melee → Infantry modules, ranged → RangedNorth). Retreat on engage with fraction-based withdrawal.

### AI

- **Player 2 AI**: AI is NOT explicitly enabled for Mongols — all behavior is scripted via MissionOMatic modules (Defend, RovingArmy, Wave).
- **Player 3**: AI disabled (`AI_Enable(player3, false)`), serves as neutral holder for Ivan leader unit.
- **Cached Paths**: `AIPlayer_SetMarkerToUpdateCachedPathToPosition` for 3 ford attack routes (ford1, ford2, ford3).
- **Attack Modules**: `AttackNorth` and `AttackSouth` RovingArmy modules with 3 waypoints each (ford attack → TC). Populated dynamically when force ratio drops below `attackThreshold` (0.40).
- **Scout Attack Modules**: `ScoutAttack1` and `ScoutAttack2` for vanguard horseman waves.
- **Southern Reinforcements**: RovingArmy with `attackMoveStyle_ignoreEverything` — moves through 5 waypoints ignoring combat. On completion calls `Ugra_ReleaseReinforcements`.
- **Retreat Logic**: `Ugra_DefendersRetreatOnEngage` monitors 5 retreat modules; when under attack, a fraction of units retreat to random map-edge markers.
- **Autotest AI**: `AI_Enable(player1, true)` + `Game_AIControlLocalPlayer()` only during automated testing.

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `prepareTimer` | 280–520s (difficulty) | Countdown for preparation phase |
| `holdFordTimer` | 900s | Countdown for hold-fords phase |
| `fordStartGraceDelay` | 60s | Grace period before evaluating ford ratios |
| `forceGraceDelay` | 8s | Delay before confirming ford attack launch |
| `attackCooldown` | 60s | Cooldown between consecutive ford attacks |
| `monReinforcePeriod` | 42–85s (difficulty) | Interval for `Ugra_ReinforceFords` wave prep |
| `monReinforceWaveDelay` | 530s | One-shot delay for southern reinforcement spawn |
| `monReinforcePhase2Delay` | 225–450s (difficulty) | One-shot to trigger Phase 2 escalation |
| `monReinforcePhase3Delay` | 450–9999s (difficulty) | One-shot to trigger Phase 3 escalation |
| `monReinforcePhase4Delay` | 675–9999s (difficulty) | One-shot to trigger Phase 4 escalation |
| `monWaveTimer` | 60s | Interval for `Ugra_ProbeFord` cavalry raids |
| `Ugra_UpdateForceCount` | 1s | Continuous force ratio evaluation loop |
| `Ugra_CheckMissionEndCondition` | 5s | Check TC destruction win/lose conditions |
| `Ugra_GatherSheep` | 20s | Periodic sheep gathering |
| `Ugra_WarnPlayerIfTheyCrossTheFords` | 2.5s | Check if player crosses to Mongol side |
| `Ugra_PrepareTimerComplete` | 66% of prepareTimer | Enable ford wave preparation |
| `Ugra_SouthernReinforcementsCheck` | 1s | Monitor if reinforcement column eliminated |
| `Ugra_DefendersRetreatOnEngage` | 1s | Check if fort defenders under attack |
| `Ugra_ConvoyRetreat` | 1s | Check if player can see packed buildings |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `gdm_chp3_ugra.scar` | `MissionOMatic/MissionOMatic.scar`, `obj_mongolwaves.scar`, `obj_holdfords.scar`, `obj_attackmongols.scar`, `ugra_combatvalue.scar`, `training_ugra.scar`, `gdm_chp3_ugra_automated.scar` |
| `gdm_chp3_ugra_automated.scar` | `GameScarUtil.scar`, `Prefabs.scar`, `standard.scar`, `scarutil.scar`, `team.scar`, `core.scar`, `MissionOMatic/MissionOMatic.scar`, `missionomatic/modules/module_rovingarmy.scar`, `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |
| `obj_attackmongols.scar` | `MissionOMatic/MissionOMatic.scar` |
| `training_ugra.scar` | `training/campaigntraininggoals.scar` |

### Shared Globals

- **Players**: `player1` (Ivan/Rus), `player2` (Mongol), `player3` (neutral holder)
- **Leader**: `g_leaderIvan` — initialized via `Missionomatic_InitializeLeader`
- **Force Ratios**: `forceRatioNorth`, `forceRatioSouth`, `attackThreshold` (0.40), `warningThreshold` (0.50)
- **Phase Tracking**: `ugraPhase` (1–4), `prepareTimerComplete`, `evaluateFord`
- **Ford Attack State**: `attackNorthCooldown`, `attackSouthCooldown`, `firstNorthAttack`, `firstSouthAttack`, `fordAttacked`
- **Waves**: `wave_ford1`, `wave_ford2` — Wave system objects for continuous Mongol reinforcement
- **Unit Values**: `unitTypeList` — 14-entry table mapping unit scar names to blueprints and computed combat values
- **SGroups**: `sg_mon_ford1/2`, `sg_mon_attacknorth/south`, `sg_mon_scoutwave1/2`, `sg_mon_southreinforce`, `sg_mon_backup1/2`
- **Achievement**: `outpostKillCounter` — tracks outpost kills for CE_ACHIEVOUTPOSTKILLSUGRA (threshold: 50)

### Inter-File Function Calls

- `obj_mongolwaves.scar` calls `Ugra_UpdateForceCount` (from `obj_holdfords.scar`) and `Ugra_PrepareTimerComplete` (from `gdm_chp3_ugra.scar`)
- `obj_holdfords.scar` calls `Ugra_Phase2/3/4`, `Ugra_ReinforceFords`, `Ugra_ProbeFord`, `Ugra_ReinforcementTrain` (all defined in same file)
- `obj_holdfords.scar` calls `Ugra_SplitAndFallback` on hold completion, then starts `OBJ_AttackMongols` (from `obj_attackmongols.scar`)
- `obj_attackmongols.scar` calls `Ugra_ReleaseReinforcements` (from `obj_holdfords.scar`) via module `onCompleteFunction`
- `gdm_chp3_ugra.scar` calls `MongolWaves_InitObjectives`, `HoldFords_InitObjectives`, `AttackMongols_InitObjectives` from objective files
- `gdm_chp3_ugra.scar` calls `Ugra_InitializeUnitValues` from `ugra_combatvalue.scar`
- `gdm_chp3_ugra.scar` calls `MissionTutorial_IvanLeaderAura` / `_XBox` from `training_ugra.scar`
- Automated script references `OBJ_FindMongols`, `SOBJ_RepelWave1/2`, `OBJ_MaintainSuperiority`, `forceRatioNorth/South`, `attackThreshold` from objective files

### MissionOMatic Modules (Recipe)

- **UnitSpawner**: 4 villager groups (sg_rus_villagers1–4) with difficulty-scaled counts
- **TownLife**: `MonVillagers` at MonFort for Mongol economy
- **Defend**: 18 modules — ford defenders (Ford1/2 × 5 sub-modules), fort ranged/infantry/cav defenders, backup groups, third ford defenders
- **RovingArmy**: 7 modules — `MonShore` (patrol), `AttackNorth/South` (assault), `ScoutAttack1/2` (vanguard), `SouthernReinforcements` + `SouthernReinforcementsBuildings` (optional intercept)
