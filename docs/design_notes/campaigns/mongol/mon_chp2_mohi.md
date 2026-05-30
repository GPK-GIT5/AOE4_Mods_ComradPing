# Mongol Chapter 2: Mohi

## OVERVIEW

The Battle of Mohi (1241) is a multi-phase Mongol campaign mission (Mission 6) where the player controls General Subutai's forces alongside ally Batu Khan against the Hungarian Army under King Bela. The mission flows through six phases: scout across a bridge into enemy territory, escape a Hungarian cavalry ambush, build up a base and army during a timed preparation period, assault across the bridge with Batu, push through two Hungarian defense lines (left and right flanks), and finally assault the fortified Hungarian camp to force a rout. The MissionOMatic recipe system drives extensive RovingArmy, Defend, and UnitSpawner modules. Difficulty scaling affects unit compositions, Batu's preparation timer, outpost upgrades, and an optional mangonels objective. An achievement tracks whether Subutai's kills exceed double Batu's kills, and a timed challenge rewards completing on Hard+ in under 15 minutes.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp2_mohi.scar | core | Main mission setup: 5 players, variables, restrictions, recipe with all MissionOMatic modules, intro/outro, bridge/ford discovery, economy fail-check, achievement tracking |
| obj_hungarianarmy.scar | objectives | Primary objective OBJ_DestroyArmy plus sub-objectives SOBJ_DriveArmyBack and SOBJ_AssaultTheCamp — defense line rout tracking, camp spawning, Batu laning logic |
| obj_scoutbridge.scar | objectives | Sub-objectives for early/mid mission: SOBJ_ScoutBridge, SOBJ_EscapeAmbush, SOBJ_SupportBatu, SOBJ_OptRepairBridge, SOBJ_OptMangonels, SOBJ_BatuTimer, SOBJ_AttackBridge |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | mon_chp2_mohi | Configure 5 players, relationships, LOS, colours |
| Mission_SetupVariables | mon_chp2_mohi | Init objectives, groups, difficulty vars, unit templates, leader |
| Mission_SetRestrictions | mon_chp2_mohi | Auto-upgrades for all players, learn Castle units |
| Mission_Preset | mon_chp2_mohi | Add resources, spawn intro units, destroy bridge, track achievement |
| Mission_Start | mon_chp2_mohi | Find MissionOMatic modules, start OBJ_DestroyArmy, setup outposts |
| GetRecipe | mon_chp2_mohi | Define recipe: locations, RovingArmy/Defend/UnitSpawner modules, titlecard |
| Mohi_AddPlayerResources | mon_chp2_mohi | Grant 2000 of each resource to player |
| Mohi_FordNotify | mon_chp2_mohi | VO stinger when player discovers shallow ford |
| Mohi_BridgeNotify | mon_chp2_mohi | VO stinger when player discovers broken bridge |
| Mohi_BridgeRepaired | mon_chp2_mohi | Detect bridge repair, update UI, add left flank hint |
| Mohi_ApplyKhanBuffs | mon_chp2_mohi | Buff Subutai ability recharge and sight radius |
| Mohi_IsPlayerEconomyLocked | mon_chp2_mohi | Check if player has no units/buildings/food to fail mission |
| Mohi_RefreshBatuMods | mon_chp2_mohi | Apply 2x received damage to Batu on Easy/Normal |
| Mohi_HealAmbushers | mon_chp2_mohi | Heal ambush defenders when no allied units nearby |
| Mohi_SpawnIntroUnits | mon_chp2_mohi | Deploy starting cavalry and horse archers for player |
| Mohi_SkippedIntroSpawning | mon_chp2_mohi | Respawn units at start position if intro skipped |
| Mohi_OutroUnitMovement | mon_chp2_mohi | Spawn routing Hungarians and Mongol celebration units |
| Mohi_OutroBurnStart | mon_chp2_mohi | Stagger tent burning across camp for outro cinematic |
| Mohi_OutroBurnMiddle | mon_chp2_mohi | Continue staggered tent burning after 2s delay |
| Mohi_OutroBurnEnd | mon_chp2_mohi | Final tent burning wave after 4s delay |
| Mohi_OutroDeadBodies | mon_chp2_mohi | Spawn corpse fields at outro marker positions |
| Achievement_TrackArmyKills | mon_chp2_mohi | GE_SquadKilled handler tracking Subutai vs Batu kills |
| Check_Completion_Time | mon_chp2_mohi | Check Hard+ completion under 15min for challenge event |
| HungarianArmy_InitObjectives | obj_hungarianarmy | Register OBJ_DestroyArmy, SOBJ_DriveArmyBack, SOBJ_AssaultTheCamp |
| HungarianArmy_CheckRout | obj_hungarianarmy | Monitor defense line, dissolve into fallback on threshold |
| HungarianArmy_DelayedComplete | obj_hungarianarmy | Complete SOBJ_DriveArmyBack after 2s delay |
| HungarianArmy_SpawnCamp | obj_hungarianarmy | Populate 13 camp Defend modules with scaled units |
| HungarianArmy_CheckWherePlayerAttacking | obj_hungarianarmy | Detect player lane choice, route Batu to opposite lane |
| HungarianArmy_MonitorSquadToStopReinforcements | obj_hungarianarmy | Disable reinforcements when player attacks defense line |
| HungarianArmy_WaitForPlayerToAssaultCamp | obj_hungarianarmy | Send Batu to camp when player engages camp units |
| HungarianArmy_MonitorTentsToStopReinforcements | obj_hungarianarmy | Disable tent spawner when tent EGroup destroyed |
| HungarianArmy_BotherPlayerIfTheyAreIdleAgain | obj_hungarianarmy | Send harassment wave if player idle for 2 minutes |
| HungarianArmy_ReinforceExistingModules | obj_hungarianarmy | Spawn MAA/crossbow reinforcements to defense lines on timer |
| ScoutBridge_InitObjectives | obj_scoutbridge | Register 7 sub-objectives for scout/ambush/buildup/attack phases |
| ScoutBridge_CanPlayerSeeAmbushUnits | obj_scoutbridge | Check if player sees any ambush groups, trigger ambush |
| ScoutBridge_SpawnStructures | obj_scoutbridge | Deploy Mongol mobile buildings (TC, barracks, stable, etc.) |
| ScoutBridge_BatuWarning | obj_scoutbridge | Halfway timer VO reminding player Batu is waiting |
| ScoutBridge_AmbushWalla | obj_scoutbridge | Play charge walla on all 3 forward guard groups |
| ScoutBridge_BotherPlayerIfIdle | obj_scoutbridge | Spawn harassment spearmen if player idle during bridge assault |
| ScoutBridge_StopReinforcingAmbushers | obj_scoutbridge | Disable ambush reinforcements on first player kill |
| ScoutBridge_SpawnFlankAmbushers | obj_scoutbridge | Spawn flanker RovingArmy if player enters flank zone |
| ScoutBridge_DelayedPursuerTargetUpdate | obj_scoutbridge | Retarget cavalry pursuers to attack zone after 10s |
| ScoutBridge_HasPlayerSeenCavalryRecently | obj_scoutbridge | Track 15s visibility timeout for cavalry groups |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_DestroyArmy | Primary | Top-level: destroy the Hungarian army; fail if economy locked |
| SOBJ_ScoutBridge | Primary | Scout across the bridge; triggers ambush on enemy visibility |
| SOBJ_EscapeAmbush | Primary | Escape cavalry ambush; completes when pursuers killed or unseen 15s |
| SOBJ_SupportBatu | Primary | Build army at flanks; completes when player attacks forward guards |
| SOBJ_OptRepairBridge | Optional | Repair the destroyed western bridge for alternate route |
| SOBJ_OptMangonels | Optional | Build 2 mangonels (Normal and below only) |
| SOBJ_BatuTimer | Primary | Countdown timer until Batu attacks regardless of readiness |
| SOBJ_AttackBridge | Battle | Assault ambush positions with Batu; progress bar tracks kills |
| SOBJ_DriveArmyBack | Battle | Push through 2 defense lines (L/R); progress bar, rout on threshold |
| SOBJ_AssaultTheCamp | Battle | Destroy Hungarian camp defenders; progress bar, rout at ~20 remaining |
| OBJ_DebugComplete | Primary | Debug cheat: instant mission complete |

### Difficulty

| Parameter | Easy | Normal | Hard | Expert | What it scales |
|-----------|------|--------|------|--------|----------------|
| batu_timer | 900s | 840s | 780s | 720s | Preparation time before Batu attacks |
| Batu army size (knights) | 26 | 26 | 26 | 16 | Batu's starting army strength |
| Batu army size (horse archers) | 26 | 26 | 26 | 16 | Batu's starting army strength |
| Batu received damage | 2x | 2x | 1x | 1x | Nerf Batu on Easy/Normal so he doesn't solo |
| Ambush pursuers (horseman) | 6 | 6 | 6 | 4 | Cavalry chase group size |
| Ambush pursuers (knight) | 0 | 0 | 0 | 4 | Expert-only extra cavalry |
| Ambush forward guards (E/N) | 20 spear + 10 archer | same | — | — | Easy/Normal ambush composition |
| Ambush forward guards (H/E) | — | — | 10-16 MAA + 20-26 xbow | same | Hard/Expert ambush composition |
| Ambush springalds | 0 | 0 | 0 | 1 | Expert-only siege at each ambush point |
| Defense line spearman | 6 | 6 | 8 | 4 | Defense line infantry count |
| Defense line MAA | 0 | 0 | 2 | 6 | Hard/Expert only melee upgrade |
| Defense line landsknecht | 0 | 0 | 2 | 6 | Hard/Expert only elite melee |
| Defense line archer | 6 | 6 | 2 | 4 | Ranged defender count |
| Defense line crossbowman | 0 | 0 | 4 | 6 | Hard/Expert ranged upgrade |
| Defense line springald | 0 | 0 | 0 | 1 | Expert-only siege |
| Camp cavalry (knights) | 10 | 10 | 15 | 20 | King Bela's guard cavalry |
| Camp melee spearman | 8 | 8 | 8 | 6 | Camp defender infantry |
| Camp melee MAA | 4 | 4 | 6 | 12 | Camp defender heavy infantry |
| Camp ranged crossbowman | 2 | 2 | 4 | 6 | Camp defender ranged |
| Outpost upgrade | arrowslits | arrowslits | arrowslits | springald | Hungarian outpost weapon |
| Harassment spearmen | 5 | 6 | 8 | 12 | Idle-penalty attack wave size |
| Optional mangonels | yes | yes | no | no | Only offered on Normal and below |

### Spawns

- **Intro units**: 4 knights + 6 horse archers spawned at `mkr_player_spawn`, moved to `mkr_player_start`
- **Ambush phase**: 3 RovingArmy forward guard groups (ambush_01/02/03) pre-placed at bridge positions with 20-30 units each; 2 cavalry pursuer groups (6-10 horsemen) chase player
- **Flank ambushers**: Triggered RovingArmy (10 MAA + 8 crossbowmen) if player enters flank zone during scout phase
- **Support phase**: Player receives 10 villagers, Subutai hero, 4 knights, 6 horse archers, plus mobile buildings (TC, barracks, stable, house, Kurultai landmark)
- **Batu's army**: 26 knights + 26 horse archers + Batu Khan hero at start; reinforced from map edge spawner to 100% strength
- **Defense lines**: 4 RovingArmy modules (def_L01, L02, R01, R02) with ~12-20 mixed infantry each; withdraw at 50% to fallback positions
- **Timed reinforcements**: 4 waves of MAA + crossbow reinforcements at 120s, 240s, 360s, 480s if defense lines not yet engaged
- **Hungarian camp**: 13 Defend modules (1 cavalry, 3 melee, 9 ranged) populated on-demand; 7 tent UnitSpawners with 10s spawn rate provide reinforcements until tents destroyed
- **Harassment waves**: Dynamic RovingArmy spawned from camp/defense positions every 120s if player is idle

### AI

- **No AI_Enable calls** — all enemy behavior is driven by MissionOMatic RovingArmy and Defend modules
- **Batu Khan AI**: RovingArmy `batu_start` holds at ally position, dissolves into `batu_attack` targeting bridge on timer expiry, then into `batu_laning` targeting the opposite lane from where player attacks; reinforced from `batu_mapedge_reinforce`
- **Ambush groups**: Forward guards leashed to bridge positions with 45-55 range combat/leash; cavalary pursuers have 150 combat / 340 leash range for extended chase
- **Defense lines**: withdrawThreshold 0.5 triggers fallback; first line falls back to second line, second line to camp center; onDeathDissolve enabled
- **Camp defenders**: Defend modules with 0.2-0.4 upper reinforcement threshold; cavalry at 0.4/0.6 threshold; UnitSpawner rate of 10s
- **Batu invulnerability**: Set invulnerable at 20% health, targeting disabled (`Targeting_None`)
- **Ambush healing**: `Mohi_HealAmbushers` restores full health to bridge defenders every 1s when no allied units nearby (prevents Batu from soloing them)

### Timers

| Timer | Type | Duration | Purpose |
|-------|------|----------|---------|
| ScoutBridge_SpawnFlankAmbushers | Rule_AddInterval | 1s | Poll for player in flank zone, spawn flankers |
| Mohi_HealAmbushers | Rule_AddInterval | 1s | Heal ambush defenders when no allies nearby |
| Mohi_FordNotify | Rule_AddInterval | 1s | Detect player at ford, play VO stinger |
| Mohi_BridgeNotify | Rule_AddInterval | 1s | Detect player at broken bridge, play VO |
| Mohi_BridgeRepaired | Rule_AddInterval | 1s | Monitor bridge repair completion |
| ScoutBridge_DelayedPursuerTargetUpdate | Rule_AddOneShot | 10s | Retarget cavalry pursuers after ambush starts |
| SOBJ_BatuTimer countdown | Objective timer | 720-900s | Preparation time before Batu attacks |
| ScoutBridge_BatuWarning | Rule_AddOneShot | timer/2 | Halfway VO reminder to player |
| ScoutBridge_BotherPlayerIfIdle | Rule_AddInterval | 120s | Spawn harassment if player idle during bridge assault |
| HungarianArmy_BotherPlayerIfTheyAreIdleAgain | Rule_AddInterval | 120s | Spawn harassment if player idle during drive-back phase |
| HungarianArmy_ReinforceExistingModules | Rule_AddOneShot | 120/240/360/480s | Timed defense line reinforcement waves |
| HungarianArmy_DelayedComplete | Rule_AddOneShot | 2s | Delay DriveArmyBack completion for polish |
| ScoutBridge_DelayDrums | Rule_AddOneShot | 1s | Play drum stinger after Batu charges |
| Mohi_OutroBurnMiddle | Rule_AddOneShot | 2s | Stagger tent burning in outro |
| Mohi_OutroBurnEnd | Rule_AddOneShot | 4s | Final tent burning wave in outro |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — imported by both mon_chp2_mohi.scar and obj_scoutbridge.scar; provides RovingArmy, Defend, UnitSpawner, DissolveModuleIntoModule, SpawnUnitsToModule, Objective system
- `obj_hungarianarmy.scar` — imported by mon_chp2_mohi.scar
- `obj_scoutbridge.scar` — imported by mon_chp2_mohi.scar

### Shared Globals
- `player1`–`player5` — defined in core, used across all files
- `sg_leaderSubutai`, `sg_leaderBatu` — leader groups shared across files
- `sg_forward_guard_01/02/03`, `sg_cavgroup_left/right` — ambush sgroups used in both objective files
- `sg_dl_1/2`, `sg_dr_1/2` — defense line sgroups shared between core recipe and obj_hungarianarmy
- `sg_hungarian_camp`, `eg_hungarian_outposts` — camp tracking groups
- `batu_start`, `batu_attack`, `batu_laning` — MissionOMatic module references shared across files
- `def_L01/L02/R01/R02`, `camp_melee_1/2/3`, `camp_ranged_1–9`, `camp_cavalry` — module references
- `ambush_01/02/03` — ambush module references used in both obj_scoutbridge and core
- `bridge_is_repaired`, `bridge_is_seen`, `bridge_UI_started` — bridge state flags
- `batu_timer` — difficulty-scaled timer value
- `visibleGroups` — array tracking ambush group visibility
- `subutaiKills`, `batuKills` — achievement counters
- `g_batuDamageMod` — modifier handle for Batu damage nerf
- `b_batu_laning_right` — lane selection flag for Batu routing
- `maximum_camp_amount` — baseline camp defender count for progress tracking

### Inter-file Function Calls
- Core calls `HungarianArmy_InitObjectives()` and `ScoutBridge_InitObjectives()` from `Mission_SetupVariables`
- obj_hungarianarmy references `Mohi_IsPlayerEconomyLocked` (core) as `OBJ_DestroyArmy.IsFailed`
- obj_hungarianarmy calls `Check_Completion_Time()` (core) on mission complete
- obj_scoutbridge references `Mohi_RefreshBatuMods` (core) as reinforcement onFulfill callback
- obj_scoutbridge calls `Mohi_HealAmbushers` (core) via Rule_AddInterval
- Both objective files reference EVENTS constants (Intro, Victory, Scout_Bridge, Scout_Bridge_Complete, Prepare_Assault, Batu_Halfway, On_Go_Button, Timer_RunOut, Subutai_Arrives, Subutai_Alone, Assault_Bridge_Complete, Drive_Back_Complete, Shallow_Crossing, Destroyed_Bridge)
- obj_scoutbridge references `DelayIntel` (core) for deferred VO playback
