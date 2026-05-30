# Hundred Years War Chapter 4: Formigny

## OVERVIEW

This mission recreates the 1450 Battle of Formigny, where the French player (player1) drives the English (player2) from Normandy. The mission begins with a large-scale intro battle at Carentan where the player must weaken Kyriell's advancing English army, then transitions to an open-world march through Normandy clearing English-held towns (Bricquebec, Saint-Sauveur), optionally saving the allied village of Valognes (player3), and culminating in a multi-phase pitched battle against Kyriell's remaining forces at Formigny. The final battle features a frenzy phase where front-line English units advance, Breton cavalry reinforcements (30 knights) arriving when player losses mount, a pivot phase where the English reposition, artillery (6 cannons) spawning when forward outposts fall, and eventual English retreat at 85% casualties. The mission ends with capturing the Formigny location and an outro parade.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp4_formigny_data.scar` | data | Defines all combat variables, army sizes, difficulty scaling, SGroup/EGroup creation, MissionOMatic module references, and the full recipe (modules, locations, unit spawners) |
| `hun_chp4_formigny.scar` | core | Main mission file — player setup, restrictions, modifiers, intro spawning, army transition logic, Valognes spawning, enemy army distribution, outro sequence, achievements |
| `obj_stopthem.scar` | objectives | Intro phase objectives — OBJ_DefendCarentan and SOBJ_WeakenKyriell with progress bar tracking |
| `obj_clearnormandy.scar` | objectives | Primary objective — OBJ_ClearNormandy, SOBJ_findKyriell, SOBJ_KillKyriellArmy; contains MonitorBattlefield, frenzy/pivot/retreat battle logic, cannon/Breton spawning, micro AI |
| `obj_opt_save_village.scar` | objectives | Optional objective — OBJ_SaveValognes, SOBJ_killEnemyValognes; triggers when player sees Valognes, rewards buildings/resources on completion |
| `obj_captureformigny.scar` | objectives | Sub-objective — SOBJ_CaptureFormigny with Location capture system; enables capture after battle, completes OBJ_ClearNormandy |
| `training_formigny.scar` | training | Tutorial goal for selling excess resources at the French market after saving Valognes |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Formigny_InitData1()` | data | Initialize combat vars, army sizes, SGroups, state flags |
| `Formigny_InitData2()` | data | Bind MissionOMatic modules, set army groupings, pivot sources |
| `GetRecipe()` | data | Return MissionOMatic recipe with all modules and locations |
| `Mission_SetupPlayers()` | core | Configure 4 players, ages, relationships, colors |
| `Mission_Preset()` | core | Apply modifiers, upgrades, restrictions, register objectives, spawn intro |
| `Mission_Start()` | core | Start OBJ_DefendCarentan, set pop cap, begin rules |
| `SetupIntroUnitsEnemy()` | core | Spawn 10 English intro squads along two march paths |
| `SpawnUnitsAndMoveAlongPath()` | core | Deploy units at path marker and move along path |
| `StartIntroSkipped()` | core | Warp all units to final positions if intro skipped |
| `IntroMovePlayerUnits()` | core | Order player intro units to formation destinations |
| `PutEnemiesIntoModules()` | core | Assign intro SGroups into RovingArmy modules |
| `FindNewTargetForModule()` | core | Retarget roving army toward closest player squad |
| `SpawnPlayerArmy()` | core | Deploy Clermont's reinforcement army (horsemen, spearmen, MAA, xbow) |
| `Transition()` | core | Destroy intro enemies, spawn final army, Valognes units |
| `SpawnEnemyArmy()` | core | Distribute surviving enemy counts across battlefield modules |
| `SpawnRemainingUnits()` | core | Round-robin distribute unit type across module array |
| `SpawnValognesUnits()` | core | Spawn Valognes enemy attackers and allied defenders |
| `GiveEnemyAmbushVision()` | core | Reveal areas to enemy for ambush defenders |
| `SetPailingsArchers()` | core | Command archers to deploy palings (Hard+ only) |
| `FranceMoveOnFormigny()` | core | Outro: destroy enemies, spawn villagers, knight parade |
| `Achievement_OnCannonDeath()` | core | Track if any cannon lost for achievement #16 |
| `CheckAchievementCompletion()` | core | Send achievement events for cannons/hard difficulty |
| `CheckForFinalFight()` | core | Expand Formigny defender range when player approaches |
| `InitObjectives_IntroObjectives()` | obj_stopthem | Register OBJ_DefendCarentan and SOBJ_WeakenKyriell |
| `InitObjectives_ClearNormandy()` | obj_clearnormandy | Register OBJ_ClearNormandy, SOBJ_findKyriell, SOBJ_KillKyriellArmy |
| `MonitorBattlefield()` | obj_clearnormandy | Main battle loop: check cannons, bretons, frenzy, pivot, retreat |
| `SpawnCannons()` | obj_clearnormandy | Deploy 6 cannons along spline path when outposts destroyed |
| `CheckCannonArrival()` | obj_clearnormandy | Trigger intel event when cannons reach river |
| `StartFrenzy()` | obj_clearnormandy | Activate aggressive frenzy mode on front-line modules |
| `StartFrenzyForModule()` | obj_clearnormandy | Set module aggression and frenzy target |
| `EndFrenzy()` | obj_clearnormandy | Deactivate frenzy, update positions, enable Breton spawn |
| `EndFrenzyForModule()` | obj_clearnormandy | Reset module to post-frenzy spawn location |
| `SpawnBretons()` | obj_clearnormandy | Deploy 2×30 Breton knights as reinforcements |
| `Pivot()` | obj_clearnormandy | Disband all armies, redistribute into 4 pivot modules |
| `Retreat()` | obj_clearnormandy | Disband remaining enemy, split into 2 retreat armies |
| `CheckForBattle()` | obj_clearnormandy | Detect player in battle zone, micro non-frenzy modules |
| `CheckForBattleFrenzy()` | obj_clearnormandy | Detect player in frenzy zone, micro frenzy modules |
| `CheckForBattlePivot()` | obj_clearnormandy | Detect player in pivot zone, micro pivot modules |
| `MicroArmy()` | obj_clearnormandy | Target modules at closest player squad in zone |
| `SendArmyBack()` | obj_clearnormandy | Return modules to spawn locations passively |
| `SendArmyBackFrenzy()` | obj_clearnormandy | Return frenzy modules to frenzy locations |
| `SendArmyBackPivot()` | obj_clearnormandy | Return pivot modules aggressively to spawn |
| `SetModuleAggression()` | obj_clearnormandy | Configure attack-move style and combat/leash range |
| `CheckForEnemyCrossingRiver()` | obj_clearnormandy | Detect English crossing river during frenzy |
| `Monitor_BricQuebecVillage()` | obj_clearnormandy | Complete when town_1 defenders eliminated |
| `Monitor_StSauveurVillage()` | obj_clearnormandy | Complete when St-Sauveur defenders/buildings eliminated |
| `Monitor_MonasteryTown()` | obj_clearnormandy | Give monastery and monks when player approaches |
| `Monitor_ReachedFormignyArea()` | obj_clearnormandy | Complete SOBJ_findKyriell when player reaches area |
| `Monitor_PlayerFoundSecret()` | obj_clearnormandy | Create minimap blips for discoverable locations |
| `Monitor_Player1Dead()` | obj_clearnormandy | Fail mission if all player units dead |
| `DestroyWallTown02_EntityKill()` | obj_clearnormandy | Celebrate when town02 palisade walls destroyed |
| `DestroyWallFormigny_EntityKill()` | obj_clearnormandy | Celebrate when Formigny stone walls destroyed |
| `InitObjectives_SaveValognes()` | obj_opt_save_village | Register OBJ_SaveValognes and SOBJ_killEnemyValognes |
| `Monitor_ValognesApproach()` | obj_opt_save_village | Start Valognes attack when player has vision |
| `StartValogneObjective()` | obj_opt_save_village | Delayed start of OBJ_SaveValognes |
| `InitObjectives_CaptureFormigny()` | obj_captureformigny | Register SOBJ_CaptureFormigny, defeat/capture sub-objectives |
| `StartFormignyCapture()` | obj_clearnormandy | Start SOBJ_CaptureFormigny with music lock |
| `Tutorials_formigny_SellResources()` | training | Create training goal for selling resources at market |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_DefendCarentan` | Primary (Battle) | Intro: defend Carentan against Kyriell's advance |
| `SOBJ_WeakenKyriell` | Sub (Battle) | Track enemy kills during intro with progress bar/counter |
| `OBJ_ClearNormandy` | Primary | Master objective: drive English from Normandy |
| `SOBJ_findKyriell` | Sub (Primary) | March through Normandy to find Kyriell's main army |
| `SOBJ_KillKyriellArmy` | Sub (Battle) | Destroy 85% of Kyriell's field army, progress bar |
| `OBJ_SaveValognes` | Optional | Save allied Valognes village from English attack |
| `SOBJ_killEnemyValognes` | Sub (Optional) | Kill all English attackers at Valognes |
| `SOBJ_CaptureFormigny` | Sub (Capture) | Capture the Formigny location (master) |
| `SOBJ_DefeatFormignyUnits` | Sub (Capture) | Defeat Formigny garrison (secondary) |
| `SOBJ_LocationFormigny` | Sub (Capture) | Location capture progress (capture) |
| `OBJ_DebugComplete` | Debug | Cheat objective to force mission complete |

### Difficulty

All use `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Values | What It Scales |
|-----------|--------|----------------|
| `ARCHER_SIZE_FINAL` | 13/15/17/18 | Base archer squad size per module (×2 for intro) |
| `SPEARMAN_SIZE_FINAL` | 13/15/17/18 | Base spearman squad size per module (×2 for intro) |
| `MANATARMS_SIZE_FINAL` | 13/15/17/18 | Base MAA squad size per module (×2 for intro) |
| Town defend units | 2-5 or 4-9 | Garrison sizes at Bricquebec, St-Sauveur, pre-towns |
| Town patrol horsemen | 4/5/7/9 | Roving patrol squad sizes |
| Pre-town defenders | 4/5/7/9 | Ambush defender squad sizes |
| Forward MAA defenders | 4/5/7/9 | Forward man-at-arms near Formigny |
| Formigny garrison | 2-5 or 4-9 | Knights, archers, spearmen defending Formigny |
| Valognes enemy archers/cavalry | 7/10/14/18 | Attacker count at Valognes |
| Valognes gold reward | 2400/1600/800/0 | Gold given on saving Valognes |
| Archer palings | Hard+ only | `deploy_palings` ability enabled on Hard/Hardest |

### Spawns

- **Intro (Carentan)**: 10 squads of English march along 2 paths — 6 archer groups (×ARCHER_SIZE_INTRO), 2 spearman groups, 2 MAA groups. Total: `ARMY_COUNT_MAX` units. Player starts with 60 units (20 MAA + 20 archers + 20 MAA).
- **Clermont Reinforcements**: Spawned after intro — 35 horsemen, 45 spearmen, 45 MAA, 45 crossbowmen (170 total).
- **Final Battle Army**: Surviving enemy from intro redistributed across 12 archer modules (front 6 + back 6), 4 spearman modules, 4 MAA modules. Uses round-robin distribution via `SpawnRemainingUnits()`.
- **Cannons**: 6 French cannons spawned along spline path when forward outposts + MAA trigger destroyed. Custom blueprint `UNIT_CANNON_4_FORM_FRE`.
- **Breton Knights**: 2 groups of 30 knights each when player count drops below 140 (minus monks) and frenzy has ended. Move to arrival markers, trigger pivot on arrival.
- **Valognes**: Enemy cavalry + archers attack; allied spearmen defend. Counts scale with difficulty.
- **Town Garrisons**: Bricquebec (3 defend + 1 patrol), St-Sauveur (2 defend + 1 roving), pre-town ambushes at multiple points.
- **Formigny Garrison**: 2 wall archers, 1 knight defend, 2 spearman defend, 2 retreat army modules.
- **Outro**: Villagers + monks spawn for celebration, 16 knights parade through Formigny at 0.5× speed.

### AI

- **RovingArmy Modules**: 10 intro armies use `attackMoveStyle_ignoreEverything` with `FindNewTargetForModule` callback to chase player. 20 battlefield modules (12 archers, 4 spearmen, 4 MAA) use `shouldHoldWhileWaiting=true` with tight combat/leash ranges (5).
- **Frenzy Phase**: Front-line modules (archers 1-6, spearmen 1-4) set to aggressive with `attackMoveStyle_attackEverything` targeting frenzy markers. Triggered at 5% army casualties.
- **Pivot Phase**: After Bretons arrive, all armies disband, units redistributed into 4 pivot modules with combat range 40/leash 60. Triggered by Breton proximity to arrival marker.
- **Retreat Phase**: At 85% casualties, remaining units split into 2 retreat army modules and leave.
- **Micro System**: `MonitorBattlefield()` runs every 1s. `CheckForBattle/Frenzy/Pivot()` detect player squads in battle zones, call `MicroArmy()` to target closest player squad, `SendArmyBack()` when player leaves zone. Uses separate zone markers for active vs leash states.
- **Town Defenders**: `Defend` type modules with `useCustomDirection=true`. Town patrols cycle between waypoints via `ARMY_TARGETING_CYCLE`.
- **Valognes Attackers**: `RovingArmy` with `attackMoveStyle_ignorePassive`, activated when player has vision.
- **Modifiers Applied**: Cannon range ×1.1, ribauldequin range ×1.5, monk speed ×1.285, English MAA speed ×0.885, English spearman speed ×0.8.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Rule_AddOneShot(SpawnPlayerArmy, 3)` | 3s | Spawn Clermont army after intro |
| `Rule_AddOneShot(Transition, 4)` | 4s | Destroy intro enemies, spawn final battle army |
| `Rule_AddOneShot(IntroMovePlayerUnits, 16)` | 16s | Move player intro units to destinations |
| `Rule_AddOneShot(PutEnemiesIntoModules, 0.1)` | 0.1s | Assign intro squads into roving modules |
| `Rule_AddOneShot(BretonsCanBeSpawned, 20)` | 20s after frenzy ends | Enable Breton spawn eligibility |
| `Rule_AddOneShot(ChangeMusic_KillKyriellArmy, 60)` | 60s | Unlock music intensity after battle start |
| `Rule_AddOneShot(SetPailingsArchers, 10)` | 10s | Deploy palings on Hard+ |
| `Rule_AddOneShot(StartValogneObjective, 3)` | 3s | Delayed Valognes objective start |
| `Rule_AddOneShot(Tutorials_formigny_SellResources, 120)` | 120s after Valognes | Show sell resources training goal |
| `Rule_AddInterval(MonitorBattlefield, 1)` | Every 1s | Main battle state machine |
| `Rule_AddInterval(Monitor_BricQuebecVillage, 1)` | Every 1s | Check Bricquebec cleared |
| `Rule_AddInterval(Monitor_StSauveurVillage, 1)` | Every 1s | Check St-Sauveur cleared |
| `Rule_AddInterval(Monitor_PlayerFoundSecret, 1)` | Every 1s | Reveal discoverable locations |
| `Rule_AddInterval(Monitor_MonasteryTown, 1)` | Every 1s | Give monastery on approach |
| `Rule_AddInterval(Monitor_ReachedFormignyArea, 1)` | Every 1s | Complete findKyriell on arrival |
| `Rule_AddInterval(Monitor_ValognesApproach, 1)` | Every 1s | Start Valognes attack on vision |
| `Rule_AddInterval(Monitor_Player1Dead, 1)` | Every 1s | Fail if all player units dead |
| `Rule_AddInterval(CheckCannonArrival, 1)` | Every 1s | Trigger intel when cannons reach river |
| `Rule_AddInterval(CheckForEnemyCrossingRiver, 1)` | Every 1s | Detect enemy crossing during frenzy |
| `Rule_AddInterval(CheckForFinalFight, 1)` | Every 1s | Expand Formigny defender range |
| `Music_LockIntensity(MUSIC_TENSE_COMBAT, 60)` | 60s lock | Lock combat music at battle start |
| `Music_LockIntensity(MUSIC_TENSE_COMBAT, 120)` | 120s lock | Lock combat music for Formigny capture |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core mission framework (RovingArmy, Defend, UnitSpawner, Location systems)
- `training/campaigntraininggoals.scar` — Training goal framework
- `training/coretrainingconditions.scar` — Core training predicates
- `hun_chp4_formigny_data.scar` — Mission data (imported by core)
- `obj_opt_save_village.scar` — Optional Valognes objective
- `obj_clearnormandy.scar` — Primary Clear Normandy objective
- `obj_stopthem.scar` — Intro Defend Carentan objective
- `obj_captureformigny.scar` — Formigny capture sub-objective
- `training_formigny.scar` — Sell resources tutorial

### Shared Globals
- `player1`–`player4` — Player handles (France, England, France ally, Breton)
- `sg_allsquads`, `eg_allentities` — Reused by `Player_GetAll()` calls
- `sg_temp` — Temporary SGroup reused across functions
- `sg_main_army` — All battlefield enemy units; used for kill tracking
- `sg_enemy_intro` — All intro enemy units; count determines final army size
- `army_count_final`, `army_killed_final` — Battle progress tracking
- `LocationFormigny` — LOCATION object with capture objectives bound
- `EVENTS.*` — Intel event constants (HUN_ECAM1450FORMIGNY_Intro, CLEAR_NORMANDY_START, OUTNUMBERED, CANT_STOP_THEM, ATTACK_KYRIELL_ARMY_START, CANNONS_ARRIVE, CANNONS_NEAR_RIVER, BRETONS_ARRIVE, ENGLISH_FRENZY, ENGLISH_PIVOT, ENGLISH_RETREAT, ENGLISH_RETREAT_NO_BRETONS, HALFWAY, BricquebecDestroyed, StSauveurDestroyed, SAVE_VILLAGE_START, SAVE_VILLAGE_COMPLETE, FORMIGNY_CAPTURE)

### Inter-File Function Calls
- `hun_chp4_formigny.scar` calls `Formigny_InitData1/2()` from data, all `InitObjectives_*()` from objective files
- `obj_stopthem.scar` → `Objective_Start(OBJ_ClearNormandy)` on intro complete
- `obj_clearnormandy.scar` → `Objective_Start(SOBJ_KillKyriellArmy)`, `Objective_Start(SOBJ_CaptureFormigny)` via `StartFormignyCapture()`
- `obj_clearnormandy.scar` → `CheckAchievementCompletion()`, `Mission_Complete()` on final completion
- `obj_opt_save_village.scar` → `Tutorials_formigny_SellResources()` from training file (via OneShot)
- `obj_captureformigny.scar` → `Objective_Complete(OBJ_ClearNormandy)` when Formigny captured
- `VillagerLife_Find("villagerlife_alliedTown")` — External villager life system for Valognes fail condition

### Key Blueprints
- `SBP.FRENCH.UNIT_CANNON_4_FORM_FRE` — Mission-specific French cannon
- `BP_GetWeaponBlueprint("weapon_cannon_4_form_fre")` — Cannon weapon (range ×1.1)
- `BP_GetWeaponBlueprint("weapon_ribauldequin_4_form_fre")` — Ribauldequin weapon (range ×1.5)
- `BP_GetAbilityBlueprint("deploy_palings")` — English archer palings ability
- `EBP.ENGLISH.BUILDING_DEFENSE_OUTPOST_ENG` — Outposts upgraded with Arrow Slits

### Achievement Tracking
- **Achievement #16 (Careful Cannons)**: `CE_ACHIEVALLCANNONSSURVIVEFORMIGNY` — Win without losing any cannon
- **Formigny Hard Victory**: `CE_FORMIGNYVICTORYHARD` — Win on Hard or Hardest difficulty
