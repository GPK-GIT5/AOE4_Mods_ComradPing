# Angevin Chapter 4: Dover

## OVERVIEW

Dover (1216) is a castle-defense mission where the player (King John / English) must hold Dover Castle against a multi-wave French siege. The mission is divided into two major phases: first, repelling an initial French assault on the castle walls, then deploying the hero Willikin of the Weald to gather longbow recruits from surrounding villages, disrupt French supply trains carrying siege equipment, and ambush reinforcements flowing to the French camp. Between Willikin's guerrilla operations, the player must defend the castle through three escalating timed siege waves — each preceded by a countdown timer — culminating in a final all-out assault. An optional objective allows the player to destroy the French siege camp's production buildings outright for an alternate victory path.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp4_dover_data.scar` | data | Initializes all global variables, SGroups, EGroups, wave composition tables, path marker lists, and the MissionOMatic recipe with all army modules |
| `ang_chp4_dover.scar` | core | Main mission script — imports, player setup, difficulty config, restrictions, intro/outro sequences, spawn helpers, and mission start/fail logic |
| `obj_holdoffsiege.scar` | objectives | Defines OBJ_HoldOffSiege (primary), SOBJ_DefeatFrenchUnits (initial attack), OBJ_SiegeStrength (info tracker), kill-count tracking via GE_EntityKilled |
| `obj_siegewaves.scar` | objectives | Defines siege wave sub-objectives (SOBJ_IncomingWave1–3, SOBJ_RepelSiege1–2, SOBJ_RepelFrenchSiege), wave timer/spawn orchestration, fallback/retreat logic |
| `obj_disruptfrench.scar` | objectives | Defines OBJ_DisruptFrench (primary), Willikin archer-gathering sub-objectives, supply train system, forest camp recruitment, siege camp destruction, road patrols |
| `training_dover.scar` | training | Tutorial goal sequences for Willikin's leader aura and trader unit hover/timeout triggers |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Dover_Data_Init` | data | Initializes all globals, SGroups, wave timers, path markers |
| `Dover_InitWaveData` | data | Defines t_wave_base, t_init_waves, t_st_waves, t_siege_south_waves |
| `GetRecipe` | data | Returns MissionOMatic recipe with all army modules |
| `Mission_SetupVariables` | core | Calls data init and all objective init functions |
| `Mission_SetupPlayers` | core | Configures 6 players, relationships, upgrades, resources |
| `Mission_SetRestrictions` | core | Removes keep scuttle, upgrades outposts to springald |
| `Mission_SetDifficulty` | core | Builds t_difficulty table with all scaling parameters |
| `Mission_Preset` | core | Inits wave data, deploys intro units, sets audio |
| `Mission_Start` | core | Starts OBJ_HoldOffSiege, adds fail/camp check rules |
| `Dover_InitEnemyUnits` | core | Deploys all French intro units to staging positions |
| `Dover_InitPlayerUnits` | core | Deploys English archers/cavalry to castle walls |
| `Dover_StartWillikinPhase` | core | Spawns Willikin, traders, villagers; transfers village ownership |
| `Dover_SendWallArchers` | core | Moves archers to wall positions during intro |
| `Dover_SpawnWave` | core | Generic wave spawner into a named module |
| `Dover_SpawnRangedSiegeNorth` | core | Spawns ranged siege unit to north attack module |
| `Dover_SpawnRangedSiegeSouth` | core | Spawns ranged siege unit to south attack module |
| `Dover_CheckFailCondition` | core | Fails mission if keep EGroup is empty |
| `Dover_CheckFrenchCampStatus` | core | Starts OBJ_DestroySiegeCamp when player nears camp |
| `Dover_SkipIntro` | core | Warps units to positions if intro is skipped |
| `Dover_InitOutro` | core | Spawns retreating French and celebratory English units |
| `HoldOffSiege_InitObjectives` | holdoffsiege | Registers OBJ_HoldOffSiege, SOBJ_DefeatFrenchUnits, OBJ_SiegeStrength |
| `Dover_OnEntityKilled` | holdoffsiege | Tracks kill counts for active siege objective progress |
| `Dover_StartInitialAttack` | holdoffsiege | Sets attack targets, triggers first siege release waves |
| `Dover_ReleaseSiegeUnits_Wave1` | holdoffsiege | Releases north defenders + spawns south init_wave 1 |
| `Dover_ReleaseSiegeUnits_Wave2` | holdoffsiege | Releases north defenders + spawns south init_wave 2 |
| `Dover_Retreat_Initial` | holdoffsiege | Transfers attackers to defend modules after wave 1 defeat |
| `Dover_Retreat_Final` | holdoffsiege | Plays celebration audio, starts SiegeWaves_StartWave1 |
| `SiegeWaves_InitObjectives` | siegewaves | Registers all siege wave sub-objectives (6 total) |
| `SiegeWaves_StartWave1` | siegewaves | Spawns south siege waves, starts countdown timer |
| `SiegeWaves_StartWave2` | siegewaves | Starts SOBJ_IncomingWave2 countdown timer |
| `SiegeWaves_StartWave3` | siegewaves | Starts SOBJ_IncomingWave3 countdown timer |
| `SiegeWaves_CompleteWave3` | siegewaves | Completes OBJ_HoldOffSiege (victory) |
| `Dover_Timer1Complete` | siegewaves | Fires siege attack, starts SOBJ_RepelSiege1 |
| `Dover_Timer2Complete` | siegewaves | Fires siege attack, starts SOBJ_RepelSiege2 |
| `Dover_Timer3Complete` | siegewaves | Starts SOBJ_RepelFrenchSiege (final wave) |
| `Dover_SiegeAttack` | siegewaves | Main attack dispatcher — transfers/spawns units, siege towers |
| `Dover_SiegeAttackFinal` | siegewaves | Releases all siege position modules into attack |
| `Dover_SiegeFallbackIfLosing` | siegewaves | Completes wave objective when all attackers eliminated |
| `Dover_SiegeRetreat` | siegewaves | Transfers all attack modules back to reserve |
| `Dover_SpawnSiegeTowerWave1` | siegewaves | Spawns siege tower wave 1 to north |
| `Dover_SpawnSiegeTowerWave2` | siegewaves | Spawns siege tower wave 2 to south |
| `Dover_SpawnSiegeTowerWave3` | siegewaves | Spawns siege tower waves to both flanks |
| `Dover_SpawnFromCart` | siegewaves | Spawns reserve units when supply cart arrives |
| `Dover_ReleaseReservesIfFull` | siegewaves | Transfers reserves to weaker defend module when >9 |
| `Dover_CheckRoadPatrols` | siegewaves | Replenishes road patrol units if below threshold |
| `Dover_GenerateSiegeRoute` | siegewaves | Returns randomized north or south siege approach |
| `Dover_ResetCartKillCount` | siegewaves | Resets cart kill counter, updates OBJ_SiegeStrength |
| `Dover_IncrementCartKillCount` | siegewaves | Increments cart kills, updates progress bar |
| `Dover_SiegeVOLine` | siegewaves | Plays VO based on wave number and cart arrival count |
| `DisruptFrench_InitObjectives` | disruptfrench | Registers all Willikin/disruption objectives (7 total) |
| `Dover_StartSupplyTrains` | disruptfrench | Starts supply train interval rule and monitoring |
| `Dover_SendSupplyTrain` | disruptfrench | Spawns supply cart with escort on north/south route |
| `Dover_OnSupplyArrival` | disruptfrench | Destroys arrived cart, dissolves escort to reserve |
| `Dover_GenerateSupplyRoute` | disruptfrench | Chooses north/south route, displays path icons |
| `Dover_CheckArcherRecruitDover` | disruptfrench | Recruits Dover town archers when Willikin nearby |
| `Dover_CheckArcherRecruitNorth` | disruptfrench | Recruits north village archers when Willikin nearby |
| `Dover_CheckArcherRecruitWest` | disruptfrench | Recruits west village archers when Willikin nearby |
| `Dover_CheckForestCamp` | disruptfrench | Detects player near forest camp, spawns allies |
| `Dover_RecruitForestCamp` | disruptfrench | Transfers forest allies to player when Willikin nearby |
| `Dover_CheckForestAllyObjective` | disruptfrench | Reveals forest camp after wave 1, starts optional obj |
| `Dover_SpawnForestCamp` | disruptfrench | Spawns monk + men-at-arms + archers at forest camp |
| `Dover_CheckSouthAmbush` | disruptfrench | Detects player near south ambush, triggers skirmish |
| `Dover_SpawnSouthAmbush` | disruptfrench | Spawns allied + enemy units at south ambush site |
| `Dover_CheckSiegeCampReinforcement` | disruptfrench | Respawns camp defenders when count drops below 20 |
| `Dover_CheckEdgeReinforcement` | disruptfrench | Respawns rearguard3 when count drops below 20 |
| `Dover_OnSquadKilled` | disruptfrench | Handles supply cart death — increments kill count |
| `Dover_EvaluateActivePaths` | disruptfrench | Clears path UI icons when no active carts on route |
| `Dover_SpawnWillikinExtras` | disruptfrench | Spawns reinforcements based on pop space in forest |
| `Dover_MonitorEscortSGroups` | disruptfrench | Unlocks escort speed when engaged; shows edge path |
| `Dover_OnSquadBuilt` | disruptfrench | Tracks trader production for SOBJ_ProduceTraders |
| `Dover_SpawnRandomForestPatrol` | disruptfrench | Spawns French patrol to random forest defend module |
| `Dover_SpawnRoadPatrol` | disruptfrench | Spawns French horseman patrol on random road |
| `MissionTutorial_DoverLeaderAura` | training | Training goal for Willikin's leader ability tooltip |
| `MissionTutorial_DoverTraders` | training | Training goal for trader unit tooltip |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_HoldOffSiege` | Primary/Battle | Hold off the French siege (parent for all siege waves); counter 0–4 |
| `SOBJ_DefeatFrenchUnits` | Battle (child) | Defeat the first French attack (kill-count or wipe attackers) |
| `OBJ_SiegeStrength` | Information | Displays enemy reinforcement level for next attack (progress bar) |
| `SOBJ_IncomingWave1` | Information (child) | Countdown timer before second French attack |
| `SOBJ_RepelSiege1` | Battle (child) | Defeat the second French attack |
| `SOBJ_IncomingWave2` | Tip (child) | Countdown timer before third French attack |
| `SOBJ_RepelSiege2` | Battle (child) | Defeat the third French attack |
| `SOBJ_IncomingWave3` | Tip (child) | Countdown timer before final French attack |
| `SOBJ_RepelFrenchSiege` | Battle (child) | Defeat the final French attack |
| `OBJ_DisruptFrench` | Primary | Disrupt French forces with Willikin (parent for guerrilla phase) |
| `SOBJ_GatherArchersDoverTown` | Primary (child) | Use Willikin to gather longbowmen from Dover town |
| `SOBJ_GatherArchersVillages` | Primary (child) | Gather longbowmen from 2 nearby villages (counter 0/2) |
| `SOBJ_AmbushSiege` | Primary (child) | Ambush French siege weapons to weaken attacks |
| `SOBJ_RecruitForestAllies` | Optional | Use Willikin to gather additional forest camp allies |
| `SOBJ_ProduceTraders` | Optional | Produce additional traders (counter 0/3) |
| `OBJ_DestroySiegeCamp` | Optional | Destroy 4 French siege camp production buildings |
| `OBJ_DebugComplete` | Debug | Kills all French, destroys gates, completes mission |

### Difficulty

All values indexed as `{Easy, Normal, Hard, Hardest}`:

| Parameter | Values | Scales |
|-----------|--------|--------|
| `supplyLoopTimer` | 60, 60, 50, 40 | Interval between supply train dispatches |
| `cartsPerStage` | 4, 4, 5, 6 | Number of supply carts per siege stage |
| `supplyEscort_escalates` | false, true, true, true | Whether escort size grows each wave |
| `supplyEscort_melee` | 2, 2, 3, 5 | Melee units per supply escort |
| `supplyEscort_ranged` | 0, 0, 1, 3 | Ranged units per supply escort |
| `supplyEscort_cav` | 0, 0, 0, 2 | Cavalry units per supply escort |
| `supply_healthMod` | 0.25, 0.5, 0.5, 0.5 | Supply cart health multiplier |
| `reserve_melee` | 2, 3, 4, 5 | Melee squads spawned per cart arrival |
| `reserve_ranged` | 2, 3, 4, 5 | Ranged squads spawned per cart arrival |
| `reserve_cav` | 2, 3, 4, 5 | Cavalry squads spawned per cart arrival |
| `reserve_siegeType` | springald, mangonel, mangonel, mangonel | Siege unit type for reserve spawns |
| `road_patrol` | 0, 0, 2, 3 | Units per road patrol squad (0 = disabled) |
| `siege_wave_base` | 5, 8, 12, 15 | Base squads per siege wave composition |
| `st_wave_base` | 4, 6, 8, 8 | Base squads per siege tower wave |
| `player_StartingResource` | 1500/600, 1500/600, 1000/400, 500/200 | Starting gold/wood/food / stone |

### Spawns

**Initial Attack (Intro):** French deploy ~60 units (spearmen, men-at-arms, archers, rams, horsemen, mangonels) across multiple staging markers. Intro attack squads have 50% HP. Two follow-up init_waves spawn to the south: Wave 1 (5 MAA, 8 spear, 5 xbow) and Wave 2 (4 MAA, 5 spear, 10 xbow, 1 ram).

**Siege Waves (t_wave_base):** Three compositions cycled per wave — crossbowmen + spearmen + ram, crossbowmen + MAA + ram, crossbowmen + knights. Squad counts scale with `siege_wave_base` difficulty.

**Siege Tower Waves (t_st_waves):** Three compositions with 1 siege tower each, paired with infantry. Wave 1 hits north, Wave 2 hits south, Wave 3 hits both flanks simultaneously. Delayed 15 seconds after main wave.

**Supply Trains:** Spawned on interval (`supplyLoopTimer`). Each train is 1 ram (visual cart) with a cycling escort of 5 compositions (spear/xbow, spear/archer, MAA/archer, spear/horseman, MAA/xbow). Escort size increases with siege wave on Hard+. Carts travel north or south path alternately. On arrival, a reserve unit group is spawned from 4 cycling compositions.

**Road Patrols:** Activated after all carts sent per stage. 10 compositions cycled (scouts, infantry, cavalry, monks). Replenished when count drops below threshold.

**French Rearguards:** Three static defend positions with 10 archers + 15 MAA each. Rearguard3 reinforced with 10 MAA + 10 archers when below 20 units.

**Camp Defenders:** 10 MAA + 15 archers at camp. Reinforced with 5 knights + 5 archers when below 20.

**Willikin Extras:** Scales 3 tiers based on forest-area pop (2 MAA + 3 archers → 3 MAA + 7 archers → 4 MAA + 11 archers).

**Forest Camp Allies:** 1 monk, 3 MAA, 3 archers (spawned as player6/forest).

**South Ambush:** 6 MAA + 2 archers (allied) vs 4 spear + 1 MAA (French), initially invulnerable.

### AI

- **AI_Enable:** Disabled for `g_playerOutro`, `g_playerForest`, `g_playerLeader`
- **French AI Pathing:** `AIPlayer_SetMarkerToUpdateCachedPathToPosition` set for north and south gate markers with 5.0 radius
- **Module System:** MissionOMatic army modules control all French behavior:
  - `AttackNorth` / `AttackSouth` — RovingArmy targeting castle gates
  - `RangedSiegeNorth` / `RangedSiegeSouth` — RovingArmy for siege weapons
  - `TowerAttackNorth` / `TowerAttackSouth` — RovingArmy for siege towers with specific wall targets
  - `DefendNorth` / `DefendSouth` — Defend modules at staging areas
  - `DefendCamp` — Defend at French main camp
  - `FrenchReserve` — Reserve pool at rally point
  - `SiegeNorth1/2`, `SiegeSouth1/2` — Static siege positions
  - `Rearguard1/2/3` — Static rearguard defend positions
  - `DefendForest/NW/NE/SW/SE` — Forest area defend positions
  - `NorthRoadPatrol` / `SouthRoadPatrol` — RovingArmy cycling patrol paths
  - `SouthAmbushFrench` / `SouthAmbushAlly` — Ambush encounter modules
- **Fallback Logic:** `Dover_SiegeFallbackIfLosing` checks every 10s if attackers are eliminated near castle; transfers survivors back to defend modules
- **Reserve Release:** When reserves exceed 9 units, auto-transferred to the weaker defend flank
- **Ranged Siege Filtering:** Mangonels/springalds filtered out of attack groups into dedicated ranged siege modules

### Timers

| Timer | Duration | Purpose |
|-------|----------|---------|
| `siegeWaveTimerInitial` | 630s (510+120) | Countdown before wave 2 (first timed wave) |
| `siegeWaveTimer` | 510s | Countdown before waves 3 and 4 |
| `supplyLoopTimer` | 60/60/50/40s | Interval between supply train dispatches |
| `Dover_StartSupplyTrains` | 120s one-shot | Delay before first supply train after Willikin starts |
| `Dover_StartTraderObjective` | 40s one-shot | Delay before showing SOBJ_ProduceTraders |
| `Dover_SiegeFallbackDelay` | 20s (waves 1-2), 60s (final) | Delay before fallback check begins |
| `Dover_SiegeFallbackIfLosing` | 10s interval | Checks if attackers are wiped for wave completion |
| `Dover_ReleaseSiegeUnits_Wave1` | 20s one-shot | Delay before releasing first batch of siege units |
| `Dover_ReleaseSiegeUnits_Wave2` | 20s after wave1 | Delay before releasing second batch of siege units |
| `Dover_SpawnSiegeTowerWave*` | 15s one-shot | Delay before siege towers spawn after main wave |
| `Dover_SiegeAttackFinal2` | 40s one-shot | Delay before second siege position transfers to attack |
| `Dover_SiegeAttackFinal` (initial) | 40s one-shot | Delay before final wave siege positions attack |
| `Dover_CheckFailCondition` | 5s interval | Checks if keep is destroyed |
| `Dover_CheckFrenchCampStatus` | 5s interval | Checks if player is near French camp |
| `Dover_CheckSiegeCampReinforcement` | 12s interval | Replenishes camp defenders |
| `Dover_CheckEdgeReinforcement` | 12s interval | Replenishes rearguard3 |
| `Dover_CheckRoadPatrols` | 30s interval | Replenishes road patrol units |
| `Dover_CheckForestAllyObjective` | 45s one-shot | Reveals forest camp after wave 1 defeat |
| `Dover_MonitorEscortSGroups` | 2s interval | Monitors escort combat state, unlocks speed |
| `Dover_CheckArcherRecruit*` | 1s interval | Proximity checks for Willikin archer recruitment |
| `Dover_CheckForestCamp` | 2s interval | Proximity check for forest camp discovery |
| `Dover_CheckSouthAmbush` | 2s interval | Proximity check for south ambush trigger |
| `Dover_RevealSouthAmbush` | 2.5s one-shot | FOW reveal after south ambush triggered |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core mission framework (Prefab_DoAction, RovingArmy_*, Defend_*, TransferModuleIntoModule, DissolveModuleIntoModule, SpawnUnitsToModule, MissionOMatic_FindModule)
- `obj_holdoffsiege.scar` — Siege defense objectives
- `obj_siegewaves.scar` — Siege wave objectives
- `obj_disruptfrench.scar` — Willikin disruption objectives
- `ang_chp4_dover_data.scar` — Data/config
- `training_dover.scar` — Tutorial goals
- `training/campaigntraininggoals.scar` — Shared training framework (CampaignTraining_TimeoutIgnorePredicate, AShortPeriodOfTimeHasPassed, Training_Goal, Training_GoalSequence, Training_AddGoalSequence)

### Shared Globals
- `g_leaderWillikin` — Missionomatic_InitializeLeader leader object
- `g_playerNorman` (player1), `g_playerFrench` (player2), `g_playerLocals` (player3), `g_playerLeader` (player4), `g_playerOutro` (player5), `g_playerForest` (player6)
- `t_difficulty` — Difficulty parameter table used across all files
- `siegeWave`, `siegeUnitCount` — Shared siege state between holdoffsiege and siegewaves
- `cartArrivedCount`, `cartSentCount`, `cartKills`, `cartsPerStage` — Supply train state shared between disruptfrench and siegewaves
- `introKillCount` — Set in core, consumed by holdoffsiege for initial attack progress
- `sg_fre_attacknorth`, `sg_fre_attacksouth`, `sg_fre_reserve`, `sg_fre_defendnorth`, `sg_fre_defendsouth` — Army SGroups shared across all objective files
- `t_wave_base`, `t_init_waves`, `t_st_waves`, `t_siege_south_waves` — Wave data tables defined in data, consumed by siegewaves and holdoffsiege
- `supply_entries`, `escort_entries` — Supply tracking arrays shared between disruptfrench files

### Inter-File Function Calls
- `ang_chp4_dover.scar` → `Dover_Data_Init()`, `HoldOffSiege_InitObjectives()`, `SiegeWaves_InitObjectives()`, `DisruptFrench_InitObjectives()`, `Dover_InitWaveData()`
- `obj_holdoffsiege.scar` → `SiegeWaves_StartWave1()`, `Dover_WallArchersHoldPosition()`, `Dover_SpawnWave()`
- `obj_siegewaves.scar` → `Dover_SiegeAttack()`, `Dover_SpawnWave()`, `Dover_ResetCartKillCount()`, `Dover_SpawnRangedSiegeNorth/South()`, `Dover_CheckForestAllyObjective()`
- `obj_disruptfrench.scar` → `Dover_StartWillikinPhase()`, `Dover_StartSupplyTrains()`, `MissionTutorial_DoverLeaderAura()`, `MissionTutorial_DoverTraders()`
- `obj_siegewaves.scar` → `Dover_EvaluateActivePaths()`, `Dover_ReleaseReservesIfFull()`

### Blueprint References
- `UPG.ENGLISH.UPGRADE_LONGBOW_MAKE_CAMP_ENG`, `UPG.ENGLISH.UPGRADE_RANGED_LONGBOW_ARROW_VOLLEY_ENG` — English longbow upgrades
- `UPG.COMMON.UPGRADE_RANGED_INCENDIARY` — Incendiary arrows for all English players
- `UPG.FRENCH.UPGRADE_RANGED_INCENDIARY_FRE` — French incendiary
- `UPG.COMMON.UPGRADE_SIEGE_WEAPON_SPEED` — French siege speed
- `UPG.COMMON.UPGRADE_OUTPOST_SPRINGALD`, `UPG.COMMON.UPGRADE_OUTPOST_STONE` — French camp outpost upgrades
- `unit_willikin_cmp_eng` — Willikin hero squad blueprint
- `leader_move_speed_activated` — Willikin's leader aura ability
