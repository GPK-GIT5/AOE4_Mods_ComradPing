# AI Patterns Index

Cross-reference of AI systems, module configurations, patrol behaviors, and custom AI logic across all campaign missions.

## System Architecture

### Army System (`army.scar`)

Primary scripted AI abstraction managing groups of units through target sequences.

**Lifecycle:** `Army_Init(params)` → target sequencing → state machine → death/revival

**Target Order Modes:**
- `TARGET_ORDER_LINEAR` — process targets sequentially
- `TARGET_ORDER_LOOP` — restart from first target after completion
- `TARGET_ORDER_PATROL` — reverse direction at endpoints
- `TARGET_ORDER_RANDOM` — select next target randomly

**States:** `ENCOUNTER_TYPE_ATTACK`, `DEFEND`, `TRANSPORT`, `EMPTY`, `NONE`

**Death Handling:**
- `onDeathFunction` — callback fired when all units die
- `onDeathReset = true` — restart from target 1 when refilled
- `onDeathDissolve = true` — permanently remove the army

**Combat Arena Defaults:**
| Parameter | Default |
|-----------|---------|
| `combatRangeAtTarget/EnRoute` | 35 |
| `leashBuffer` | 10 |
| `idleTime` | 0 |
| `ramsBuiltWhenBlocked` | 1 |
| `ramPassengerCount` | 8 |
| `openPathThreshold` | 120 |
| `brokenWallThreshold` | 30 |

**Building Engagement Presets:** `BUILDINGS_NONE`, `BUILDINGS_ALL`, `BUILDINGS_ALL_BUT_TC`, `BUILDINGS_THREATENING`, `BUILDINGS_IMPORTANT`

### ArmyEncounterFamily (`army_encounter.scar`)

Handles armies with squads too spread out for a single encounter:
1. `SGroup_DivideIntoClusters` (50-unit threshold)
2. First cluster = parent encounter, others = children
3. Each gets own `AIStateTree_SpawnRootControllerWithStateModelTunings`
4. Parent promotion on completion; army-level callback when all done

**End Reasons:** `AtDestination`, `EnemiesAtTargetCleared`, `Timeout`, `CombatThreshold`, `ShouldFallback`, `SelfSquadsEmpty`, `CannotReachDestination`, `Torndown`, `WasAttacked`

### Encounter Plans

Plans registered via `Encounter_RegisterPlan()` with phases, start/notification/end callbacks, and `defaultGoalData`.

**Attack Plan:** Single `Main` phase. StateTree branch `campaign_encounters\scar_encounters\AttackDefault`. Tunings blueprint `campaign_attack_default`. Supports form-up, idle-at-end, fallback thresholds, archer repositioning, ram building.

**Attack-Move Styles:**
| Style | Behavior |
|-------|----------|
| `attackMoveStyle_ignoreEverything` | Bypass all buildings |
| `attackMoveStyle_ignorePassive` | Skip houses/farms/economy |
| `attackMoveStyle_normal` | Default building engagement |
| `attackMoveStyle_aggressive` | Heightened building engagement |
| `attackMoveStyle_attackEverything` | Engage all except settlements/walls |
| `attackMoveStyle_excludeTC` | Attack everything except town centers |

**Defend Plan:** Two phases (`Idle` → `Main`). Idle monitors at 0.5s: `triggerOnSight`, `triggerOnEngage`, `triggerOnUnderAttack`. Uses `campaign_defend_default` tunings.

**Move Plan:** Three phases (`FormUp` → `Move` → `Intercept`). Legacy `AI_CreateRestoreEncounter` API. 90% threshold for form-up.

**DoNothing Plan:** Placeholder — reserves encounter ID without commands.

**TownLife Plan:** Legacy `AIEncounterType_TownLife`. Villagers work in area; optional `canBuild`.

### StateTree Tuning Parameters

| Category | Key Parameter | Purpose |
|----------|--------------|---------|
| Boolean | `clear_enemy_squads/buildings` | Whether to engage units/buildings |
| Boolean | `exit_on_path_blocker_detected` | Exit on wall detection |
| Boolean | `should_hold_position` | Hold while idle at target |
| Boolean | `allow_attack_move` | Attack-move vs forced attack |
| Float | `combat_area` | Fight-continuation radius (default 30) |
| Float | `combat_leash` | Max pursuit distance |
| Float | `enemy_scan_range` | Enemy detection radius |
| Float | `idle_at_end_seconds` | Post-arrival idle time |
| Float | `fallback_combat_rating` | Combat rating retreat threshold |
| Float | `fallback_squad_health_threshold` | Health-based retreat |
| Float | `archer_reposition_time_interval` | Archer micro timing |
| Integer | `override_encounter_id` | SCAR-assigned encounter ID |
| Integer | `ram_number_to_build` | Rams to construct when blocked |

---

## Module Types (from `missionomatic.md`)

All modules share: `Init → Monitor → GetSGroup/AddSGroup/RemoveSGroup → Disband → IsDefeated`

### Defend Modules
- Hold position with Defend encounter plan
- Supports `withdrawData` — flee on spotted/units-left/custom-condition
- `combatRange` and `leashRange` parameters constrain engagement area
- Monitor interval: 1s
- Can provide units to other modules via `Defend_UnitRequest_Start`

### Attack Modules
- Assault target with Attack encounter plan
- Monitor interval: 5s (checks reinforcement needs)
- Supports dynamic target updates via `Attack_UpdateTargetLocation`
- Can provide units to requester modules

### RovingArmy Modules
- Mobile force cycling through target waypoints
- **Targeting modes:** `Discard`, `Cycle`, `Reverse`, `Proximity`, `Random`, `RandomMeandering`
- State machine: `EMPTY | ATTACKING | DEFENDING | DISSOLVED | DISSOLVING_INTO_MODULE`
- Supports `withdrawThreshold` for automatic fallback to withdraw marker
- Monitor interval: 1s

### TownLife Modules
- AI economy — villager production, gathering, building
- Uses skirmish AI via `AIPlayer_GetOrCreateHomebase`
- Produces units for other modules via internal wave manager
- Monitor interval: 5s
- Acts as primary unit provider in reinforcement pipeline

### UnitSpawner Modules
- Barebones spawner for initial unit placement or off-map reinforcement
- Configurable `spawnRate`
- Acts as unit provider with production time estimate
- Often used for pre-placed tutorial/garrison units

---

## Campaign AI Usage

### Abbasid Dynasty

#### abb_bonus
**Modules used:** Army_Init (RovingArmy-style) — 7 patrol armies, P2 attack-wave armies, P5 naval raids. All hand-scripted.
**Patrol behaviors:** 7 patrol routes (2 cavalry, 1 infantry, 4 spear) via Army_Init. P5 naval raiders patrol in 3 groups.
**Special AI logic:** P2 cavalry raiders retreat when outnumbered 3:1. Economy-driven wave scaling. No `AI_Enable`.
**Difficulty-based AI tuning:** `unitCount_low` (2/3/4/5), `unitCount_med` (4/6/8/10), `raidSpawnMod` (1.6/1.4/1.2/1.0).

#### abb_m1_tyre
**Modules used:** UnitSpawner (player forces), RovingArmy (patrols), Army (mole escorts, ambush pairs)
**Patrol behaviors:** 4 camps with patrol armies. 4 ambush pairs. Escort splitting at mole trigger points.
**Special AI logic:** Custom villager AI state machine (gather→flee→garrison→attack-move→reconstruct→return). No encounter plans.
**Difficulty-based AI tuning:** `skirmish_attack_threshold` (10→20), `ram_weapon_cooldown` (2→1s), `ambush_delay` (120→30s).

#### abb_m2_egypt
**Modules used:** RovingArmy — custom heatmap/quadrant targeting. No `AI_Enable`.
**Patrol behaviors:** None (heatmap replaces patrols). `AssignOldestWaitingArmyToBestTarget` every 1s.
**Special AI logic:** Heatmap evaluation every 0.125s with aggression factors. `AI_AGGRESSION_LOSINGMULTIPLIER` boosts when AI holds <5 points.
**Difficulty-based AI tuning:** `attack_group_size` (10/10/10/15), `ATTACK_INTERVAL` (20/20/20/15), dynamic aggression values.

#### abb_m3_redsea
**Modules used:** NavalArmy_Init (fleets), Army_Init (garrison), pirate island garrison (4 modules)
**Patrol behaviors:** Pirate patrol fleet on fixed route. Hunter fleet with random routes, `SGroup_CanSeeSGroup` detection. `TARGET_ORDER_LOOP` for waypoints.
**Special AI logic:** `Pirates_Monitor` hunter fleet behavior. Pirate dock auto-rebuild every 5s. Net formation (3 fleets closing). Wave interval decay (1.0→0.4). `BUILDINGS_ALL` for blockaders.
**Difficulty-based AI tuning:** `pirateRespawnDelay` (90→15s), raider routes (4→6), `raiderFinaleNetMultiplier` (1.0→2.0).

#### abb_m4_hattin
**Modules used:** UnitSpawner. `CRUSADERS_USE_AI = false` — custom path-following.
**Patrol behaviors:** None — marker-based path following, not AI patrols.
**Special AI logic:** Custom path-following via `Crusaders_ManageEntry`. Non-AI pursuit within `CRUSADER_PURSUIT_LEASH` (225), leash back after 90s. Straggler detection.
**Difficulty-based AI tuning:** Unit counts and combat parameters scale, not AI behavior directly.

#### abb_m5_mansurah
**Modules used:** Army_Init — 34 defending armies, holy orders, ambush squads, invasion forces
**Patrol behaviors:** Holy orders: `TARGET_ORDER_PATROL` (combatRange 45, leashRange 85). Singles: bounce-patrol, looping, stationary modes.
**Special AI logic:** Camp pool system — 7 pools with weighted random activity (Wander→Idle→Rest/Lighthouse/Patrol). No encounter plans.
**Difficulty-based AI tuning:** Front army units (5/6/9/12), attack lanes (N only Easy/Normal, W/N/E Hard/Expert), `DEFAULT_IDLE_DELAY` (3/2.5/2/1.5).

#### abb_m6_aynjalut
**Modules used:** Army with `USE_AI_GLOBAL = true` for side cohorts. Rank formation spawning.
**Patrol behaviors:** Completed armies switch to `TARGET_ORDER_PATROL` targeting Afula.
**Special AI logic:** Custom force order system (hill→half→field→battle→town→finish_afula). Road forces NOT using AI until phase-triggered.
**Difficulty-based AI tuning:** `player_prepare_time` (60/52/46/40).

#### abb_m7_acre
**Modules used:** Army — `TARGET_ORDER_PATROL` for patrols, `TARGET_ORDER_LINEAR` for attacks
**Patrol behaviors:** 3 cavalry patrol waypoint sets. 2 ship patrol sets.
**Special AI logic:** Counter-attack: periodic redirection of nearest armies to siege camp, escalating. Amortized spawning (0.005s). AI_Enable only in autotest.
**Difficulty-based AI tuning:** `CAVALRY_PATROL_SIZE` (4/4/4/6), `COUNTER_ATTACK_TIMER` (600/400/300/300), naval attacks Hard+ only.

#### abb_m8_cyprus
**Modules used:** Army/NavalArmy — 5 Nicosia defenders, cavalry/infantry patrols, Famagusta defenders, Kyrenia cavalry. BuildingTrainer for waves.
**Patrol behaviors:** `TARGET_ORDER_PATROL` for cavalry, `TARGET_ORDER_RANDOM` for Famagusta. Naval raids patrol 6 destination markers.
**Special AI logic:** `Nicosia_Attack_Blocked` dissolves army + retreats when path blocked. BuildingTrainer wave production, 10s build override. Nicosia retreat at threshold. Kyrenia reinforces Nicosia at final zone.
**Difficulty-based AI tuning:** `nicosia_grace_timer` (220/160/100/40), `nicosia_attacks_timer` (420/360/300/240), upgrades on Hard+.

---

### Angevin Empire

#### ang_chp0_intro
**Modules used:** UnitSpawner (horsemen, archers), Defend (spearmen — combatRange 60, leashRange 85), RovingArmy (cavalry scout, spearman patrol)
**Patrol behaviors:** Scout patrols 2 markers. Spearmen roving across 4 waypoints + clifftop.
**Special AI logic:** Tutorial — scripted enemies. Defenders dissolve into roving via `DissolveModuleIntoModule`. Villagers flee at 1.15× speed.
**Difficulty-based AI tuning:** None — tutorial.

#### ang_chp1_hastings
**Modules used:** Defend (DefendHillLeft/Center/Right, DefendHaroldLeft/Center/Right, KingHaroldDefenders1–4), UnitSpawner (shield wall, reinforcements), Encounter (enc_kingHarold — combatRange 10, leashRange 15)
**Patrol behaviors:** None — positional Defend with dynamic retargeting (nearest player concentration, 3s interval, staggered 0/1/2s).
**Special AI logic:** Shield wall with row-based backfill. Harold striker system pulls Defend units. Threshold decay (-0.1/adjustment, limit 0.5). Feigned retreat breaks wall at 65% kill.
**Difficulty-based AI tuning:** `maxNumberOfWilliamAttackers` (2/2/3/4). Reinforcement limits per unit type.

#### ang_chp1_york
**Modules used:** RovingArmy (WestPatrol, BaileyPatrol, KeepPatrol, CavalryRaiders, DaneAttackers1/2/3, EarlyRaiders, RiverRebels, BridgeGuards), Defend (MiddlethorpeRebels, FulfordRebels, DaneDefenders, NorthGateRebels, CityRebels, KeepDefenders, OutpostGuards)
**Patrol behaviors:** WestPatrol/BaileyPatrol/KeepPatrol — dynamic targets based on `rebels_attackGroupCount`. Dane raiders: traveling→raiding→retreating cycle.
**Special AI logic:** 3-faction simultaneous (Village Rebels, City Rebels, Danes). Dane withdraw at 50%. Early raider escalation cycle. Defend-the-keep redirects patrols.
**Difficulty-based AI tuning:** `danes_spawnDelay` (240/200/160/120), `danes_raiderCountCap` (16/20/30/40), `rebels_patrolCount` (3/6/8/12), `rebels_maxModuleSize` (10/15/25/35).

#### ang_chp2_bayeux
**Modules used:** RovingArmy (cavalry patrols, gate infantry×3, wall defenders), Defend (wall archers, wood mill)
**Patrol behaviors:** Cavalry with `ARMY_TARGETING_REVERSE`, combatRange 40, leashRange 500, withdrawThreshold 0.45. 5–9 groups by difficulty.
**Special AI logic:** Idle attack system (disabled on Story). Push attack directs infantry. Rush detection: all modules rush if player army < 5. Dissolution cascade: withdrawn cavalry → wall defense. `attackMoveStyle_ignoreEverything` for wall holders.
**Difficulty-based AI tuning:** `enemyCavalry` (10/12/14/10), `enemyKnights` (0/0/1/5), `idleattacktimer` (0/6/4/1 min), `rovingArmy_DefendPositions` (5/5/7/9).

#### ang_chp2_bremule
**Modules used:** RovingArmy (FrenchArmy1, Louis_Retinue, scouts, ram), Encounter (Camp_Defense — combatRange 90, leashRange 160, `attackMoveStyle_attackEverything`), VillagerLife
**Patrol behaviors:** Scouts with `ARMY_TARGETING_RANDOM` across 8 waypoints, respawn on death. Louis at 0.35× speed.
**Special AI logic:** Camp/patrol dissolves to Encounter on player proximity. Counter-attacks: 25% army split as disposable roving (`onDeathDissolve`). VillagerLife rebuilds captured buildings.
**Difficulty-based AI tuning:** `attackWaveScale` (0/0/1/2), `attackWaveFrequency` (15/15/10/5 min), Easy uses `CYCLE` targeting, others `DISCARD`.

#### ang_chp2_tinchebray
**Modules used:** Defend (3 Robert army modules — 20 spearmen + 10 archers), RovingArmy (DukeRobert, relief army, village guards, scouts)
**Patrol behaviors:** Scouts with `ARMY_TARGETING_RANDOM` across 11 markers. Relief army: 8 sequential waypoints.
**Special AI logic:** Robert state machine: defend → sally out (dissolve to RovingArmy) → attack (`ARMY_TARGETING_CYCLE`). AI tracking: attacks visible player, continues to last known position, reverts on losing sight. Relief army merges into Robert's modules.
**Difficulty-based AI tuning:** `enemy_mainarmy_maa` (10/15/15/15), `enemy_mainarmy_knight` (0/0/10/18).

#### ang_chp3_lincoln
**Modules used:** RovingArmy (GeneralGroup, Besiegers1–5, RoyalGuard1–2, FinalAttackers1–3, LeftPatrol, RightPatrol, FieldPatrol, Welsh A/B/C), Defend (CampLeftDefend1, CampMiddleDefend1–2, CampRightDefend1–2)
**Patrol behaviors:** LeftPatrol/RightPatrol — archer patrols between camp waypoints. FieldPatrol — 8 archers along field line.
**Special AI logic:** Stealth ambush with reinforcement column interception. Besiegers cycle-target `t_besiege_targets`. FinalAttackers with forced retreat. Flank respawning every 10s. Welsh allies split into archers + spearmen.
**Difficulty-based AI tuning:** `enemy_fa_maa` (6/8/12/15), `camp_defender_count` (8/10/12/14).

#### ang_chp3_wallingford
**Modules used:** Defend (3 fort defenders + 2 front-line each, 4 RovingArmy defenders), RovingArmy (siege_patrol_1–5, patrol_1–7), Wave system
**Patrol behaviors:** MAA patrols with random targeting (10–12s idle). Knight cavalry with reverse targeting across 10 waypoints (3s idle). Mixed patrols with reverse/random targeting.
**Special AI logic:** Multi-lane wave system (NE/N/NW). Reinforcement dissolution at 50% strength (2 rounds). Assault retreat on outpost destruction. 125s repeating interval.
**Difficulty-based AI tuning:** Defender counts scale significantly (spearmen 5/7/10/14, fort MAA 5/7/10/14, mangonels 0/0/1/2).

#### ang_chp4_dover
**Modules used:** RovingArmy (AttackNorth/South, RangedSiege, TowerAttack), Defend (DefendNorth/South, DefendCamp, Rearguard1–3, forest modules)
**Patrol behaviors:** Road patrols (10 cycling compositions — Hard+ only, replenished below threshold). Forest patrols to random Defend modules.
**Special AI logic:** Multi-wave siege with countdown timers. Siege tower waves delayed 15s. Supply train system (escort + cart, reserve on arrival). Reserve transfer to weaker Defend when >9. `AIPlayer_SetMarkerToUpdateCachedPathToPosition`.
**Difficulty-based AI tuning:** `supplyLoopTimer` (60/60/50/40), `road_patrol` count (0/0/2/3).

#### ang_chp4_lincoln
**Modules used:** Defend (RebelDefenders1–3, FortDefenders, CampGuards1–5), RovingArmy (RebelAttack1–3, FrenchAttackA/B, FrenchPatrolA, FrenchFortSpringaldA/B)
**Patrol behaviors:** FrenchPatrolA cycling between gate markers (5 MAA + 5 crossbowmen).
**Special AI logic:** Rebel wave escalation (8 compositions × 3 channels). French activate after rb buildings destroyed. Premature attack on player scouting. `PlayerUpgrades_Auto`.
**Difficulty-based AI tuning:** `rebelDefenderCount` (5/5/10/15), `enemyTargetLevel` (0/0/1/2 — French path complexity).

#### ang_chp4_rochester
**Modules used:** RovingArmy (DefendVillage/Rochester/Keep, WallHoleDefense, SiegeCounter, attack waves), dynamic marker-based defenders (`mkr_infantry/elite/cavalry/siege_defender`) with `onDeathDissolve = true`
**Patrol behaviors:** DefendCountryside — cavalry on farm destruction. DefendTraderoute — cavalry on first trade cart kill.
**Special AI logic:** Siege entropy: 20% non-critical units surrender on side objective. CounterSiegeHunt tracks wall attackers. PushAttack every 30s redirects Defend at player. Cost-budget wave system. Story mode disables waves.
**Difficulty-based AI tuning:** `defenderValue` multiplier (1/1/1.15/1.25), `baseWaveValue` (5/5/5/10), `waveDownTime` ranges.

---

### Challenges

#### challenge_advancedcombat
**Modules used:** None (scripted waypoints via `Cmd_FormationAttackMove`)
**Special AI logic:** `RespondToPlayerAttack` polls 1.5s, redirects idle AI. Wave 6 knight split. Building vulnerability acceleration.

#### challenge_basiccombat
**Modules used:** None (scripted waypoints)
**Special AI logic:** `RespondToPlayerAttack` polls 1.5s. Village buildings get `Modify_TargetPriority = 100`.

#### challenge_earlyeconomy
No AI — pure economy tutorial.

#### challenge_earlysiege
**Modules used:** Defend (4 zones), TownLife (4)
**Special AI logic:** Reactive defense repositioning post-wall-breach.

#### challenge_lateeconomy
No AI — economy challenge.

#### challenge_latesiege
**Modules used:** Defend (4), TownLife (2)
**Patrol behaviors:** Knight 3-point patrol with proximity triggers. Gate sally-forth on approach.

#### challenge_malian
**Modules used:** None (WaveGenerator-based paths)
**Special AI logic:** Waves path along predefined markers (west/south/east). Target switching to nearest pit mine. Monk conversion. Cost scaling.

#### challenge_montgisard
**Modules used:** Defend, RovingArmy
**Patrol behaviors:** 7 bidirectional patrols. `CheckForIdleAroundSS` recaptures sites.
**Special AI logic:** `AI_Enable` for 5 players with `default_campaign` personality. `FocusTrebs` anti-trebuchet response.

#### challenge_ottoman
**Modules used:** RovingArmy (30 rounds × 9 lanes)
**Special AI logic:** Custom `attackMoveStyle` with `attackBuildings`. Endless wrap after round 30.

#### challenge_safed
**Modules used:** Army_Init encounters, WaveGenerator
**Patrol behaviors:** 17 patrol encounters with `TARGET_ORDER_PATROL`.
**Special AI logic:** `AI_Enable(player3/4, false)`. Siege camp proximity activation.

#### challenge_towton
**Modules used:** Army_Init (town defenders), RovingArmy (wave armies)
**Special AI logic:** Raider split-off system. Siege redirection logic. Conqueror Mode 1.3× multiplier.

#### challenge_walldefense
**Modules used:** RovingArmy (all waves)
**Special AI logic:** Custom `attackMoveStyle_targetWonder` (ignoreEverything, target only Wonder). 4-lane routing after wave 16. Ranged wave `onBlockedFunction`.

#### challenge_agincourt
**Modules used:** None
**Patrol behaviors:** 5 horsemen on 9-waypoint `TARGET_ORDER_PATROL` loop.
**Special AI logic:** Wave leaders with lane-targeting. Conqueror Mode doubles reinforcements.

---

### Hundred Years War

#### hun_chp1_combat30
**Modules used:** RovingArmy (Attack1, EnglishRaid1/2, EnglishArchers1–7), Defend (DefendEngBase, DefendRecruit1/2)
**Special AI logic:** English transferred from passive player5 to aggressive player2 for combat.

#### hun_chp1_paris
**Modules used:** UnitSpawner (3, spawnRate 0.25), Defend (3 siege camps), RovingArmy (3 invaders, 3 standby, 15 siege defenders with leashRange 45, 2 resource raiders)
**Special AI logic:** Round-robin reinforcement. Trebuchet range ×0.8. `attackEverything` on siege defenders.

#### hun_chp2_cocherel
**Modules used:** Defend (all garrisons — combatRange 35–90), RovingArmy (attack paths)
**Patrol behaviors:** Garrison rotation between paired Defend modules.
**Special AI logic:** Wave pipeline with 5s build time overrides.

#### hun_chp2_pontvallain
**Modules used:** RovingArmy (`onDeathFunction` callbacks), Defend (bandits)
**Patrol behaviors:** Bandit patrol with `ARMY_TARGETING_REVERSE`.

#### hun_chp3_orleans
**Modules used:** RovingArmy (4-lane assault), Defend (12 siege_defend, 10 rear_defend, 8 patrol routes)
**Patrol behaviors:** 12 siege_defend patrols with `TARGETING_RANDOM`.
**Special AI logic:** Dynamic power-scaling: `1500 + 15*min(m,71) + (1/15000)*min(m,71)^4`. Fort destruction adds 20s to wave interval. `attackMoveStyle_aggressive` and `attackMoveStyle_ignorePassive`.

#### hun_chp3_patay
**Modules used:** RovingArmy (Rearguard1–4, BattleGroup1–3, Regiment1–3), Defend (SigmundDefenders, PatayDefenders, BlockadeMangonel)
**Special AI logic:** Regiments start stationary, activate on timer/proximity. Scatter groups flee and merge. `DissolveModuleIntoModule` for skipping.

#### hun_chp4_formigny
**Modules used:** RovingArmy (20 battlefield modules with `shouldHoldWhileWaiting`), dynamic pivot/retreat modules
**Special AI logic:** Frenzy Phase: `attackEverything`. Pivot Phase: disband + redistribute into 4 pivot modules. Retreat at 85% casualties. `MicroArmy()` targeting closest player squad. `MonitorBattlefield()` 1s state machine.

#### hun_chp4_rouen
**Modules used:** RovingArmy, Wave system, Defend
**Patrol behaviors:** 3 patrol routes with `ARMY_TARGETING_REVERSE`.
**Special AI logic:** Polynomial wave power. Village defender dissolution. CounterMonks every 680s. Anti-ram counter spawns. `PlayerUpgrades_Auto(player2, false)`.
**Difficulty-based AI tuning:** Pressure waves on Hard+ only.

---

### Mongol Empire

#### mon_chp1_kalka_river
**Modules used:** RovingArmy (20+ Rus attack groups), Defend (cart stockade)
**Patrol behaviors:** 2 scout patrols with `ARMY_TARGETING_CYCLE` (10 waypoints). Knight parade with phased rotation.
**Special AI logic:** Army merge below threshold. Reinforcement balancing support/attack. Rus speed modification (0.8× → 1.25×).

#### mon_chp1_zhongdu
**Modules used:** RovingArmy, Defend, Raiding_Init
**Patrol behaviors:** Raiding_Init probes with scouts.
**Special AI logic:** Raiding_Init for Jin raids with probe scouting. Revenge raids on kill events. Skirmisher dissolution into landmark defenders. Wall archers hold position.
**Difficulty-based AI tuning:** Base hunting enabled Hard+ only.

#### mon_chp1_juyong
**Modules used:** Defend (20+), RovingArmy (7 patrols), Wave (5)
**Patrol behaviors:** 7 RovingArmy patrol routes.
**Special AI logic:** Withdraw-on-sight behavior. Dynamic retreat: capture triggers recall to inner defenses. Overflow management above 30 squads.

#### mon_chp2_kiev
**Modules used:** RovingArmy (district assault), Defend (gate + sprawl), TownLife
**Patrol behaviors:** 4 gate defenders with `ARMY_TARGETING_CYCLE`, `onDeathReset`.
**Special AI logic:** `TARGETING_DISCARD`, `withdrawThreshold 0.3`. Gate damage retargets RovingArmy. Wave cap suppression.

#### mon_chp2_liegnitz
**Modules used:** RovingArmy (17 modules across 3 zones)
**Patrol behaviors:** `ARMY_TARGETING_REVERSE` and `ARMY_TARGETING_CYCLE`.
**Special AI logic:** Staggered engagement: sort by distance, `RovingArmy_SetTarget` 5s apart. Reactive retargeting on player stables move.

#### mon_chp2_mohi
**Modules used:** RovingArmy (Batu Khan, ambush, defense lines), Defend (camp), UnitSpawner (rate 10s)
**Special AI logic:** Batu Khan: hold → dissolve into attack → opposite-side lane targeting. Ambush groups with extended 150/340 combat/leash. Defense line `withdrawThreshold 0.5`. Ambush healing when no allies nearby.

#### mon_chp3_lumen_shan
**Modules used:** RovingArmy (wallbreakers), Defend, Raiding_Init
**Special AI logic:** AI cached pathfinding (`AIPlayer_SetMarkerToUpdateCachedPathToPosition`) for blockade evaluation. `ARMY_TARGETING_DISCARD` for wallbreakers. Straggler module management.

#### mon_chp3_xiangyang_1267
**Modules used:** RovingArmy (final sally, allied cavalry), Defend (repositionable modules), Raiding_Init
**Special AI logic:** Flanking AI: `CampFlanks` detects approach direction, repositions all Defend via `Defend_UpdateTargetLocation`. `ARMY_TARGETING_PROX` for final sally. Bridgeblaster hold position.

#### mon_chp3_xiangyang_1273
**Modules used:** RovingArmy, Defend (6+ garrison), Raiding_Init
**Special AI logic:** Dynamic composition updates (mangonels after tower kills). Garrison shifting across bridges based on health/aggro. Inner defense collapse: archer modules merge into `last_stand`. Keep avengers on 10s cooldown.
**Difficulty-based AI tuning:** Retaliation system Normal+ only.

---

### Rise of Moscow

#### gdm_chp1_moscow
**Modules used:** RovingArmy (18 modules: MongolAttackers1a–4e, ProbingMongolAttacks)
**Special AI logic:** Intro raider state machine (attack buildings → switch targets → retaliate; Hard: prefer spearmen, Expert: prefer villagers; flee at ≤20% HP). Khan flees when heavily damaged or ≤3 raiders. Random spawn location selection.
**Difficulty-based AI tuning:** Probing attacks disabled on Easy. Fire damage 0.35–1.0×. Probing frequency 1.2–2 min. Wave 4 Hard/Expert only.

#### gdm_chp2_kulikovo
**Modules used:** RovingArmy (3 static Mongol + dynamic per-wave + 3 ally), Defend (defense lines)
**Special AI logic:** Dynamic wave modules via `MongolWaves_GenerateModule` with `onDeathDissolve`. FOW reveals for correct engagement. Wave 10 absorbs static armies. Allied replenished per phase. Wave 10 retreat via `Cmd_FormationMove`.
**Difficulty-based AI tuning:** Per-unit squad counts scale via `Util_DifVar`. Tier-3 units on Hard/Expert. Siege at waves 6+ (springalds), 7+ (mangonels Normal+).

#### gdm_chp2_tribute
**Modules used:** RovingArmy (dynamic bandits, punitive Mongol army), Defend (bandit camps)
**Patrol behaviors:** Bandits with `ARMY_TARGETING_RANDOM_MEANDERING` for roaming patrol.
**Special AI logic:** Zone-based dynamic bandits (7 settlement + 1 wanderer zones). Strength threshold scales with trade/settlements/difficulty/cycle. Combat pause system. Post-purchase: double creation delay. Punitive Mongol army: 12 waves of 15 squads.
**Difficulty-based AI tuning:** Extensive: creation frequency (25–45s), zone modifiers (-1 to +2), tribute amount/escalation/threshold all scale.

#### gdm_chp3_moscow
**Modules used:** RovingArmy (main waves, raiders, blockade, Khan's Army, infinite final), Defend (inner city)
**Special AI logic:** `ARMY_TARGETING_DISCARD`. Resource raiders: `ignoreEverything` en route, `attackEverything` at target. Wood/stone retarget via `GetOutsideTarget()`. Khan's Army at 0.33× speed, constraint removed at 75% evacuation. Inner-city breach failure countdown.
**Difficulty-based AI tuning:** Total squads 300–500. Max simultaneous 60–200. Max rams 0–8. Breach timer 30–120s.

#### gdm_chp3_novgorod
**Modules used:** Defend (7 fort + 6 infantry + 2 wall guard), RovingArmy (5 wave configs)
**Special AI logic:** Phased escalation (6+ phases per origin). Infantry → cavalry → mixed progression. Story mode: waves disabled entirely.
**Difficulty-based AI tuning:** Build times 10–30s (standard), 14–40s (elite). Wave intervals 60–170s. `Wave_OverrideUnitBuildTime` on Hard.

#### gdm_chp3_ugra
**Modules used:** Defend (18 modules), RovingArmy (7 — MonShore patrol, AttackNorth/South, ScoutAttack, SouthernReinforcements), TownLife (MonVillagers), Wave
**Patrol behaviors:** MonShore RovingArmy patrol.
**Special AI logic:** Tug-of-war force-ratio evaluation every 1s (`Ugra_UpdateForceCount`). When ratio < 0.40, defenders transfer to attack. `AIPlayer_SetMarkerToUpdateCachedPathToPosition` for 3 ford routes. Southern reinforcements at 50% speed with `attackMoveStyle_ignoreEverything`. Fraction-based retreat.
**Difficulty-based AI tuning:** Prepare timer 280–520s. Reinforce period 42–85s. Phase delays (some 9999 = "never" on lower). Probe compositions 6–12 units.

#### gdm_chp4_kazan
**Modules used:** RovingArmy (CavAttackWave, AttackWest, patrols), Defend (30+ modules: outposts, gates, walls, interior), TownLife (KazanVillagers + 2 others), Wave
**Patrol behaviors:** WestRoad/WestForest/EastForest/NorthGate/SouthGatePatrol — cycling/reverse targeting.
**Special AI logic:** 8-tier intensity system (incremented by events). `intensityFlex` randomization (max +2). Fallback cascade: disable reinforcements → retreat 1/3 outer → transfer to inner defense → redistribute archers. `AIPlayer_SetMarkerToUpdateCachedPathToPosition`. All Defend reinforced from TownLife at 80%.
**Difficulty-based AI tuning:** Wave interval 150–210s. Cavalry/west waves disabled on Easy. Elite knights 14–28, handcannon 8–20.

#### gdm_chp4_smolensk
**Modules used:** Defend (villages, outposts, Smolensk walls/interior/staging), RovingArmy (`ARMY_TARGETING_DISCARD`/`CYCLE`), Wave (staging + auto_launch)
**Special AI logic:** Supply meter: caravan arrivals fill supply (100/1000), triggers waves when full. Polynomial time-scaling for wave power (up to 3×). Caravan escort escalation at kill thresholds. Wall defenders dissolve into `smolensk_wall` on capture. Counter-attacks from uncaptured villages.
**Difficulty-based AI tuning:** Extensive: defender scaling, tower upgrades, wave routes (1/1/2/3), caravan death limit 5/route.

---

### Rogue (The Sultans Ascend)

#### rogue_maps
**Modules used:** RovingArmy (patrols, UGC escort), Defend (Outlaws system), Army_Init (shinobi, guard patrols). Lane system via `Rogue_AddLane` + `Rogue_UseDefaultSchedule`.
**Patrol behaviors:**
- Coastline: Naval raid with `TARGET_ORDER_PATROL` across 4 waypoints. Side base patrols.
- Steppe: 8 guard patrols (a–h) with `WALK_SPEED` via `Modify_UnitSpeedWhenNotInCombat`.
- UGC: 2 RovingArmy with `ARMY_TARGETING_REVERSE`.
**Special AI logic:**
- Coastline: Pirate naval raids (2 combat ships max). Transport ship landings. `Outlaws_InitRaiding`.
- Forest: Income-based spawning with exponential scaling. Naval disabled.
- Daimyo: Shinobi `shinobi_spy_jpn` ability, leashRange 50. Abandoned Village ambush trap with victim-tracking. Shrine secret mechanic.
- Steppe: Income → spawn → fill defender pool → overflow to attacker pool → target villagers. Idle recovery every 15s.
- UGC: `default_campaign` personality.
**Difficulty-based AI tuning:** `rogue_wave_strength` (0.85–1.0). Naval raid delay 300–2100s. Ship respawn: `300 - difficulty*15`. Raider income 1.0–4.0×.

---

### The Normans (Salisbury)

#### sal_chp1_rebellion
No AI — camera/movement tutorial.

#### sal_chp1_valesdun
**Modules used:** None (scripted `Cmd_AttackMove`/`Cmd_Move`)
**Special AI logic:** Enemy retreat at 75% casualties (1.2× speed + `Cmd_Move` to retreat marker). Reinforcement safety nets respawn depleted units.

#### sal_chp2_dinan
**Modules used:** RovingArmy (2 patrol modules), Defend (garrison)
**Patrol behaviors:** Patrol 01: 3+3, 4-waypoint `ARMY_TARGETING_CYCLE`. Patrol 02: 3+3, 3-waypoint `ARMY_TARGETING_REVERSE`.
**Special AI logic:** Scripted raids at 0.8× speed. Garrison rally on proximity. `Entity_SetInvulnerableMinCap(0.01)`.

#### sal_chp2_township
No AI — economy tutorial.

#### sal_chp2_womanswork
No AI — economy tutorial.

#### sal_chp3_brokenpromise
**Modules used:** Defend (5 Pevensey — combatRange 55, leashRange 60; 15 Hastings — combatRange 50, leashRange 65)
**Special AI logic:** Beach ambush via `Cmd_AttackMove`. Garrison rally on player approach. Transport ships at 1.2× speed. Reinforcements spawned on Hastings discovery.

---

## Cross-Mission Patterns

### Most Common Module Types

| Module Type | Usage Count | Primary Campaigns |
|-------------|------------|-------------------|
| **RovingArmy** | 50+ missions | All campaigns extensively |
| **Defend** | 45+ missions | All campaigns — most common static positioning |
| **TownLife** | 8–10 missions | Challenges, Mongol, Russia (unit production) |
| **UnitSpawner** | 10–12 missions | Tutorials, pre-placed forces, Mongol |
| **Attack** | 5–8 missions | Less common — RovingArmy often preferred |

### Standard Patrol/Defend Setups

| Pattern | Target Order | Typical Usage |
|---------|-------------|---------------|
| Point defense | Defend, `combatRange` 35–60, `leashRange` 50–85 | Gate/wall/camp garrisons |
| Waypoint patrol | RovingArmy, `TARGETING_CYCLE/REVERSE` | Road patrols, camp circuits |
| Random patrol | RovingArmy, `TARGETING_RANDOM` | Scout detection, area coverage |
| Meandering roam | RovingArmy, `TARGETING_RANDOM_MEANDERING` | Bandit roaming (gdm_chp2_tribute) |
| Proximity hunt | RovingArmy, `TARGETING_PROX` | Final sally forces, reactive defense |

### Difficulty-Scaling of AI Behavior

| What Scales | How | Examples |
|-------------|-----|---------|
| **Module counts** | More patrol/defend modules on harder | ang_chp2_bayeux (5→9 positions) |
| **Unit counts per module** | Linear `Util_DifVar` scaling | Most missions (e.g., 5/7/10/14) |
| **Feature toggles** | Systems enabled/disabled per difficulty | Probing attacks (Easy: off), naval raids (Hard+), pressure waves (Hard+) |
| **Timer intervals** | Shorter attack/patrol intervals | ang_chp1_york danes_spawnDelay (240→120s) |
| **Aggression parameters** | Combat ratings, leash ranges adjust | abb_m2_egypt AI_AGGRESSION values |
| **Targeting intelligence** | Smarter targeting on harder | gdm_chp1_moscow (Hard: prefer spearmen, Expert: prefer villagers) |
| **Upgrade unlocks** | Building/unit upgrades on harder | abb_m8_cyprus (Arrowslits/Springald/Cannon by difficulty) |

### Custom vs. Standard Encounter Plan Usage

| Approach | Missions | Description |
|----------|----------|-------------|
| **No AI_Enable** (most common) | ~50 missions | All behavior via MissionOMatic modules + Army system, no skirmish AI |
| **AI_Enable with default_campaign** | challenge_montgisard, rogue UGC | Standard campaign AI personality for autonomous play |
| **Custom state machines** | abb_m2_egypt, ang_chp2_tinchebray, hun_chp4_formigny | Fully custom decision logic replacing encounter plans |
| **Hybrid (AI for subsets)** | abb_m6_aynjalut, mon_chp2_mohi | AI enabled for specific unit groups, disabled for others |
| **AI_Enable(false) explicit** | 20+ missions | Explicitly disable AI to prevent interference with scripted behavior |

### Notable Custom AI Systems

| System | Mission | Description |
|--------|---------|-------------|
| Heatmap targeting | abb_m2_egypt | Quadrant aggression evaluation at 0.125s |
| Camp pool system | abb_m5_mansurah | 7 pools × 6 behavioral states |
| Villager AI state machine | abb_m1_tyre | 7-state gather→flee→garrison→reconstruct cycle |
| Shield wall + striker | ang_chp1_hastings | Row-based backfill + dynamic unit pulling |
| Robert's army state machine | ang_chp2_tinchebray | Defend→sally→attack transitions |
| MonitorBattlefield | hun_chp4_formigny | 1s state machine for frenzy/pivot/retreat |
| Siege entropy | ang_chp4_rochester | 20% surrender on side objectives |
| Intensity system | gdm_chp4_kazan | 8-tier event-driven escalation |
| Supply meter | gdm_chp4_smolensk | Caravan-driven wave triggering |
| Force-ratio tug-of-war | gdm_chp3_ugra | 1s evaluation with 0.40 attack threshold |
| Flanking detection | mon_chp3_xiangyang_1267 | Direction-based Defend repositioning |
| Raider income system | rogue (Steppe) | Income → spawn → fill pools → overflow to attack |
