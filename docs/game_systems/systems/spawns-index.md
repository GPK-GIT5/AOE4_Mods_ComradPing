# Spawns & Wave Patterns Index

Cross-reference of all spawn systems, wave patterns, and army compositions across campaign missions, extracted from Phase 3 summaries.

## System Reference

### WaveGenerator (`wave_generator.scar`)

Timed unit production for campaign AI waves with simulated build-time delays.

**Lifecycle:** `WaveGenerator_Init` → `WaveGenerator_SetUnits` → `WaveGenerator_Prepare` → `WaveGenerator_Launch`

- Units created one at a time with simulated build-time delays (not real production)
- Monitored every 1s via `WaveGenerator_Monitor`
- `WaveGenerator_FilterUnitsByDifficulty` strips units not matching current difficulty
- Auto-launch modes: `auto_launch_after_prepare` (immediate/delayed), `auto_launch_after_ready` (on completion)

**Simulated Build Times:**

| Category | Time |
|----------|------|
| Villager / Scout | 20s |
| Spearman / Archer / Militia | 15s |
| MAA / Crossbow / Horseman / Landsknecht | 22s |
| Knight / Camel / Horse Archer / Handcannoneer | 35s |
| Monk | 30s |
| Ram / Springald / Siege Tower | 30s |
| Mangonel / Trebuchet | 40s |
| Cannon / Bombard / Culverin / Ribauldequin | 45s |

**Spawn Types:** barracks → infantry, archery_range → ranged, stable → cavalry, siege_workshop → siege, town_center → town_center, monastery → religious, universal → all.

### MissionOMatic Wave System (`missionomatic_wave.scar`)

Higher-level wave system built on WaveGenerator, integrated into the recipe pipeline.

- `Wave_New(data)` → `Wave_Prepare` → `Wave_Launch`
- Targets **modules** (not raw Armies) — staging module → assault module transfer
- Supports `auto_launch`, `use_separate_spawns`, difficulty filtering
- Monitored at 1s interval by `Wave_MonitorAllWaves`

### Module Types

All modules share: `Init → Monitor → GetSGroup/AddSGroup/RemoveSGroup → Disband → IsDefeated`

| Module | Purpose | Monitor Interval |
|--------|---------|-----------------|
| **TownLife** | AI economy, villager production, unit provider | 5s |
| **Defend** | Hold position, supports withdraw conditions | 1s |
| **Attack** | Assault target, dynamic retargeting | 5s |
| **RovingArmy** | Mobile patrol cycling through waypoints | 1s |
| **UnitSpawner** | Simple off-map/on-map spawner | configurable |

**RovingArmy targeting modes:** `Discard`, `Cycle`, `Reverse`, `Proximity`, `Random`, `RandomMeandering`

### Unit Request Pipeline (Reinforcement System)

1. Combat module Monitor calls `Reinforcement_AreReinforcementsNeeded`
2. `MissionOMatic_RequestUnits` solicits estimates from provider modules
3. Best provider starts production via `UnitRequest_Start`
4. `MissionOMatic_RequestComplete` delivers units to requester

### Key Spawn Functions

| Function | Purpose |
|----------|---------|
| `UnitEntry_DeploySquads` | Universal spawn call for all modules/waves |
| `ResolveSpawnLocation` | Resolves marker/egroup/position to valid spawn point |
| `Action_SpawnUnits_Do` | Recipe action: spawn units at location |
| `Action_SpawnUnitsToModule_Do` | Recipe action: spawn units into a module |
| `DissolveModuleIntoModule` | Transfer all units between modules |

---

## By Campaign

### Abbasid Dynasty

#### abb_bonus

**Wave sources:** P2 economy-driven attack waves; P2 cavalry raiders; P5 naval raiders
**Compositions:** 7 unit mix tiers cycling through spearmen/archers/horsemen/MaA/knights/mangonels/springalds (escalating with economy); cavalry raiders = horsemen; naval raiders = warships
**Timing:** Attack waves every 400s (escalating); cavalry raiders every 14s × `raidSpawnMod`; naval raids triggered by P5 activation
**Static defenders:** Wall/bastion garrisons across 7 patrol routes; 6 P2 Defend armies; 3 P3 holy order armies; 2 P5 naval defend armies
**Reinforcement mechanics:** Economy-driven — wave size scales with P2 resource income rate
**Named modules:** `P2Defend1–6` (Defend), `P3HolyOrder1–3` (Defend), `P5NavalDefend1–2` (Defend), `P2Attack` (RovingArmy), `P2CavRaiders` (RovingArmy), `P5NavalRaid1–3` (RovingArmy)
**Special mechanics:** Economy-driven wave scaling (not timer-based); 7-tier unit composition progression tied to income thresholds

---

#### abb_m1_tyre

**Wave sources:** Ram escort armies; skirmish armies; 4 camp systems with villager AI; 4 ambush pairs; transport ship reinforcements
**Compositions:** The Beast (ram) with 3 escort armies (infantry mixes); skirmish armies (spearmen/archers/horsemen); camp villager squads; ambush pairs (hidden infantry)
**Timing:** Phase-driven spawning tied to mole trigger points; transport ships on event triggers
**Static defenders:** Camp defenders with villager AI across 4 camps
**Reinforcement mechanics:** Escort splitting at mole trigger points; ram garrison waves backfill from transport ships
**Named modules:** Escort armies (3), skirmish armies, camp systems (4), ambush pairs (4), transport reinforcements
**Special mechanics:** The Beast ram system with escort splitting; garrison waves triggered by mole progress; villager AI at camps

---

#### abb_m2_egypt

**Wave sources:** Quadrant heatmap targeting AI; budget-based enemy reinforcements; garrison spawns; transport ships
**Compositions:** Typed squad rotation: archer → spearman → horseman → militia; templars added after 300s; garrison spawns (1 per 10s, cap 15)
**Timing:** Squad rotation cycling; garrison spawns every 10s (capped at 15); templars after 300s
**Static defenders:** Control point garrisons; tug-of-war position holders
**Reinforcement mechanics:** Budget-based spawning — AI allocates resources to unit types based on player pressure quadrant
**Named modules:** Quadrant heatmap modules, garrison spawner, transport ship modules
**Special mechanics:** Tug-of-war control point battle; heatmap targeting selects weakest quadrant; typed squad rotation cycle

---

#### abb_m3_redsea

**Wave sources:** 6 raid wave templates; finale wave with Reynald's flagship; pirate dock system; trade convoys
**Compositions:** Fleets, net formations, marines, demolishers; finale = Reynald's flagship + escort fleet; pirate ships; trade convoys (8 ships per convoy, 3 convoys)
**Timing:** Raid waves on escalating intervals; pirate dock rebuild timer; 3 trade convoys dispatched sequentially
**Static defenders:** Pirate dock garrisons with rebuild mechanic
**Reinforcement mechanics:** Pirate docks rebuild after destruction, spawning new pirate ships; trade convoy escorts scale up
**Named modules:** 6 raid wave templates, Reynald flagship module, pirate system modules, trade convoy modules
**Special mechanics:** Net formation closing mechanic; demolition ships; civil unrest meter affected by trade success/failure

---

#### abb_m4_hattin

**Wave sources:** 8 crusader waves from 3 spawn lanes (north/south/mid)
**Compositions:** Escalating infantry/cavalry mixes; rank formation spawning (units spawn in formation rows)
**Timing:** 8 waves dispatched sequentially across the mission from 3 directional lanes
**Static defenders:** None (open-field battle)
**Reinforcement mechanics:** Custom non-AI path following through location network; units march along trade road waypoints
**Named modules:** 8 wave modules across 3 lanes
**Special mechanics:** Burnable fields mechanic with smoke debuffs; rank formation spawning; custom path network (not AI pathing)

---

#### abb_m5_mansurah

**Wave sources:** Pool/Member/Wander/Lighthouse/Rest/Patrol camp system; 14 invasion rounds; 34 defending army instances; 3 holy orders; Baybars reinforcement rows
**Compositions:** Cost-based scaling for invasion rounds; holy order cavalry with flee mechanic; Baybars = 10 rows of mixed units at 0.75s intervals
**Timing:** 14 invasion rounds with cost-based escalation; Baybars reinforcements at 0.75s row intervals
**Static defenders:** 34 defending army instances across camp positions; 3 holy order positions
**Reinforcement mechanics:** Baybars reinforcements (10 rows at 0.75s intervals); holy orders flee at threshold then regroup
**Named modules:** Camp system (Pool/Member/Wander/Lighthouse/Rest/Patrol), 34 Defend instances, `HolyOrder1–3` (RovingArmy), Baybars reinforcement module
**Special mechanics:** Spy stealth phase → siege defense phase transition; camp system with 6 behavioral states; cost-based invasion scaling

---

#### abb_m6_aynjalut

**Wave sources:** 5 rounds with 11 cohorts; 5 timed player reinforcement waves
**Compositions:** Rank-based force spawning (mixed infantry/cavalry cohorts); player reinforcements with dynamic ratio scaling (0.4–1.0)
**Timing:** `RANK_INTERVAL` = 1.5s between rank spawns within a cohort; 5 player reinforcement waves at fixed phase triggers
**Static defenders:** Road/side spawn lane defenders
**Reinforcement mechanics:** Dynamic ratio scaling (0.4–1.0) adjusts player reinforcement wave size based on losses; cohorts spawn rank-by-rank
**Named modules:** 11 cohort modules across 5 rounds, 5 player reinforcement modules
**Special mechanics:** Force order state machine (hill → field → town → afula phases); rank-based spawning at 1.5s intervals per row

---

#### abb_m7_acre

**Wave sources:** Amortized enemy army spawning; cyclic attack wave compositions; counter-attack system; Genoese naval assault; Frankish marines
**Compositions:** Cycling: MELEE/RANGED/CAVALRY/SIEGE/MILITIA compositions; Genoese = naval assault force; Frankish marines (Hard+ only)
**Timing:** Amortized spawning at 0.005s intervals; counter-attacks with escalating army count; Genoese naval at 1291s countdown
**Static defenders:** Base garrison defenders
**Reinforcement mechanics:** Counter-attack system with escalating army count per wave; Frankish marines only on Hard+
**Named modules:** Cyclic attack modules (MELEE/RANGED/CAVALRY/SIEGE/MILITIA), counter-attack modules, Genoese naval module, Frankish marine module
**Special mechanics:** 1291s countdown to Genoese naval assault (historical year reference); amortized 0.005s spawn intervals; barrage ability system

---

#### abb_m8_cyprus

**Wave sources:** BuildingTrainer-based Nicosia attack waves; Famagusta naval raids; Kyrenia cavalry raids
**Compositions:** 10 cycling compositions (every 4th = boss wave) for Nicosia; 3 naval raid compositions for Famagusta; cavalry for Kyrenia
**Timing:** BuildingTrainer production intervals for Nicosia; naval raids on event triggers; cavalry raids periodic
**Static defenders:** Prison camp guards; Limassol garrison
**Reinforcement mechanics:** BuildingTrainer system produces units from enemy buildings that march to attack; boss waves every 4th cycle
**Named modules:** Nicosia BuildingTrainer modules (10 compositions), Famagusta naval raid modules (3), Kyrenia cavalry module
**Special mechanics:** 8 players across multiple factions; prison camp liberation mechanic; BuildingTrainer wave system

---

### Angevin Empire

#### ang_chp0_intro

**No dynamic spawn system.** Tutorial mission — all units pre-placed via UnitSpawner modules.
**Static defenders:** Spearman village Defend module
**Named modules:** UnitSpawner modules (horsemen, archers, spearmen), Defend (village), RovingArmy (cavalry scout)

---

#### ang_chp1_hastings

**Wave sources:** Shield wall system; player reinforcements (3 zones); enemy reinforcements (stolen from later phases); staggered phase releases
**Compositions:** Shield wall: 136 units + 26 spearmen across 3 segments; player reinforcements: type-ratio-based (archers/infantry/cavalry); enemy reinforcements from Phases 2–5
**Timing:** Player reinforcements at 7s min interval (difficulty-limited); phase releases staggered across Phases 2–5
**Static defenders:** Shield wall segments (3); phase-locked unit groups
**Reinforcement mechanics:** Player reinforcements: type-ratio-based with 7s minimum interval, difficulty-capped count; enemy reinforcements "stolen" from later phases to backfill losses
**Named modules:** Shield wall segments (3), player reinforcement zones (3), phase release modules (Phases 2–5)
**Special mechanics:** Feigned retreat mechanic (bait AI into pursuit); shield wall backfill system

---

#### ang_chp1_york

**Wave sources:** 3 rebel wave modules; Dane raid system (3 groups); early raiders (cycling)
**Compositions:** Rebel waves: spearmen/archers/horsemen; Dane raids: escalating count to cap; early raiders: cycling unit types
**Timing:** Rebel waves on interval timer; Dane raids escalate count per dispatch; early raiders cycle types periodically
**Static defenders:** WestPatrol, BaileyPatrol, KeepPatrol defenders
**Reinforcement mechanics:** Dane raid system with escalating group count up to cap; village capture triggers new wave spawners
**Named modules:** `WestPatrol`, `BaileyPatrol`, `KeepPatrol` (RovingArmy), `CavalryRaiders` (RovingArmy), `DaneAttackers1/2/3` (RovingArmy), `EarlyRaiders` (RovingArmy), rebel wave modules (3)
**Special mechanics:** Village capture mechanics unlock spawners; tribute/diplomacy UI system

---

#### ang_chp2_bayeux

**Wave sources:** Cavalry patrol defenders; wall archers; gate infantry; idle attack poke system
**Compositions:** Cavalry patrols: 5–9 groups of horsemen/knights; wall archers (Defend); gate infantry (3 RovingArmy positions)
**Timing:** Cavalry patrols cycle between waypoints; poke attacks fire periodically when idle
**Static defenders:** Wall archer Defend modules; gate infantry RovingArmy (3 positions)
**Reinforcement mechanics:** Dissolution system — withdrawn cavalry merge into wall defense Defend modules
**Named modules:** Cavalry patrol groups (5–9), wall archer Defend modules, gate infantry RovingArmy (3), poke system
**Special mechanics:** Ram siege chain tutorial; dissolution system merging withdrawn cavalry into wall defense

---

#### ang_chp2_bremule

**Wave sources:** French advance army; hunting roving army; ram siege waves; ambush force; camp/patrol system; counterattack system
**Compositions:** French advance army: ~200 units (mixed infantry/cavalry); ram siege waves (polynomial time-scaling); ambush force (hidden infantry); counterattack = 25% army split
**Timing:** Ram siege waves use polynomial time-scaling formula; counterattack triggers on specific events
**Static defenders:** Camp defenders; patrol routes
**Reinforcement mechanics:** Counterattack system splits 25% of army; village capture triggers AI rebuild
**Named modules:** French advance army, hunting RovingArmy, ram siege wave modules, ambush force, Louis camp/patrol system, counterattack module
**Special mechanics:** Hunting roving army retargets to visible player units; polynomial time-scaling for ram waves

---

#### ang_chp2_tinchebray

**Wave sources:** Gold-based reinforcement purchasing (4 named reserves); Robert's army state machine; relief army interception
**Compositions:** 4 named reserve groups (purchasable with gold); Robert's army (defend → sally → attack states); relief army
**Timing:** Player-driven (purchase timing); Robert's state machine transitions based on conditions
**Static defenders:** Robert's initial defend-state army; enemy scouts
**Reinforcement mechanics:** Gold-based purchasing — player buys reserves through diplomacy UI repurposed as Buy Reserves panel
**Named modules:** 4 named reserve modules, Robert's army state machine module, relief army module, enemy scout modules
**Special mechanics:** Diplomacy UI repurposed as Buy Reserves panel; Robert's army state machine (defend → sally → attack)

---

#### ang_chp3_lincoln

**Wave sources:** 3 enemy reinforcement columns (ERG); 5 besieger modules; 3 FinalAttacker modules; 2 RoyalGuard modules; flank assault forces
**Compositions:** ERG columns escalate with mixed infantry. Besiegers cycle: archer/archer → archer/spearman → archer/MaA → spearman/MaA. Siege cycle: ram → mangonel → siege tower → mangonel → ram. FinalAttackers: 5 archers + MaA + 1 mangonel each.
**Timing:** Besiegers reinforced every 50–80s by difficulty; ERG columns spawned sequentially during ambush phase; flank forces reinforced every 10s
**Static defenders:** 3 siege camp positions (Left/Middle/Right) with spearmen, MaA, patrol archers, line archers. Field army: 3 infantry lines of 20 spearmen + archers + springalds.
**Reinforcement mechanics:** Besieger waves escalate: count + wave_number (capped at 2×); ERG survivors merge into market defenders; Welsh reinforced if < 15 units
**Named modules:** `Besiegers1–5`, `FinalAttackers1–3`, `RoyalGuard1–2`, `GeneralGroup`, `CampLeftDefend1`, `CampMiddleDefend1–2`, `CampRightDefend1–2`, `LeftPatrol`, `RightPatrol`, `FieldPatrol`, `LineInfantry1–3`, `FieldSiege`, `TradePostGuards1–2`, `MarketPerimeter1–3`, `FlankGuards1–3`, `FlankAssault1–3`, `EastPatrol`, `WelshArmy A–C`, `WelshDefenders`, `ERG1–3_1–4`
**Special mechanics:** Stealth forest ambush phase; King Stephen with 0.25× received damage until bodyguards < 50%; ERG column march at 0.8× speed; Welsh allies (3 RovingArmy groups)

---

#### ang_chp3_wallingford

**Wave sources:** 3 intro assault waves (NE/N/NW lanes); ongoing prepared waves (repeating); final wave on camp destruction
**Compositions:** Waves 1–5: infantry-heavy + rams + siege towers. Waves 6–10: add horsemen, knights, mangonels, springalds. Final wave: 9/12/17/24 units each by difficulty. 10 wave compositions per difficulty tier.
**Timing:** Wave 1 at t=0, Wave 2 at t=100s, Wave 3 at t=225s, then every ~125s. `PREPARE_TIME` = 210s; auto-launch 20s after preparation.
**Static defenders:** 3 fort defenders (NE/N/NW) with front-line positions (2 per direction); 4 RovingArmy defenders; 7+ patrol modules
**Reinforcement mechanics:** Defender backfill: when any of 4 modules drops below 50% → `ReinforceFirst()` (3 sources dissolve); second drop → `ReinforceSecond()` (2 sources). Player reinforcements (Henry, t=600s): up to 63 squads.
**Named modules:** 3 intro assault, ongoing assault, `enemy_defend_fort` NE/N/NW, `enemy_defend_front_1/2`, `enemy_defend_1–4`, `siege_patrol_1–5`, `patrol_1–7`, final wave module
**Special mechanics:** Wave system with `Wave_Prepare`/`Wave_Pause`; lane selection avoids recent repeats; 600s survive-until-reinforcements countdown

---

#### ang_chp4_dover

**Wave sources:** Initial French attack; 3 timed siege waves; siege tower waves; supply train system; road patrols
**Compositions:** Initial: ~60 units at 50% HP. Siege waves: 3 cycling compositions (5/8/12/15 base squads). Supply escort: 5 cycling compositions. Reserve spawns: 4 compositions on cart arrival.
**Timing:** Wave 2 countdown: 630s. Waves 3–4: 510s each. Supply trains every 40–60s by difficulty.
**Static defenders:** 3 French rearguards (10 archers + 15 MaA each); camp defenders
**Reinforcement mechanics:** Supply train system — each arriving cart spawns reserve units. Rearguard3 reinforced when < 20 units.
**Named modules:** `AttackNorth/South`, `RangedSiegeNorth/South`, `TowerAttackNorth/South`, `DefendNorth/South`, `DefendCamp`, `FrenchReserve`, `SiegeNorth1/2`, `SiegeSouth1/2`, `Rearguard1/2/3`, `DefendForest/NW/NE/SW/SE`, `NorthRoadPatrol`, `SouthRoadPatrol`, `SouthAmbushFrench/Ally`
**Special mechanics:** Willikin of the Weald guerrilla phase; supply train interception reduces siege strength (progress bar); siege entropy through cart kills

---

#### ang_chp4_lincoln

**Wave sources:** 3 rebel wave channels; 2 French fort wave channels; initial French attack
**Compositions:** Rebel: 8 escalating unit table entries each. French: 2 compositions, 8 entries each. Build times: infantry 7–13s, siege 20–35s.
**Timing:** Rebel waves every 80–130s. French Fort A at t=350s; Fort B at 600s after A. French waves every 280–600s (+30s offset B).
**Static defenders:** `RebelDefenders1–3` (5–15 squads), `FortDefendersA1–A2`, `FortDefendersB1–B3`, `CampGuards1–5`
**Reinforcement mechanics:** Rebel waves suppressed if strongpoint count > cap (30/30/40/50). French waves suppressed if > cap (70/70/85/100).
**Named modules:** `RebelDefenders1–3` (Defend), `RebelAttack1–3` (RovingArmy), `FrenchAttackA/B` (RovingArmy), `FortDefendersA1–A2`, `FortDefendersB1–B3` (Defend), `CampGuards1–5` (Defend), `FrenchFortSpringaldA/B` (RovingArmy), `FrenchPatrolA` (RovingArmy)
**Special mechanics:** Dual enemy factions (rebels + French); wave suppression caps; 360s defend-until-reinforcements timer

---

#### ang_chp4_rochester

**Wave sources:** `ConstructWave()` time-based formula; poke waves; wall breach defenders; siege counter force; trade convoys; monk recapture
**Compositions:** Attack waves: cost-budgeted unit pool (archer=1, horseman=1, MaA=1, crossbow=2, knight=2, ram=3, mangonel=4). Spearmen fill remaining (+4 base). Pokes: 5+i spearmen + 5 MaA + 3 horsemen.
**Timing:** Wave power: `(gameTime/4) + (gameTime^6 / 10^9)`, capped at 66 at 60 min. Downtime: 0–180s. Pokes every 3–5 min.
**Static defenders:** `DefendVillage` (spearman+archer), `DefendRochester` (crossbowman), `DefendKeep` (MaA+knight+crossbow). Dynamic marker-based defenders (wall archers, infantry, elite, cavalry, siege) all with ×defenderValue and `onDeathDissolve = true`.
**Reinforcement mechanics:** Siege entropy — on side objective completion, 20% of non-critical AI units surrender. Wall breach triggers `Init_FallenWallDefense()`.
**Named modules:** `DefendVillage`, `DefendRochester`, `DefendKeep` (RovingArmy), dynamic `mkr_wall_archer`/`mkr_infantry_defender`/`mkr_elite_defender`/`mkr_cavalry_defender`/`mkr_siege_defender` (auto-generated Defend), `WallHoleDefense`, `SiegeCounter`, `CounterMonks`
**Special mechanics:** Polynomial wave power scaling; siege entropy mechanic; `PushAttack` redirects defenders to intercept; `CounterSiegeHunt` targets units attacking walls; Story mode skips attack waves entirely

---

### Challenges

#### challenge_advancedcombat
6 sequential waves of Abbasid attackers (10–20 units each). Player selects HRE unit groups before each wave.

#### challenge_basiccombat
5 sequential waves of French attackers. Player picks HRE defenders before each wave.

#### challenge_earlyeconomy
No spawn system — economy tutorial.

#### challenge_earlysiege
No wave system — player assaults static Rus garrison (4 Defend modules + 5 MaA patrol).

#### challenge_lateeconomy
No spawn system — economy tutorial.

#### challenge_latesiege
No wave system — player assaults static HRE garrison (4 Defend modules — knight patrol, gate sally-forth, reactive landmark defense).

#### challenge_malian
3-path endless waves via WaveGenerator. 7-wave repeating pattern with escalating cost per cycle. Player purchases reinforcements via diplomacy UI (tower defense style).

#### challenge_montgisard
6 reinforcement wave tables per fortress (4 Sacred Sites). Reinforcements every 6 min; attacks every 7 min. Conqueror mode doubles reinforcements.

#### challenge_ottoman
30 scripted rounds across 3×3 lanes. 9-lane grid system. Endless mode via wave wrapping after round 30.

#### challenge_safed
WaveGenerator from 4 mine towns (5–7 waves each) + trebuchet/ram siege waves. Fortress defense with mine-town escort waves.

#### challenge_towton
5-phase defense with ~60+ waves across ~22.5 min. Conqueror mode scaling (1.3× multiplier). Raider split-off, siege redirection, beacon reinforcements.

#### challenge_walldefense
24 main waves + 12 patrol + 12 ranged waves across 900s. Bronze/Silver/Gold scoring tiers with resource trickle scaling.

#### challenge_agincourt
3 main waves + English counterattack. Wave 1: ~100 cavalry in 5 lanes. Wave 2: ~112 mixed infantry with named leaders. Wave 3: ~93 units + 3 cannons. Conqueror mode scaling.

---

### Hundred Years War

#### hun_chp1_combat30
Champion recruitment via mini-encounters; 2-round arena combat with difficulty-scaled compositions.

---

#### hun_chp1_paris

**Wave sources:** 3-lane invasion with RovingArmy + 8-wave siege phase
**Compositions:** Mixed infantry/cavalry per lane; bonus flanking waves in siege phase
**Timing:** Lane-based + sequential siege waves; wave pipeline: staging → assault
**Special mechanics:** Flanking wave bonus; 3-lane attack routing with staging areas

---

#### hun_chp2_cocherel

**Wave sources:** 3 rebel village captures + Routier raids + Navarre attacks
**Compositions:** Escalating peasant waves; Routier raids; counter-monk system
**Timing:** Counter-monk system every 340s; Routier raids periodic
**Special mechanics:** Counter-monk waves that hunt player monks; escalating peasant rebellion system

---

#### hun_chp2_pontvallain

**Wave sources:** 3 timed raids + 3 armies at 15:00
**Compositions:** Mixed cavalry/infantry raids; allied waves produce spearmen + archers
**Timing:** Raids at 3:00 / 7:00 / 11:00; major armies at 15:00
**Reinforcement mechanics:** Allied waves spawn spearmen + archers periodically

---

#### hun_chp3_orleans

**Wave sources:** Dynamic power-scaling wave system across 4 assault lanes
**Compositions:** Power formula: `1500 + 15*min(m,71) + (1/15000)*min(m,71)^4`, scaled by difficulty multiplier (0.8/1.0/1.4/2.0)
**Timing:** Continuous, scaling with game time (minutes)
**Special mechanics:** Trade convoy system; fort destruction slows wave power; polynomial power scaling

---

#### hun_chp3_patay

**Wave sources:** Rearguard ambush (4 RovingArmies); road blockers; St. Sigmund garrison; 3 battle groups; 3 chase regiments
**Compositions:** Difficulty-scaled regiments; purchasable reinforcements
**Reinforcement mechanics:** Purchasable: archers 400g, MAA+xbow 600g, horsemen 800g, knights 1000g
**Special mechanics:** Multi-phase pursuit mission; purchasable reinforcement tiers

---

#### hun_chp4_formigny

**Wave sources:** 20 battlefield modules (12 archer + 4 spear + 4 MAA) + Breton knights
**Compositions:** 6 French cannons; 2×30 Breton knights; town garrisons with dissolve-on-death
**Timing:** Phased: frenzy/pivot/retreat stages
**Special mechanics:** Multi-phase pitched battle with frenzy/pivot/retreat; garrison dissolve-on-death

---

#### hun_chp4_rouen

**Wave sources:** Dynamic attack wave system with polynomial power scaling
**Compositions:** wavePower = `(t/4) + (t^6 / 10^9)` where t = game time
**Timing:** North/center/south lanes; counter-monks every 680s; pressure waves on Hard+
**Special mechanics:** University capture → cannon research → wall breach → landmark destruction; anti-ram counter spawns

---

### Mongol Empire

#### mon_chp1_kalka_river

**Wave sources:** 3 staggered Rus waves + stockade defenders
**Compositions:** Spear/archer groups, 24–40 per group by difficulty
**Timing:** Setup timer 50–70s; staggered arrivals
**Reinforcement mechanics:** Support module reinforcement balancing; army merge at threshold
**Special mechanics:** Ambush mission; enclosed stockade defenders

---

#### mon_chp1_zhongdu

**Wave sources:** 4 supply caravan routes (120s interval) + revenge raid system
**Compositions:** Caravan escorts scale with progress; raiding forces
**Timing:** 120s caravan interval; raids scale with village destruction
**Reinforcement mechanics:** Gold-based reinforcement stages
**Special mechanics:** Phase 2: burn 3 landmarks; dynamic raid scaling with village destruction

---

#### mon_chp1_juyong

**Wave sources:** 5 village wave sources (destroy village = stop source) + Juyong sortie
**Compositions:** Mixed infantry, difficulty-scaled; extra squads at Hard/Expert
**Timing:** Staggered starts at 210–660s; intervals 270–570s per source
**Special mechanics:** 4-phase Great Wall siege; village destruction permanently stops wave source

---

#### mon_chp2_kiev

**Wave sources:** Gate reinforcement waves + district-specific defenders on wall breach + 16 sprawl proximity-triggered positions
**Compositions:** Mixed; wave suppression cap 50–120 units by difficulty
**Timing:** District attack waves + sprawl waves (60–120s intervals)
**Special mechanics:** 3-district destruction siege; wave suppression cap prevents overwhelming spawns; Easy: no attack waves

---

#### mon_chp2_liegnitz

**Wave sources:** 15 RovingArmy modules across field/ridge/valley + templar patrol
**Compositions:** Staggered engagement (5s apart); difficulty-scaled
**Timing:** Bohemian army timer: 19–24 min failure deadline
**Special mechanics:** 3-zone battlefield sweep; Bohemian army spawns on timer failure; Nest of Bees siege unit

---

#### mon_chp2_mohi

**Wave sources:** 4 timed reinforcement waves + harassment waves on idle + 7 tent UnitSpawners
**Compositions:** Mixed; 13 camp Defend modules; Batu Khan AI attacks opposite player position
**Timing:** 6-phase mission: ambush → escape → build → bridge assault → defense lines → camp
**Special mechanics:** Forward guards heal when no allies nearby; Batu targets opposite lane from player

---

#### mon_chp3_lumen_shan

**Wave sources:** 8 wallbreaker waves (50s interval) + bonus cavalry raids every N waves
**Compositions:** Rams + difficulty-scaled siege; Phase 4 remedial sally (53–93 units)
**Timing:** 50s interval between wallbreaker waves; bonus raids on modulo wave count
**Special mechanics:** Wall-building blockade mission; AI pathfinding evaluates blockade effectiveness; straggler module management

---

#### mon_chp3_xiangyang_1267

**Wave sources:** Breadcrumber lure waves + swarmer escalation + 5-wave finale (250–325 total units)
**Compositions:** Phase 1: flanking detection AI + ally escort of 4 trebuchets. Phase 2: 3 bridgehead surround zones
**Timing:** Road patrols every 90s; raiding system ongoing
**Special mechanics:** Flanking detection AI; breadcrumber lure system; 2-phase siege

---

#### mon_chp3_xiangyang_1273

**Wave sources:** Cavalry raids + garrison repositioning + final militia rush + keep avenger spawns
**Compositions:** Horsemen/knights/fire lancers + mangonels (added after tower kills); militia: 30 + 4×waveIdx
**Timing:** Retaliation every 90–180s; keep avenger spawns on 10s cooldown
**Special mechanics:** Huihui Pao trebuchet; dynamic garrison repositioning; inner defense collapse system

---

### Rise of Moscow

#### gdm_chp1_moscow

**Wave sources:** Intro Mongol raiders + probing attacks during countdown + 4-wave final assault
**Compositions:** Intro: 5–9 horsemen. Probing: escalating 1 scout → 4 horse archers. Final: horsemen → spearmen → horse archers (Hard+ wave 4)
**Timing:** Probing attacks escalate during countdown phase (1.2–2 min intervals)
**Special mechanics:** Defend/rebuild/expand Moscow; wolves spawned every 30s; scared villagers in forest cabins

---

#### gdm_chp2_kulikovo

**Wave sources:** 10-wave defense across 3 defense lines (fords → hill → Don)
**Compositions:** Infantry/cavalry/hybrid alternation; Wave 10 hybrid absorbs static Mongol armies; focus lane multiplier 2–3× base count
**Timing:** Phased across 3 defense line transitions
**Reinforcement mechanics:** Cavalry detachment (1 knight/9s, max 40, one-time signal); ally replenishment per phase transition
**Special mechanics:** Focus lane system (2–3× base on targeted lane); cavalry detachment UI panel

---

#### gdm_chp2_tribute

**Wave sources:** Dynamic zone-based bandit system (7 settlement zones + wanderer zone) + punitive Mongol army on tribute failure
**Compositions:** Bandits: 10 strength levels × 5 loadout tiers (RovingArmy with meandering patrol). Punitive: 12 waves of 15 squads
**Timing:** Tribute payment cycles every 7.5 min (escalating gold)
**Special mechanics:** Settlement purchasing system; bandits spawn as RovingArmy with RandomMeandering patrol

---

#### gdm_chp3_moscow

**Wave sources:** Mongol invasion waves + Khan's Army finale + infinite final Mongol spawner
**Compositions:** 300–500 total squads (60–200 max simultaneous). Khan's Army: ~196 squads (50 MAA, 65 horse archers, 55 knights, 10 mangonels, 4 rams, 7 trebuchets, 4 siege towers)
**Timing:** 90–120s wave interval; infinite spawner scales with refugee progress
**Reinforcement mechanics:** Vassal reinforcement "Request Aid" panel (7 settlements); refugee evacuation (100–300 villagers)
**Special mechanics:** Infinite final Mongol spawner; inner city breach failure countdown (30–120s)

---

#### gdm_chp3_novgorod

**Wave sources:** 5 RovingArmy attack waves across 4 origins (Kuklino, Soltsy, Skirino, Novgorod)
**Compositions:** Phased escalation (6+ phases per origin); infantry → cavalry → mixed progression. Build time 8s/unit.
**Timing:** Wave intervals: 60–170s. Per-origin intervals: Kuklino 0/150/130/110s, Soltsy 170/170/150/70s, Skirino 90/90/75/60s, Novgorod 150/150/130/110s.
**Static defenders:** Kuklino (archers + spearmen + militia 20–30), Soltsy (3 defend zones), Shelon Fort (7 modules: militia 10–50 + mixed), Novgorod (6 infantry + 2 wall guard zones, 12 spawn points)
**Named modules:** Wave 1–5 (RovingArmy, CYCLE/REVERSE targeting)
**Special mechanics:** Story mode disables all attack waves; wave origins activate progressively

---

#### gdm_chp3_ugra

**Wave sources:** Vanguard scouts + continuous ford reinforcement waves + probe cavalry raids + southern reinforcement column
**Compositions:** Ford waves: start 1 spear + 1 archer, escalate through 4 phases adding MAA/crossbow/horseman/knight. Southern column: 6–10 horsemen + 4–10 horse archers + 0–4 MAA + mangonels + rams + 3 mobile buildings
**Timing:** Ford interval: 42–85s. Probe interval: 60s. Phase escalation triggers at 25–50% of hold timer
**Static defenders:** Ford garrisons (spearmen, MAA, archers, crossbow per ford × 4 sub-modules)
**Named modules:** AttackNorth/AttackSouth (RovingArmy), ScoutAttack1/2, SouthernReinforcements, DefendMonFort, 18 Defend modules total
**Special mechanics:** Tug-of-war force ratio system at both fords (attack threshold 0.40, warning 0.50); southern reinforcements at 50% speed with mobile buildings

---

#### gdm_chp4_kazan

**Wave sources:** Intensity-driven cavalry attack waves (8 tiers) + west ford periodic waves
**Compositions:** Tier 1: 2 horsemen + 2 horse archers → Tier 8: ~34 squads mixing all unit types + siege. West ford base: 2 spearmen + 2 MAA + 3 archers, escalating every 5 cycles.
**Timing:** Wave interval: 150–210s. West ford: 120s. Intensity check: 10s.
**Static defenders:** 6 gate/wall sectors, 12 outer wall + 6 inner wall positions, elite guards (14–28 knights + 8–20 handcannoneers)
**Reinforcement mechanics:** All modules reinforced from "KazanVillagers" TownLife at 80% threshold; disabled on inner wall breach
**Named modules:** CavAttackWave, AttackWest, WestRoad/WestForest/EastForest/NorthGate/SouthGatePatrol, DefendWoodcutters, DefendNorthOutpost1–3, DefendWestRoad1–2, DefendFieldGate1–3, KazanOuterWall1–12, KazanInnerWall1–6, KazanInnerDefense, KazanElite
**Special mechanics:** Intensity system (0–8) — increments on settlement destroy, outpost wipe, every 5th wave, outer wall breach; `intensityFlex` randomization; outer defenders fallback to inner defense (self-destruct 1/3)

---

#### gdm_chp4_smolensk

**Wave sources:** Village counter-attack raids (3 types) + supply meter-driven Smolensk attack waves (3 routes) + caravan escorts
**Compositions:** Raids from Roslavl (cavalry), Yelnya (ranged), Vyazma (melee). Smolensk waves: base 4 spear + 4 MAA + 6 archer + 2 crossbow, scaling up to 3× via polynomial. Caravans: 1 cart + 2 spearmen (escalating with kills).
**Timing:** Raids: 240–500s random delay. Caravans: every 48s. Supply meter: waves launch when supply reaches 1000 (100 per caravan).
**Static defenders:** Village garrisons (cavalry/ranged/melee per village). Outpost defenders. Smolensk walls: 4 sections. Interior garrison.
**Named modules:** roslavl/yelnya/vyazma_defend, west/east_outpost_defend, smolensk_defend_e/w_1/2, smolensk_melee/ranged/cavalry/siege/wall/trebuchet, smolensk_left/center/right_wave_assault
**Special mechanics:** Supply meter system (0–1000, caravans add 100, wave on full); caravan death escalation (escorts grow, route closes at 5 kills); polynomial time-scaling

---

### Rogue (The Sultans Ascend)

#### rogue_maps

**Wave sources:** Lane-based wave system via `Rogue_UseDefaultSchedule()` across 4 maps (Coastline/Forest/Daimyo/Steppe)
**Compositions per map:**
- **Coastline:** 3 lanes (west/north/east). Pirate naval raids. Transport ship landings. 4 Byzantine side bases. Pirate units tiered: pirate/pirate_archer/MAA/crossbow/handcannon.
- **Forest:** 3 lanes, `rogue_wave_strength = 0.85`. 5 bandit camps. Outlaws: bandit/axeman/swordsman/horseman. Naval disabled.
- **Daimyo:** 3 lanes with unit-type validators: North = ranged only (boss: Oda Nobunaga), East = melee only (boss: Hojo Ujinao), West = cavalry only (boss: Takeda Shingen). Shinobi secondary threat. Day/night cycle.
- **Steppe:** 3 lanes requiring cavalry, `rogue_wave_strength = 0.9`. Horse archer raiders with economy-based spawning (income rate 1.0–4.0×). 8 guard patrols (a–h).
**Timing:** Difficulty-scaled intervals. Naval raids: 300–2100s start delay. Raider attacks: exponentially scaled.
**Special mechanics:** Wonder defense mode; 12 boss units across 4 factions; lane validators (unit-type restrictions); shinobi ambush traps

---

### The Normans (Salisbury)

#### sal_chp1_rebellion
No spawn system — camera/movement tutorial.

#### sal_chp1_valesdun
Scripted tutorial encounters — not wave-based. Safety nets respawn units during encounters if depleted. 7 sequential objective phases teaching combat.

#### sal_chp2_dinan
2 scripted raids triggered by building completion (horsemen after stables, archers after range). Dinan garrison: ~53 defenders across 10+ zones. Tutorial: base-building → military → siege.

#### sal_chp2_township
No spawn system — economy/age-up tutorial.

#### sal_chp2_womanswork
No spawn system — economy tutorial.

#### sal_chp3_brokenpromise
Beach ambush (15 MaA on disembark) + static garrisons. Pevensey: 5 Defend groups (17 units). Hastings: 15 Defend groups (75 units). Player reinforcements spawned when Hastings discovered.
**Special mechanics:** Naval invasion tutorial; production rate 2×, build time 0.5×; transport ships 1.2× speed

---

## Reusable Patterns

### Common Spawn Functions
- **`UnitEntry_DeploySquads`** — Universal spawn call used by all modules and waves
- **`ResolveSpawnLocation`** — Resolves marker/egroup/position to valid spawn point
- **`DissolveModuleIntoModule`** — Transfers all units between modules (used by RovingArmy fallback, Defend withdrawal)
- **`Wave_Prepare`/`Wave_Launch`** — Two-phase staging → assault pattern

### Wave Escalation Patterns

| Pattern | Missions | Description |
|---------|----------|-------------|
| Linear count increase | Most standard missions | Unit counts scale linearly with wave index |
| Polynomial power scaling | hun_chp3_orleans, hun_chp4_rouen, ang_chp4_rochester, gdm_chp4_smolensk | `(t/4) + (t^6/10^9)` or similar formulas |
| Cost-budget system | abb_m5_mansurah, ang_chp4_rochester | Wave allocates a "budget" to buy unit types by cost |
| Economy-driven | abb_bonus, gdm_chp2_tribute | Wave size scales with AI resource income |
| Intensity tier system | gdm_chp4_kazan | Discrete intensity levels (0–8) triggered by events |
| Supply meter | gdm_chp4_smolensk | Waves launch when accumulated supply reaches threshold |

### Reinforcement Mechanisms

| Mechanism | Missions | Description |
|-----------|----------|-------------|
| TownLife provider | gdm_chp4_kazan, gdm_chp3_novgorod | TownLife module produces units for combat modules |
| Module dissolution | ang_chp2_bayeux, ang_chp3_wallingford | Retreating units merge into another module |
| Player purchase panels | ang_chp2_tinchebray, hun_chp3_patay, challenge_malian | Gold-based unit purchasing via diplomacy UI |
| Cavalry detachment UI | gdm_chp2_kulikovo | One-time cavalry signal panel |
| Vassal "Request Aid" | gdm_chp3_moscow | Request reinforcements from multiple ally settlements |
| Escalating escort | ang_chp4_dover, gdm_chp4_smolensk | Escort force grows after each convoy/caravan event |
| Wave suppression cap | mon_chp2_kiev, ang_chp4_lincoln | New waves suppressed if enemy count exceeds threshold |

### Standard Unit Composition Templates

| Squad Type | Typical Easy Count | Typical Expert Count | Pattern |
|------------|-------------------|---------------------|---------|
| Small (low) | 2–3 | 5–6 | Garrison/barricade positions |
| Medium | 4–5 | 10–14 | Patrol and escort groups |
| Standard (high) | 6–7 | 14–15 | Most common defender count |
| Large | 8–10 | 20–24 | Major garrison/army modules |
| Massive | 14–18 | 28–35 | Boss armies, final waves |

### Difficulty Scaling Patterns for Spawns

| What Scales | How | Examples |
|-------------|-----|---------|
| **Timing** | Intervals decrease on harder | 570→270s (mon_chp1_juyong), 480→120s (mon_chp1_zhongdu) |
| **Count** | Squad sizes increase linearly | {6,7,10,14} pattern in 10+ missions |
| **Composition** | Unit types substituted | Horsemen→knights, spearmen→MAA, militia→crossbowmen |
| **Feature toggle** | Systems enabled/disabled | Attack waves off on Easy (hun_chp4_rouen), raids off on Easy (gdm_chp4_kazan) |
| **Power multiplier** | Float multiplier on wave strength | 0.8/1.0/1.4/2.0 (hun_chp3_orleans) |
| **Build time** | Faster unit production on harder | 30→12s (ang_chp1_york), 13→7s (ang_chp4_lincoln) |
