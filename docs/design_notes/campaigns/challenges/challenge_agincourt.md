# Historical Challenge: Agincourt

## OVERVIEW

The Agincourt Historical Challenge recreates the 1415 Battle of Agincourt as a multi-wave defensive/offensive scenario. The player controls House of Lancaster (English) forces led by Henry V against three successive French army divisions advancing across a 5-lane battlefield. The French Vanguard (Wave 1: cavalry), Main Division (Wave 2: mixed infantry), and Reserves (Wave 3: infantry with cannons) each use sophisticated lane-based movement, staggered sub-wave breakoff timing, and leader-driven "Battlefield Promotion" mechanics that upgrade units mid-battle. A Conqueror Mode unlocks if the player defeats Wave 1 within 5 minutes, strengthening all subsequent French forces. Timed medal objectives (Gold ≤16 min, Silver ≤20 min, Bronze = completion) and player reinforcement waves scale the difficulty dynamically. Flanking counterattacks from Agincourt and Tramecourt towns add pressure alongside the main waves.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_agincourt.scar` | core | Main mission setup, player/enemy init, global update loop, reinforcements, event handlers, intro NIS, victory/defeat logic |
| `challenge_agincourt_obj.scar` | objectives | Defines all OBJ_/SOBJ_ objective constants, medal system, tug-of-war strength bars, wave completion checks |
| `challenge_agincourt_wave1.scar` | spawns | Wave 1 (French Vanguard) — cavalry spawn, 5-lane advance, sub-wave splits at 2/5/6.5 min, leader rally/promotion mechanic |
| `challenge_agincourt_wave2.scar` | spawns | Wave 2 (Main Division) — mixed infantry spawn, timed sub-wave breakoffs, dual leader AI with healing/AoE damage abilities |
| `challenge_agincourt_wave3.scar` | spawns | Wave 3 (French Reserves) — 3-lane advance with cannons, defensive pavise circles, militia-to-MAA promotion by roaming leader |
| `challenge_agincourt_counterattack.scar` | spawns | Flanking raids from Agincourt (horsemen) and Tramecourt (crossbowmen) towns plus hidden cavalry counterattack |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | core | Initializes bools, constants, medal times, debug flags |
| `Mission_SetupPlayers` | core | Creates 8 players, sets colors, diplomacy references |
| `Mission_SetRestrictions` | core | Grants Lancaster upgrades, removes wall/dock production |
| `ChallengeMission_SetupDiplomacy` | core | Sets complex multi-player relationship matrix |
| `Mission_PreInit` | core | Registers global events: killed, destroyed, projectile, ability |
| `Mission_Start` | core | Starts objectives, spawns French army, sets resources |
| `HC_Agincourt_Update` | core | Main loop: reinforcements, prison, failure check, UI update |
| `HC_Agincourt_SpawnFrenchArmy` | core | Spawns all 3 waves plus defenders, patrol, hidden army |
| `HC_Agincourt_SpawnPlayerUnits` | core | Deploys Lancaster yeomen, spearmen, hobelars, villagers, Henry V |
| `HC_Agincourt_SpawnGaiaUnits` | core | Spawns 8 sheep as world-owned herdables |
| `HC_Agincourt_OnSquadKilled` | core | Detects Henry V death, triggers 31s respawn timer |
| `HC_Agincourt_RespawnHenry` | core | Respawns Henry V with +25 bonus HP (up to 250) |
| `HC_Agincourt_OnDestruction` | core | Tracks Agincourt/Tramecourt town center destruction |
| `HC_Agincourt_OnProjectileFired` | core | Adds bouncing cannonball AoE damage for buffed cannons |
| `HC_Agincourt_SpawnCannonHitEffect` | core | Applies primary cannon AoE ring damage (15 dmg) |
| `HC_Agincourt_SpawnBounceHitEffect` | core | Applies secondary bounce damage (10 dmg per bounce) |
| `HC_Agincourt_OnAbilityExecuted` | core | Resets yeoman synchronized shot on leader rally |
| `HC_Agincourt_EndChallenge` | core | Stores KPI data, plays victory intel, completes mission |
| `HC_Agincourt_IntroSetup` | core | Spawns all units for intro NIS camera sequence |
| `HC_Agincourt_IntroTeardown` | core | Destroys intro-only units, cleans up reticules |
| `HC_Agincourt_InitObjectives` | objectives | Registers all objectives with callbacks and timers |
| `HC_Agincourt_UpdateObjectiveUI` | objectives | Updates medal failures, tug-of-war bars, conqueror timer |
| `HC_Agincourt_CheckWave1Ended` | objectives | Checks Wave 1 all-dead, triggers Wave 2 reveal |
| `HC_Agincourt_CheckWave2Ended` | objectives | Checks Wave 2 all-dead, triggers Wave 3 launch |
| `HC_Agincourt_CheckWave3Ended` | objectives | Checks Wave 3 all-dead for victory condition |
| `HC_Agincourt_FinishWave1Attack` | objectives | Cleans Wave 1 UI, starts Wave 2 objective |
| `HC_Agincourt_CompleteWave2` | objectives | Completes Wave 2 objective, launches Wave 3 attack |
| `HC_Agincourt_LaunchWave3Attack` | objectives | Cleans Wave 2 UI, schedules Wave 3 start |
| `HC_Agincourt_SpawnFrenchWave1` | wave1 | Spawns 5 cavalry lanes (~100 units), reveals, applies debuffs |
| `HC_Agincourt_Wave1_PreStart` | wave1 | Pre-combat advance: 15s step intervals to 0.8 progress |
| `HC_Agincourt_Wave1_PreUpdate` | wave1 | Manages timed sub-wave splits at 2/5/6.5 min marks |
| `HC_Agincourt_Wave1_Start` | wave1 | Commits all remaining Wave 1 units to full attack |
| `HC_Agincourt_Wave1_Update` | wave1 | Combat update: leader promotion, conqueror mode check |
| `HC_Agincourt_Wave1_GatherAroundLeader` | wave1 | Gathers up to 12 units, transfers to debuffed player |
| `HC_Agincourt_Wave1_UpdateLeaderCombat` | wave1 | Initiates promotion when leader surrounded and in combat |
| `HC_Agincourt_Wave1_UpdateLeader` | wave1 | Moves Wave 1 leader to lane with most units |
| `HC_Agincourt_Wave1_CheckProgress` | wave1 | Tracks 5-lane advance progress, triggers lane reform |
| `HC_Agincourt_Wave1_ResumeLanes` | wave1 | Resumes attack-move after lane alignment pause |
| `HC_Agincourt_Wave1_SendBackToLane` | wave1 | Projects group to lane line at target progress |
| `HC_Agincourt_Wave1_CheckLaneProgress` | wave1 | Calculates lane progress ratio from start to end marker |
| `HC_Agincourt_GetPointOnLane` | wave1 | Projects point onto lane line segment (vector math) |
| `HC_Agincourt_SpawnFrenchWave2` | wave2 | Spawns 5-lane mixed army (~112 units) + 2 leaders |
| `HC_Agincourt_RevealFrenchWave2` | wave2 | Reveals Wave 2 on minimap, starts 8:30 countdown |
| `HC_Agincourt_Wave2_Start` | wave2 | Commits Wave 2 sub-group to attack, enables leader AI |
| `HC_Agincourt_Wave2_Update` | wave2 | Early-attack response, timed breakoffs, fit checking |
| `HC_Agincourt_Wave2_BreakOffGroup` | wave2 | Splits sub-wave by preset count tables per lane |
| `HC_Agincourt_Wave2_UpdateLeader` | wave2 | Sends Leader A to lane with most units, retreats on damage |
| `HC_Agincourt_Wave2_UpdateLeader2` | wave2 | Sends Leader B to lane with fewest units |
| `HC_Agincourt_Wave2HealingAbilities` | wave2 | Leader A AoE heal every 30s when nearby units damaged |
| `HC_Agincourt_Wave2DamageAbilities` | wave2 | Leader B AoE damage every 15s when player units nearby |
| `HC_Agincourt_Wave2_Begin_AoE` | wave2 | Deploys pavise, becomes invulnerable, starts AoE charge-up |
| `HC_Agincourt_Wave2_Apply_AoE` | wave2 | Deals 30 (normal) or 50 (conqueror) AoE damage |
| `HC_Agincourt_Wave2_CheckFit` | wave2 | Corrects lanes drifting >50% off path |
| `HC_Agincourt_Wave2_SendBackToLane` | wave2 | Projects and redirects group to correct lane position |
| `HC_Agincourt_SpawnFrenchWave3` | wave3 | Spawns 3-lane army with cannons, militia, defenders |
| `HC_Agincourt_RevealFrenchWave3` | wave3 | Reveals Wave 3, adds gunpowder aura to cannons |
| `HC_Agincourt_Wave3_Start` | wave3 | Initiates 4-phase advance with 60s intervals per step |
| `HC_Agincourt_Wave3_BeginLaneAdvance` | wave3 | Advances specific lane to target progress fraction |
| `HC_Agincourt_Wave3_Lane1/3/5Attack` | wave3 | Commits lane to final attack-move on player base |
| `HC_Agincourt_Wave3_Update` | wave3 | State machine: Advance→Circle→Deploy→Fire→Idle→Attack |
| `HC_Agincourt_Wave3_UpdateLeader` | wave3 | 6-phase leader patrol promoting militia to MAA |
| `HC_Agincourt_Wave3_GatherAroundLeader` | wave3 | Replaces militia with men-at-arms (Age 4 in conqueror) |
| `HC_Agincourt_Wave3_SendBackToLane` | wave3 | Lane positioning with defensive circle formation support |
| `HC_Agincourt_StartCounterAttacks` | counterattack | Starts raids + hidden army counterattack after 6 min |
| `HC_Agincourt_SpawnMainCounterAttack` | counterattack | Spawns 6 or 12 militia from Agincourt + hidden horsemen |
| `HC_Agincourt_SpawnAgincourtRaid` | counterattack | Spawns 3/5 horsemen from Agincourt every 90s |
| `HC_Agincourt_SpawnTramecourtRaid` | counterattack | Sends 3/5 crossbowmen from Tramecourt every 90s |
| `HC_Agincourt_PulseThreatBlip` | counterattack | Minimap blips for active raider groups every 15s |

## KEY SYSTEMS

### Objectives

| Constant | Purpose |
|----------|---------|
| `OBJ_Victory` | Primary: Defeat all 3 French Divisions (count-up timer) |
| `OBJ_Army` | French Strength tracker (sub-objective, not always started) |
| `SOBJ_Defend` | Defend Capital Town Center (failure = TC destroyed) |
| `OBJ_ConquerorMedal` | Bonus: Defeat strengthened French army (conqueror mode) |
| `OBJ_GoldMedal` | Bonus: Complete within 16 minutes |
| `OBJ_SilverMedal` | Bonus: Complete within 20 minutes (registered after gold fails) |
| `OBJ_BronzeMedal` | Bonus: Complete the challenge (registered after silver fails) |
| `SOBJ_AttackWave1` | Attack the French Vanguard (8 min countdown) |
| `SOBJ_AttackWave2` | Attack the Main French Division (8:30 countdown) |
| `SOBJ_AttackWave3` | Defeat the Remaining French Army |
| `SOBJ_AttackWave1Strength` | Tug-of-war bar: player vs. Wave 1 resource cost |
| `SOBJ_AttackWave2Strength` | Tug-of-war bar: player vs. Wave 2 resource cost |
| `SOBJ_AttackWave3Strength` | Tug-of-war bar: player vs. Wave 3 resource cost |
| `OBJ_Conqueror` | Bonus: Attack vanguard within 5 min for greater challenge |
| `SOBJ_W1LeaderRally` | Battlefield Promotion indicator (progress bar) |
| `SOBJ_Progress1-5` | Debug: Lane progress tracking (disabled by default) |
| `SOBJ_Fit1-5` | Debug: Lane fit/drift tracking (disabled by default) |

### Difficulty / Conqueror Mode

No `Util_DifVar` calls. Difficulty is binary via `conquerorModeActivated`:

| Parameter | Normal | Conqueror |
|-----------|--------|-----------|
| Wave 1 rally unit max | 6 (after conqueror fails) | 12 |
| Wave 2 start time multiplier | 80 | 70 (faster sub-wave breakoffs) |
| Wave 2 Leader B AoE damage | 30 | 50 |
| Wave 2 leader abilities | Activate once | Repeatable (30s/15s cooldowns) |
| Wave 3 militia promotion | MAA Age 3 | MAA Age 4 |
| Wave 3 side cannons (1, 5) | No gunpowder aura | +Gunpowder aura |
| Cannon bounce count | 3 (normal targets) | Same, but all 3 cannons buffed |
| Counterattack raiders | Horsemen 2 (3), Crossbow 3 (2) | Horsemen 3 (5), Crossbow 3 (4) |
| Main counterattack militia | 6 | 12 |
| Enemy melee/ranged upgrades | None extra | +1 melee, +1 ranged damage |
| Player reinforcements | 4 waves (5:10, 10:00, 16:10, 19:30) | None |
| Wave 2 Leader B aura | None | GENERAL_AURA_ARMOR |
| Wave 2 Leader A aura | None | LORD_OF_LANCASTER_AURA |

### Spawns

**Wave 1 — French Vanguard (5 lanes, ~100 units):**
- Lane 1: 16 Horseman II + 2 Knight II
- Lane 2: 6 Horseman II + 14 Knight II
- Lane 3: 24 Knight II
- Lane 4: 6 Horseman II + 14 Knight II
- Lane 5: 16 Horseman II + 2 Knight II
- Leader: Boucicaut (2.5x HP)
- Speed modifier: 0.8x; Damage taken modifier for debuffed player: 2.5x
- Sub-wave splits at 2 min, 5 min, 6:30 (counts: {4,4,6,4,4}, {4,4,6,4,4}, {4,5,6,5,4})
- Pre-combat advance: steps every 15s from 0.3 to 0.8 progress

**Wave 2 — Main Division (5 lanes, ~112 units):**
- Lane 1: 22 Horseman III
- Lane 2: 10 Spearman II + 10 MAA III
- Lane 3: 10 Spearman II + 15 MAA III
- Lane 4: 20 Archer II
- Lane 5: 25 Spearman II
- Leader A: Edward III (3.5x HP, healing aura)
- Leader B: John I (3.5x HP, AoE damage + DEPLOY_PAVISE)
- All leaders: 1.3x speed modifier
- Sub-wave split counts: {5,5,6,5,6}, {8,7,9,8,9}, {9,8,10,9,10}, {9,9,10,9,10}
- Timed breakoffs at 2x, 4x, 6x, 8x `wave2StartTimeMultiplier` seconds

**Wave 3 — French Reserves (3 lanes, ~93 units + 3 cannons):**
- Lanes 1, 3, 5 each: 16 Spearman/Crossbow II-III + 14 Shield Militia (1.5x HP) + 1 Royal Cannon IV
- Lane 3 defender type: Crossbowman III (others: Spearman II)
- Leader: Charles d'Albret (3x HP)
- Shield Militia: 1.5x speed modifier
- Defenders have DEPLOY_PAVISE ability
- Advance pattern: 60s intervals, 4 steps (0.2→0.4→0.6→0.8), with advance→circle→deploy→fire→idle state machine
- Cannon targeting: progressive markers per lane step
- Leader promotes militia to MAA via 6-phase roaming schedule across empty lanes (2, 4)

**Counterattacks (after Wave 1):**
- Agincourt raids: 3/5 Horsemen every 90s (stops if town destroyed)
- Tramecourt raids: 3/5 Crossbowmen every 90s (uses existing defenders first)
- Main counterattack at 6 min: 8 hidden Horsemen III + militia from Agincourt
- Hidden army follows 4-waypoint path to player base

**Static Defenders:**
- Agincourt: 12 Spearman II + 4 Horseman II
- Tramecourt: 30 Crossbowman III + 3 Spearman II
- Camp: 8 Crossbowman III
- Prison: 6 Spearman II (killing frees 6 captured Knight IV for player)
- Patrol: 5 Horseman III on 9-waypoint patrol loop
- Woodcutters: 10 Villagers

**Player Starting Forces:**
- 28 Yeoman IV, 17 Spearman IV, 8 Hobelar IV, 2 Scouts
- Henry V (hero, +150 HP, 1.25x speed, respawns after 31s with +25 HP each time)
- 22 Villagers (6 wood, 7 sheep, 4 farms, 5 gold)
- Starting resources: 500 Food, 600 Wood, 300 Gold, 300 Stone

**Player Reinforcements (normal mode only):**
- 5:10 — 8 Spearman IV
- 10:00 — 10 Crossbowman III
- 16:10 — 8 Earlsguard IV + 12 Crossbowman IV + 12 Spearman IV
- 19:30 — 20 Earlsguard IV + 4 Culverin IV

### AI

- No `AI_Enable` calls — all enemy behavior is fully scripted
- **Patrol Army:** 5 Horseman III on `enemyPatrolPlayer`, 9-waypoint `TARGET_ORDER_PATROL` via `Army_Init`
- **Wave 1 Leader:** Moves to lane with highest unit count; initiates Battlefield Promotion when under attack with ≥5 nearby player units — gathers up to 12 units, transfers to `enemyPlayer3` (debuffed), then upgrades to Knight IV / Horseman IV via `enemyPlayer2` (fully upgraded)
- **Wave 2 Leader A:** Follows largest lane group; retreats to waiting units when health drops >40%; casts AoE heal every 30s
- **Wave 2 Leader B:** Follows smallest lane group; casts AoE damage (pavise + invulnerability + Jeanne d'Arc ability) every 15s; 5s charge-up warning with reticule
- **Wave 3 Leader:** 6-phase schedule across lanes promoting militia to men-at-arms; phases tied to `advanceInterval` multiples (60s each)
- **Lane Fit Correction:** All waves check lateral drift from lane center; groups redirected when fit exceeds 50% of `LANE_MAX_WIDTH` (40 units)
- **Early Attack Response (Wave 2):** If waiting units are attacked, timer advances to next breakoff threshold; attacked lane immediately commits all units

### Timers

| Timer | Type | Value | Purpose |
|-------|------|-------|---------|
| `HC_Agincourt_Update` | Interval | 0.125s | Main game loop (reinforcements, failure, UI) |
| `HC_Agincourt_Wave1_PreUpdate` | Interval | 1s | Wave 1 pre-combat advance and sub-wave scheduling |
| `HC_Agincourt_Wave1_Update` | Interval | 0.125s | Wave 1 combat: leader promotion, conqueror check |
| `HC_Agincourt_Wave1_UpdateLeader` | Interval | 1s | Wave 1 leader lane targeting |
| `HC_Agincourt_Wave1_GatherAroundLeader` | Interval | 0.5s | Battlefield Promotion unit gathering |
| `HC_Agincourt_Wave1_UpdateLeaderReticule` | Interval | 0.125s | Promotion charge-up visual effect |
| `HC_Agincourt_Wave2_Update` | Interval | 0.125s | Wave 2 advance, breakoffs, fit correction |
| `HC_Agincourt_Wave2_UpdateLeader` | Interval | 0.25s | Wave 2 Leader A lane targeting |
| `HC_Agincourt_Wave2_UpdateLeader2` | Interval | 0.25s | Wave 2 Leader B lane targeting |
| `HC_Agincourt_Wave2HealingAbilities` | Interval | 1s | Leader A heal check (30s cooldown) |
| `HC_Agincourt_Wave2DamageAbilities` | Interval | 1s | Leader B damage check (15s cooldown) |
| `HC_Agincourt_Wave3_Update` | Interval | 0.125s | Wave 3 state machine, fit, victory check |
| `HC_Agincourt_Wave3_UpdateLeader` | Interval | 3s | Wave 3 leader 6-phase promotion schedule |
| `HC_Agincourt_Wave3_UpdateLeaderCombat` | Interval | 0.5s | Wave 3 leader promotion execution |
| `HC_Agincourt_Wave3_GatherAroundLeader` | Interval | 0.5s | Wave 3 militia replacement gathering |
| `HC_Agincourt_Wave3_BeginLaneAdvance` | OneShot | 0/60/120/180s | Lane advance steps (per lane, staggered) |
| `HC_Agincourt_Wave3_Lane1/3/5Attack` | OneShot | 250s | Final lane assault |
| `HC_Agincourt_SpawnMainCounterAttack` | OneShot | 360s (6 min) | Hidden army + militia counterattack |
| `HC_Agincourt_SpawnAgincourtRaid` | Interval | 90s | Horsemen raids from Agincourt |
| `HC_Agincourt_SpawnTramecourtRaid` | Interval | 90s | Crossbow raids from Tramecourt |
| `HC_Agincourt_PulseThreatBlip` | Interval | 15s | Minimap blips for active raiders |
| `HC_Agincourt_CheckWave1Ended` | Interval | 0.125s | Wave 1 completion check |
| `SOBJ_AttackWave1` countdown | Timer | 8 min | Wave 1 approach timer |
| `OBJ_Conqueror` countdown | Timer | 5 min | Conqueror mode unlock window |
| `SOBJ_AttackWave2` countdown | Timer | 8:30 | Wave 2 approach timer |
| `HC_Agincourt_RespawnHenry` | OneShot | 31s | Henry V respawn delay |
| `HC_Agincourt_Wave2_Apply_AoE` | OneShot | 5s | Leader B AoE charge-up duration |

## CROSS-REFERENCES

### Imports (all files share)
- `MissionOMatic/MissionOMatic.scar` — Cardinal mission framework
- `MissionOMatic/MissionOMatic_utility.scar` — Utility helpers (core + obj only)
- `missionomatic/missionomatic_artofwar.scar` — Art of War / challenge framework
- `training/coretraininggoals.scar` — Training goals system
- `challenge_agincourt.events` — Event/intel definitions (EVENTS.Camera_Intro, EVENTS.French_Battalion, EVENTS.Conqueror_Unlock, EVENTS.Victory, EVENTS.Victory_Conqueror, EVENTS.Defeat)
- `cardinal.scar` — Cardinal base scripts

### Core → Sub-file Imports
- `challenge_agincourt.scar` imports all sub-files: `_obj`, `_wave1`, `_wave2`, `_wave3`, `_counterattack`

### Inter-file Function Calls
- Core calls: `HC_Agincourt_InitObjectives()`, `HC_Agincourt_SpawnFrenchWave1/2/3()`, `HC_Agincourt_StartCounterAttacks()`
- Objectives calls: `HC_Agincourt_Wave1_Start()`, `HC_Agincourt_Wave2_Start()`, `HC_Agincourt_Wave3_Start()`, `HC_Agincourt_RevealFrenchWave2/3()`, `HC_Agincourt_CheckWave2Ended()`, `HC_Agincourt_CheckWave3Ended()`
- Wave 2 update calls: `HC_Agincourt_RevealFrenchWave3()` (triggers wave 3 reveal when wave 2 units all dead)
- Wave 3 update calls: `HC_Agincourt_EndChallenge()` (triggers victory when wave 3 units all dead)
- All waves use: `HC_Agincourt_GetPointOnLane()` (defined in wave1, shared geometry helper)

### Shared Globals
- `conquerorModeActivated` — Set in wave1 update, read by all files for difficulty branching
- `missionTime` — Updated in core loop, read by wave1/wave2 for sub-wave timing
- `enemyPlayer` / `localPlayer` / `allyPlayer` / `enemyPlayer2` / `enemyPlayer3` / `enemyPatrolPlayer` / `capturedUnitsPlayer` / `enemyCannonPlayer` — 8-player references used across all files
- `sg_wave1_AllUnits` / `sg_wave2_AllUnits` / `sg_wave3_AllUnits` — Unit group totals for strength bars and completion checks
- `agincourtTownAlive` / `tramecourtTownAlive` — Destruction flags controlling raid spawns
- `GOLD_MEDAL_TIME` (960s) / `SILVER_MEDAL_TIME` (1200s) — Medal thresholds
- `gatheringAroundLeader` / `gatherAroundTimeLimit` (15s) — Promotion mechanic state
- `wave2StartTimeMultiplier` — Controls wave 2 breakoff pacing (80 normal, 70 conqueror)
- `w3LaneState` enum — {Idle=0, Advancing=1, SetupCircle=2, CompleteCircle=3, Deploying=4, Firing=5, Attacking=6}

### Blueprint References
- **Lancaster:** UNIT_HENRY_5_CMP, UNIT_YEOMAN_4, UNIT_SPEARMAN_4, UNIT_HOBELAR_4, UNIT_CROSSBOWMAN_3/4, UNIT_EARLSGUARD_4, UNIT_KNIGHT_4, UNIT_SIEGE_CULVERIN_4
- **French:** UNIT_HORSEMAN_2/3, UNIT_KNIGHT_2, UNIT_MANATARMS_3/4, UNIT_SPEARMAN_2, UNIT_ARCHER_2, UNIT_CROSSBOWMAN_3, UNIT_CANNON_4_ROYAL, UNIT_SHIELD_VILLAGER_CMP, UNIT_VILLAGER_1
- **French Leaders:** UNIT_BOUCICAUT_CMP (W1), UNIT_EDWARD_III_CMP + UNIT_JOHN_I_CMP (W2), UNIT_CHARLES_D_ALBRET_CMP (W3), UNIT_OLIVIER_ARREL_CMP + UNIT_CARON_DE_BOSDEGAS_CMP (speed modifiers only)
- **Abilities:** DEPLOY_PAVISE_FRE, JEANNE_D_ARC_AOE_DAMAGE_ABILITY_FRE_HA_01, LEADER_HEALING_ACTIVATED_LOWCD, LEADER_REDUCE_ARMOR_ACTIVATED_LOWCD, GENERAL_AURA_ARMOR, GENERAL_AURA_GUNPOWDER, LORD_OF_LANCASTER_AURA_LAN, LEADER_RALLY_YEOMEN_CMP_LAN, YEOMAN_SYNCHRONIZED_LAN
- **Custom Event:** `CE_AGINCOURTCONQ` — Sent on conqueror mode victory
