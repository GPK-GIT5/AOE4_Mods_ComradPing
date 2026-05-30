# Angevin Chapter 2: Bayeux

## OVERVIEW

Bayeux (1106) is the third mission of the Norman/Angevin campaign. The player commands King Henry's English forces (player1) against Robert's French rebel forces (player2) in a multi-phase siege mission. The flow begins with an opening cavalry ambush that the player must survive, followed by capturing a wood mill village to establish an economic base. The player then builds siege infrastructure (Blacksmith → Siege Engineers upgrade → Battering Rams) before breaching Bayeux's stone walls and burning the town. The mission features extensive tutorial sequences covering palings, attack move, height advantage, blacksmith construction, siege engineering, ram building, and control groups, with Xbox-specific input branching for several tutorials.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| ang_chp2_bayeux.scar | core | Main mission setup: players, variables, difficulty tuning, recipe with modules/spawns, cavalry/archer/infantry defenders, passive combat rules, idle attack system |
| obj_destroy.scar | objectives | Primary "Burn Bayeux" objective chain: OBJ_Destroy, OBJ_Rams (Blacksmith → Siege Engineer → Build Rams), SOBJ_Breach, SOBJ_BurnBuildings, SOBJ_Defenders |
| obj_capturewood.scar | objectives | Wood mill capture objective: location capture, defender defeat check, villager/economy spawning on completion, resource grants |
| obj_controlgroups.scar | objectives | Optional control group tutorial objective: checks if player has created archer-only and spearman-only control groups |
| training_bayeux.scar | training | Tutorial goal sequences for palings deployment, attack move, height advantage, blacksmith building, siege engineer research, ram construction; Xbox/KBM input branching |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_SetupPlayers | ang_chp2_bayeux | Configure 3 players, colours, ages, relationships, disable AI p3 |
| Mission_SetupVariables | ang_chp2_bayeux | Create SGroups/EGroups, init leader, define patrol positions |
| Mission_SetDifficulty | ang_chp2_bayeux | Define difficulty table for unit counts and idle timers |
| Mission_SetRestrictions | ang_chp2_bayeux | Remove walls/towers/trade from player build options |
| Mission_Preset | ang_chp2_bayeux | Init objectives, upgrade outposts/towers, spawn archer/infantry defenders |
| Mission_Start | ang_chp2_bayeux | Register wall damage events, start palings tutorial, kill rules |
| GetRecipe | ang_chp2_bayeux | Define recipe: locations, Defend/RovingArmy modules, title card |
| HintPoint_Cavalry | ang_chp2_bayeux | Create hint points and minimap blips for cavalry threats |
| Reinforce_Archers | ang_chp2_bayeux | Spawn player reinforcements, start height/idle attack rules |
| Cavalry_Cleared | ang_chp2_bayeux | On cavalry defeat: start OBJ_Destroy, init cavalry defenders |
| Init_Cavalry_Attackwave | ang_chp2_bayeux | Create initial RovingArmy cavalry attack wave module |
| Init_Cavalry_Defenders | ang_chp2_bayeux | Spawn difficulty-scaled cavalry patrol groups across map |
| Init_Archer_Defenders | ang_chp2_bayeux | Place archer Defend modules on wall positions with hold |
| Init_Infantry_Defenders | ang_chp2_bayeux | Create RovingArmy infantry defenders at 3 Bayeux positions |
| Init_Infantry_Extra_Defenders | ang_chp2_bayeux | Spawn additional infantry defenders from hidden spawn points |
| ClearArchers | ang_chp2_bayeux | Destroy unseen archer defenders to reduce unit count |
| Advance_OnEntityKilled | ang_chp2_bayeux | Wall killed: reveal town, transition to burn phase |
| Advance_OnEntityDamage | ang_chp2_bayeux | Wall damaged with infantry on walls: transition to burn phase |
| Dissolve_WithdrawnCavalry | ang_chp2_bayeux | Merge withdrawn cavalry modules into wall defense group |
| BayeuxBurning | ang_chp2_bayeux | Track town health, complete burn at 75% damage |
| PushWhenNeeded | ang_chp2_bayeux | Reactively push defenders toward player as town burns |
| DissolveInArchers | ang_chp2_bayeux | Merge remaining archer defenders into wall defense module |
| IdleAttack | ang_chp2_bayeux | Send nearest cavalry to attack idle player after timer |
| NewAtackerGroup | ang_chp2_bayeux | Spawn new spearman poke wave targeting idle player |
| PushAttack | ang_chp2_bayeux | Direct closest infantry module to attack player in town |
| PlayerRush | ang_chp2_bayeux | All modules target player when army below 5 squads |
| VillagerFlee | ang_chp2_bayeux | Periodically spawn fleeing villagers from burning town |
| PlayerDeath_PreTown | ang_chp2_bayeux | Fail mission if all non-Henry units die (pre-capture) |
| PlayerDeath_PostTown | ang_chp2_bayeux | Fail mission if player base buildings destroyed (post-capture) |
| CleanUp_Cavalry | ang_chp2_bayeux | Destroy unseen cavalry or merge visible into wall defense |
| Destroy_InitObjectives | obj_destroy | Register all primary/sub objectives for destroy chain |
| Destroy_OnStart | obj_destroy | Add Bayeux icon, reinforce archers, start wall spotting |
| Destroy_IsComplete | obj_destroy | Complete when both BurnBuildings and Defenders done |
| Destroy_OnComplete | obj_destroy | Trigger Mission_Complete |
| Rams_OnStart | obj_destroy | Play battering rams intel event part 2 |
| Blacksmith_IsComplete | obj_destroy | Check if completed blacksmith exists |
| Blacksmith_OnComplete | obj_destroy | Play intel, start siege engineer sub-objective |
| SiegeEngineer_OnStart | obj_destroy | Launch siege engineer tutorial (Xbox or PC) |
| SiegeEngineer_IsComplete | obj_destroy | Check Player_HasUpgrade for siege engineers |
| SiegeEngineer_OnComplete | obj_destroy | Play intel, start build siege sub-objective |
| BuildSiege_IsComplete | obj_destroy | Count completed rams, complete at 3, remove tower modifiers |
| Rams_OnComplete | obj_destroy | AutoSave, play intel, start breach objective |
| Breach_SetupUI | obj_destroy | Add wall hint UI element for breach objective |
| Bayeux_Walls_Spotted | obj_destroy | Trigger stone wall intel when player sees walls |
| Bayeux_Gate_Spotted | obj_destroy | Trigger gate intel when player sees gates |
| Defenders_Track | obj_destroy | Track and display defender defeat progress bar |
| CaptureVillage_InitObjectives | obj_capturewood | Register capture village and hamlet defender objectives |
| CaptureVillage_PreStart | obj_capturewood | Enable location capture, remove Bayeux icon |
| CaptureVillage_IsComplete | obj_capturewood | Complete when all wood defenders eliminated |
| CaptureVillage_OnComplete | obj_capturewood | Spawn villagers/economy, grant resources, start rams objective |
| CaptureVillage_IsFailed | obj_capturewood | Fail if player has zero squads |
| ControlGroup_InitObjectives | obj_controlgroups | Register optional control group objectives |
| ControlGroup_Check | obj_controlgroups | Start objective if no control groups assigned |
| CGArchers_IsComplete | obj_controlgroups | Check for archer-only control group |
| CGSpears_IsComplete | obj_controlgroups | Check for spearman-only control group |
| MissionTutorial_Palings | training_bayeux | Setup palings deploy tutorial goal sequence |
| Palings_TriggerPredicate | training_bayeux | Trigger when 5+ units near marker with undeployed palings |
| MissionTutorial_AttackMove | training_bayeux | Setup attack move tutorial goal sequence |
| AttackMove_TriggerPredicate | training_bayeux | Trigger when archers and enemies both on screen |
| MissionTutorial_HeightAdvantage | training_bayeux | Setup elevation advantage tutorial goal sequence |
| MissionTutorial_Blacksmith | training_bayeux | Setup blacksmith construction tutorial with Xbox branching |
| MissionTutorial_SiegeEngineer | training_bayeux | Setup siege engineer upgrade tutorial (PC version) |
| MissionTutorial_SiegeEngineer_Xbox | training_bayeux | Setup siege engineer tutorial with radial menu steps |
| MissionTutorial_Ram | training_bayeux | Setup ram construction tutorial with Xbox branching |
| Ram_TutorialBranch | training_bayeux | Chain blacksmith → siege engineer → ram tutorials |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_Destroy | Primary | Burn Bayeux — parent objective for the siege phase |
| OBJ_Rams | Primary | Build Rams — parent for blacksmith/siege/build chain |
| SOBJ_Blacksmith | Sub (OBJ_Rams) | Build a Blacksmith building |
| SOBJ_SiegeEngineer | Sub (OBJ_Rams) | Purchase the Siege Engineers upgrade |
| SOBJ_BuildSiege | Sub (OBJ_Rams) | Use infantry to construct 3 rams (counter: X/3) |
| SOBJ_Breach | Sub (OBJ_Destroy) | Breach the walls of Bayeux |
| SOBJ_BurnBuildings | Sub (OBJ_Destroy) | Destroy Bayeux buildings (progress bar, completes at 75% damage) |
| SOBJ_Defenders | Sub (OBJ_Destroy) | Defeat the city defenders (progress bar) |
| OBJ_CaptureVillage | Primary | Capture the Wood Mill — prerequisite to siege phase |
| SOBJ_DefeatHamletRebels | Sub (OBJ_CaptureVillage) | Defeat defenders at the Wood Mill |
| SOBJ_LocationHamlet | Sub (OBJ_CaptureVillage) | Wood Mill location capture marker |
| OBJ_ControlGroups | Optional | Create control groups using CTRL+0-9 |
| SOBJ_CGArchers | Sub (OBJ_ControlGroups) | Group only archers into a control group |
| SOBJ_CGSpears | Sub (OBJ_ControlGroups) | Group only spearmen into a control group |
| OBJ_DebugComplete | Debug | Cheat objective to skip to mission complete |
| OBJ_VideoCapture | Debug | Video capture mode with full base/army spawn |

### Difficulty

All values indexed as `{Story, Easy, Medium, Hard}`:

| Parameter | Values | What It Scales |
|-----------|--------|----------------|
| archerAmounts | {3, 3, 5, 8} | Archer count per wall Defend module |
| playerSpearmen | {40, 30, 30, 30} | Spearmen in player reinforcement wave |
| playerArchers | {70, 70, 70, 70} | Target archer count for player reinforcements |
| enemyCavalry | {10, 12, 14, 10} | Horsemen per cavalry patrol group |
| enemyKnights | {0, 0, 1, 5} | Knights per cavalry patrol group |
| gateDefenders.spearmanCount | {5, 6, 8, 12} | Spearmen at each gate infantry position |
| gateDefenders.archerCount | {5, 6, 10, 14} | Archers at each gate infantry position |
| idleattacktimer | {0, 6, 4, 1} | Minutes of idle time before cavalry attack (0 = disabled for Story) |
| rovingArmy_DefendPositions | varies | Number of cavalry patrol routes: Story/Easy=5, Medium=7, Hard=9 |

### Spawns

- **Initial cavalry wave**: 1 knight + 15 horsemen as RovingArmy targeting `mkr_cavalry_target`, spawned from `mkr_field_cavalry_spawn`
- **Player reinforcements** (`Reinforce_Archers`): 3 scouts + difficulty-scaled spearmen + archers to fill up to 70, deployed at `mkr_player_reinforce`
- **Cavalry patrol defenders**: Difficulty-scaled number of patrol groups (5–9), each with `enemyCavalry` horsemen + `enemyKnights` knights, roving between pairs of patrol markers with 45% withdraw threshold falling back to `mkr_bayeux_cavalry_withdraw`
- **Wall archer defenders**: One Defend module per `mkr_wall_archers` marker, `archerAmounts` archers each, hold position with spread formation
- **Gate infantry defenders**: 3 RovingArmy modules at `mkr_bayeux_infantry_1/2/3`, each with `gateDefenders.spearmanCount` spearmen + `gateDefenders.archerCount` archers
- **Extra infantry defenders**: Spawned on wall breach from hidden spawn positions, half gate defender counts per module
- **Wood mill defenders**: Static Defend module with 10 spearmen + 10 archers + 5 horsemen
- **Bayeux wall defenders**: RovingArmy module with 15 spearmen + 10 archers using `attackMoveStyle_ignoreEverything`
- **Idle poke waves**: 20 spearmen spawned from `mkr_bayeux_archer_spawn` when player is idle beyond difficulty timer
- **Fleeing villagers**: 1–3 villagers spawned periodically (20–45s) from random buildings, 1.3x speed boost, move-and-destroy to flee markers
- **Village capture economy**: On wood mill capture, villagers deployed for roaming, food, wood, stone, gold tasks; resources granted (Story: 1000g/2000w/1000f/500s; other: 500g/1000w/500f/0s)

### AI

- `AI_Enable(player3, false)` — Downed Leader (neutral holder) has AI disabled
- `PlayerUpgrades_Auto(player2, true)` — Robert's forces auto-upgrade
- **Cavalry patrols**: RovingArmy modules with `ARMY_TARGETING_REVERSE`, patrol between marker pairs, `combatRange=40`, `leashRange=500`, `withdrawThreshold=0.45`, fallback to `mkr_bayeux_cavalry_withdraw`
- **Wall defenders**: `attackMoveStyle_ignoreEverything` to prioritize holding position
- **Idle attack system**: `IdleAttack` checks every 15s if player hasn't been attacked within `idleattacktimer` minutes; sends nearest cavalry patrol or spawns new spearman wave; disabled for Story mode
- **Push attack**: `PushAttack` directs closest infantry module toward player squads inside Bayeux, triggered reactively as town health drops
- **Player rush detection**: `PlayerRush` (15s interval) — if player army < 5 squads, all modules retarget to player army
- **Dissolution system**: Withdrawn cavalry modules merge into `defend_bayeux_walls` via `DissolveModuleIntoModule`; archer defenders also dissolve into main defense as town burns
- **Tower modifications**: Enemy towers get arrow slit upgrades; weapon damage set to 1x, range to 0.6x, received damage to 1x (modifiers removed when rams are built)
- **Outpost upgrades**: All enemy outposts get `UPGRADE_OUTPOST_ARROWSLITS` at mission start

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| `BayeuxBurning` | 1s | Track town health percentage for burn progress bar |
| `PlayerDeath_PreTown` | 1s | Check if all non-Henry player units are dead |
| `PlayerDeath_PostTown` | 1s | Check if player base buildings are destroyed |
| `TowerDeathAudio` | 1s | Play celebration audio when bridge towers are destroyed |
| `PlayerRush` | 15s | All-in attack if player army critically low |
| `IdleAttack` | 15s | Poke player with cavalry if idle beyond difficulty timer |
| `CavalryAudioTrigger_2` | 0.5s | Audio trigger for cavalry attack wave |
| `Bayeux_Walls_Spotted` | 1s | Check if player can see Bayeux walls |
| `Bayeux_Gate_Spotted` | 1s | Check if player can see Bayeux gates |
| `VillagerFlee` | OneShot 20s, then 20–45s | Spawn fleeing villagers from burning Bayeux |
| `PushWhenNeeded` | OneShot 30s, then 3s repeating | Push defenders toward player inside town |
| `MissionTutorial_AttackMove` | OneShot 15s | Start attack move tutorial after OBJ_Destroy begins |
| `MissionTutorial_Blacksmith` | OneShot 30s | Start blacksmith tutorial after village captured |
| `Music_CombatMusicOnly` | OneShot 1s | Switch to combat-only music after cavalry cleared |

## CROSS-REFERENCES

### Imports

| Import | Source |
|--------|--------|
| `MissionOMatic/MissionOMatic.scar` | Core mission framework (Cardinal, modules, recipes) |
| `obj_destroy.scar` | Burn Bayeux objective chain |
| `obj_capturewood.scar` | Wood mill capture objective |
| `obj_controlgroups.scar` | Optional control group objective |
| `training_bayeux.scar` | Tutorial goal sequences |
| `training/campaigntraininggoals.scar` | Shared campaign training framework (imported by training_bayeux) |

### Shared Globals

- `g_leaderHenry` — Leader struct initialized via `Missionomatic_InitializeLeader`, used for hero unit management
- `sg_player_army` — Central player army SGroup referenced across all files
- `sg_bayeux_defenders` — Shared defender SGroup populated by multiple modules
- `t_AllCavalryModules` — Table tracking all cavalry RovingArmy modules for idle attacks and cleanup
- `t_AllArcherDefenders` — Table tracking wall archer Defend modules for dissolution
- `t_bayeux_extra_infantry` — Table tracking infantry defender modules for push attacks
- `t_difficulty` — Difficulty parameters table accessed across objective and core files
- `b_debugStart` — Debug flag checked in both obj_destroy and obj_capturewood
- `eg_bayeux_town` / `eg_bayeux_walls` / `eg_bayeux_gates` — Town entity groups used by objectives and passive rules
- `bayeuxHealthTotal` — Baseline health for burn progress calculations
- `mod_towerDMG` / `mod_towerARM` / `mod_gateARM` — Tower/gate modifiers removed when rams are built
- `villagerlife_woodtown` — Town life data (villager counts, markers) used in capture completion

### Inter-File Function Calls

- `ang_chp2_bayeux.scar` calls `Destroy_InitObjectives()`, `CaptureVillage_InitObjectives()`, `ControlGroup_InitObjectives()` from objective files
- `ang_chp2_bayeux.scar` calls `MissionTutorial_Palings()` from training_bayeux at mission start
- `ang_chp2_bayeux.scar` calls `MissionTutorial_HeightAdvantage()`, `MissionTutorial_AttackMove()` from training_bayeux during reinforcement
- `obj_destroy.scar` calls `MissionTutorial_Blacksmith()`, `MissionTutorial_SiegeEngineer()`, `MissionTutorial_SiegeEngineer_Xbox()`, `MissionTutorial_Ram()` from training_bayeux
- `obj_destroy.scar` calls `Reinforce_Archers()`, `Init_Cavalry_Defenders()`, `BayeuxBurning()`, `Defenders_Track()` from core
- `obj_capturewood.scar` calls `ControlGroup_Check()` from obj_controlgroups
- `obj_capturewood.scar` calls `MissionTutorial_Blacksmith()` from training_bayeux
- `training_bayeux.scar` calls `Ram_TutorialBranch()` which chains `MissionTutorial_Blacksmith()` → `MissionTutorial_SiegeEngineer()` → `MissionTutorial_Ram()`
- Module system uses `MissionOMatic_FindModule()`, `RovingArmy_Init()`, `RovingArmy_SetTarget()`, `Defend_Init()`, `DissolveModuleIntoModule()` from MissionOMatic framework

### Audio/Event References

- Campaign: `ang`, Mission: `rts1106bayeux`
- Music race code: `french`
- Intel events: `EVENTS.Intro`, `EVENTS.Victory`, `EVENTS.Cavalry_Down`, `EVENTS.Stone_Wall`, `EVENTS.Gate_Visibility`, `EVENTS.Robert_Attack`, `EVENTS.Robert_Attack_Completed`, `EVENTS.BatteringRams_Start_Part1`, `EVENTS.BatteringRams_Start_Part2`, `EVENTS.BlacksmithDone`, `EVENTS.SiegeyDone`, `EVENTS.BatteringRams_Complete`, `EVENTS.Inside_Bayeux`, `EVENTS.Defeat_Defenders_Complete`
- Title card: ID 11160632 (Bayeux), date ID 11160633 (1105), icon `icons/campaign/campaign_angevin_possession`
