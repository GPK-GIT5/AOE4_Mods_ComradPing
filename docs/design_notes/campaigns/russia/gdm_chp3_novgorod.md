# Russia Chapter 3: Novgorod

## OVERVIEW

This mission recreates Ivan the Great's 1478 conquest of Novgorod across a four-phase campaign. The player (Rus, Castle Age) must first capture two outlying towns — Kuklino and Soltsy — establishing an economic base with villagers, Hunting Cabins, and Holy Sites. Phase 2 requires eliminating the people's militia garrison at the Shelon River fort. Phase 3 tasks the player with breaching Novgorod's outer and inner walls. The final phase demands destroying the Veche Bell inside the city to complete the conquest. A robust wave system sends escalating attacks from all enemy settlements, with unit compositions and timing scaling across four difficulty levels. The mission also features an extensive tutorial/training layer for Rus-specific mechanics (Hunting Bounty, Hunting Cabins, Ivan III's leader aura, Holy Sites).

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp3_novgorod.scar` | core | Main mission file: player setup, difficulty, recipe, intro/outro, wave system, wildlife spawns, villager life |
| `obj_capture_village.scar` | objectives | Phase 1: Capture Kuklino and Soltsy towns, optional objectives (cabins, holy sites, hunting) |
| `obj_middle_battle.scar` | objectives | Phase 2: Defeat militia at Shelon River fort with progress tracking |
| `obj_getthroughnovgorod.scar` | objectives | Phase 3: Breach Novgorod walls and enter the city |
| `obj_destroy_novgorod.scar` | objectives | Phase 4: Destroy Veche Bell (and commented-out Kremlin/University targets) |
| `obj_getagefour.scar` | other | Entirely commented out; vestigial Age 4 upgrade objective |
| `training_novgorod.scar` | training | Tutorial goal sequences for Hunting Bounty, Hunting Cabin, Holy Sites, Ivan III leader aura |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Configure 4 players, names, ages, relationships, colours |
| `Mission_SetupVariables` | core | Create SGroups/EGroups, wolf/animal markers, leader init |
| `Mission_SetRestrictions` | core | Reduce player max pop cap by 10 |
| `Mission_Preset` | core | Upgrades, objective init, villager jobs, wave setup, spawn units |
| `Mission_SetDifficulty` | core | Define difficulty table for resources, thresholds, build times |
| `Mission_Start` | core | Grant resources, start objectives, init training, deploy militia |
| `GetRecipe` | core | Return MissionOMatic recipe with modules, locations, NIS |
| `Novgorod_SpawnStartingUnits` | core | Deploy player army (Ivan, knights, horsemen, infantry) |
| `Novgorod_MoveStartingUnits` | core | Choreograph intro march with speed modifiers |
| `SetupAttackWaves` | core | Define 5 RovingArmy assault wave configs |
| `PreparekuklinoWaveTosoltsy` | obj_capture_village | Escalating phase-based waves from Kuklino to Soltsy |
| `PreparesoltsyWaveTokuklino` | obj_capture_village | Escalating phase-based waves from Soltsy to Kuklino |
| `PrepareSkirinoWave` | core | Phase-based waves from Skirino after both towns captured |
| `PrepareNovgorodWave` | core | Phase-based Novgorod waves after middle battle complete |
| `Start_SkorinoWaves` | core | Enable Skirino wave system and proximity monitor |
| `Start_NovgorodWaves` | core | Enable Novgorod wave system post-Phase 2 |
| `Mission_AddMoreWolvesNovgorod` | core | Respawn wolves at random positions out of player sight |
| `Mission_AddMoreAnimalsNovgorod` | core | Respawn boars for hunting bounty |
| `Mission_AddMoreAnimalsNovgorodTown01` | core | Respawn deer near first town |
| `Mission_SpawnDeersStartArea` | core | Initial deer spawn near starting area |
| `Novgorod_SkirinoVillagerLife` | core | Spawn villager life groups at Skirino (east/west/front) |
| `Novgorod_NovgorodVillagerLife` | core | Spawn villager life groups at Novgorod city |
| `Novgorod_OutroSequence` | core | Burn buildings, spawn Ivan march, victory sequence |
| `IvanMovesOnTown` | core | Outro: deploy cheering units and Ivan escort |
| `Novgorod_ProxFunctionCall` | core | Generic proximity trigger that calls a function on approach |
| `Novgorod_CountSGroups` | core | Count spawned squads across an SGroup table |
| `Novgorod_SoltsyWallWalla` | core | Audio stinger on first Soltsy wall breach |
| `Novgorod_SkirinoWallWalla` | core | Audio stinger + weather transition on Skirino wall breach |
| `Novgorod_NovgorodOuterWallWalla` | core | Audio stinger on Novgorod outer wall breach |
| `Novgorod_NovgorodInnerWallWalla` | core | Audio stinger on Novgorod inner wall breach |
| `CaptureLocations_Initkuklino` | obj_capture_village | Register Kuklino capture objective and sub-objectives |
| `CaptureLocations_Initsoltsy` | obj_capture_village | Register Soltsy capture objective and sub-objectives |
| `CaptureLocations_InitOptionalObjectives` | obj_capture_village | Register optional: build cabins, capture holy site, hunt |
| `CaptureVillagesNov_OnComplete` | obj_capture_village | Complete OBJ_SettleBase when both towns captured |
| `Monitor_HolySites` | obj_capture_village | Trigger holy site tutorial when monk exists but no site owned |
| `MonitorPlayerGold` | obj_capture_village | Trigger cabin hint when gold runs low |
| `SendVillagers_Farm_soltsy` | obj_capture_village | Spawn/assign villagers after Soltsy capture |
| `Delayed_MilitiaAddition` | core | Warp militia to Kuklino TC and attack-move |
| `middle_battle_InitObjectives` | obj_middle_battle | Register Phase 2 objectives: defeat militia at Shelon fort |
| `CountEnemiesKilledFortShelon` | obj_middle_battle | Count tagged enemy squads at fort |
| `MiddleBattle_OnCompleteTimer` | obj_middle_battle | Delayed start of Phase 3 after fort cleared |
| `GetThroughNovgorodDefences_InitObjectives` | obj_getthroughnovgorod | Register Phase 3: conquer + enter Novgorod objectives |
| `NovgorodMarchThrough_SetMusic` | obj_getthroughnovgorod | Lock combat music intensity for 60s on Novgorod entry |
| `DestroyNovgorod_InitObjectives` | obj_destroy_novgorod | Register Phase 4: destroy Veche Bell objective |
| `FindVecheBell_Monitor` | obj_destroy_novgorod | Play bell sound when player first sees it |
| `VecheBell_VOThresholdTrigger` | obj_destroy_novgorod | Trigger VO/SFX at 33% and 25% bell HP |
| `DestroyTheKremlin_Monitor` | obj_destroy_novgorod | Monitor Kremlin Armoury destruction (commented-out obj) |
| `DestroyUniversity_Monitor` | obj_destroy_novgorod | Monitor University destruction (commented-out obj) |
| `Training_InitNov` | training_novgorod | Init training system, selection callbacks, hover callbacks |
| `Tutorials_novgorod_HintHuntingBounty` | training_novgorod | Tutorial: select villager, view Rus hunting bounty |
| `Tutorials_novgorod_HintCabin` | training_novgorod | Tutorial: build a Hunting Cabin (PC) |
| `Tutorials_novgorod_HintCabin_Xbox` | training_novgorod | Tutorial: build a Hunting Cabin (Xbox) |
| `Tutorials_novgorod_HintHolySite` | training_novgorod | Tutorial: capture Holy Site with monk |
| `MissionTutorial_IvanLeaderAura` | training_novgorod | Tutorial: use Ivan III leader production ability (PC) |
| `MissionTutorial_IvanLeaderAura_XBox` | training_novgorod | Tutorial: use Ivan III leader production ability (Xbox) |
| `Nov_PickConvenientVillager` | training_novgorod | Find idle/on-screen villager for tutorial targeting |

## KEY SYSTEMS

### Objectives

| Constant | Phase | Purpose |
|----------|-------|---------|
| `OBJ_ConquerNovgorod` | Master | Top-level primary: conquer Novgorod (complete when all subs done) |
| `OBJ_SettleBase` | 1 | Capture outlying towns (Kuklino + Soltsy) |
| `SOBJ_CaptureKuklino` | 1 | Sub: capture Kuklino village |
| `SOBJ_DefeatkuklinoRebels` | 1 | Sub: defeat Kuklino defenders |
| `SOBJ_Locationkuklino` | 1 | Sub: location capture tracking |
| `SOBJ_CaptureSoltsy` | 1 | Sub: capture Soltsy village |
| `SOBJ_DefeatsoltsyRebels` | 1 | Sub: defeat Soltsy defenders |
| `SOBJ_Locationsoltsy` | 1 | Sub: location capture tracking |
| `OBJ_OptionalHelp` | 1 | Optional parent: economy guidance |
| `SOBJ_BuildCabins` | 1 | Optional: build 3 gold-generating Hunting Cabins |
| `SOBJ_CaptureHolySites` | 1 | Optional: capture 1 Holy Site |
| `SOBJ_HuntGaia` | 1 | Optional: hunt 5 animals for bounty |
| `OBJ_MiddleBattle` | 2 | Eliminate militia at Shelon River fort |
| `SOBJ_KillUnitsAtFort` | 2 | Sub: defeat all militiamen (progress bar tracked) |
| `SOBJ_GetThroughNovgorod` | 3 | Enter Novgorod (proximity check) |
| `SOBJ_DestroyVecheBell` | 4 | Destroy the Veche Bell to complete mission |
| `SOBJ_DestroyKremlin` | 4 | Destroy Kremlin Armoury (commented out / not registered) |
| `SOBJ_DestroyUniversity` | 4 | Destroy University (commented out / not registered) |
| `OBJ_DebugComplete` | — | Debug: instant mission complete cheat |

### Difficulty

All values are `Util_DifVar({Story, Easy, Normal, Hard})`:

| Parameter | What It Scales |
|-----------|---------------|
| `given_resources_gold` | Starting gold: 1000/800/400/250 |
| `given_resources_wood` | Starting wood: 200/200/150/100 |
| `given_resources_food` | Starting food: 200/200/150/100 |
| `given_resources_stone` | Starting stone: 100/100/70/60 |
| `i_request_Nov_upperThreshold` | AI request upper threshold: 0.6–0.9 |
| `i_request_Nov_lowerThreshold` | AI request lower threshold: 0.15–0.1 |
| `i_request_Nov_desiredStrength` | AI desired strength: 0.7–1.0 |
| `i_maximumNumberOfWolves` | Max wolf spawns: 10/10/8/6 |
| `i_maximumNumberOfAnimals` | Max boar spawns: 30/22/20/15 |
| `i_maximumNumberOfAnimalsTown01` | Max deer near town 01: 20/15/12/10 |
| `enemy_unitBuildTime` | Standard unit build time: 30/25/10/12 |
| `enemy_eliteUnitBuildTime` | Elite unit build time: 40/30/15/14 |

Additional difficulty gates:
- Story mode: attack waves disabled entirely, extra villagers on capture, optional objectives on Easy/Normal only
- Hard: `Wave_OverrideUnitBuildTime` applied to all unit types
- Non-Story: wooden forts get springald upgrades for player2

### Spawns

**Player Starting Army:** Ivan the Great (hero), 4 horsemen, 2 monks, 4 knights, 8 spearmen, 8 men-at-arms, 4 crossbowmen, 4 archers. All deployed via `UnitEntry_DeploySquads` with individual spawn markers.

**Kuklino Defenders (player4):** Archers (2–3 per spawn × 5 spawns) + spearmen (4–5 per spawn × 3 spawns), scaling by difficulty. Additional militia (20–30) deployed via `UnitEntry_DeploySquads`.

**Soltsy Defenders (player4):** Three defend zones — gate (archers 5–10), secondary gate (archers, spearmen, militia 10–20), center (militia 15–30 × 3 spawns, spearmen, MAA, archers — heavy garrison).

**Shelon Fort Defenders (player2):** 7 defend modules with mixed compositions — militia (10–50), spearmen, archers, MAA, crossbowmen, knights, horsemen. All tagged `"RusFort"` for progress tracking.

**Novgorod City Defenders (player2):** 6 infantry defend zones + 2 wall guard zones. Spawned on Phase 3 start: spearmen (4–9), MAA (2–6), archers (3–10) per zone × 12 spawn points, plus wall archers (3–5 × 2).

**Attack Wave System (5 waves):**
- Wave 1: Kuklino → Soltsy (player4, RovingArmy, CYCLE targeting)
- Wave 2: Soltsy → Kuklino (player4, RovingArmy, CYCLE targeting)
- Wave 3: Skirino → Soltsy/Kuklino (player2, CYCLE, starts after both towns captured)
- Wave 4: Novgorod front → Skirino/Soltsy/Kuklino (player2, REVERSE, starts after Phase 2)
- Wave 5: Novgorod back → same targets (player2, REVERSE, alternate for wave 4)

All waves use phased escalation (6+ phases per wave origin), compositions shift from infantry to cavalry to mixed. Timing between waves: 60–170s depending on difficulty. Build time overrides: 8s per unit (default), difficulty can further modify.

### AI

- No direct `AI_Enable` calls; enemy behavior driven entirely by `MissionOMatic` Defend modules and `RovingArmy` Wave system
- 7 Defend modules for Shelon River fort (player2, leash-based)
- 6 Defend modules + 2 wall guard modules for Novgorod city (player2)
- 2 Defend modules per captured town (player4) with staging areas
- `SkorinoForcesApproachTown_Monitor`: proximity-based intel trigger when player2 forces reach Soltsy
- `CheckPlayerReachedSkirino`: triggers `OBJ_MiddleBattle` when player approaches fort

### Timers

| Timer/Rule | Interval | Purpose |
|------------|----------|---------|
| `Novgorod_ProxFunctionCall` | 1s interval | Proximity trigger for Skirino/Novgorod villager life spawns |
| `CaptureVillage_KuklinoProximityStinger` | 0.5s interval | Combat music stinger near Kuklino |
| `CaptureVillage_SoltsyProximityVO` | 0.5s interval | VO trigger near Soltsy |
| `PreparesoltsyWaveTokuklino` | OneShot 170/170/150/70s | Recurring wave prep from Soltsy |
| `PreparekuklinoWaveTosoltsy` | OneShot 0/150/130/110s | Recurring wave prep from Kuklino |
| `PrepareSkirinoWave` | OneShot 90/90/75/60s | Recurring wave prep from Skirino |
| `PrepareNovgorodWave` | OneShot 150/150/130/110s | Recurring wave prep from Novgorod |
| `CaptureVillage_DelayedMiddleBattleStart` | OneShot 5s | Start Phase 2 after both towns captured |
| `MiddleBattle_OnCompleteTimer` | OneShot 5s | Start Phase 3 after fort cleared |
| `FindVecheBell_Monitor` | 1s interval | Bell reveal SFX when visible |
| `VecheBell_VOThresholdTrigger` | 1s interval | VO at 33%/25% bell HP |
| `ResetMusicRegularEnterNov` | OneShot 60s | Unlock music intensity after Novgorod entry |
| `Tutorials_novgorod_HintCabin` | OneShot 30s | Trigger Hunting Cabin tutorial |
| `Tutorials_novgorod_HintHuntingBounty` | OneShot 30s | Trigger Hunting Bounty tutorial |
| `Ivan_SendOutroCav` | OneShot 2.5s | Outro: move Ivan to final position |
| `Game_TransitionToState("tiaga_winter_sunset")` | 450s transition | Weather/lighting shift during gameplay |
| `Game_TransitionToState("tiaga_winter_dusk")` | 300s transition | Second weather shift on Skirino wall breach |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Cardinal campaign framework (core)
- `obj_capture_village.scar` — imported by core
- `obj_middle_battle.scar` — imported by core
- `obj_getthroughnovgorod.scar` — imported by core
- `obj_destroy_novgorod.scar` — imported by core
- `training_novgorod.scar` — imported by core
- `training/campaigntraininggoals.scar` — imported by training file
- `training/rustrainingconditions.scar` — imported by training file

### Shared Globals
- `player1`–`player4`: player handles used across all files
- `g_leaderKingIvan`: leader struct initialized in core, referenced in training and outro
- `t_difficulty`: difficulty table set in core, read across objective files
- `difficulty`: raw difficulty value from `Game_GetSPDifficulty()`
- `wave_1`–`wave_5`: Wave objects created in core, prepared in obj_capture_village and core
- `sg_allsquads` / `eg_allentities`: temporary global groups reused across files
- `b_skorino_units_approachTowns`: flag shared between core and wave monitoring
- `i_kuklino_phase`, `i_soltsy_phase`, `i_skorino_phase`, `i_novgorod_phase`: wave escalation counters

### Inter-File Function Calls
- Core calls: `CaptureLocations_Initkuklino()`, `CaptureLocations_Initsoltsy()`, `CaptureLocations_InitOptionalObjectives()`, `middle_battle_InitObjectives()`, `GetThroughNovgorodDefences_InitObjectives()`, `DestroyNovgorod_InitObjectives()`, `Training_InitNov()`
- `obj_capture_village` calls: `Start_SkorinoWaves()`, `Start_NovgorodWaves()` (from core), `Tutorials_novgorod_HintCabin()`, `Tutorials_novgorod_HintHuntingBounty()`, `Tutorials_novgorod_HintHolySite()`, `MissionTutorial_IvanLeaderAura()` / `_XBox()` (from training)
- `obj_middle_battle` calls: `Novgorod_CountSGroups()` (from core), `SpawnUnitsToModule()` / `MissionOMatic_FindModule()` (from MissionOMatic)
- `obj_getthroughnovgorod` calls: `SpawnUnitsToModule()`, `MissionOMatic_FindModule()` (from MissionOMatic), `Mission_Complete()` / `Mission_Fail()` (from Cardinal)
- `obj_destroy_novgorod` calls: `Mission_Complete()` (from Cardinal)
- Training file references: `g_leaderKingIvan.sgroup`, `EBP.RUS.*`, `SBP.RUS.*`, Cardinal training API (`Training_Goal`, `Training_GoalSequence`, `Training_AddGoalSequence`)

### EVENTS Constants Referenced
- `EVENTS.HUN_FALLNOVGOROD_Intro` (intro NIS)
- `EVENTS.Victory` (outro NIS)
- `EVENTS.CaptureBackNovTowns`, `EVENTS.Capturekuklino`, `EVENTS.Show_Capturesoltsy`
- `EVENTS.CaptureBoth` (Phase 2 intel)
- `EVENTS.DestroyNovgorod` (Phase 3 intel)
- `EVENTS.DestroyLandmarks`, `EVENTS.DestroyBell` (Phase 4 intel)
- `EVENTS.SkorinoForcesApproachPlayerTown`, `EVENTS.Gold_Exhausted`
