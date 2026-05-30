# Difficulty Index

Consolidation of all difficulty-scaling parameters across campaign missions, extracted from Phase 3 summaries.

## API Reference

### `Util_DifVar({easy, normal, hard, expert})`

The primary difficulty-scaling function used across all standard campaign missions. Takes a 4-element array and selects one value based on `Game_GetSPDifficulty()`. Used throughout for timing, unit counts, resource amounts, and thresholds.

Three difficulty mechanisms exist in the MissionOMatic system:
1. **`Util_DifVar` value selection** — picks one of 4 values from an array based on current difficulty setting
2. **Wave `difficulty` field** — per-unit filtering that removes units not matching current difficulty (via `Wave_FilterUnitsByDifficulty`)
3. **Module `difficulty` field** — conditional initialization of entire modules based on difficulty level

### `Rogue_DifVar({d1, d2, d3, d4, d5, d6, d7, d8})`

Used exclusively in the Rogue campaign, which has a 7–8 tier difficulty system (unlike the standard 4-tier). Takes up to 8 values.

---

## By Campaign

### Abbasid Dynasty

#### abb_bonus

Tiers: **Easy → Expert** (4 levels)

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `researchLevel` | 1 | 2 | 3 | 4 | P2/P5 outpost upgrade tiers at mission start |
| `researchInterval` | 420 | 360 | 300 | 240 | Seconds between P2 auto-tech-upgrades |
| `econMod` | 0.55 | 0.70 | 0.85 | 1.0 | P2 economy strength ramp multiplier |
| `unitCount_low` | 2 | 3 | 4 | 5 | Squad count for small army/patrol modules |
| `unitCount_med` | 4 | 6 | 8 | 10 | Squad count for medium army modules |
| `unitCount_high` | 6 | 9 | 12 | 15 | Squad count for large army modules |
| `raidSpawnMod` | 1.6 | 1.4 | 1.2 | 1.0 | Raider spawn delay multiplier (higher = slower) |
| `extraVillagerCount` | 0 | 0 | 0 | 0 | Location extra villagers (unused) |

---

#### abb_m1_tyre

Tiers: **Easy → Expert** (4 levels, labeled Easy/Hardest in source)

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `villager_speed` | 0.8 | — | — | 1.0 | Enemy villager movement speed multiplier |
| `villager_reaction_delay` | 4s | — | — | 2.5s | Delay before villagers flee from player |
| `camp_max_garrison` | 1 | — | — | 4 | Max villagers garrisoning per outpost |
| `skirmish_spawn_delay` | 15s | — | — | 4s | Delay between skirmish wave spawns |
| `skirmish_attack_threshold` | 10 | — | — | 20 | Unit count before skirmish army attacks |
| `skirmish_unit_mix_cap` | 1 | — | — | 6 | Cap on advanced unit types in skirmish waves |
| `ram_weapon_cooldown` | 2s | — | — | 1s | Ram attack cooldown |
| `ram_health_multiplier` | 1 | — | — | 1.5 | Ram HP multiplier |
| `research_level` | 1 | — | — | 4 | Enemy tech level |
| `ambushes_trigger` | false | — | true | true | Whether ambushes activate (Hard/Expert only) |
| `ambush_delay` | 120s | — | — | 30s | Time before ambush army attacks |
| `enemy_resource_target` | 2000 | — | — | 5000 | Resources Franks need before assault |
| `enemy_gather_delay` | 20s | — | — | 7s | Interval for enemy resource tick |
| `numSquads_*` | varies | — | — | varies | 20+ scaling params for army/escort/ram counts |

> Note: Source lists only Easy→Expert endpoints. Intermediate values follow linear interpolation across 4 tiers.

---

#### abb_m2_egypt

Tiers: **Easy / Normal / Hard / Expert**

**Player Mods:**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `STARTING_SPEARMEN` | 10 | 10 | 5 | 5 | Initial player spearmen |
| `STARTING_ARCHERS` | 10 | 10 | 5 | 5 | Initial player archers |
| `STARTING_HORSEMEN` | 10 | 10 | 5 | 5 | Initial player horsemen |

**Enemy Mods:**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `STARTING_SPEARMEN` | 40 | 40 | 50 | 80 | Initial enemy spearmen |
| `STARTING_ARCHERS` | 100 | 100 | 100 | 80 | Initial enemy archers |
| `STARTING_MANATARMS` | 20 | 30 | 40 | 50 | Initial enemy MaA |
| `STARTING_HORSEMEN` | 20 | 50 | 40 | 50 | Initial enemy horsemen |
| `STARTING_ARMYBUDGET` | 20 | 30 | 50 | 75 | Initial enemy reinforcement budget |
| `attack_group_size` | 10 | 10 | 10 | 15 | Units per enemy attack wave |
| `ATTACK_GROUP_SIZE_ACCELERATION` | 0 | 5 | 5 | 10 | Group size increase per 300s |
| `ATTACK_GROUP_SIZE_CEILING` | 10 | 20 | 40 | 50 | Max attack group size |
| `ATTACK_INTERVAL` | 20 | 20 | 20 | 15 | Seconds between enemy squad spawns |
| `ATTACK_ACCELERATION` | 5 | 5 | 10 | 5 | Interval reduction per 300s |
| `ATTACK_INTERVAL_FLOOR` | 15 | 10 | 5 | 5 | Minimum attack interval |
| `QUADRANT_COOLDOWN` | 90 | 90 | 30 | 10 | Cooldown between same-quadrant reassign |
| `HOSTILECHECK_RADIUS` | 100 | 100 | 100 | 100 | Scan radius for heatmap |
| `AVOID_HOSTILE_COUNT_MULITPLIER` | 0 | 1 | 1.5 | 2 | Weight of hostile presence in targeting |
| `RANGE_PRIORITY_MULTIPLIER` | 1.5 | 1 | 0.5 | 0 | Weight of distance in targeting |
| `AI_AGGRESSION_EMPTYLOCATION` | 200 | 1200 | 2000 | 10 | Heat bonus for undefended points |
| `AI_AGGRESSION_WEAKLOCATION` | 200 | 400 | 800 | 1200 | Heat bonus for weak points |
| `AI_AGGRESSION_FORTIFIEDLOCATION` | 200 | 400 | 400 | 800 | Heat bonus for fortified points |
| `AI_AGGRESSION_LOSINGMULTIPLIER` | 1 | 1.2 | 2 | 3 | Aggression boost when AI holds <5 points |

---

#### abb_m3_redsea

Tiers: **Story / Easy / Intermediate / Hard**

| Parameter | Story | Easy | Hard | Expert | Scales |
|-----------|-------|------|------|--------|--------|
| `victoryGoldThreshold` | 30k | 30k | 35k | 35k | Gold to win |
| `productionSpeedBonus` | 2.0x | — | — | 1.0x | Player production speed |
| `unrestStartValue` | 0.05 | — | — | 0.15 | Starting unrest level |
| `extraGuidance` | true | true | false | false | Tip objectives shown |
| `raiderWaveInterval` | 6min | — | — | 3min | Wave spacing (decays 0.2/wave, min 0.4x) |
| `raiderWaveCleanupTime` | 8min | — | — | 5min | Wave cleanup timeout |
| `raiderCampSpearmen` | 6 | — | — | 10 | Coastal camp spearmen garrison |
| `raiderCampArchers` | 4 | — | — | 8 | Coastal camp archer garrison |
| `raiderFleetGalleys` | ~2 | — | — | ~8 | Fleet galley count |
| `raiderFleetHulks` | ~2 | — | — | ~8 | Fleet hulk count |
| `raiderFleetSiegeGalleys` | ~2 | — | — | ~8 | Fleet siege galley count |
| `raiderDemolishers` | 2 | — | — | 12 | Demolition ships |
| `raiderMarinesCount` | 8 | — | — | 48 | Marine landing party size |
| `raiderMarinesSiege` | Springald | — | — | Mangonel | Siege type for marines |
| `raiderReynaldHulks/Galleys` | varies | — | — | varies | Reynald escort fleet sizes |
| `raiderFinale*` | varies | — | — | varies | Finale fleet sizes, prep 300s→60s, net mult 1.0→2.0 |
| `pirateRespawnDelay` | 90s | — | — | 15s | Pirate respawn timer |
| `pirateHunter*` | varies | — | — | varies | Pirate hunter/patrol fleet composition |
| `pirateLandUnits1-3/Siege` | varies | — | — | varies | Pirate island garrison sizes |
| `pirateOutpostWeapons` | Arrowslits | — | — | Springald | Outpost upgrade tier (stone on Hard+) |
| Military build time mult | 0.5 | 0.75 | 1 | 1 | Build speed bonus |

**Difficulty-conditional logic:** Easy/Story restricts raider routes to 4 (vs 6 on higher difficulties). `PlayerUpgrades_ApplyHealthBonuses` applies health bonuses based on difficulty and console.

---

#### abb_m4_hattin

Tiers: **Easy / Medium / Normal / Hard**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `extraGuidance` | true | true | false | false | Enables placement/build guidance objectives |
| `emergencyReinforcements` | true | false | false | false | Auto-spawns cavalry when troops < 40 (Easy only) |
| `playerStartFood` | 1400 | 1200 | 1000 | 800 | Starting food |
| `playerStartWood` | 1000 | 800 | 700 | 600 | Starting wood |
| `playerStartGold` | 1000 | 800 | 700 | 600 | Starting gold |
| `playerStartStone` | 800 | 800 | 500 | 500 | Starting stone |
| `productionSpeedBonus` | 2.0 | 1.8 | 1.25 | 1.0 | Military build time multiplier |
| `playerFarmerStart` | 8 | 6 | 5 | 3 | Starting farmer villagers per group |
| `crusadePrepTime` | 180 | 120 | 90 | 90 | Seconds before first wave |
| `crusaderHasSiege` | 0 | 1 | 1 | 1 | Whether crusaders bring siege |
| `crusaderWaveInterval` | 120 | 90 | 90 | 90 | Seconds between waves |
| `crusaderDifficultyTopUp` | 0 | 0 | 5 | 10 | Extra squads per group |
| `crusaderDifficultyTopUpHolyOrders` | 0 | 0 | 2 | 6 | Extra holy order squads |
| `smokeDebuffDuration` | 90 | 75 | 60 | 45 | Seconds debuff lasts |
| `smokeDebuffSpeed` | 0.5 | 0.5 | 0.5 | 0.5 | Speed multiplier on debuffed units |
| `smokeDebuffDmgDealt` | 0.1 | 0.2 | 0.5 | 0.6 | Damage dealt multiplier when debuffed |
| `smokeDebuffDmgReceived` | 4.0 | 3.0 | 3.0 | 3.0 | Damage received multiplier when debuffed |
| `fieldBurndownTime` | 120 | 90 | 60 | 60 | Seconds until field expires |
| `hornsOfHattinBurnTime` | 180 | 120 | 90 | 75 | Final field burn duration |

---

#### abb_m5_mansurah

Tiers: **Easy / Normal / Hard / Expert**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `ENEMY_REINFORCEMENT_DELAY` | -1 (off) | -1 (off) | 800 | 400 | Seconds before dead camp followers respawn |
| `INVASION_DELAY_AFTER_TRANSITION` | 200 | 180 | 160 | 140 | Seconds before first invasion wave |
| `INVASION_INTERVAL` | 300 | 270 | 240 | 210 | Seconds between invasion waves |
| `COST_UPPER` | 900 | 1200 | 1750 | 2400 | Max resource cost threshold for active enemies |
| Front army unit counts | 5 | 6 | 9 | 12 | Per-army squad count for defending/camp |
| Holy order Teuton count | 14 | 16 | 22 | 28 | Teuton holy order members |
| Holy order Hosp/Temp count | 7 | 8 | 11 | 14 | Hospitaller/Templar counts |
| Starting resources (wood/food) | 350 | 300 | 250 | 200 | Player starting resources |
| Starting stone | 150 | 100 | 50 | 0 | Player starting stone |
| Military build time modifier | 0.5 | 0.75 | 1 | 1 | Ayyubid build time multiplier |
| Attack lanes | North only | North only | W/N/E | W/N/E | Number of invasion approach lanes |
| Enemy military upgrades | 0 | 0 | 1 | 2 | Military upgrade level for player2 |
| `DEFAULT_IDLE_DELAY` | 3 | 2.5 | 2 | 1.5 | Patrol idle delay for single units |

---

#### abb_m6_aynjalut

Tiers: **Easy / Normal / Hard / Hardest**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `player_prepare_time` | 60 | 52 | 46 | 40 | Seconds of warning before each wave |
| `ARMY_SIZE_*` (8 tiers) | varies | varies | varies | varies | numRanks/numFiles/extra/numSquads per tier |
| `ARMY_SIZE_*_SPECIAL` (3 tiers) | varies | varies | varies | varies | Crusader/special force scaling |
| Player upgrades | diff ≤ 2 | diff ≤ 1 | diff ≤ 0 | none | Extra ranged/melee damage upgrades on easier |
| `Player_ModifyAyyubidMilitaryBuildTimes` | 0.5 | 0.75 | 1 | 1 | Faster military build on easier difficulties |

> The `ARMY_SIZE_*` parameters use a complex nested format with numRanks/numFiles/extra/numSquads per force tier—see the full mission doc for specific values.

---

#### abb_m7_acre

Tiers: **Easy / Normal / Hard / Expert**

**Player Mods:**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `STARTING_SPEARMEN` | 20 | 20 | 20 | 20 | Initial spearmen |
| `STARTING_ARCHERS` | 20 | 20 | 20 | 30 | Initial archers |
| `STARTING_HORSEMEN` | 12 | 12 | 12 | 12 | Initial horsemen |
| `STARTING_MANATARMS` | 20 | 20 | 10 | 10 | Initial MaA |
| `STARTING_KNIGHTS` | 20 | 20 | 16 | 10 | Initial knights |
| `STARTING_MANGONELS` | 4 | 3 | 3 | 2 | Initial mangonels |
| `STARTING_TREBUCHETS` | 3 | 2 | 2 | 1 | Initial trebuchets |
| `STARTING_VILLAGERS` | 11 | 9 | 7 | 4 | Wood-gathering villagers |
| `BERRY_VILLAGERS` | 5 | 3 | 0 | 0 | Berry villagers (mill removed on Hard+) |
| `RES_TRICKLE_AMOUNT` | 800 | 500 | 500 | 300 | Gold/food/wood trickle per min (disabled) |
| `ALLY_RESPAWN_DELAY` | 2 | 5 | 6 | 10 | Seconds before allied respawn check |
| `RES_PICKUP_SPAWN_CHANCE_NAVAL` | 1 | 1 | 2 | 4 | Ship kills per wood pickup (lower = more) |
| `RES_PICKUP_SPAWN_AMOUNT_LAND` | 3 | 3 | 2 | 1 | Stone pickups per building kill |

**Enemy Mods:**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `ACRE_COMMON_INFANTRY_SIZE` | 4 | 4 | 4 | 6 | Spearmen per defender group |
| `ACRE_COMMON_INFANTRY_SGT` | 0 | 1 | 2 | 3 | MaA sergeants per infantry group |
| `ACRE_ELITE_INFANTRY_SIZE` | 4 | 4 | 4 | 6 | Elite infantry per group |
| `ACRE_ELITE_INFANTRY_SGT` | 0 | 1 | 2 | 3 | Teutonic elite per group |
| `ACRE_ARCHER_SIZE` | 4 | 5 | 6 | 8 | Archers per wall garrison |
| `ACRE_ANTISIEGE_ENGINE_SIZE` | 0 | 1 | 1 | 2 | Springalds per anti-siege point |
| `ACRE_ANTISIEGE_GUARD_SIZE` | 0 | 2 | 4 | 8 | Guards per anti-siege point |
| `ACRE_CAVALRY_PATROL_SIZE` | 4 | 4 | 4 | 6 | Horsemen per patrol |
| `ACRE_CAVALRY_PATROL_SGT` | 0 | 1 | 2 | 3 | Knights per patrol |
| `ACRE_SHIP_SIZE` | 3 | 2 | 3 | 4 | Galleys per ship group |
| `ACRE_ELITE_SHIP_SIZE` | 0 | 1 | 1 | 2 | Hulks per ship group |
| `ACRE_GENOESE_CROSSBOWS_PERBOAT` | 10 | 9 | 6 | 5 | Crossbowmen per transport |
| `ACRE_GENOESE_SGT_PERBOAT` | 0 | 1 | 1 | 2 | MaA per Genoese transport |
| `ACRE_GENOESE_TRANSPORTS_PERSPAWN` | 1 | 1 | 2 | 4 | Transports per spawn point |
| `ACRE_ENEMY_REINFORCEMENT_TIMER` | 120 | 60 | 40 | 35 | Seconds between enemy respawns |
| `ACRE_ENEMY_NAVAL_REINFORCEMENT_TIMER` | 0 | 0 | 240 | 180 | Naval reinforcement interval (Hard+ only) |
| `ACRE_ATTACK_WAVE_TIMER` | 120 | 120 | 90 | 90 | Seconds between attack waves |
| `ACRE_ATTACK_WAVE_DELAY` | 180 | 180 | 120 | 120 | Initial delay before first wave |
| `COUNTER_ATTACK_TIMER` | 600 | 400 | 300 | 300 | Seconds between counter-attacks |
| `COUNTER_ATTACK_INITIAL_AMOUNT` | 4 | 4 | 6 | 6 | Armies redirected per counter-attack |
| `COUNTER_ATTACK_RAMP_AMOUNT` | 0 | 0.5 | 1 | 1.5 | Additional armies per subsequent counter |
| `NAVAL_ATTACK_TIMER` | 0 | 0 | 120 | 120 | Marine landing interval (Hard+ only) |
| `NAVAL_TRANSPORT_REBUILD` | 0 | 0 | 360 | 240 | Transport rebuild interval (Hard+ only) |
| `NAVAL_MAX_TRANSPORTS` | 0 | 0 | 4 | 5 | Max simultaneous transports |

---

#### abb_m8_cyprus

Tiers: **Easy / Normal / Hard / Expert**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `prisoner_guardAmount` | 3 | 4 | 5 | 10 | MaA guarding each prison |
| `navalLootChance` | 35% | 30% | 25% | 20% | Loot drop chance per enemy ship |
| `nicosia_grace_timer` | 220 | 160 | 100 | 40 | Seconds before Nicosia attacks |
| `nicosia_attacks_timer` | 420 | 360 | 300 | 240 | Interval between Nicosia waves |
| `navy_raid_timer` | 400 | 350 | 300 | 240 | Interval between naval raids |
| `init_navy_raid_delay` | 420 | 360 | 300 | 240 | Delay before first naval raid |
| `init_kyrenia_raid_delay` | 690 | 660 | 630 | 600 | Delay before first Kyrenia raid |
| `nicosia_retreat_threshold` | 7 | 7 | 8 | 9 | Squad count to trigger retreat |
| `nicosia_keep_garrisonAmount` | 0 | 5 | 10 | 15 | MaA garrisoned in Nicosia keep |
| Outpost upgrades | — | Arrowslits | Springald | Cannon | Outpost emplacement tier |
| Keep upgrades | — | Arrowslits | Springald | Cannon | Keep emplacement tier |
| Enemy tech tiers | Mil 0 / Unit 3 | Mil 2 / Unit 3 | Mil 3 / Unit 4 | Mil 4 / Unit 4 | Military and unit upgrade levels |
| Factional upgrades | — | — | Yes | Yes | Hard+ only: Armor-Clad, Crossbow buffs, Cavalry barding |

Unit count variables scale linearly (e.g., `num_12_to_20` = {12,14,16,20}, `num_15_to_30` = {15,20,25,30}).

---

### Angevin Empire

#### ang_chp0_intro

**No difficulty scaling.** Fixed-difficulty tutorial mission. All parameters are hardcoded constants. No `Util_DifVar` calls.

---

#### ang_chp1_hastings

Tiers: **Story / Easy / Normal / Hard**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `enableLimitedReinforcements` | false | true | true | true | Whether reinforcement count is limited |
| `maximumNumberOfReinforcements` | -1 (∞) | 35 | 20 | 10 | Max reinforcement waves (Story=unlimited) |
| `maxNumberOfWilliamAttackers` | 2 | 2 | 3 | 4 | Max enemies targeting Duke William |

**Difficulty-conditional logic:** Post-downed William (Story mode only): `maxNumberOfWilliamAttackers` reduced to 1.

---

#### ang_chp1_york

Tiers: **Easy / Normal / Hard / Hardest**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `danes_goldAmount` | 500 | 500 | 800 | 1200 | Gold tribute required / gold pickups spawned |
| `danes_spawnDelay` | 240 | 200 | 160 | 120 | Sec between repeating Dane raid spawns |
| `danes_initRaid_Countdown` | 150 | 150 | 120 | 90 | Timer (sec) for initial raid repel |
| `danes_raiderCount1` | 2 | 3 | 5 | 7 | Dane attack group 1 & 3 squad count |
| `danes_raiderCount2` | 4 | 4 | 5 | 6 | Dane attack group 2 squad count |
| `danes_raiderCountCap` | 16 | 20 | 30 | 40 | Max Dane raider squads (repeating) |
| `danes_defenderCount` | 8 | 10 | 15 | 20 | Dane camp defender squad count |
| `rebels_earlyRaiderCount` | 0 | 1 | 2 | 3 | Base early raider spawns (0 = disabled) |
| `rebels_earlyRaidInterval` | 200 | 200 | 160 | 120 | Sec between early raider spawns |
| `rebels_defenderCount` | 3 | 4 | 5 | 5 | City rebel defenders per module |
| `rebels_patrolCount` | 3 | 6 | 8 | 12 | Rebel patrol units per module |
| `rebels_attackStartDelay` | 240 | 240 | 120 | 60 | Delay (sec) before rebel patrols go offensive |
| `rebels_attackGroupCount` | 0 | 1 | 2 | 3 | Rebel patrol groups on offense |
| `rebels_initNumSquads` | 3 | 4 | 5 | 6 | Initial rebel wave escalation counter |
| `rebels_reinforceDelay` | 300 | 240 | 200 | 160 | Sec between rebel reinforcement waves |
| `rebels_maxModuleSize` | 10 | 15 | 25 | 35 | Max squads per rebel wave module |
| `enemy_unitBuildTime` | 30 | 25 | 20 | 12 | Wave unit build time override (sec) |
| `upgradeLevel` | 0 | 0 | 1 | 2 | Outpost arrowslit upgrade (0=none, 1=city, 2=all) |
| `extraVillagerCount` | 12 | 9 | 6 | 6 | Extra villagers on village capture |

**Difficulty-conditional logic:** On Easy, player starts with bonus gold equal to `danes_goldAmount`. On Hard+, rebel villagers spawn to repair the keep when player is not nearby.

---

#### ang_chp2_bayeux

Tiers: **Story / Easy / Medium / Hard**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `archerAmounts` | 3 | 3 | 5 | 8 | Archers per wall Defend module |
| `playerSpearmen` | 40 | 30 | 30 | 30 | Spearmen in player reinforcement wave |
| `playerArchers` | 70 | 70 | 70 | 70 | Target archer count for reinforcements |
| `enemyCavalry` | 10 | 12 | 14 | 10 | Horsemen per cavalry patrol group |
| `enemyKnights` | 0 | 0 | 1 | 5 | Knights per cavalry patrol group |
| `gateDefenders.spearmanCount` | 5 | 6 | 8 | 12 | Spearmen per gate infantry position |
| `gateDefenders.archerCount` | 5 | 6 | 10 | 14 | Archers per gate infantry position |
| `idleattacktimer` | 0 | 6 | 4 | 1 | Min of idle before cavalry attack (0=disabled) |
| `rovingArmy_DefendPositions` | 5 | 5 | 7 | 9 | Number of cavalry patrol routes |

---

#### ang_chp2_bremule

Tiers: **Story / Easy / Normal / Hard**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `scoutsAmount` | 4 | 4 | 8 | 12 | French scout waypoints active |
| `invasionScale` | 0.18 | 0.5 | 0.75 | 1.0 | Multiplier on backfill/ambush army sizes |
| `attackWaveScale` | 0 | 0 | 1 | 2 | Hunting wave power scaling factor |
| `attackWaveFrequency` | 15 | 15 | 10 | 5 | Minutes between hunting army respawns |
| `ramWaveFrequency` | 10 | 10 | 5 | 5 | Minutes between ram wave respawns |
| `storyStartingVillagers` | 2 | 0 | 0 | 0 | Extra villagers at Fleury (Story only) |
| `matchUpSimplify.ranged` | 0 | 0 | 1 | 1 | Ranged unit multiplier in ambush |
| `matchUpSimplify.infantry` | 2 | 2 | 1 | 1 | Infantry multiplier in ambush |
| `enemyStartsMaxed` | false | false | false | true | French start at max composition (Hard only) |
| `t_frenchScoutCamps` | 4 | 4 | 6 | 8 | Scout camp waypoints |

**Difficulty-conditional logic:** Hunting army, ram waves, and scouts only spawn on Normal+. `OBJ_FuncKeys` only starts on Normal or below. Counter-attack targeting uses `ARMY_TARGETING_CYCLE` on Easy, `ARMY_TARGETING_DISCARD` otherwise. Siege targets exclude Fleury on Easy.

---

#### ang_chp2_tinchebray

Tiers: **Easy / Normal / Hard / Hardest**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `upgradeLevel` | 0 | 0 | 1 | 2 | Enemy upgrade tier |
| `enemy_reinforcements_horseman` | 20 | 30 | 15 | 5 | Relief army horsemen |
| `enemy_reinforcements_knight` | 0 | 0 | 15 | 25 | Relief army knights (Hard+ only) |
| `enemy_reinforcements_infantry` | 12 | 15 | 20 | 25 | Relief army spearmen AND archers each |
| `enemy_mainarmy_maa` | 10 | 15 | 15 | 15 | Robert's main army MaA |
| `enemy_mainarmy_knight` | 0 | 0 | 10 | 18 | Robert's main army knights (Hard+ only) |
| `enemy_scout_limit` | 3 | 4 | 5 | 6 | Max concurrent enemy scouts |

---

#### ang_chp3_lincoln

Tiers: **Easy / Normal / Hard / Hardest**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `enemy_bodyguardCount` | 5 | 5 | 8 | 12 | Horsemen guarding King Stephen |
| `enemy_siegeInterval` | 80 | 60 | 55 | 50 | Sec between siege reinforcement waves |
| `enemy_fa_maa` | 6 | 8 | 12 | 15 | MaA per FinalAttacker module |
| `enemy_siege_max` | 1 | 2 | 3 | 4 | Max simultaneous siege engines |
| `enemy_besieger_count` | 5 | 6 | 8 | 10 | Base unit count per besieger wave |
| `enemy_siege_diff` | 1 | 1 | 2 | 3 | Siege distribution index (frequency control) |
| `camp_defender_count` | 8 | 10 | 12 | 14 | Spearman/MaA defenders per siege camp |

---

#### ang_chp3_wallingford

Tiers: **Story / Easy / Normal / Hard**

| Parameter | Story | Easy | Hard | Expert | Scales |
|-----------|-------|------|------|--------|--------|
| Defender spearman | 5 | 7 | 10 | 14 | Per defender module |
| Defender crossbow/archer | 4–5 | 5–7 | 7–10 | 10–14 | Per defender module |
| Fort defenders (MAA) | 5 | 7 | 10 | 14 | Per fort position |
| Fort defenders (archer) | 7 | 10 | 14 | 20 | Per fort position |
| Fort defenders (mangonel) | 0 | 0 | 1 | 2 | Per fort position |
| Siege patrol (MAA) | 4 | 5 | 7 | 10 | Per patrol module |
| Cavalry patrol (knight) | 4 | 5 | 7 | 10 | Per patrol module |
| Enemy reinforcements (springald) | 0 | 0 | 1 | 2 | Per reinforcement source |
| Final wave (per unit type) | 9 | 12 | 17 | 24 | MAA + spearmen + horsemen |
| Knight patrols | 4–5 | 5–7 | 7–10 | 10–14 | Per patrol module |
| Player starting villagers (wood) | 6 | 4 | 4 | 4 | Wood gatherers |
| Player starting villagers (gold) | 4 | 3 | 3 | 3 | Gold gatherers |
| Player starting villagers (stone) | 2 | 1 | 1 | 1 | Stone gatherers |
| Player starting resources | 800 each | 800 each | 600 each | 400 each | All resource types |

**Difficulty-conditional logic:** Wave unit tables are entirely separate per difficulty (`wave_units_story`, `wave_units_easy`, `wave_units_normal`, `wave_units_hard`) — smaller squads and fewer siege on easier, larger squads with more rams/mangonels/springalds on harder.

---

#### ang_chp4_dover

Tiers: **Easy / Normal / Hard / Hardest**

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `supplyLoopTimer` | 60 | 60 | 50 | 40 | Sec between supply train dispatches |
| `cartsPerStage` | 4 | 4 | 5 | 6 | Supply carts per siege stage |
| `supplyEscort_escalates` | false | true | true | true | Whether escort size grows each wave |
| `supplyEscort_melee` | 2 | 2 | 3 | 5 | Melee per supply escort |
| `supplyEscort_ranged` | 0 | 0 | 1 | 3 | Ranged per supply escort |
| `supplyEscort_cav` | 0 | 0 | 0 | 2 | Cavalry per supply escort |
| `supply_healthMod` | 0.25 | 0.5 | 0.5 | 0.5 | Supply cart health multiplier |
| `reserve_melee` | 2 | 3 | 4 | 5 | Melee squads per cart arrival |
| `reserve_ranged` | 2 | 3 | 4 | 5 | Ranged squads per cart arrival |
| `reserve_cav` | 2 | 3 | 4 | 5 | Cavalry squads per cart arrival |
| `reserve_siegeType` | springald | mangonel | mangonel | mangonel | Siege unit type for reserves |
| `road_patrol` | 0 | 0 | 2 | 3 | Units per road patrol (0=disabled) |
| `siege_wave_base` | 5 | 8 | 12 | 15 | Base squads per siege wave |
| `st_wave_base` | 4 | 6 | 8 | 8 | Base squads per siege tower wave |
| `player_StartingResource` | 1500/600 | 1500/600 | 1000/400 | 500/200 | Starting gold+wood+food / stone |

---

#### ang_chp4_lincoln

Tiers: **Easy / Standard / Hard / Hardest**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `enemyTargetLevel` | 0 | 0 | 1 | 2 | French attack path complexity |
| `enemyUnitBuildTime` | 13 | 11 | 9 | 7 | Wave infantry build time (sec) |
| `siegeUnitBuildTime` | 35 | 30 | 25 | 20 | Wave siege build time (sec) |
| `rebelWaveInterval` | 130 | 110 | 90 | 80 | Sec between rebel wave dispatches |
| `rebelSiegeMax` | 3 | 4 | 6 | 8 | Max rebel siege weapons alive |
| `frenchWaveInterval` | 600 | 400 | 340 | 280 | Sec between French wave dispatches |
| `rebelDefenderCount` | 5 | 5 | 10 | 15 | Squads per rebel Defend module |
| `frenchDefenderCount` | 3 | 4 | 7 | 10 | Squads per French fort Defend module |
| `enemyInitUnitIndex` | 1 | 1 | 2 | 3 | Starting wave escalation index |
| `enemyEndUnitIndex` | 3 | 4 | 6 | 8 | Max wave escalation index (cap) |

**Additional difficulty scaling:**
- `strongpoint_unit_cap`: 30 / 30 / 40 / 50 — max rebel units near strongpoint before wave suppressed
- `french_unit_cap`: 70 / 70 / 85 / 100 — max French units near fort before wave suppressed
- Easy mode spawns extra wall archers (markers 8–12) and 4 additional villagers

---

#### ang_chp4_rochester

Tiers: **Story / Easy / Normal / Hard**

| Parameter | Easy | Standard | Hard | Expert | Scales |
|-----------|------|----------|------|--------|--------|
| `defenderValue` | 1 | 1 | 1.15 | 1.25 | Multiplier on all defender squad counts |
| `baseWaveValue` | 5 | 5 | 5 | 10 | Base size for attack waves |
| `easyWaveMod` | 0 | 0 | 1 | 1 | Additional wave modifier |
| `waveDownTimeMin` | 180 | 120 | 0 | 0 | Min seconds between attack waves |
| `waveDownTimeMax` | 180 | 120 | 60 | 30 | Max seconds between attack waves |
| `earlyPokes` | 2 | 2 | 3 | 5 | Number of early probing attacks |
| `pokeTimer` | 3 | 3 | 4 | 5 | Minutes between poke attacks |

**Additional difficulty scaling:**
- `VillageRepopulate()`: Story gets +6 wood villagers, others get +4; Story gets +1 stone/gold villagers.
- `ConstructWave()`: Story/Easy wave budget capped at 15; Hard gets 1.5× multiplier.
- Attack waves only start on Normal+; Story skips `Init_AttackWaves()` and `SendPoke()`.
- Siege tutorial (`OBJ_SiegeTut`) only available on Easy/Normal.

---

### Challenges (Medal Tiers)

Challenges use a medal-based scoring system instead of `Util_DifVar`. PC and Xbox thresholds differ. Some challenges also include a Conqueror Mode that dynamically scales difficulty based on player performance.

#### challenge_advancedcombat

| Medal | Max Units Died (PC) | Max Units Died (Xbox) |
|-------|---------------------|-----------------------|
| Gold | 15 | 18 |
| Silver | 30 | 35 |
| Bronze | 40 | 45 |

**Difficulty-conditional logic:** Xbox thresholds relaxed via `UI_IsXboxUI()` check.

---

#### challenge_basiccombat

| Medal | Max Units Died (PC) | Max Units Died (Xbox) |
|-------|---------------------|-----------------------|
| Gold | 15 | 18 |
| Silver | 20 | 25 |
| Bronze | 35 | 40 |

**Difficulty-conditional logic:** Xbox thresholds relaxed via `UI_IsXboxUI()` check. All players set to `AGE_FEUDAL`.

---

#### challenge_earlyeconomy

| Medal | Time Limit (PC) | Time Limit (Xbox) |
|-------|-----------------|-------------------|
| Gold | 5m 10s | 5m 20s |
| Silver | 6m 00s | 6m 30s |
| Bronze | 7m 30s | 8m 00s |

**Difficulty-conditional logic:** Xbox thresholds relaxed via `UI_IsXboxUI()` check.

---

#### challenge_earlysiege

| Medal | Time (PC) | Time (Xbox) |
|-------|-----------|-------------|
| Gold | 6 min | 7 min |
| Silver | 10 min | 12 min |
| Bronze | 20 min | 20 min |

**Difficulty-conditional logic:** Production speed 10x. Ram build time 0.1x. Siege Engineers pre-completed.

---

#### challenge_lateeconomy

| Medal | PC Time | Xbox Time |
|-------|---------|-----------|
| Gold | 10m 30s | 10m 45s |
| Silver | 15m 30s | 16m 00s |
| Bronze | 19m 30s | 20m 00s |

**Difficulty-conditional logic:** Xbox gets slightly relaxed medal times via `UI_IsXboxUI()` check.

---

#### challenge_latesiege

| Medal | Time (PC) | Time (Xbox) |
|-------|-----------|-------------|
| Gold | 6 min | 7 min |
| Silver | 9 min | 10 min |
| Bronze | 15 min | 16 min |

**Difficulty-conditional logic:** Xbox medal thresholds relaxed by +1 minute each tier. Starting resources dynamically calculated via `CalculateLateSiegeStartingResources()`.

---

#### challenge_malian

| Medal | Threshold (PC) | Threshold (Xbox) |
|-------|----------------|-------------------|
| Gold | ≥7000 gold | ≥6500 gold |
| Silver | ≥7000 gold | ≥6500 gold |
| Bronze | ≥4500 gold | ≥4000 gold |

**Difficulty-conditional logic:** Xbox thresholds reduced by ~500 gold per tier. After 2 intervals, if gold income rate < 411/min, supplemental gold added every 10s. Wave cost starts at 800, increases by 50–75/wave. Wave interval starts ~50s, decreases over time; big waves (4, 7) get +30s before and +20s after.

---

#### challenge_ottoman

| Medal | Threshold (PC) | Threshold (Xbox) |
|-------|----------------|-------------------|
| Gold | ≥21 min | ≥16 min |
| Silver | ≥15 min | ≥12 min |
| Bronze | ≥10 min | ≥8 min |

**Difficulty-conditional logic:** Xbox medal time thresholds reduced. Wave timing: first arrival at 120s; subsequent spacing starts 75s, decreases by 2s/meta-round to min 45s. After round 30, replays last 3 rounds indefinitely.

---

#### challenge_walldefense

| Tier | Time Window | Waves | Key Threats |
|------|-------------|-------|-------------|
| Bronze | 0–300s | 1–8 | Rams, spearmen, men-at-arms, springalds, traction trebuchet |
| Silver | 300–600s | 9–16 | Siege towers, mangonels, larger infantry groups, trebuchets |
| Gold | 600–900s | 17–24 | Bombards, hand cannoneers, massive combined siege forces |

**Difficulty-conditional logic:** Resource trickle multiplier scales with tier: 1x (bronze), 2x (silver), 3x (gold).

---

#### challenge_agincourt

No `Util_DifVar` calls. Difficulty is binary via `conquerorModeActivated`.

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

Medal thresholds: Gold ≤16 min (`GOLD_MEDAL_TIME` = 960s), Silver ≤20 min (`SILVER_MEDAL_TIME` = 1200s), Bronze = completion.

**Difficulty-conditional logic:** Conqueror Mode activates if Wave 1 defeated within 5 minutes. When active, all subsequent French forces strengthened, player reinforcements removed.

---

#### challenge_montgisard

| Medal | Threshold |
|-------|-----------|
| Gold | <17 min |
| Silver | <25 min |
| Bronze | <60 min |
| Conqueror | <25 min (in Conqueror Mode) |

**Difficulty-conditional logic:**
- Conqueror Mode doubles all reinforcement `numSquads` values via `Montgisard_GetConquerorUnits`
- Conqueror Mode adds wave-specific bonus units (+2 per type per fortress for waves 2–6)
- Enemy upgrades on Conqueror activation: Melee/Ranged Armor I+II, Melee/Ranged Damage I+II
- `attackStrenghtCM` starts at 24, increases by 4 per attack in Conqueror Mode
- `attackStrenghtPostBronze` starts at 20, decreases by 4 per attack (min 8) after wave 5 in normal mode

---

#### challenge_safed

| Parameter | Value | Effect |
|-----------|-------|--------|
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE` | 0.145 | Base multiplier on all fortress damage received |
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE_ENDING` | 0.5 | Additional damage reduction after mine 4 depleted |
| `SAFED_FORTRESS_DAMAGE_EMPATHY_THRESHOLD` | 0.35 | Fortress HP% below which empathy damage kicks in |
| `SAFED_FORTRESS_DAMAGE_RECEIVED_SCALE_EMPATHY` | 0.5 | Empathy damage reduction multiplier (bronze medal range) |
| `SAFED_CM_ACTIVATE_TIME` | 300s (5:00) | Deadline to meet conqueror mode conditions |
| `SAFED_CM_VILLAGER_COUNT` | 7 | All villagers alive required for conqueror mode |
| `SAFED_STONE_DEPLETED_COUNT == 2` | — | Must have mined 2 deposits before 5:00 for CM |
| CM unit scaling | 1-10% | Adds units to all existing enemy armies when CM activates |

**Difficulty-conditional logic:** Medal scoring based on fortress health percentage at completion. Conqueror Mode activates if all 7 villagers alive AND 2 stone deposits mined before 5:00.

---

#### challenge_towton

| Mechanism | What It Scales |
|-----------|---------------|
| Conqueror mode (1.3x multiplier) | All wave unit counts scaled up when conqueror is active |
| `conquerorModeFailed` wave reduction | Boss wave siege units reduced by 0.8x if conqueror not active |
| Manor destruction scaling | Wave unit counts reduced by 0.75x if prior manor destroyed |
| Silver medal failed scaling | Wave unit counts reduced by 0.825x |
| Gold medal failed scaling | Wave unit counts reduced by 0.9x |
| Reinforcement count scaling | Reinforcement army size proportional to defense duration (time/phaseDuration × base) |
| Player combat unit count | Extra reinforcements added if player has <10/15/20/25/30 combat units |
| Outpost auto-upgrade | Allied outposts upgraded to stone+arrowslits when buildings lost (non-conqueror only) |
| Additional reinforcement unit types | Earls Guard and Culverins added to NE reinforcements if medals failed |

Medal thresholds: Gold (35+ buildings saved), Silver (20+ buildings saved), Bronze (survive all waves), Conqueror Medal (survive all strengthened waves).

**Difficulty-conditional logic:** Conqueror Mode unlocks if player kills 2 enemy scouts and preserves all outer houses before 5:30. Adds extra conqueror-only waves and scales all unit counts by 1.3x.

---

### Hundred Years War

#### hun_chp1_combat30

| Parameter | Story | Easy | Normal | Hard | Scales |
|-----------|-------|------|--------|------|--------|
| `combat30_unitCompositions_*` | table 1 | table 2 | table 3 | table 4 | English army composition — Landsknecht count (4/6/4+4/4+5), cavalry mix |
| Recruit4 archer count | 9 | 10 | 11 | 12 | Number of archers in Recruit 4 initial wave |
| Recruit4 wave horsemen | 4 | 4 | 5 | 5 | Horsemen per tower-defense wave |
| Recruit4 wave spearmen | 3 | 4 | 5 | 6 | Spearmen per tower-defense wave |
| Recruit4 wave MAA | 3 | 4 | 4 | 5 | Men-at-arms per tower-defense wave |
| Recruit4 wave knight | 1 | 1 | 1 | 2 | Knights per tower-defense wave |
| Starting gold | 750 | 750 | 450 | 150 | Player starting gold resources |

**Difficulty-conditional logic:** player2/5 get Melee Armor III + Damage III on Expert. Round 2 English can be rebuilt to counter player's most-killed unit type (on Normal/Hard).

---

#### hun_chp1_paris

All values are `Util_DifVar({Story, Easy, Normal, Hard})`:

| Parameter | Story | Easy | Normal | Hard | Scales |
|-----------|-------|------|--------|------|--------|
| Starting resources (each) | 400 | 300 | 200 | 100 | Food/Wood/Stone/Gold |
| Invader MAA per lane | 11 | 13 | 18 | 26 | Initial invasion force size |
| Standby MAA (lane 1/3) | 15 | 18 | 27 | 39 | Standby reinforcement pool |
| Standby MAA (lane 2) | 10 | 12 | 18 | 26 | Standby reinforcement pool |
| Stone/Gold raider MAA | 6 | 7 | 10 | 14 | Resource-denial raider group |
| Fort defenders (MAA) | 6 | 7 | 10 | 14 | Siege camp garrison MAA |
| Fort defenders (xbow) | 6 | 7 | 10 | 14 | Siege camp garrison crossbowmen |
| Fort defenders (springald) | 1 | 2 | 3 | 4 | Siege camp garrison springalds |
| Siege defenders (archer) | 5 | 6 | 8 | 10 | Field defender archers |
| Siege defenders (spearman) | 5 | 6 | 8 | 10 | Field defender spearmen |
| Ram passenger count | 10 | 10 | 10 | 10 | Troops loaded in rams |
| Siege tower passenger count | 3 | 4 | 6 | 8 | Troops loaded in siege towers |
| Gold villagers (extra) | 4 | 2 | 1 | 0 | Player starting gold villagers |
| Stone villagers (extra) | 4 | 2 | 1 | 0 | Player starting stone villagers |
| Wood villagers (extra) | 5 | 2 | 1 | 0 | Player starting wood villagers |
| Wave compositions | Smallest | Small | Medium | Large | Total units per wave |

**Difficulty-conditional logic:** None beyond the scaling table.

---

#### hun_chp2_cocherel

All values use `Util_DifVar({Easy, Normal, Hard, Expert})`:

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `given_resources_gold` | 500 | 400 | 300 | 200 | Starting gold |
| `given_resources_wood` | 1000 | 800 | 600 | 400 | Starting wood |
| `given_resources_food` | 1000 | 800 | 600 | 400 | Starting food |
| `given_resources_stone` | 250 | 200 | 150 | 100 | Starting stone |
| `i_numberUnitsToKillCharles` | 83 | 97 | 124 | 159 | Kill threshold for final objective |
| `findHolySite_NearbyDistance` | 140 | 110 | 80 | 50 | Proximity hint range for holy sites |
| `routiers_goldDemanded` | 800 | 800 | 1000 | 1400 | Gold required to pay off Routiers |
| `routiers_firstAttackDelay` | 90 | 90 | 60 | 30 | Seconds before first Routier base attack |
| `routiers_attackFrequency` | 180 | 180 | 150 | 120 | Interval between Routier base attacks |
| `cocherel_firstAttackDelay` | 50 | 50 | 30 | 10 | Delay before inter-village attacks |
| `cocherel_attackFrequency` | 180 | 180 | 150 | 120 | Interval between inter-village attacks |
| `routier_attackCocherelDelay` | 120 | 120 | 100 | 80 | Delay before Routiers attack Cocherel |
| `routier_attackCocherelInterval` | 180 | 180 | 150 | 120 | Interval of Routier-Cocherel attacks |
| `charles_firstAttackDelay` | 70 | 70 | 50 | 30 | Delay before Charles attacks Cocherel |
| `charles_attackInterval` | 180 | 180 | 150 | 120 | Interval of Charles's knight waves |

**Difficulty-conditional logic:** Additional per-unit scaling via `Util_DifVar` in spawn definitions (villagers: 4/3/3/3, garrison shield villagers: 6-20 range, Navarre archers: 14-25). Player pop cap reduced by 15. Pop cap increases +5 per village captured. Village capture rewards scale with difficulty (200-500 resources). Gold pickup amounts at Routier camp: 1000/800/600/400. Holy site blip hints disabled on Expert. MaA added to Routier waves on Hard+. Inter-village attacks only triggered on Normal+.

---

#### hun_chp2_pontvallain

All scaling uses `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| Starting resources (Food/Wood/Stone/Gold) | 400 | 300 | 200 | 100 | Player starting economy |
| Player woodcutters | 8 | 4 | 4 | 4 | Starting villager count at wood |
| Raid 1 horsemen | 6 | 8 | 11 | 15 | First raiding party size |
| Raid 2 horsemen | 8 | 10 | 14 | 20 | Second raid cavalry |
| Raid 2 knights | 3 | 4 | 6 | 9 | Second raid heavy cavalry |
| Raid 3 knights | 12 | 15 | 21 | 30 | Third raid heavy cavalry |
| Army 1 archers | 14 | 18 | 25 | 35 | First army ranged |
| Army 1 MAA | 14 | 18 | 25 | 35 | First army melee infantry |
| Army 2 archers | 14 | 18 | 25 | 35 | Second army ranged |
| Army 2 MAA | 14 | 18 | 25 | 35 | Second army melee infantry |
| Army 3 archers | 14 | 18 | 25 | 35 | Third army ranged |
| Army 3 MAA | 10 | 13 | 17 | 25 | Third army melee infantry |
| Army 3 knights | 7 | 10 | 14 | 20 | Third army heavy cavalry |
| Bandit defenders (spearmen) | 4 | 5 | 7 | 10 | Static bandit camp defense |
| Bandit defenders (archers) | 4 | 5 | 7 | 10 | Static bandit camp defense |
| Bandit patrol (horsemen) | 6 | 7 | 10 | 14 | Roving bandit patrol |
| Optional build objective | shown | shown | hidden | hidden | Only Easy/Normal get build hint |

**Difficulty-conditional logic:** None beyond the scaling table and build hint visibility.

---

#### hun_chp3_orleans

All values use `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `Orleans_SiegeTowerPassengerCount` | 3 | 4 | 6 | 8 | Passengers loaded into siege towers |
| `PREPARE_TIME` | 60 | 70 | 90 | 120 | Seconds for wave to build before auto-launch |
| `intro_units_1/1a/1b/2/2a` | 4 | 5 | 7 | 10 | Men-at-arms per intro assault group |
| `siege_defense_units_a–d` | 6 | 7 | 10 | 14 | Spearman/MAA/archer/crossbow per siege defend group |
| `rear_defense_units_a` | 8 | 10 | 14 | 20 | Men-at-arms per rear defend post |
| `rear_defense_units_b` | 11 | 13 | 17 | 25 | Archers per rear defend post |
| `rear_defense_units_c` | 9 | 11 | 15 | 23 | Horsemen per rear defend post |
| Fort defenders (various) | 3–10 | 4–12 | 6–16 | 9–24 | Units per fort defend module |
| Enemy longbow spawners 1–6 | 2 | 2 | 3 | 4 | Archers per longbow position |
| Enemy longbow spawners 7–8 | 6 | 7 | 10 | 15 | Archers per large longbow position |
| Patrol units (various) | 3–6 | 4–7 | 6–10 | 9–14 | Units per patrol route |
| Ambush reinforcement count | 3 | 4 | 8 | 14 | Horsemen in trade route ambush |
| Player wood/gold/stone villagers | 6/3/3 | 4/2/2 | 4/2/2 | 4/2/2 | Starting villager counts |
| Player crossbow spawners | 4 | 3 | 3 | 3 | Crossbowmen per wall group |
| Starting resources | 400 | 300 | 200 | 100 | Each resource type (food/wood/stone/gold) |
| Wave power multiplier | 0.8 | 1.0 | 1.4 | 2.0 | Scales `Orleans_GetPower()` output |
| Ram damage (Easy only) | 0.8x | — | — | — | Weapon damage modifier for rams |

**Difficulty-conditional logic:** Power budget formula: `1500 + 15*min(minutes,71) + (1/15000)*min(minutes,71)^4`, scaled by difficulty multiplier.

---

#### hun_chp3_patay

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `regimentWakeTimer` | 60 | 40 | 30 | 30 | Seconds before each regiment activates (multiplied by 1x/3x/5x per regiment) |
| `regimentBaseCount` | 9 | 10 | 10 | 10 | Base multiplier for regiment unit squads |
| `regimentSiegeCount` | 1 | 2 | 2 | 2 | Number of siege units (springalds/mangonels) per regiment |

**Difficulty-conditional logic:** Static thresholds: `road_blocker_threshold = 5`, `sigmund_threshold = 5`, `main_line_threshold = 10` (reduced to 3 if player skips St. Sigmund), `battle_group_threshold = 6` (reduced to 1 if skipped).

---

#### hun_chp4_formigny

All use `Util_DifVar({Easy, Normal, Hard, Hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `ARCHER_SIZE_FINAL` | 13 | 15 | 17 | 18 | Base archer squad size per module (×2 for intro) |
| `SPEARMAN_SIZE_FINAL` | 13 | 15 | 17 | 18 | Base spearman squad size per module (×2 for intro) |
| `MANATARMS_SIZE_FINAL` | 13 | 15 | 17 | 18 | Base MAA squad size per module (×2 for intro) |
| Town defend units | 2-5 | 3-6 | 4-8 | 5-9 | Garrison sizes at Bricquebec, St-Sauveur, pre-towns |
| Town patrol horsemen | 4 | 5 | 7 | 9 | Roving patrol squad sizes |
| Pre-town defenders | 4 | 5 | 7 | 9 | Ambush defender squad sizes |
| Forward MAA defenders | 4 | 5 | 7 | 9 | Forward men-at-arms near Formigny |
| Formigny garrison | 2-5 | 3-6 | 4-8 | 5-9 | Knights, archers, spearmen defending Formigny |
| Valognes enemy archers/cavalry | 7 | 10 | 14 | 18 | Attacker count at Valognes |
| Valognes gold reward | 2400 | 1600 | 800 | 0 | Gold given on saving Valognes |
| Archer palings | No | No | Yes | Yes | `deploy_palings` ability enabled on Hard/Hardest |

**Difficulty-conditional logic:** Archer palings only on Hard+. Achievement: `CE_FORMIGNYVICTORYHARD` — Win on Hard or Hardest difficulty.

---

#### hun_chp4_rouen

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `given_resources_gold` | 3000 | 2500 | 2200 | 2000 | Starting gold after university capture |
| `given_resources_wood` | 2400 | 1200 | 700 | 500 | Starting wood after university capture |
| `given_resources_food` | 3000 | 2500 | 2000 | 1200 | Starting food after university capture |
| `given_resources_stone` | 1000 | 1000 | 500 | 0 | Starting stone after university capture |
| `initial_lane_timer_top/mid/below` | 150 | 150 | 120 | 110 | Seconds between attack waves per lane |
| `i_request_upperThreshold` | 0.6 | 0.6 | 0.7 | 0.75 | AI request strength upper bound |
| `i_request_lowerThreshold` | 0.2 | 0.2 | 0.2 | 0.1 | AI request strength lower bound |
| `i_request_desiredStrength` | 0.7 | 0.7 | 0.8 | 1.0 | AI desired army strength |
| `defenderValue` | 0.66 | 0.75 | 1.0 | 1.20 | Multiplier on all defender squad counts |
| `timerMod` | 0 | 0 | 45 | 90 | Seconds subtracted from wave timers (faster waves) |

**Difficulty-conditional logic:**
- Attack waves disabled entirely on Easy (Story) difficulty
- Pressure waves only on Hard+ with varying delays: Hard {300,900,1200}s, Expert {120,300,600}s
- Anti-Ram counter spawns only on Hard+ (every 360s)
- Counter-monk armies spawn every 680s on Normal+
- Siege defenders at `mkr_siege_defender_medium` only on Hard+, `mkr_siege_defender_hard` only on Expert
- Village reinforcement unit counts scale per difficulty via inline `Util_DifVar`

---

### Mongol Empire

#### mon_chp1_kalka_river

All values ordered `{Easy, Normal, Hard, Hardest}`:

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `rusReinforceThreshold` | 18 | 20 | 22 | 26 | Unit count below which attack groups receive reinforcements |
| `rusMergeThreshold` | 70 | 100 | 130 | 160 | Total Rus below which remaining armies merge together |
| `earlyKillThreshold` | 130 | 160 | 190 | 220 | Enemy count below which lure objective auto-fails |
| `i_Troops01Player2` | 24 | 24 | 26 | 30 | First Rus wave spearmen per sub-group (×3 groups) |
| `i_Troops02Player2` | 24 | 24 | 26 | 30 | Second Rus wave spearmen per sub-group (×4 groups) |
| `i_Troops03Player2` | 32 | 32 | 36 | 40 | Third Rus wave archers per sub-group (×4 groups) |
| `i_TroopsPlayer2Enclosed` | 20 | 20 | 25 | 27 | Enclosed Rus per defend group (×3 = total) |
| `i_Knights01Player1` | 28 | 10 | 0 | 0 | Player's western ambush knights (replaced by horsemen on Hard+) |
| `i_Knights02Player1` | 28 | 28 | 28 | 28 | Player's central ambush knights (constant) |
| `i_Knights03Player1` | 28 | 10 | 0 | 0 | Player's eastern ambush knights (replaced by horsemen on Hard+) |
| `i_Horsemen01Player1` | 0 | 18 | 28 | 28 | Player's western ambush horsemen (inverse of knights) |
| `i_Horsemen03Player1` | 0 | 18 | 28 | 28 | Player's eastern ambush horsemen (inverse of knights) |
| `i_HorseArchersPlayer1` | 36 | 36 | 36 | 36 | Player's Mangudai horse archers (constant) |
| `OBJ_RusTimer` | 70 | 60 | 50 | 50 | Seconds before Rus army arrives (setup phase timer) |

**Difficulty-conditional logic:** On higher difficulties, player receives weaker horsemen instead of knights in flanking positions, while facing larger Rus armies. Setup timer also reduced.

---

#### mon_chp1_zhongdu

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `g_guardsPrimary` | 8 | 9 | 18 | 27 | Zhongdu main garrison squad count |
| `g_guardsLandmarks` | 5 | 6 | 12 | 18 | Landmark defender squad count |
| `g_guardsSkirmish` | 2 | 3 | 6 | 9 | Roving skirmisher patrol squad count |
| `g_guardsWalls` | 6 | 8 | 12 | 16 | Wall archer squad count |
| `g_guardsTowns` | 4 | 6 | 12 | 18 | Village garrison squad count |
| `scoutTiming` | 330 | 300 | 270 | 210 | Seconds before first raid scout |
| `partySize` | 4 | 4 | 6 | 9 | Initial raiding party squad count |
| `raidTiming` | 480 | 360 | 240 | 120 | Seconds between raid launches |
| `escortHorsemen` (scaling) | +2 | +2 | +4 | +7 | Convoy horseman escorts (scaled by progress ratio) |
| `escortSpearmen` (scaling) | +3 | +4 | +6 | +10 | Convoy spearman escorts (scaled by progress ratio) |
| `escortArchers` (scaling) | +5 | +6 | +9 | +12 | Convoy archer escorts (scaled by progress ratio) |
| Base hunt reset timer | 360 | 360 | 300 | 210 | Seconds between attacks on player base (Hard+ only) |

**Difficulty-conditional logic:**
- Easy/Normal: All village outposts removed; bridge at riverbend destroyed; `OBJ_EasyHint` shown after first reinforcement wave
- Expert: All outposts upgraded to Stone Outposts (`UPGRADE_OUTPOST_STONE`)

---

#### mon_chp1_juyong

| Parameter | Easy → Expert | Scales |
|-----------|---------------|--------|
| `yanqingWavePeriod` | 570 → 270s | Interval between Yanqing attack waves |
| `northWavePeriod` | 570 → 270s | Interval between North village attack waves |
| `south1WavePeriod` | 570 → 270s | Interval between South1 village attack waves |
| `south2WavePeriod` | 570 → 270s | Interval between South2 village attack waves |
| `juyongWavePeriod` | 570 → 270s | Interval between Juyong sortie waves |
| `wave_north` units | 3 → 5+6 spearmen | North wave base squad count per spawn |
| `wave_south1` units | 3 → 5+6 archers | South1 wave base squad count per spawn |
| `wave_south2` units | 3 → 5+6 spearmen | South2 wave base squad count per spawn |
| `wave_yanqing` units | 2+3 → 4+5+5+5 spear/archer | Yanqing wave mixed composition |
| `wave_juyong` units | 3+4 → 6+8+5+5 spear/xbow | Juyong wave mixed composition |
| Reinforcement villagers | 14 → 10 | Fewer villagers on harder difficulties |
| YanqingPatrol extra | 0 → +5+5 | Extra spear/archer squads at Hard/Expert |
| SouthPatrol extra | 0 → +4+4+5+5 | Extra horseman/spear squads at Hard/Expert |
| NorthPatrol extra | 0 → +3+3+5+5 | Extra spear/archer squads at Hard/Expert |
| ZhangjiakouDefend extra | 0 → +3+2+3+3 | Extra spear/archer squads at Hard/Expert |
| Wall archer garrisons | 3 → 3+1+1 | Extra archers per wall section at Hard/Expert |
| JinYanqing4/5 xbows | 2+2 → +2+2+2+2 | Extra repeater crossbow/archers at Yanqing |
| JinJuyong manatarms | 6 → +4+4 | Extra men-at-arms and crossbows at Juyong |
| Yanqing waves skip | Story mode | Yanqing waves disabled on Easy/Story difficulty |

**Difficulty-conditional logic:** Yanqing waves disabled entirely on Easy/Story. Patrol and garrison extras only appear on Hard/Expert.

---

#### mon_chp2_kiev

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `forts_have_springalds` | false | false | true | true | Gate fort springald upgrades |
| `forts_have_garrisons` | false | true | true | true | Auto-garrison gate forts |
| `spawn_attack_waves` | false | true | true | true | Enable counter-attack waves |
| `defender_count_high` | 6 | 8 | 12 | 16 | Spearman/MAA counts at gates |
| `defender_count_med` | 3 | 4 | 6 | 8 | Archer/horsearcher counts |
| `defender_count_low` | 2 | 2 | 3 | 5 | Horseman/secondary ranged counts |
| `defender_count_very_low` | 1 | 1 | 2 | 3 | Springald/monk counts |
| `main_attack_interval` | 360 | 360 | 300 | 180 | Seconds between district attack waves |
| `patrol_unit_cap` | 50 | 60 | 80 | 120 | Max patrol units before wave suppression |
| `sprawl_wave_intervals` | 60-120 | 60-120 | 60-120 | 40-100 | Seconds between sprawl area attacks |

**Difficulty-conditional logic:**
- Easy: No springalds at forts, no auto-garrisons, no attack waves
- Normal+: Attack waves enabled, garrisons enabled
- Hard+: Fort springalds enabled
- Wave suppression: no new waves if `sg_patrol_units_count` exceeds difficulty-based cap (50-120)

---

#### mon_chp2_liegnitz

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `bohemian_timer` | 1440s (24m) | 1320s (22m) | 1200s (20m) | 1140s (19m) | Time before Bohemian reinforcements arrive |
| `player_resources.food` | 1000 | 800 | 600 | 400 | Starting food |
| `player_resources.wood` | 1000 | 800 | 600 | 400 | Starting wood |
| `player_resources.gold` | 1000 | 800 | 600 | 400 | Starting gold |
| `player_resources.stone` | 500 | 400 | 300 | 200 | Starting stone |
| Nest of Bees count | 5 | 4 | 3 | 2 | Player Nest of Bees |
| Field cavalry (horsemen) | 7 | 8 | 10 | 12 | Enemy field horsemen |
| Field cavalry (knights) | 1 | 2 | 3 | 4 | Enemy field knights |
| Field center archers | 8 | 10 | 14 | 18 | Enemy field archers |
| Field center spearmen | 3 | 4 | 6 | 8 | Enemy field spearmen |
| Field patrol spearmen | 6 | 7 | 10 | 14 | Enemy patrol spearmen |
| Field patrol archers | 4 | 5 | 7 | 10 | Enemy patrol archers |
| Ridge left horsemen | 8 | 9 | 13 | 18 | Enemy ridge horsemen |
| Ridge left knights | 2 | 3 | 4 | 5 | Enemy ridge knights |
| Ridge right spearmen | 7 | 8 | 12 | 16 | Enemy ridge spearmen |
| Ridge center archers | 7 | 8 | 12 | 18 | Enemy ridge archers |
| Ridge center spearmen | 8 | 10 | 12 | 14 | Enemy ridge spearmen |
| Ridge patrol spearmen | 5 | 7 | 10 | 14 | Enemy ridge patrol spearmen |
| Ridge patrol archers | 4 | 5 | 7 | 10 | Enemy ridge patrol archers |
| Valley front landsknechts | 6 | 7 | 10 | 14 | Enemy valley landsknechts |
| Valley center archers | 11 | 13 | 19 | 26 | Enemy valley archers |
| Valley back knights (T4) | 7 | 8 | 12 | 16 | Enemy valley elite knights |
| Valley left/right spearmen | 7 | 8 | 12 | 16 | Enemy valley spearmen |
| Valley patrol spearmen | 6 | 7 | 10 | 14 | Enemy valley patrol spearmen |
| Valley patrol archers | 3 | 4 | 6 | 8 | Enemy valley patrol archers |
| Roving templars (T4 knights) | 12 | 14 | 20 | 28 | Roving Templar patrol |
| Bohemian knights | 6 | 7 | 10 | 14 | Bohemian army knights |
| Bohemian horsemen | 6 | 7 | 10 | 14 | Bohemian army horsemen |
| Bohemian archers | 6 | 7 | 10 | 14 | Bohemian army archers |
| Bohemian men-at-arms | 6 | 7 | 10 | 14 | Bohemian army MAA |

**Difficulty-conditional logic:** Bohemian army only spawns on timer failure.

---

#### mon_chp2_mohi

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `batu_timer` | 900s | 840s | 780s | 720s | Preparation time before Batu attacks |
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

**Difficulty-conditional logic:** Hard/Expert substitute spearmen/archers with MAA/crossbowmen/landsknechts at defense lines. Expert adds springalds at ambush points and camp outposts. Optional mangonels objective disabled on Hard+. Achievement: complete on Hard+ in under 15 minutes.

---

#### mon_chp3_lumen_shan

All `Util_DifVar` arrays ordered `{Easy, Normal, Hard, Expert}`:

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| Raider horseman ratio | 0.8 | 0.8 | 0.6 | 0.4 | Proportion of horsemen in raid parties |
| Raider knight ratio | 0.0 | 0.0 | 0.2 | 0.3 | Knights added on Hard/Expert |
| Raider firelancer ratio | 0.2 | 0.2 | 0.2 | 0.3 | Fire lancers in raids |
| Raider party limit | 1 | 1 | 2 | 3 | Max concurrent raid parties |
| Raider party size | 12 | 12 | 18 | 24 | Units per raid party |
| Raid timing | 30 | 30 | 25 | 20 | Seconds between raids |
| Wallbreaker spawn delay | 15 | 15 | 30 | 30 | Initial delay before first wallbreaker wave |
| Wallbreaker unit count | 12 | 14 | 16 | 20 | Melee/ranged squad count per wave |
| Wallbreaker rams | 1 | 1 | 1 | 1 | Battering rams per wave |
| Wallbreaker springalds | 0 | 0 | 1 | 0 | Springalds on Hard |
| Wallbreaker mangonels | 0 | 0 | 0 | 1 | Mangonels on Expert |
| Raid frequency modulo | 4 | 4 | 3 | 2 | Wallbreaker wave interval for bonus raids |
| Song sally men-at-arms | 15 | 15 | 20 | 25 | Phase 4 sally melee count |
| Song sally spearmen | 12 | 12 | 16 | 20 | Phase 4 sally spear count |
| Song sally archers | 10 | 10 | 12 | 14 | Phase 4 sally ranged count |
| Song sally crossbowmen | 8 | 8 | 10 | 12 | Phase 4 sally crossbow count |
| Song sally repeater xbow | 6 | 6 | 9 | 12 | Phase 4 sally elite ranged |
| Song sally grenadiers | 2 | 2 | 6 | 10 | Phase 4 sally grenadiers |

**Difficulty-conditional logic:** Easy/Normal wallbreakers include militia; Hard adds grenadiers to ranged pool; Expert uses repeater crossbows and mangonels. `SOBJ_Towers` only starts on Easy/Normal/Hard (not Expert). Song return sally totals 53–93 units depending on difficulty.

---

#### mon_chp3_xiangyang_1267

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `g_finalWaveTiming` | 40 | 40 | 35 | 30 | Seconds between finale sally waves |
| `g_sizeWoodenPost` | 6 | 8 | 12 | 18 | Garrison size at wooden camp defend modules |
| `g_sizeBarricades` | 2 | 3 | 4 | 5 | Unit count per barricade position |
| `g_sizeSiegeAttackers` | 12 | 16 | 20 | 26 | Song siege attacker RovingArmy size |
| `g_finalWaveTotalSize` | 250 | 275 | 300 | 325 | Total units across all 5 finale waves |
| Raiding partySize | 12 | 12 | 14 | 16 | Horseman/knight/firelancer raid party count |
| Raiding raidTiming | 40 | 40 | 30 | 20 | Seconds between raid launches |
| Road patrol archers | 2 | 4 | 5 | 6 | Archer count in road patrol groups |
| Breadcrumber squads | 4 | 6 | 8 | 10 | Spearmen and archers per breadcrumb wave |
| SongPost1 archers | 4 | 4 | 6 | 8 | Initial Song watchpost ranged garrison |
| SongPost1 MAA | 0 | 0 | 2 | 2 | Men-at-arms at initial watchpost |
| Camp springalds | 0 | 0 | 1 | 2 | Springalds at wooden camp southwest |
| Finale ranged types | varies | varies | +grenadiers | +repeater xbow | Grenadiers/repeater crossbows on Hard/Expert |

**Difficulty-conditional logic:** Grenadiers and repeater crossbows appear in finale only on Hard/Expert.

---

#### mon_chp3_xiangyang_1273

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `g_allyCounts` | 60 | 50 | 45 | 40 | Yuan allied army size (fewer allies on harder) |
| `g_enemyCountWalls` | 6 | 8 | 12 | 14 | Archer count per wall defence module (×6 modules) |
| `g_enemyCountGarrison` | 18 | 26 | 34 | 40 | Fancheng garrison size per guard group (×3 groups) |
| raiderComposition horseman | 0.7 | 0.7 | 0.5 | 0.4 | Horseman ratio in raid parties |
| raiderComposition knight | 0.15 | 0.15 | 0.25 | 0.3 | Knight ratio in raid parties |
| raiderComposition firelancer | 0.15 | 0.15 | 0.25 | 0.3 | Fire lancer ratio in raid parties |
| partyLimit | 2 | 2 | 3 | 4 | Max simultaneous raid parties |
| partySize | 12 | 12 | 14 | 18 | Units per raid party (grows +1 each raid) |
| raidTiming | 45 | 45 | 42 | 40 | Seconds between raid spawns |
| partySize max cap | 20 | 20 | 24 | 28 | Maximum raid party size cap |
| Xiangyang guards (per module) | 8-36 | 8-36 | 10-24 | 12-18 | Xiangyang defender counts (5 guard groups) |
| retaliation timer | 180 | 180 | 135 | 90 | Seconds between Xiangyang counter-attacks |
| retaliation militia | 18 | 24 | 0 | 0 | Militia count in retaliation waves |
| retaliation melee | 0 | 0 | 10 | 12 | Spearman count in retaliation waves |
| retaliation ranged | 0 | 0 | 12 | 16 | Crossbowman count in retaliation waves |

**Difficulty-conditional logic:** Raiding only targets the player on Normal+ when idle (Story mode retreats raiders). Retaliation system only active on Normal+ difficulty. After 8 tower kills, mangonels added to raid parties at 5% ratio; after 16 kills, 10%. Hard/Hardest replace militia with spearmen+crossbowmen in retaliation waves.

---

### Rise of Moscow (Grand Duchy of Moscow)

#### gdm_chp1_moscow

All values indexed by `{Easy, Normal, Hard, Expert}` via `Util_DifVar`:

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `maximumNumberOfWolves` | 10 | 15 | 20 | 30 | Max wolf count on map |
| `findVillagers_NearbyDistance` | 75 | 75 | 50 | 0 | Proximity for cabin hint ping (0 = no hint) |
| `fireDamageRate` | 0.35 | 0.4 | 0.7 | 1.0 | Fire damage multiplier on buildings |
| `fireThreshold` | 0.5 | 0.5 | 0.55 | 0.6 | Health % at which buildings catch fire |
| `numberOfScaredVillagers` | 6 | 6 | 5 | 3 | Number of findable villager groups |
| `mongolAttackDelay` | 10 | 10 | 8 | 5 | Minutes before final Mongol attack |
| `probingAttackFrequency` | 2 | 2 | 1.6 | 1.2 | Minutes between probing attacks |
| `probingAttackLevelAdjustment` | 0 | 0 | 1 | 2 | Offset added to probing attack escalation level |

**Difficulty-conditional logic:**
- Intro Mongol horseman counts scale with `Util_DifVar` (1-2 squads per spawn point)
- Intro spearman groups restricted by difficulty flags (`GD_EASY`, `GD_NORMAL`, `GD_HARD`)
- Final attack wave 4 is Hard/Expert only; Expert gets extra units in every wave
- Probing attacks disabled entirely on Easy (`GD_EASY`)

---

#### gdm_chp2_kulikovo

All 10 waves use `Util_DifVar({Easy, Normal, Hard, Expert})` per unit type:

| Parameter | Scales |
|-----------|--------|
| Wave squad counts | Each unit type per wave has 4-value difficulty array |
| Unit tier upgrades | Hard/Expert substitute tier-2 with tier-3 units (spearman_3, horseman_3, knight_3, manatarms_3) |
| Siege additions | Springalds appear wave 6+ (all difficulties); Mangonels wave 7+ (Normal+) |
| Village raid composition | Easy/Normal: horseman_1 ×8; Hard: horseman_2 ×8 + horse_archer_2 ×6; Expert: knight_2 ×6 + horse_archer_2 ×9 |
| Wave 10 hybrid army | Scales from ~30 squads/lane (Easy) to ~42 squads/lane (Expert) with siege |
| Gold pickup hint | `OBJ_OptionalFindVillage` only starts on Easy/Normal |

**Difficulty-conditional logic:** Hard/Expert use tier-3 units instead of tier-2. Mangonels only on Normal+. Gold pickup hint hidden on Hard/Expert.

---

#### gdm_chp2_tribute

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `bandits_GlobalCreationFrequency` | 45 | 35 | 30 | 25 | Seconds between any new bandit group globally |
| `bandits_ZoneCreationFrequency` | 90 | 90 | 75 | 55 | Seconds per zone between bandit spawns |
| `bandits_CreationFrequency_CampBonus` | 10 | 10 | 10 | 10 | Added delay per destroyed camp |
| `bandits_PauseReleaseTimer` | 25 | 25 | 15 | 15 | Seconds after combat before paused bandits resume |
| `bandits_SettlementsModifier` | -1 | 0 | 1 | 2 | Modifier to settlement "value" for bandit strength |
| `bandits_WanderersModifier` | -2 | -1 | 0 | 1 | Extra wandering bandit groups |
| `bandits_NumCamps` | 6 | 6 | 6 | 6 | Number of bandit camps placed |
| `bandits_CampDestructionBonusModifier` | -2 | -1 | -1 | -1 | Strength reduction after destroying a camp |
| `bandits_CampDestructionBonusPeriod` | 150 | 150 | 120 | 90 | Duration of camp destruction bonus (seconds) |
| `payTheMongols_BaseAmount` | 1300 | 1300 | 1500 | 1700 | Initial Mongol gold demand |
| `payTheMongols_ExtraAmountPerCycle` | 100 | 200 | 200 | 300 | Extra gold per cycle (from cycle 3+) |
| `buySettlements_TradeAmountNeededToBuy` | 500 | 500 | 750 | 1000 | Gold earned from trade before purchase unlocks |
| `buySettlements_PurchasePrice` | 300 | 300 | 500 | 700 | Gold cost to purchase a settlement |
| `buySettlements_NumSettlementsNeeded` | 3 | 3 | 4 | 5 | Settlements required for victory |
| `findSettlements_NearbyDistance` | 125 | 125 | 75 | 0 | Proximity hint radius for undiscovered settlements |

**Difficulty-conditional logic:**
- Bandit loadouts (Strength1–5) scale squad counts per `Util_DifVar`
- Starting villagers at town center: Easy gets 4, others get 2
- Easy gets +500 starting gold
- Bandit camp defenders: 7 spearmen base; Hard/Expert add +3 spearmen +4 archers; Expert adds +2 more spearmen +8 archers

---

#### gdm_chp3_moscow

All values indexed as `{Story, Easy, Intermediate, Hard}`:

| Parameter | Story | Easy | Intermediate | Hard | Scales |
|-----------|-------|------|-------------|------|--------|
| `totalMongols` | 300 | 300 | 400 | 500 | Total Mongol squads across all waves |
| `maxMongols` | 60 | 80 | 120 | 200 | Max simultaneous Mongol squads on field |
| `mongolFrequency` | 120 | 120 | 120 | 90 | Seconds between wave spawn attempts |
| `mongolMaxRams` | 0 | 3 | 5 | 8 | Max rams in wave compositions |
| `timeTillFailure` | 120 | 60 | 30 | 30 | Seconds before inner breach causes failure |
| `siegeWaves` | 120 | 120 | 200 | 240 | Threshold where siege units begin appearing |
| `preperationTime` | 420 | 420 | 300 | 300 | Seconds of preparation before attack |
| `escapingVillagers` | 100 | 100 | 200 | 300 | Number of refugees needed for evacuation victory |
| Starting resources Gold | 1500 | 1000 | 500 | 0 | Player starting gold |
| Starting resources Wood | 5000 | 3000 | 2000 | 1000 | Player starting wood |
| Starting resources Food | 3000 | 2400 | 1200 | 600 | Player starting food |
| Starting resources Stone | 1000 | 600 | 300 | 100 | Player starting stone |
| Villager count | 9 | 8 | 8 | 8 | Villagers per resource gathering group |

**Difficulty-conditional logic:** Story mode uses simplified compositions (horsemen instead of knights, no siege), resource raiders disabled. Final infinite Mongols: Story capped at 20 with 15s delay; other difficulties cap at 20 + (refugeesSpawned/10) with 5 × (1 - refugeesSpawned/500)s delay.

---

#### gdm_chp3_novgorod

All values are `Util_DifVar({Story, Easy, Normal, Hard})`:

| Parameter | Story | Easy | Normal | Hard | Scales |
|-----------|-------|------|--------|------|--------|
| `given_resources_gold` | 1000 | 800 | 400 | 250 | Starting gold |
| `given_resources_wood` | 200 | 200 | 150 | 100 | Starting wood |
| `given_resources_food` | 200 | 200 | 150 | 100 | Starting food |
| `given_resources_stone` | 100 | 100 | 70 | 60 | Starting stone |
| `i_request_Nov_upperThreshold` | — | — | — | 0.6–0.9 | AI request upper threshold |
| `i_request_Nov_lowerThreshold` | — | — | — | 0.15–0.1 | AI request lower threshold |
| `i_request_Nov_desiredStrength` | — | — | — | 0.7–1.0 | AI desired strength |
| `i_maximumNumberOfWolves` | 10 | 10 | 8 | 6 | Max wolf spawns |
| `i_maximumNumberOfAnimals` | 30 | 22 | 20 | 15 | Max boar spawns |
| `i_maximumNumberOfAnimalsTown01` | 20 | 15 | 12 | 10 | Max deer near town 01 |
| `enemy_unitBuildTime` | 30 | 25 | 10 | 12 | Standard unit build time |
| `enemy_eliteUnitBuildTime` | 40 | 30 | 15 | 14 | Elite unit build time |

**Difficulty-conditional logic:**
- Story mode: attack waves disabled entirely, extra villagers on capture, optional objectives on Easy/Normal only
- Hard: `Wave_OverrideUnitBuildTime` applied to all unit types
- Non-Story: wooden forts get springald upgrades for player2

---

#### gdm_chp3_ugra

| Parameter | Easy | Standard | Hard | Hardest | Scales |
|-----------|------|----------|------|---------|--------|
| `prepareTimer` | 520 | 520 | 400 | 280 | Countdown for preparation phase (seconds) |
| `monReinforcePeriod` | 85 | 54 | 48 | 42 | Interval for wave prep (seconds) |
| `monReinforcePhase2Delay` | 450 (50%) | 450 (50%) | 297 (33%) | 225 (25%) | One-shot to trigger Phase 2 escalation |
| `monReinforcePhase3Delay` | 9999 (never) | 9999 (never) | 594 (66%) | 450 (50%) | One-shot to trigger Phase 3 escalation |
| `monReinforcePhase4Delay` | 9999 (never) | 9999 (never) | 9999 (never) | 675 (75%) | One-shot to trigger Phase 4 escalation |
| `monWaveTimer` | 60 | 60 | 60 | 60 | Interval for cavalry raids (seconds) |
| Villager count (sg_rus_villagers2) | 8 | 6 | 6 | 6 | Starting villagers group 2 |
| Villager count (sg_rus_villagers3/4) | 4 | 3 | 3 | 3 | Starting villagers groups 3/4 |
| Ford1 spearman | 4 | 6 | 6 | 6 | Ford garrison spearmen |
| Ford1 archer | 8 | 10 | 10 | 10 | Ford garrison archers |
| Ford1 crossbow | 3 | 5 | 5 | 5 | Ford garrison crossbowmen |
| Probe horseman (Ph1) | 4 | 4 | 6 | 6 | Cavalry raid horsemen |
| Probe horsearcher (Ph1) | 2 | 2 | 2 | 4 | Cavalry raid horse archers |
| Probe knight (Ph1) | 0 | 0 | 0 | 2 | Cavalry raid knights (Hardest only) |
| Southern reinforce horseman | 6 | 6 | 6 | 8 | Southern column horsemen |
| Southern reinforce horsearcher | 4 | 6 | 8 | 10 | Southern column horse archers |
| Southern reinforce MAA | 0 | 2 | 4 | 4 | Southern column men-at-arms |
| Southern reinforce archer | 4 | 6 | 8 | 10 | Southern column archers |
| Southern reinforce mangonel | 0 | 1 | 2 | 2 | Southern column mangonels |
| Southern reinforce ram | 1 | 1 | 1 | 2 | Southern column rams |

**Difficulty-conditional logic:** Phase 3 only on Hard+. Phase 4 only on Hardest. Easy/Standard never escalate beyond Phase 2. Rams added to probe waves if player has walls.

---

#### gdm_chp4_kazan

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `kazan_waveinterval` | 210 | 210 | 180 | 150 | Seconds between cavalry attack waves |
| Villager count | 11 | 8 | 8 | 8 | Villagers per transport group |
| NorthGate archers | 3 | 6 | 6 | 6 | Archer squads at north gate |
| NorthGate handcannon | 2 | 2 | 2 | 6 | Handcannon squads at north gate |
| Wall defenders (typical) | 5 | 8 | 8 | 10 | Archers per wall section |
| Wall handcannon (typical) | 2 | 4 | 4 | 8 | Handcannon per wall section |
| Elite knights | 14 | 20 | 24 | 28 | Khan's Guard knight squads |
| Elite handcannon | 8 | 12 | 16 | 20 | Khan's Guard handcannon squads |
| Outer wall archers | 3-4 | 5 | 5 | 8 | Archers per outer wall segment |
| Inner wall mixed | 0-4 | 2-4 | 2-4 | 6-8 | Archers+handcannon per inner wall segment |
| Outpost upgrades | Springald | Springald | Springald | Cannon | Outpost weapon type |
| Tower upgrades | Springald | Springald | Cannon | Cannon | Tower weapon type |
| DefendWoodcutters spearman | — | — | 4 | 4 | Extra spearmen on Hard/Expert only |
| DefendNorthOutpost1 units | 4 spear | 4 spear | 6 MAA | 6 MAA | Unit type swaps by difficulty |
| DefendWestRoad2 units | +4 spear | +4 spear | +6 MAA | +6 MAA | Extra defenders by difficulty |
| Wave compositions | Smaller | Smaller | Larger + siege | Larger + siege | Per-intensity wave unit counts |
| West ford loop | Active | Active | Active | Active | West ford waves |
| Cavalry waves | Skipped | Active | Active | Active | No recurring waves on Easy |

**Difficulty-conditional logic:**
- Cavalry waves skipped entirely on Easy
- West ford loop skipped on Easy
- Hard/Expert: mangonels at tier 3+, trebuchets at tier 5+
- Hard/Expert: unit type swaps from spearmen to MAA at outposts
- Tower upgrades: Cannon on Hard/Expert for towers, Cannon on Expert for outposts

---

#### gdm_chp4_smolensk

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| Roslavl defenders (horseman) | 6 | 8 | 8 | 10 | Horseman squads at Roslavl |
| Roslavl defenders (knight) | 4 | 6 | 6 | 14 | Knight squads at Roslavl |
| Yelnya defenders (archer) | 8 | 10 | 10 | 6 | Archer squads at Yelnya |
| Yelnya defenders (crossbow) | 2×2 | 2×3 | 2×4 | 2×6 | Crossbow squads (two spawn points) |
| Yelnya defenders (handcannon) | 2×1 | 2×1 | 2×2 | 2×4 | Handcannon squads (two spawn points) |
| Vyazma defenders (spearman) | 2×4 | 2×5 | 2×5 | 2×8 | Spearman squads (two spawn points) |
| Vyazma defenders (MAA) | 4 | 6 | 6 | 12 | Men-at-arms squads at Vyazma |
| West outpost (spearman) | 2×2 | 2×4 | 2×4 | 2×8 | Spearman squads (two flanks) |
| West outpost (MAA) | 2×2 | 2×4 | 2×4 | 2×6 | MAA squads (two flanks) |
| East outpost (spearman) | 6 | 8 | 8 | 12 | Spearman squads |
| East outpost (MAA) | 4 | 6 | 6 | 8 | MAA squads |
| East outpost (archer) | 6 | 8 | 8 | 12 | Archer squads |
| East outpost (crossbow) | 4 | 6 | 6 | 8 | Crossbow squads |
| Tower upgrades | Springald | Springald | Cannon | Cannon | Smolensk tower weapon type |
| Wall defenders (crossbow) | 8 | 8 | 10 | 10 | Crossbow per wall section |
| Wall defenders (handcannon) | 4 | 4 | 6 | 8 | Handcannon per wall section |
| Smolensk melee (spearman) | 4 | 4 | 6 | 8 | Interior spearman squads |
| Smolensk melee (MAA) | 2 | 4 | 6 | 8 | Interior MAA squads |
| Smolensk ranged (crossbow) | 2×5 | 2×6 | 2×8 | 2×12 | Interior crossbow (two groups) |
| Smolensk ranged (handcannon) | 2×3 | 2×4 | 2×8 | 2×12 | Interior handcannon (two groups) |
| Smolensk cavalry (horseman) | 6 | 8 | 8 | 16 | Interior horseman squads |
| Smolensk siege (cannon) | 1 | 2 | 4 | 4 | Interior cannon squads |
| Smolensk wave attacks | 1 route | 1 route | 2 routes | 3 routes | Number of simultaneous attack routes |
| Extra starting villagers | +4 | +0 | +0 | +0 | Bonus villagers on Story difficulty |

**Difficulty-conditional logic:** Difficulty determines how many of 3 routes launch simultaneously (1 on Easy/Normal, 2 on Hard, 3 on Expert). Tower upgrades: Cannon on Hard/Expert.

---

### Rogue (The Sultans Ascend)

Uses a unique 7–8 tier difficulty system via `Rogue_DifVar` instead of the standard 4-tier `Util_DifVar`.

#### rogue_maps

| Parameter | Values | Map | Scales |
|-----------|--------|-----|--------|
| `Util_DifVar({0,1,1,2,2,3,3})` | 0/1/1/2/2/3/3 | coastline_data | Minor naval unit count at POIs |
| `Rogue_DifVar({0,0,10,35,50,65,80,100})` | 0/0/10/35/50/65/80/100 | forest, daimyo | Wolf spawn chance percentage |
| `Rogue_DifVar({2100,1500,1000,900,800,600,450,300})` | 2100/1500/1000/900/800/600/450/300 | coastline | Naval raid start delay (seconds) |
| `naval_raid_spawn_delay = 300 - (difficulty * 15)` | Formula | coastline_pirates | Ship respawn interval (seconds) |
| `GetIntegerInExponentialRange(600, 200)` | 600→200 | steppe_raiders | Raid start time (inversely scaled) |
| `GetIntegerInExponentialRange(450, 150)` | 450→150 | steppe_raiders | Raid frequency interval |
| `GetFloatInExponentialRange(1.0, 4.0)` | 1.0→4.0 | steppe_raiders | Raider income accumulation rate |
| `GetIntegerInExponentialRange(3, 9)` | 3→9 | steppe_raiders | Defender count at raider base |
| `rogue_wave_strength` | 0.85–1.0 | all rogue maps | Global wave power multiplier |
| `WAVE_STAGING_DURATION` | 1 (daimyo) / 5 (steppe) | daimyo, steppe | Seconds waves idle before attacking |
| Outpost upgrade tier | arrowslits→cannon | steppe_raiders | Scales with `Game_GetSPDifficulty()` |

**Difficulty-conditional logic:** `Rogue_DifVar` takes up to 8 values for the 7-tier system. Steppe attacks only launch if difficulty > 0. Forest/Daimyo wave strength set to 0.85. Steppe wave strength set to 0.9. Naval raids disabled on lowest difficulties (2100s = 35 min delay).

---

### The Normans (Salisbury)

#### sal_chp1_rebellion — No difficulty scaling. Fixed tutorial.
#### sal_chp1_valesdun — No difficulty scaling. Fixed tutorial.
#### sal_chp2_dinan — No difficulty scaling. Fixed tutorial.
#### sal_chp2_township — No difficulty scaling. Fixed tutorial.
#### sal_chp2_womanswork — No difficulty scaling. Fixed tutorial.
#### sal_chp3_brokenpromise — No difficulty scaling. Fixed tutorial.

---

## Cross-Mission Comparison

### Common Scaling Categories

#### Starting Resources
The most universally scaled parameter across all campaigns. Typical pattern: `{400, 300, 200, 100}` per resource type.

| Range | Missions |
|-------|----------|
| 400/300/200/100 (per type) | hun_chp1_paris, hun_chp2_pontvallain, hun_chp3_orleans |
| 1000/800/600/400 (per type) | hun_chp2_cocherel (wood/food), mon_chp2_liegnitz |
| 5000→1000 (wood) | gdm_chp3_moscow (most extreme range) |
| 3000→2000 (gold) | hun_chp4_rouen |

#### Wave/Attack Intervals
Timing between enemy wave dispatches — shorter = harder.

| Range (seconds) | Missions |
|-----------------|----------|
| 570→270 | mon_chp1_juyong (multiple wave sources) |
| 480→120 | mon_chp1_zhongdu (raid timing) |
| 360→180 | mon_chp2_kiev (main attack interval) |
| 600→280 | ang_chp4_lincoln (French wave interval) |
| 300→210 | abb_m5_mansurah (invasion interval) |
| 180→90 | gdm_chp3_moscow (Mongol frequency) |
| 210→150 | gdm_chp4_kazan (wave interval) |

#### Unit Counts (Per Squad/Module)
Standard scaling ratios used across campaigns.

| Pattern | Typical Values | Usage |
|---------|---------------|-------|
| Standard linear | {6, 7, 10, 14} | Most common defender/patrol count (appears in 10+ missions) |
| Low-count linear | {2, 3, 4, 5} | Small garrison/barricade positions |
| Medium linear | {4, 5, 7, 10} | Patrol and escort groups |
| High-count linear | {8, 10, 14, 20} | Large garrison/army modules |
| Aggressive ramp | {6, 9, 12, 15} | abb_bonus unitCount_high pattern |
| Expert spike | {4, 4, 4, 6} | Common pattern where Expert gets a notable jump |

#### Military Build Time Modifiers
Production speed bonuses for the player on easier difficulties.

| Values | Missions |
|--------|----------|
| 0.5 / 0.75 / 1 / 1 | abb_m5_mansurah, abb_m6_aynjalut, abb_m7_acre |
| 2.0 / 1.8 / 1.25 / 1.0 | abb_m4_hattin |
| 0.5 / 0.75 / 1 / 1 | abb_m3_redsea |

#### Upgrade/Emplacement Tiers
Outpost and tower upgrade levels that scale by difficulty.

| Pattern | Missions |
|---------|----------|
| —/Arrowslits/Springald/Cannon | abb_m8_cyprus |
| Springald/Springald/Springald/Cannon | gdm_chp4_kazan (outposts) |
| Springald/Springald/Cannon/Cannon | gdm_chp4_kazan (towers), gdm_chp4_smolensk |
| Arrowslits/Arrowslits/Arrowslits/Springald | mon_chp2_mohi |
| Arrowslits→Cannon | rogue steppe_raiders |

#### Unit Type Substitutions
Higher difficulties often replace weaker unit types with stronger ones.

| Substitution | Missions |
|-------------|----------|
| Horsemen → Knights | mon_chp1_kalka_river (player army), mon_chp3_xiangyang_1273 (raider composition) |
| Spearmen → MAA | mon_chp2_mohi (defense lines), gdm_chp4_kazan (outpost defenders) |
| Archers → Crossbowmen | mon_chp2_mohi (defense lines) |
| Militia → Spearmen+Crossbowmen | mon_chp3_xiangyang_1273 (retaliation waves) |
| Tier-2 → Tier-3 units | gdm_chp2_kulikovo (all unit types) |
| Springald → Cannon | gdm_chp4_kazan (tower upgrades) |

### Difficulty Mechanisms Summary

| Mechanism | Count | Description |
|-----------|-------|-------------|
| `Util_DifVar` numeric scaling | ~50 missions | Standard 4-tier value selection |
| Feature enable/disable | ~15 missions | Entire systems toggled on/off (e.g., attack waves on Easy) |
| Unit type substitution | ~10 missions | Weaker → stronger unit types on harder |
| Upgrade tier scaling | ~8 missions | Building/outpost emplacement upgrades |
| Attack lane expansion | ~3 missions | More approach routes on harder (abb_m5, gdm_chp4_smolensk) |
| Conqueror Mode (challenges) | 5 challenges | Dynamic difficulty based on player performance |
| Medal tiers (challenges) | 13 challenges | Score-based grading (time, kills, resources) |
| `Rogue_DifVar` 7-8 tier | 1 campaign | Unique multi-tier system for roguelike mode |
| Production speed bonuses | ~6 missions | Faster military build on easier difficulties |
| Hint/guidance toggling | ~8 missions | Optional objectives and proximity hints hidden on harder |

### Missions with No Difficulty Scaling

| Mission | Reason |
|---------|--------|
| ang_chp0_intro | Fixed tutorial |
| sal_chp1_rebellion | Fixed tutorial |
| sal_chp1_valesdun | Fixed tutorial |
| sal_chp2_dinan | Fixed tutorial |
| sal_chp2_township | Fixed tutorial |
| sal_chp2_womanswork | Fixed tutorial |
| sal_chp3_brokenpromise | Fixed tutorial |

All 7 non-scaling missions are tutorial/introductory missions from the Salisbury (Normans) and Angevin campaigns.
