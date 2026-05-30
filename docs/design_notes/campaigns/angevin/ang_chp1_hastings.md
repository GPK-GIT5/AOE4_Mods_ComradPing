# Angevin Chapter 1: Hastings

## OVERVIEW

The Battle of Hastings (1066) is a scripted RTS battle where the player commands Duke William's Norman forces assaulting King Harold's Saxon army atop Senlac Hill. The mission progresses through a linear phase chain: an initial charge up the hill into a Saxon shield wall, a feigned retreat that breaks the wall, then sequential phases that unlock archers, cavalry, and finally a push to kill King Harold. A custom shield wall system manages defensive Saxon formations with row-based unit positioning and automatic backfill. Player reinforcements are dynamically spawned based on unit-type ratios with difficulty-scaled limits, while enemy reinforcements maintain pressure through timed spawning from reserve pools. Tutorial goal sequences teach leader abilities, unit selection, and rock-paper-scissors counter mechanics.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| ang_chp1_hastings.scar | core | Main mission setup: players, variables, difficulty, recipe (modules/spawns), unit positioning, outro |
| obj_initialattack.scar | objectives | Manages the opening charge, staggered attack orders, archer activation, and shield wall reinforcement loop |
| obj_feign.scar | objectives | Detects player retreat from wall, triggers shield wall break with staggered segment releases |
| obj_defeatsaxons.scar | objectives | Orchestrates Phases 2–5 (Fyrd, Archers, Spearmen, Cavalry), player/enemy reinforcement systems, RPS boosts |
| obj_killharold.scar | objectives | Final objective: Harold encounter AI, striker system, defender module management, epilogue/retreat |
| shieldwall_hastings.scar | systems | Custom shield wall formation: row-based positioning, backfill replacement, unit-killed callbacks |
| training_hastings.scar | training | Tutorial goal sequences for leader ability, Ctrl+A, archer attack-move, cavalry, enemy spearmen hints |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_SetupPlayers | ang_chp1_hastings | Configure 4 players, relationships, colours, disable AI for p4 |
| Mission_SetupVariables | ang_chp1_hastings | Create all SGroups, initialize leader, set LINE_FORMATION |
| Mission_SetDifficulty | ang_chp1_hastings | Define difficulty table: reinforcement limits, William attackers |
| Mission_Preset | ang_chp1_hastings | Shield walls, archer range nullification, phase blocker setup |
| Mission_Preset_PartB | ang_chp1_hastings | Zero resources, create shield walls, spread units along splines |
| Mission_Start | ang_chp1_hastings | Find defend modules, start OBJ_DefeatSaxons, time-of-day transition |
| Mission_CheckForFail | ang_chp1_hastings | Fail if limited reinforcements exhausted and no units remain |
| GetRecipe | ang_chp1_hastings | Define UnitSpawner modules, Defend modules, reinforcement spawners |
| Hastings_PassControlOfUnitsToPlayer | ang_chp1_hastings | Transfer units from neutral player3 to player1 |
| Hastings_SpreadUnitsAlongSpline | ang_chp1_hastings | Position squads evenly along marker spline paths |
| Hastings_StaggeredAttack | ang_chp1_hastings | Send squads in waves toward target with configurable style |
| Hastings_ForceAttackWilliam | ang_chp1_hastings | Force nearby enemy units to target Duke William |
| Mission_PrepOutro | ang_chp1_hastings | Stop all modules, spawn outro units, create corpse field |
| InitialAttack_WaitForPlayerToIssueCommand | obj_initialattack | Detect player move command, launch center/flank charges |
| InitialAttack_MoveFlanksUpHill | obj_initialattack | Send left/right flanks charging with staggered attack |
| InitialAttack_UnitsAtTopOfHill | obj_initialattack | Detect arrival at shield wall, show leader ability hint |
| InitialAttack_ShieldWallUnitsKilled | obj_initialattack | After 4 kills or 15s engaged, trigger feign objective |
| InitialAttack_EnableWilliamsArchers | obj_initialattack | Set archer range to 2.6x, stagger first volley |
| InitialAttack_StartReinforcements | obj_initialattack | Start player and shield wall reinforcement loops |
| InitialAttack_ReinforcePlayer | obj_initialattack | Draw from second line, backfill with spawned replacements |
| InitialAttack_ReinforceShieldWall | obj_initialattack | Spawn 2 shield wall units when count drops by 2 |
| Feign_StartObjective | obj_feign | Start OBJ_Feign, lock music to tense |
| Feign_HasPlayerRetreated | obj_feign | Monitor 13 zones for player withdrawal from wall |
| Feign_TriggerShieldWallBreak | obj_feign | Release all 3 wall segments with staggered delays |
| Feign_BreakShieldWall | obj_feign | Kill 65% of frontline, release wall, send shaggy attack |
| Feign_Complete | obj_feign | Remove William damage reduction, Harold rejoins entourage |
| DefeatSaxons_InitReinforcementCounterObjective | obj_defeatsaxons | Setup reinforcement counter UI with progress bar |
| DefeatSaxons_StartObjective | obj_defeatsaxons | Start Phase 2, music lock, hill defend module rules |
| DefeatSaxons_Phase2_Complete | obj_defeatsaxons | Complete when ≤30 fyrd remain, boost damage x7 cleanup |
| DefeatSaxons_Phase3_Start | obj_defeatsaxons | Release 7 spearmen groups with staggered delays |
| DefeatSaxons_Phase3_PreStart | obj_defeatsaxons | Pass archers to player, apply archer RPS boost |
| DefeatSaxons_EnemyReinforcements | obj_defeatsaxons | Timed enemy reinforcements with kill/time thresholds |
| DefeatSaxons_Phase4_PreStart | obj_defeatsaxons | Release spearmen escorts, activate enemy archers at 2.5x range |
| DefeatSaxons_Phase5_PreStart | obj_defeatsaxons | Pass cavalry to player, apply cavalry RPS boost |
| DefeatSaxons_SetPlayerReinforcementFocus | obj_defeatsaxons | Adjust reinforcement thresholds per unit type per phase |
| DefeatSaxons_PlayerReinforcements | obj_defeatsaxons | Spawn reinforcements for lowest-ratio unit type |
| DefeatSaxons_PlayerReinforcements_Create | obj_defeatsaxons | Pick best zone, deploy units, play horn, update counter |
| DefeatSaxons_UpdateHillDefendModules | obj_defeatsaxons | Reassign idle Saxon units to defend modules, retarget |
| BoostRPS_Add | obj_defeatsaxons | Apply weapon/received-damage modifiers per unit type |
| BoostRPS_Remove | obj_defeatsaxons | Remove active boost modifiers and tracking sgroup |
| KillHarold_Init | obj_killharold | Store Harold entity ID, set non-targetable/non-selectable |
| KingHarold_RejoinEntourage | obj_killharold | Move Harold to rear position, enable projectile blocking |
| KingHarold_SpawnLastLines | obj_killharold | Deploy 56 last-line defenders across left/center/right |
| KillHarold_StartObjective | obj_killharold | Complete OBJ_DefeatSaxons, start OBJ_KillHarold, enable targeting |
| KingHarold_PreStart | obj_killharold | Create encounters for Harold, entourage, defenders, strikers |
| KingHarold_ManageStrikers | obj_killharold | Pull units from defender modules to attack Harold's assailants |
| KillHarold_CloseInOnHarold | obj_killharold | When player near Harold, reassign 30% defenders to his position |
| KillHarold_Killed | obj_killharold | Stop all modules, retarget encounters to death position |
| KillHarold_RunAway | obj_killharold | Gradually retreat Saxon units after Harold dies |
| ShieldWall_Create | shieldwall_hastings | Build multi-row formation from posA to posB with backfill |
| ShieldWall_Release | shieldwall_hastings | Remove all wall modifiers, unlock hold position |
| ShieldWall_WallUnitKilled | shieldwall_hastings | Replace killed wall unit from next row or backfill |
| ShieldWall_WallUnit_HoldGround | shieldwall_hastings | Apply 3x damage, 0.75x received, 19/20 melee block |
| MissionTutorial_Init | training_hastings | Initialize tutorial system from Mission_Start |
| MissionTutorial_AddHintToLeaderAbility | training_hastings | Goal sequence: select William, hover ability |
| MissionTutorial_AddHintToArchers | training_hastings | Goal sequence: select archers, attack-move tutorial |
| MissionTutorial_AddHintToCavalry | training_hastings | Goal sequence: select cavalry for counter tutorial |
| MissionTutorial_AddHintToEnemySpearmen | training_hastings | Hint about spearmen countering cavalry |

## KEY SYSTEMS

### Objectives

| Constant | Purpose |
|----------|---------|
| OBJ_DefeatSaxons | Primary: "Attack Harold's Army" — umbrella objective for Phases 2–5 |
| SOBJ_Phase2_KillFyrd | Sub: Kill the Fyrd from the shield wall (post-feign melee) |
| SOBJ_Phase3_UseArchers | Sub: Use archers against enemy spearmen |
| SOBJ_Phase4_KillSpearmen | Sub: Kill enemy spearmen to allow cavalry |
| SOBJ_Phase5_UseCavalry | Sub: Use cavalry against enemy archers |
| OBJ_Feign | Primary: Feign a retreat to lure Saxons from shield wall |
| OBJ_KillHarold | Primary: Defeat King Harold — final objective |
| OBJ_Reinforcements | Information: Remaining reinforcement waves counter (progress bar) |
| OBJ_DebugComplete | Debug: Force mission complete |

### Difficulty

| Parameter | Story | Easy | Normal | Hard |
|-----------|-------|------|--------|------|
| enableLimitedReinforcements | false | true | true | true |
| maximumNumberOfReinforcements | -1 (unlimited) | 35 | 20 | 10 |
| maxNumberOfWilliamAttackers | 2 | 2 | 3 | 4 |

Post-downed William (Story mode only): `maxNumberOfWilliamAttackers` reduced to 1.

### Spawns

**Player (William) — Initial Army:**
- Center: 21 men-at-arms, 4 horsemen + Duke William
- Left/Right flanks: 32 men-at-arms, 4 horsemen each
- Second line: 54 men-at-arms (20 left, 14 center, 20 right) — held by player3
- Archers: 44 total (11 per section × 4 sections) — held by player3
- Cavalry: 20 horsemen (5 per section × 4 sections) — held by player3

**Player Reinforcements:**
- 3 active zones (zones 2–4), 7-second minimum interval between waves
- Type chosen by lowest ratio vs threshold (MAA: 40–50, Archers: 15–30, Cavalry: 8–14)
- Focus shifts per phase: manatarms → archers → cavalry → final (mixed)
- Units spawn as player3, pass to player1 after 5s move delay

**Saxon (Harold) — Defenders:**
- Shield wall: 136 shieldwall units + 26 spearmen across 3 segments (A: 42+8, B: 52+10, C: 42+8)
- Phase 3 spearmen: 63 (7 groups × 9)
- Phase 4 spearmen: 48 (5 groups × ~10)
- Phase 5 archers: 25 archers + 10 men-at-arms (5 groups)
- Harold's entourage: 4 MAA + 10 spearmen + 2 MAA + 8 shieldwall defenders
- Last lines (spawned Phase 4+): 18 left (6 spear + 12 MAA), 20 center (MAA), 18 right (6 spear + 12 MAA)

**Enemy Reinforcements (Phases 3–4):**
- Phase 3: threshold 50 active, steal 4–7 from phase 4 pool, minTime 45s, maxTime 150s, 100 kills required
- Phase 4: threshold 30 active, spawn from marker, 4–7 per wave, minTime 45s, maxTime 150s, 50 kills required
- Stolen units are backfilled with fresh spawns at original positions

### AI

- **player4 AI disabled** (`AI_Enable(player4, false)`) — downed-state holder
- **DefendHillLeft/Center/Right** — Defend modules for Saxon hillside forces; target location dynamically updated based on nearest player concentration (3s interval per module, staggered 0/1/2s)
- **DefendHaroldLeft/Center/Right** — Last-line defend modules with reinforcement chains; threshold decays (-0.1 per adjustment, limit 0.5)
- **KingHaroldDefenders1–4** — Inner defend modules around Harold with cross-reinforcement
- **enc_kingHarold** — Defend encounter: combatRange 10, leashRange 15, hold while waiting
- **enc_kingHaroldEntourage** — Defend encounter tracking Harold's sgroup, combatRange 10, leashRange 10
- **enc_kingHaroldStrikers** — Reactive Attack encounter; pulls 1 unit from each defender module to counter ranged attackers, returns to DoNothing when targets die
- **enc_KingHaroldDefenders** — Created when player approaches Harold; 30% of last-line units reassigned, combatRange 15, leashRange 20
- **Hastings_ForceAttackWilliam** — Forces up to N enemy units (difficulty-scaled) to attack William; disengages if >7m away
- **ReinforcementsHaroldCenter/Left/Right** — UnitSpawner modules with spawnRate 2.5, useDynamicSpawn

### Timers

| Timer | Type | Delay/Interval | Purpose |
|-------|------|----------------|---------|
| Mission_Preset_PartB | OneShot | 0.125s | Zero resources, create shield walls, position units |
| Mission_Start_PartB | OneShot | 15s | Transition to daytime over 10 minutes |
| Mission_CheckForFail | Interval | 1s | Check for player defeat when reinforcements exhausted |
| DefeatSaxons_InitPlayerReinforcements | OneShot | 5s | Initialize player reinforcement zones |
| DefeatSaxons_PlayerReinforcements | Interval | 1s | Check and spawn player reinforcements (7s min gap) |
| DefeatSaxons_PlayerReinforcements_PassControl | OneShot | 5s | Transfer spawned reinforcements to player1 |
| DefeatSaxons_PlayerReinforcements_MonitorForCommands | Interval | 4s delay, 1s interval | Track if reinforcements received orders; auto-charge after 15s |
| DefeatSaxons_UpdateHillDefendModules | Interval | 3s (staggered) | Reassign idle Saxons to defend modules |
| DefeatSaxons_EnemyReinforcements | Interval | 1s | Enemy reinforcement spawning per phase |
| DefeatSaxons_Phase2/3/4/5_Complete | Interval | 1s | Check phase completion thresholds |
| DefeatSaxons_Phase*_CleanUp | Interval | 1s | Kill stragglers after 10s if still alive |
| Feign_HasPlayerRetreated | Interval | 0.5s | Monitor 13 zones for player withdrawal |
| Feign_BreakShieldWall | OneShot | stagger1/2/3 (0.125/6.5/10s) | Break wall segments in sequence |
| Feign_Complete | OneShot | 3s | Post-feign cleanup, Harold repositioning |
| InitialAttack_MoveFlanksUpHill | OneShot | 1s, 2s | Send left/right flanks after center |
| InitialAttack_EnableWilliamsArchers | OneShot | 2s | Unlock archer range to 2.6x |
| InitialAttack_UnitsAtTopOfHill | Interval | 1s | Detect arrival at shield wall |
| InitialAttack_UnitsAtTopOfHill_PartB | OneShot | 10s | Trigger engaged intel, start kill tracking |
| Feign_StartObjective | OneShot | 15s | Start feign after shield wall engaged dialogue |
| DefeatSaxons_StartObjective | OneShot | 10s | Start Defeat Saxons after feign completes |
| KingHarold_ManageStrikers | Interval | 1s | Manage striker attack/return cycle (5s cooldown) |
| KillHarold_CloseInOnHarold | Interval | 1s | Detect player proximity to Harold (<10m or health <90%) |
| KillHarold_RunAway | Interval | 1s | Gradually retreat Saxons post-Harold death |
| KillHarold_MissionEnd | OneShot | 4s | Call Mission_Complete after epilogue |
| InitialAttack_ReinforceShieldWall | Interval | 2s | Backfill shield wall with 2 units when count drops |
| InitialAttack_ReinforcePlayer | Interval | 1s (staggered 0.25/0.5/0.75s) | Replace frontline losses from second line |
| BoostRPS_Manager | Interval | 2s | Apply weapon/armor modifiers to newly spawned matching units |
| Hastings_StaggeredAttack_Manager | Interval | 0.25s | Send squads in batches of 5 toward target |
| Feign_MonitorShieldWallEngagers | Interval | 0.5s | Track which player units have engaged the wall |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Mission framework (Cardinal scripts)
- `ShieldWall_Hastings.scar` — Custom shield wall system
- `Training_Hastings.scar` — Tutorial goal sequences
- `obj_InitialAttack.scar` — Initial attack phase
- `obj_Feign.scar` — Feign retreat phase
- `obj_DefeatSaxons.scar` — Phases 2–5
- `obj_KillHarold.scar` — Final objective
- `training/campaigntraininggoals.scar` — Base campaign training predicates
- `ang_chp1_hastings.scar` — Imported by obj_feign.scar (circular, for `Hastings_StaggeredAttack`)

### Shared Globals
- `player1`–`player4` — Player handles used across all files
- `sg_dukewilliam`, `sg_kingharold`, `sg_archers`, `sg_cavalry` — Key unit groups referenced everywhere
- `sg_saxons_phase2_all` through `sg_saxons_phase5_all` — Phase-specific enemy pools
- `sg_activeUnits_player1`, `sg_activeUnits_player2` — Active unit tracking for reinforcement balancing
- `sg_shieldwall_a/b/c` — Shield wall segment groups shared between core, feign, and initial attack
- `wallid_a/b/c` — Shield wall data objects created in core, used in feign and initial attack
- `b_shieldWallBroken` — Set by feign, checked by initial attack reinforcement loops
- `b_archersUnlocked`, `b_cavalryUnlocked` — Gate reinforcement type availability
- `b_playerReinforcementsStopped` — Set when reinforcement limit reached, checked by fail condition
- `g_leaderWilliam` — Leader state object (MissionOMatic leader system)
- `t_difficulty` — Difficulty parameter table
- `modid_playerArcherRange`, `modid_enemyArcherRange`, `modid_williamReducedDamage` — Modifier IDs passed between files
- `EVENTS.*` — Intel/NIS event table (Intro, Outro, phase transitions, reinforcement VO)
- `DefendHillLeft/Center/Right` — Module references found in core, used in defeatsaxons and killharold
- `enc_kingHarold`, `enc_kingHaroldEntourage`, `enc_kingHaroldStrikers` — Encounter handles created in killharold

### Inter-File Function Calls
- `obj_initialattack` → `Feign_StartObjective()` (after shield wall engaged)
- `obj_feign` → `DefeatSaxons_StartObjective()`, `Hastings_ForceAttackWilliam()`, `KingHarold_RejoinEntourage()` (on feign complete)
- `obj_defeatsaxons` → `KillHarold_StartObjective()` (Phase 5 complete), `KingHarold_SpawnLastLines()` (Phase 4 start)
- `obj_defeatsaxons` → `Hastings_PassControlOfUnitsToPlayer()`, `Hastings_StaggeredAttack()` (from core)
- `obj_killharold` → `DefeatSaxons_UpdateActiveUnitCounts()` via `KillHarold_MonitorModules`
- `obj_initialattack` → `InitialAttack_ShieldWallUnitKilled()` (callback from ShieldWall system)
- `training_hastings` → References `sg_dukewilliam`, `sg_archers`, `sg_cavalry`, objective states
