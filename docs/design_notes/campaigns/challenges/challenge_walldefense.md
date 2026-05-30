# Challenge Mission: Wall Defense

## OVERVIEW

The Wall Defense challenge mission is a Chinese-civilization Art of War scenario where the player must first construct a Wonder (Forbidden Palace), then defend it against 24 waves of Mongol attackers over a 900-second (15-minute) countdown timer. Three medal tiers (bronze at 300s, silver at 600s, gold at 900s) correspond to escalating wave groups that introduce progressively heavier siege. Concurrent patrol cavalry and ranged harassment waves provide flanking pressure alongside the main assault columns, which target the Wonder exclusively via custom AI attack plans. A 6-shot pre-intro cinematic demonstrates wall garrison, tower construction, cavalry sorties, siege tower assaults, and Chinese unique units before gameplay begins.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `challenge_mission_walldefense.scar` | core | Main mission logic: wave spawning, objectives, victory timer, resource trickle, AI attack plans, villager respawn, VO triggers |
| `challenge_mission_walldefense_preintro.scar` | other (cinematic) | Pre-intro cinematic with 6 scripted shots demonstrating wall defense techniques including garrison, towers, cavalry charges, and siege towers |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | core | Initializes wave data, timings, resource rates, unit lists |
| `Mission_SetupPlayers` | core | Creates 3 Imperial Age players with colors |
| `Mission_Preset` | core | Applies upgrades, restrictions, spawns units, destroys TC |
| `Mission_Start` | core | Heals walls, starts objectives, registers villager respawn |
| `GetRecipe` | core | Returns mission recipe with pre-intro NIS event |
| `WallD_InitObjectives` | core | Defines ConstructWonder, Victory, and tip objectives |
| `WallD_SpawnPlayerUnits` | core | Deploys 8 villagers and 3 imperial officials |
| `WallD_SpawnWaves` | core | Pre-spawns all waves in tier to north/south positions |
| `WallD_SendWave` | core | Dispatches next wave via RovingArmy along routes |
| `WallD_PatrolWaves` | core | Spawns cavalry patrol waves on flanking paths |
| `WallD_RangedWaves` | core | Spawns ranged harassment waves near walls |
| `WallD_CheckRangedName` | core | Validates if module name matches ranged wave pattern |
| `WallD_CheckArchersBlocked` | core | Monitors ranged modules, splits blocked units off |
| `WallD_CheckIdleRanged` | core | Reassigns idle ranged units to nearby targets |
| `WallD_ArchersBlocked` | core | Callback: removes blocked ranged from RovingArmy |
| `WallD_TimerComplete` | core | Completes victory objective when 900s timer expires |
| `WallD_AwardResources` | core | Grants bonus food/wood/gold/stone to player |
| `WallD_StartBronze` | core | Initiates bronze tier, sends first wave |
| `WallD_StartSilver` | core | Initiates silver wave tier spawning |
| `WallD_StartGold` | core | Initiates gold wave tier spawning |
| `WallD_BronzeComplete` | core | Fires bronze intel, starts silver, doubles trickle |
| `WallD_SilverComplete` | core | Fires silver intel, starts gold, triples trickle |
| `WallD_HealWalls` | core | Transfers walls to player1, heals to full HP |
| `WallD_WallsDamagedCheck` | core | Fires VO event when walls first take damage |
| `WallD_ApproachingWaveContains` | core | Checks if nearby enemies contain a blueprint type |
| `WallD_TrickleResources` | core | Periodic scaled resource income every 5 seconds |
| `_WallD_QueueVillagerRespawn` | core | GE_SquadKilled handler queuing villager respawn |
| `WallD_VillagerRespawn` | core | Respawns one villager if below 8 and pop available |
| `WallD_SpawnUnspawnedVillagers` | core | Handles deferred spawns when pop cap temporarily full |
| `WallD_ResetVillagerCTA` | core | Resets villager CTA cooldown boolean |
| `WallD_TraderLoop` | core | Spawns cosmetic trader carts on looping route |
| `WallD_RamCheck` | core | VO trigger when rams approach player gates |
| `WallD_TowerCheck` | core | VO trigger when siege towers approach gates |
| `WallD_MangonelCheck` | core | VO trigger when mangonels approach gates |
| `WallD_TrebuchetCheck` | core | VO trigger when trebuchets/bombards approach gates |
| `WallD_SpendResources1` | core | VO reminder to spend resources post-bronze |
| `WallD_SpendResources2` | core | VO reminder to spend resources post-silver |
| `Walld_Disable_Tax` | core | Toggles auto-collect tax then removes ability |
| `MissionOMatic_PreStart_IntroNISFinished` | core | Override: checks cinematic completion to release hold |
| `WallD_Intro_Spawn` | preintro | Places and instant-constructs Forbidden Palace wonder |
| `WallD_PreIntro_Shot01_Units` | preintro | Deploys wall garrison and attacking infantry scene |
| `WallD_PreIntro_Shot01_CleanUp` | preintro | Destroys shot 1 enemy and infantry squads |
| `WallD_PreIntro_Shot02_Units` | preintro | Deploys enemies, builds tower, stages tower attack |
| `WallD_PreIntro_Shot02_AttackTower` | preintro | Redirects enemies to attack stone wall tower |
| `WallD_PreIntro_Shot01b_HoldPosition` | preintro | Instant-setups team weapons for background groups |
| `WallD_PreIntro_Shot01b` | preintro | Weakens enemies to 10% HP, grants Murder Holes |
| `WallD_PreIntro_Shot02_CleanUp` | preintro | Destroys shot 2 enemies, heals tower to full |
| `WallD_PreIntro_Shot03_Units` | preintro | Deploys rams and cavalry for charge vignette |
| `WallD_PreIntro_Shot03_CavalryCharge` | preintro | Cavalry attack-move toward enemy spawn (6s delay) |
| `WallD_PreIntro_Shot03_CleanUp` | preintro | Destroys shot 3 squads, heals tower |
| `WallD_PreIntro_Shot04_Units` | preintro | Deploys mangonels, cavalry, and counter-forces |
| `WallD_PreIntro_Shot04_b` | preintro | Spawns 20 reinforcing spearmen (8s delay) |
| `WallD_PreIntro_Shot04_c` | preintro | Background enemies charge gate (14s delay) |
| `WallD_PreIntro_Shot04_CleanUp` | preintro | Destroys all shot 4 squads |
| `WallD_PreIntro_Shot05_Units` | preintro | Deploys 3 siege tower RovingArmy modules |
| `WallD_PreIntro_Shot05_CleanUp` | preintro | Destroys all siege tower and archer squads |
| `WallD_PreIntro_Shot06_Units` | preintro | Deploys Chinese unique units demonstration |
| `WallD_PreIntro_Shot06_CleanUp` | preintro | Destroys shot 6 squads, removes Murder Holes |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_ConstructWonder` | `ObjectiveType_Battle` | Build the Forbidden Palace Wonder before waves begin |
| `SOBJ_SpendResources` | `ObjectiveType_Tip` | Hint: spend resources on defenses before Wonder completes |
| `SOBJ_QuickBuild` | `ObjectiveType_Tip` | Hint: units and tech complete instantly until Wonder built |
| `OBJ_Victory` | `ObjectiveType_Battle` | Survive the 900s countdown; fails if Wonder destroyed |

### Difficulty

No `Util_DifVar` usage. Difficulty is implicit through the escalating wave/medal tier system:

| Tier | Time Window | Waves | Key Threats |
|------|-------------|-------|-------------|
| Bronze | 0–300s | 1–8 | Rams, spearmen, men-at-arms, springalds, traction trebuchet |
| Silver | 300–600s | 9–16 | Siege towers, mangonels, larger infantry groups, trebuchets |
| Gold | 600–900s | 17–24 | Bombards, hand cannoneers, massive combined siege forces |

Resource trickle multiplier scales with tier: 1x (bronze), 2x (silver), 3x (gold).

### Spawns

**Player (Chinese, Imperial Age)**:
- 8 villagers (2 groups of 4), auto-respawn 30s after death (capped at 8)
- 3 imperial officials with auto-collect tax toggled then ability stripped
- Starting resources: 3000 food, 2400 wood, 2400 gold, 600 stone
- Pop cap override: 200
- Production rate modifier: 1000x until Wonder built
- Full Imperial upgrades for spearmen, archers, horsemen, horse archers, knights, crossbowmen, fire lancers, zhuge nu
- Town center destroyed at start; multiple economy buildings and naval production removed
- Walls initially owned by player3, transferred and healed to player1 at mission start

**Enemy Main Waves (Mongol, Imperial Age)** — dispatched at ~30.4s intervals (`(900-200)/23`), alternating north/south spawns:

**Bronze (waves 1–8):**

| Wave | Composition |
|------|-------------|
| 1 | 1 ram |
| 2 | 4 spearmen, 1 ram |
| 3 | 4 spearmen, 2 men-at-arms |
| 4 | 4 spearmen, 2 men-at-arms |
| 5 | 8 spearmen, 1 ram |
| 6 | 4 spearmen, 1 springald, 1 ram |
| 7 | 8 spearmen, 1 springald, 1 ram |
| 8 | 8 spearmen, 4 men-at-arms, 2 rams, 1 traction trebuchet |

**Silver (waves 9–16):**

| Wave | Composition |
|------|-------------|
| 9 | 1 siege tower, 8 men-at-arms |
| 10 | 1 siege tower, 8 men-at-arms, 4 archers |
| 11 | 1 mangonel, 1 ram, 8 men-at-arms |
| 12 | 2 mangonels, 1 ram, 8 men-at-arms, 3 spearmen |
| 13 | 1 mangonel, 1 ram, 1 springald, 8 spearmen |
| 14 | 1 mangonel, 1 ram, 1 siege tower, 8 spearmen, 4 men-at-arms |
| 15 | 1 traction trebuchet, 4 men-at-arms, 8 spearmen |
| 16 | 2 traction trebuchets, 4 men-at-arms, 8 spearmen |

**Gold (waves 17–24):**

| Wave | Composition |
|------|-------------|
| 17 | 2 rams, 1 mangonel, 1 springald |
| 18 | 1 ram, 1 bombard, 4 men-at-arms, 8 spearmen |
| 19 | 1 mangonel, 1 ram, 1 bombard, 8 spearmen, 4 hand cannoneers |
| 20 | 1 mangonel, 1 springald, 1 ram, 1 bombard, 4 men-at-arms, 8 hand cannoneers |
| 21 | 2 bombards, 1 traction trebuchet, 1 ram, 1 siege tower, 4 men-at-arms, 8 spearmen |
| 22 | 2 bombards, 1 traction trebuchet, 1 mangonel, 1 ram, 4 men-at-arms, 8 spearmen, 1 springald |
| 23 | 2 bombards, 1 traction trebuchet, 1 ram, 4 men-at-arms, 8 spearmen, 1 springald |
| 24 | 1 bombard, 1 mangonel, 1 traction trebuchet, 1 ram, 1 siege tower, 8 men-at-arms, 8 spearmen, 8 archers, 1 springald |

**Patrol Waves** (spawned every other main wave, 12 total compositions):

| Wave | Composition |
|------|-------------|
| 1–2 | 6 horsemen |
| 3 | 6 crossbowmen |
| 4 | 4 knights |
| 5 | 6 horse archers |
| 6 | 6 horsemen, 6 knights |
| 7 | 6 hand cannoneers |
| 8 | 6 horse archers, 6 knights |
| 9 | 8 archers, 6 hand cannoneers |
| 10 | 8 horse archers, 8 knights |
| 11 | 8 crossbowmen, 6 hand cannoneers |
| 12 | 8 horse archers, 8 horsemen, 8 knights |

Patrol targets alternate between `mkr_mongol_horse_patrol_2` and `mkr_mongol_horse_patrol_3` based on wave index modulo 4. Use `attackMoveStyle_attackEverything` with `onDeathDissolve`.

**Ranged Waves** (spawned every other main wave, 12 total compositions):

| Wave | Composition |
|------|-------------|
| 1 | 8 archers |
| 2 | 8 archers, 1 mangonel |
| 3 | 8 crossbowmen, 1 mangonel |
| 4 | 8 crossbowmen, 1 springald |
| 5–6 | 12 archers, 1 mangonel |
| 7–8 | 12 crossbowmen, 1 springald |
| 9 | 16 archers, 1 mangonel |
| 10 | 16 crossbowmen, 1 mangonel |
| 11 | 16 crossbowmen, 1 springald, 1 mangonel |
| 12 | 16 archers, 1 springald, 1 mangonel |

Ranged waves alternate between two spawn/path pairs and use `WallD_ArchersBlocked` callback when pathfinding is blocked.

### AI

- No `AI_Enable`. All enemy behavior is scripted via `RovingArmy` modules.
- Main waves use custom `attackMoveStyle_targetWonder`:
  - **En route**: `attackMoveStyle_ignoreEverything` — waves do not engage while traveling.
  - **At target**: targets only the Wonder; excludes houses, farms, settlements, walls, production/economy/research/defensive structures. Uses `ai_formation_coordinator_challenge_attack_wonder_only`.
  - `scanRange = 30`, `allowAttackMove = false` to prevent distraction.
- After wave 16, routing switches from 2 lanes (north/south direct) to 4 lanes (north/south with alternate left/right flanking paths).
- All main waves set to `core_formation_spread` after initialization.
- Patrol waves use `attackMoveStyle_attackEverything` with `onDeathDissolve = true` — they dissolve when destroyed rather than respawning.
- Ranged waves have `onBlockedFunction = WallD_ArchersBlocked`:
  - Blocked ranged units are removed from their RovingArmy module and placed in `sg_idleRanged`.
  - `WallD_CheckIdleRanged` individually retargets idle ranged to nearby player units within 50 range (preferring ranged targets), or attack-moves toward the Wonder if no valid targets found.
  - Split units are prevented from merging back for 3 seconds after splitting.
  - `cavalryCanBuildRams = false` prevents ranged wave units from constructing rams.
- Enemy outposts upgraded with `UPGRADE_OUTPOST_CANNON_MON` at map start.
- FOW fully revealed for player2 (`FOW_PlayerRevealAll`).
- Each spawned wave SGroup is FOW-revealed to the player with radius 20.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| `Objective_StartTimer(OBJ_Victory, COUNT_DOWN, 900)` | 900s | Main victory countdown displayed to player |
| `Rule_AddInterval(WallD_SendWave, waveSpawnInterval)` | ~30.4s | Dispatches next pre-spawned wave from queue |
| `Rule_AddOneShot(WallD_BronzeComplete, 300)` | 300s | Transitions to silver tier, fires intel event |
| `Rule_AddOneShot(WallD_SilverComplete, 600)` | 600s | Transitions to gold tier, fires intel event |
| `Rule_AddOneShot(WallD_TimerComplete, 900)` | 900s | Completes `OBJ_Victory`, triggers mission win |
| `Rule_AddInterval(WallD_TrickleResources, 5)` | 5s | Trickles scaled food/wood/gold/stone to player |
| `Rule_AddInterval(WallD_TraderLoop, 10)` | 10s | Spawns cosmetic trader carts on loop |
| `Rule_AddInterval(WallD_CheckArchersBlocked, 1)` | 1s | Monitors all ranged modules for wall-blocked units |
| `Rule_AddInterval(WallD_RamCheck, 4)` | 4s | VO trigger when rams detected near gates |
| `Rule_AddInterval(WallD_WallsDamagedCheck, 4)` | 4s | VO trigger when walls first take damage |
| `Rule_AddInterval(WallD_TowerCheck, 4)` | 4s | VO trigger when siege towers detected near gates |
| `Rule_AddInterval(WallD_MangonelCheck, 4)` | 4s | VO trigger when mangonels detected near gates |
| `Rule_AddInterval(WallD_TrebuchetCheck, 4)` | 4s | VO trigger when trebuchets/bombards detected |
| `Rule_AddOneShot(WallD_VillagerRespawn, 30)` | 30s | Respawns dead villager after delay |
| `Rule_AddOneShot(WallD_ResetVillagerCTA, 60)` | 60s | Resets villager CTA cooldown flag |
| `Rule_AddInterval(WallD_SpendResources1, {delay=60, interval=1})` | 60s delay, 1s poll | VO reminder to spend resources post-bronze |
| `Rule_AddInterval(WallD_SpendResources2, {delay=60, interval=1})` | 60s delay, 1s poll | VO reminder to spend resources post-silver |
| `Rule_AddOneShot(Walld_Disable_Tax, 0)` | next frame | Disables official auto-tax ability on spawn |
| `Rule_AddOneShot(_WallD_DelayTraderDepart, 8)` | 8s | Trader departs after brief market pause |
| `Rule_AddInterval(WallD_SpawnUnspawnedVillagers, 2)` | 2s | Retries deferred villager spawns when pop frees |

### Pre-Intro Cinematic System

The pre-intro consists of 6 choreographed shots demonstrating wall defense concepts:

| Shot | Theme | Player Units (Chinese) | Enemy Units |
|------|-------|------------------------|-------------|
| 1 | Wall garrison defense | 8 spearmen (gate), 8 zhuge nu, 8 archers, 10 crossbowmen (walls) | 30 spearmen + men-at-arms (3 groups, 30% HP, weapons disabled) |
| 2 | Tower defense | — (tower built by player3) | 24 spearmen + 6 men-at-arms (25% HP, +25% range); 2 background groups (archers + men-at-arms + mangonels) |
| 3 | Cavalry sortie vs rams | 15 horsemen | 3 rams (40% HP) |
| 4 | Counter-siege (mangonels) | 20 horsemen | 3 mangonels (60% HP); 20 spearmen reinforcements (8s); background groups charge (14s) |
| 5 | Siege tower assault | Archers on walls (reduced to 20% HP) | 3 siege tower groups (8 spearmen + 1 siege tower each) via RovingArmy |
| 6 | Chinese unique units | 8 fire lancers, 8 zhuge nu, 8 grenadiers, 3 nest of bees | 24 archers |

- Shot 1: Player infantry have weapons disabled (cosmetic melee only). Walls temporarily transferred to player3 during cinematic.
- Shot 2: A Chinese defense tower is instant-constructed via `Modify_EntityConstructionTime(0.1)` + `Entity_ForceSelfConstruct`. Murder Holes upgrade applied via `WallD_PreIntro_Shot01b` at 16s.
- Shot 5: Uses `RovingArmy_Init` with `ARMY_TARGETING_DISCARD` to path siege towers toward wall targets.
- Shot 6: Nest of Bees spawned via explicit blueprint `unit_nest_of_bees_4_chi`.
- `WallD_Intro_Spawn`: Places and instant-constructs the Forbidden Palace wonder, making it available for gameplay. Construction cancel is disabled via `Entity_DisableCancelConstructionCommand`.

## CROSS-REFERENCES

### Imports

**core (`challenge_mission_walldefense.scar`)**:
- `MissionOMatic/MissionOMatic.scar` — Cardinal framework
- `MissionOMatic/MissionOMatic_utility.scar` — utility functions
- `missionomatic/missionomatic_artofwar.scar` — Art of War challenge framework
- `challenge_mission_walldefense_preintro.scar` — pre-intro cinematic
- `challenge_mission_walldefense.events` — event/intel definitions
- `training/coretraininggoals.scar` — training goal framework

**preintro (`challenge_mission_walldefense_preintro.scar`)**:
- `MissionOMatic/MissionOMatic.scar` — Cardinal framework

### Shared Globals

- `player1` / `player2` / `player3` — Chinese player, Mongol enemy, ally/wall owner (all Imperial Age)
- `sg_player_villagers` — villager SGroup shared across respawn system
- `sg_player_traders` — trader SGroup for cosmetic loop
- `sg_player_officials` — official SGroup with tax abilities stripped
- `eg_player_wonder` — Wonder EGroup used by both preintro spawn and victory condition
- `eg_player_walls` — wall EGroup transferred between preintro and core
- `sg_idleRanged` — SGroup holding ranged units split from blocked RovingArmy modules
- `waveModuleTable` — table of active RovingArmy modules for main waves
- `waveSGroups` — queue of pre-spawned SGroups awaiting dispatch
- `unitList` — nested table (bronze/silver/gold) defining all 24 wave compositions
- `patrolWaveUnits` — table of 12 patrol wave compositions
- `rangedWaveUnits` — table of 12 ranged wave compositions
- `waveSentCount` / `waveSpawnedCount` / `medalWaveCount` — wave tracking counters
- `trickleIncomeMult` — resource trickle multiplier (1/2/3 by tier)
- `bool_CTACooldown` — prevents duplicate villager respawn CTA events
- `wallDArcherSplitTime` — timestamp preventing premature idle-ranged merging
- `attackMoveStyle_targetWonder` — custom AI attack plan targeting only the Wonder
- `EVENTS` — event table from `.events` import (PreIntro, WaveStart, BronzeComplete, SilverComplete, WallsDamaged, Rams, SiegeTowers, Mangonels, Trebuchets, SpendResources1, SpendResources2)
- `cinematicFinished` — boolean flag checked by `MissionOMatic_PreStart_IntroNISFinished`

### Inter-File Function Calls

- Core → Preintro: `WallD_Intro_Spawn()` called from pre-intro event sequence to place Wonder
- Core → Preintro: `WallD_PreIntro_Shot*` functions called by the `EVENTS.PreIntro` cinematic event sequence
- Preintro → Core: reads/writes shared globals (`player1`, `player2`, `player3`, `eg_player_walls`, `eg_player_wonder`)
- Core overrides `MissionOMatic_PreStart_IntroNISFinished` to gate mission start on `cinematicFinished` flag
- `Missionomatic_ChallengeInit` called with `kpiType = "countDown"` and medal time thresholds
- `SpawnUnitsToModule` used in preintro Shot 5 to deploy siege tower groups into RovingArmy modules

### Notable Implementation Details

- Wonder completion (`EGroup_GetAvgHealth == 1.0`) triggers transition from build phase to defense phase — production rate modifier is removed and the 900s countdown starts.
- `waveSpawnInterval` is computed as `math.floor((900 - 200) / 23) ≈ 30` seconds, evenly distributing 24 waves across the defense phase minus a travel-time buffer.
- All waves are pre-spawned at the start of each tier via `WallD_SpawnWaves`, then dispatched one at a time by the interval rule.
- The ranged-blocked system (`WallD_ArchersBlocked` / `WallD_CheckIdleRanged` / `WallD_CheckArchersBlocked`) implements a custom micro-AI for ranged units that cannot path through walls: they split off, fight independently, and attempt to merge back after 3 seconds of inactivity.
- Villager respawn system handles pop cap overflow by queuing unspawned villagers and retrying via `WallD_SpawnUnspawnedVillagers` every 2 seconds.
- VO event triggers (`RamCheck`, `TowerCheck`, etc.) each fire once and self-remove, with a 30-second global cooldown (`eventCD`) between any two VO events.
- Cosmetic trader carts spawn every 10 seconds, pause at market for 8 seconds, then `Cmd_MoveToAndDestroy` back to spawn.
