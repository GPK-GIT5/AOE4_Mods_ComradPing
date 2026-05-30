# Mongol Chapter 2: Kiev

## OVERVIEW

The Siege of Kiev (1240) is a large-scale destruction mission where the player controls Mongke Khan's Mongol forces (Feudal→Castle) against Rus-controlled Kiev (Castle age). The mission flows through three phases: breach the main gate with a starting army and trebuchets, establish a forward base by unpacking Mongol mobile structures, then systematically destroy all buildings across three city districts (Industrial, Outer, Inner). Kiev's layered wall defenses spawn district-specific defenders when breached, while periodic attack waves counter-assault the player from surviving production buildings. Fire propagation, atmospheric haze transitions, and trade cart raiding provide environmental storytelling. Training hints teach Arsenal research, incendiary weapon usage, and Mongke Khan's leader production ability.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp2_kiev.scar | core | Main mission setup: players, difficulty, restrictions, recipe, gate tracking, spawning, fire/atmospherics, attack waves |
| obj_destroygate.scar | objectives | First objective — breach the main outer gate by destroying wall segments |
| obj_forwardbase.scar | objectives | Second objective — deploy and unpack Mongol mobile structures as a forward base |
| obj_destroykiev.scar | objectives | Primary objective with 3 sub-objectives — destroy all buildings in Industrial, Outer, and Inner districts |
| training_kiev.scar | training | Tutorial goal sequences for Arsenal, incendiary weapons, and Mongke leader ability (PC + Xbox) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | mon_chp2_kiev | Configure 4 players: Mongol, Kiev, neutral, trade partner |
| Mission_SetupVariables | mon_chp2_kiev | Init objectives, groups, gate constants, leader reference |
| Mission_SetDifficulty | mon_chp2_kiev | Define difficulty table and sprawl defender templates |
| Mission_SetRestrictions | mon_chp2_kiev | Remove trebuchets/landmarks, auto-upgrades, springald garrison |
| Mission_Preset | mon_chp2_kiev | Gate refs, wall tracking, weaken structures, spawn traders |
| Mission_Start | mon_chp2_kiev | Start DestroyGate objective, garrison forts on difficulty |
| GetRecipe | mon_chp2_kiev | Define recipe: locations, RovingArmy/Defend/TownLife modules, titlecard |
| Kiev_CheckGateDamage | mon_chp2_kiev | Detect attack on gate area, retarget RovingArmy defenders |
| Kiev_CheckDefenderStatus | mon_chp2_kiev | Monitor melee count, trigger reinforcement spawns |
| Kiev_SpawnResistance | mon_chp2_kiev | Spawn replacement defenders to gate defend modules |
| Kiev_SpawnTraders | mon_chp2_kiev | Deploy trade carts between outer and industrial markets |
| Kiev_StartTrading | mon_chp2_kiev | Issue trade command to spawned trade cart |
| Kiev_GateTracking | mon_chp2_kiev | Detect wall breach, trigger district spawns, play walla |
| MongkeCall | mon_chp2_kiev | Play Mongke VO when leader present at breached wall |
| Kiev_InitializeTrainingHints | mon_chp2_kiev | Enable leader training hint after forward base complete |
| Kiev_WaitForArsenalHint | mon_chp2_kiev | Poll for arsenal building before enabling hint |
| Kiev_WaitForIncendiaryHint | mon_chp2_kiev | Poll for incendiary upgrade before enabling hint |
| Kiev_WaitForLeaderHint | mon_chp2_kiev | Poll for forward base completion before leader hint |
| Kiev_CheckGroupsForFire | mon_chp2_kiev | Spread fire to all members of a burning egroup |
| Kiev_StructureFireSpread | mon_chp2_kiev | On entity killed, ignite nearby structures (disabled) |
| Kiev_WeakenStructures | mon_chp2_kiev | Apply 0.5x health modifier to non-military buildings |
| Kiev_UpdateBurningAtmospherics | mon_chp2_kiev | Transition to haze after 20+ buildings destroyed |
| Kiev_SpawnAttackWave2 | mon_chp2_kiev | Pick random surviving district, launch Wave attack |
| Kiev_SpawnSprawlAttackWave | mon_chp2_kiev | Launch sprawl wave if source buildings alive |
| Kiev_CheckTraderKilled | mon_chp2_kiev | Trigger VO event when first trade cart killed |
| Kiev_SpawnFirstGateDefenders | mon_chp2_kiev | Spawn initial defenders at industrial and outer gates |
| Kiev_SetupSprawlProxChecking | mon_chp2_kiev | Init 7 proximity checks for sprawl RovingArmy spawns |
| Kiev_SprawlProxCheck | mon_chp2_kiev | Spawn sprawl defenders when player units detected nearby |
| Kiev_SpawnIndustrialDistrictUnits | mon_chp2_kiev | Spawn defenders into industrial defend modules |
| Kiev_SpawnOuterDistrictUnits | mon_chp2_kiev | Spawn cavalry/ranged defenders into 5 outer defend modules |
| Kiev_SpawnOuterDistrictWallDefenders | mon_chp2_kiev | Spawn archer RovingArmies on outer wall positions |
| Kiev_SpawnInnerDistrictUnits | mon_chp2_kiev | Spawn MAA/crossbow/monk/knight defenders in 7 inner positions |
| Kiev_SpawnInnerDistrictWallDefenders | mon_chp2_kiev | Spawn crossbow RovingArmies on inner wall positions |
| Kiev_SpawnIntroUnits | mon_chp2_kiev | Deploy starting army: scouts, cavalry, infantry, Mongke, trebuchets |
| DestroyGate_InitObjectives | obj_destroygate | Register OBJ_DestroyGate with start/complete/fail logic |
| DestroyGate_EntityKilled | obj_destroygate | GE_EntityKilled handler for gate destruction (disabled) |
| DestroyKiev_InitObjectives | obj_destroykiev | Register OBJ_DestroyKiev and 3 sub-objectives with progress UI |
| DestroyKiev_PreStart | obj_destroykiev | Start OBJ_DestroyKiev objective |
| DestroyKiev_AssignGateReferences | obj_destroykiev | Set up gate damage checking for 3 inner gates |
| DestroyKiev_Complete | obj_destroykiev | Destroy all units, spawn outro units, sunset atmosphere |
| DestroyKiev_SetupWaveData | obj_destroykiev | Create Wave_New for industrial/outer/inner attack waves |
| DestroyKiev_SetupSprawlWaveData | obj_destroykiev | Create 4 sprawl Wave_New with staggered intervals |
| DestroyKiev_SurvivorCallout | obj_destroykiev | Add per-entity hintpoints when buildings below threshold |
| DestroyKiev_CheckEntityMarker | obj_destroykiev | Track individual marked entities, remove on destruction |
| DestroyKiev_PlayDestructionWalla | obj_destroykiev | Play scaled celebration walla on nearby player squads |
| ForwardBase_InitObjectives | obj_forwardbase | Register OBJ_ForwardBase with unpack completion check |
| ForwardBase_PreStart | obj_forwardbase | Spawn packed structures + villagers, start objective |
| ForwardBase_SpawnPlayerStructures | obj_forwardbase | Deploy 5 mobile Mongol buildings and build entity egroup |
| ForwardBase_CheckForStructuresDropped | obj_forwardbase | Remove hintpoint when structure unpacked from squad |
| Kiev_InitializeArsenalTrainingHints | training_kiev | Goal sequence: select arsenal → research arrows |
| Kiev_InitializeIncendiaryWeaponTrainingHints | training_kiev | Goal sequence: select ranged unit → attack structure |
| Kiev_InitializeLeaderTrainingHints | training_kiev | Goal sequence: select Mongke → use production ability (PC) |
| Kiev_InitializeLeaderTrainingHints_Xbox | training_kiev | Goal sequence: select Mongke → open radial → use ability (Xbox) |
| Kiev_SkipTraining | training_kiev | Bypass training if OBJ_DestroyKiev complete |
| Kiev_PlayerHasArsenal | training_kiev | Trigger arsenal hint when bowyer built and resources available |
| Kiev_PlayerIsSelectingArsenal | training_kiev | Check if player has selected arsenal building |
| Kiev_PlayerIsResearchingUpgrade | training_kiev | Check if incendiary upgrade queued or hovered |
| Kiev_PlayerHasIncendiaryUpgrade | training_kiev | Trigger incendiary hint when upgrade researched + ranged unit exists |
| Kiev_PlayerHasSelectedRanged | training_kiev | Check if player selected ranged unit for fire attack |
| Kiev_PlayerHasAttackedStructuresWithArrows | training_kiev | Check if ranged unit attacked a structure |
| Structure_AttackedByArchers | training_kiev | GE_DamageReceived handler for ranged-on-building damage |
| Kiev_LeaderAndStructuresExist | training_kiev | Trigger leader hint when forward base done + Mongke on screen |
| Kiev_LeaderAndStructuresExist_Xbox | training_kiev | Xbox variant of leader hint trigger |
| Kiev_PlayerHasSelectedLeader | training_kiev | Check if Mongke sgroup is selected |
| Kiev_LeaderIsNearStructures | training_kiev | Check if leader ability hovered/used or timeout |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_DestroyGate | Primary | Breach the main outer gate by destroying wall segments |
| OBJ_ForwardBase | Primary | Unpack at least one mobile Mongol structure |
| OBJ_DestroyKiev | Primary | Parent: destroy all buildings in 3 districts |
| SOBJ_DestroyIndustrial | Sub | Destroy all non-wall buildings in Industrial district |
| SOBJ_DestroyOuter | Sub | Destroy all non-wall buildings in Outer city |
| SOBJ_DestroyInner | Sub | Destroy all non-wall buildings in Inner city |
| OBJ_DebugComplete | Debug | Cheat objective: kill inner city and complete mission |

**Flow:** OBJ_DestroyGate → OBJ_ForwardBase (5s delay) → OBJ_DestroyKiev + all SOBJs (20s delay after forward base starts).

### Difficulty

| Parameter | Easy | Normal | Hard | Hardest | What it scales |
|-----------|------|--------|------|---------|----------------|
| forts_have_springalds | false | false | true | true | Gate fort springald upgrades |
| forts_have_garrisons | false | true | true | true | Auto-garrison gate forts |
| spawn_attack_waves | false | true | true | true | Enable counter-attack waves |
| defender_count_high | 6 | 8 | 12 | 16 | Spearman/MAA counts at gates |
| defender_count_med | 3 | 4 | 6 | 8 | Archer/horsearcher counts |
| defender_count_low | 2 | 2 | 3 | 5 | Horseman/secondary ranged counts |
| defender_count_very_low | 1 | 1 | 2 | 3 | Springald/monk counts |
| main_attack_interval | 360 | 360 | 300 | 180 | Seconds between district attack waves |
| patrol_unit_cap | 50 | 60 | 80 | 120 | Max patrol units before wave suppression |
| sprawl_wave_intervals | 60-120 | 60-120 | 60-120 | 40-100 | Seconds between sprawl area attacks |

### Spawns

**Starting Army (player1):** 2 scouts, 1 ram, 6 knights, 12 horse archers, 30 spearmen, 18 archers, Mongke Khan, 2 traction trebuchets. Spawned via intro with march-in destinations.

**Forward Base Delivery:** 5 mobile Mongol buildings (TC, cavalry stable, infantry barracks, house, Deer Stones landmark) + 12-16 villagers (difficulty-scaled).

**Gate Defenders (per gate):** RovingArmy modules with spearmen (high count) + archers (med count). Up to 3 reinforcement waves per gate, triggered when melee count ≤ 3. Reinforcements stop if gate wall destroyed.

**District Defenders (spawned on wall breach):**
- Industrial: Spearmen + archers + springalds in 2 defend modules, reinforced from TownLife.
- Outer: 5 defend positions with horsemen, horse archers, crossbowmen, MAA, archers. Inner gate defenders also spawned.
- Inner: 7 RovingArmy positions with MAA, crossbowmen, monks, knights (difficulty-scaled).

**Wall Defenders:** 2 outer wall archer groups (5 each), 4 inner wall crossbow groups (4-5 each, difficulty-scaled).

**Sprawl Defenders:** 16 proximity-triggered RovingArmy positions (7 proximity zones) with spearmen + archers, spawned when player enters area. `onDeathDissolve = true`.

**Attack Waves (difficulty-gated):**
- District waves: Random source (industrial/outer/inner), spawned every `main_attack_interval` seconds. Industrial = spearmen + archers + springalds. Outer = horsemen + horse archers. Inner = MAA + crossbowmen + monks.
- Sprawl waves: 4 sources with staggered start delays (180/200/220/240s) and varying intervals (40-120s by difficulty). Units = single type per source (spearmen, horsemen, archers, spearmen).
- All waves use RovingArmy assault modules targeting player muster point and sprawl attack markers.
- Wave suppression: no new waves if `sg_patrol_units_count` exceeds difficulty-based cap (50-120).

**Trade Carts:** 2 traders per route between outer market and industrial market (player2 and player4).

### AI

- **No AI_Enable calls** — all enemy behavior driven by MissionOMatic modules (RovingArmy, Defend, TownLife).
- **RovingArmy modules:** 4 gate defenders (ARMY_TARGETING_CYCLE, onDeathReset), sprawl defenders (onDeathDissolve), district assault groups (ARMY_TARGETING_DISCARD with withdrawThreshold 0.3 and fallback markers).
- **Defend modules:** 7 city defense positions (2 industrial with TownLife reinforcements, 5 outer), 3 staging areas for wave assembly, 4 sprawl staging areas.
- **TownLife modules:** 3 instances (industry, outer, inner) with `canBuild = false`, no units spawned directly.
- **Gate damage detection:** `Kiev_CheckGateDamage` polls every 1s, retargets RovingArmy to multiple attack markers when structures under attack.
- **PlayerUpgrades_Auto:** Enabled for both player1 (with `true` flag) and player2.

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| Kiev_GateTracking | 0.5s interval | Monitor wall segment counts for industrial/outer/inner breaches |
| Kiev_SpawnIntroUnits | 10s one-shot | Deploy player starting army after mission load |
| Kiev_CheckGateDamage | 1s interval | Detect when gate defenders are engaged |
| Kiev_CheckDefenderStatus | 1s interval | Monitor melee unit count for reinforcement trigger |
| Kiev_SpawnResistance | 15s one-shot (delay param) | Spawn gate reinforcements after brief delay |
| Kiev_UpdateBurningAtmospherics | 5s interval | Check building count for haze transition |
| Kiev_SpawnAttackWave2 | main_attack_interval (180-360s) | Periodic counter-attacks from surviving districts |
| Kiev_SpawnSprawlAttackWave | 40-120s interval, 180-240s delay | Staggered sprawl area counter-attacks |
| Kiev_SprawlProxCheck | 1s interval | Detect player proximity to spawn sprawl defenders |
| ForwardBase_PreStart | 5s interval | Wait for gate area clear, then spawn forward base |
| DestroyKiev_PreStart | 20s one-shot | Start district destruction objective |
| DestroyKiev_SurvivorCallout | 1s interval | Add per-building markers when count below threshold |
| Kiev_WaitForLeaderHint | 5s interval | Poll for forward base completion to enable leader training |
| Kiev_WaitForArsenalHint | 5s interval | Poll for arsenal construction (currently disabled) |
| Kiev_WaitForIncendiaryHint | 5s interval | Poll for incendiary upgrade (currently disabled) |

### Atmosphere & Audio

- `Kiev_WeakenStructures`: Non-military enemy buildings receive 0.5x health modifier at mission start.
- `Kiev_UpdateBurningAtmospherics`: Transitions to `winter_afternoon_haze` after 20+ buildings destroyed.
- `DestroyKiev_Complete`: Transitions to `winter_sunset` for outro.
- Music intensity set to minimum tense (801) when outer district breached.
- `Music_UnlockIntensity` check determines forced music mode.
- Walla sounds scaled by nearby unit count (small/medium/large).
- Khan spawning disabled via `khan_spawning_disabled` state model bool.

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core campaign framework (Cardinal scripts included)
- `obj_destroygate.scar` — Gate breach objective
- `obj_forwardbase.scar` — Forward base objective
- `obj_destroykiev.scar` — District destruction objective
- `training_kiev.scar` → `training/campaigntraininggoals.scar` — Shared training goal predicates

### Shared Globals
- `player1`–`player4`: Player references used across all files
- `t_difficulty`: Difficulty table referenced by spawning and wave code in all files
- `eg_main_gate`, `eg_industrial_gate`, `eg_outer_gate`, `eg_inner_gate`: Gate egroups shared between core and objectives
- `destroyedGate[]`: Gate status table checked by spawning and objective code
- `remainingSpawns[]`: Reinforcement counter per gate
- `sg_leaderMongke`: Leader sgroup used by core, obj_forwardbase (trigger), and training_kiev
- `OBJ_DestroyGate`, `OBJ_ForwardBase`, `OBJ_DestroyKiev`: Objective tables cross-referenced for flow control
- `SOBJ_DestroyIndustrial`, `SOBJ_DestroyOuter`, `SOBJ_DestroyInner`: Sub-objectives
- `eg_kiev_industrial`, `eg_kiev_outer`, `eg_kiev_inner`: District building egroups
- `wall_count_main`, `wall_count_industrial`, etc.: Wall counts set in Preset, checked in objectives
- `GATE_MAIN/INDUSTRIAL/OUTER/INNER`: Gate ID constants (1-4)
- `sprawl_defenders`: Unit template defined in difficulty, used by proximity spawns
- `EVENTS.*`: Intel event references (Intro, Victory, Breach_MainGate, etc.)
- `sg_patrol_units_count`: Shared sgroup tracking total enemy patrol units for wave cap
- `b_EntityAttackedByRanged`: Flag set by `Structure_AttackedByArchers`, read by training hints
- `CampaignTraining_TimeoutIgnorePredicate`: From campaigntraininggoals.scar

### Inter-File Function Calls
- `obj_destroygate` → `Kiev_SetupSprawlProxChecking()`, `Kiev_SpawnFirstGateDefenders()`, `DestroyKiev_AssignGateReferences()` (in core/obj_destroykiev)
- `obj_forwardbase` → `Kiev_InitializeTrainingHints()` (in core)
- `obj_destroykiev` → `Kiev_SpawnAttackWave2()`, `Kiev_SpawnSprawlAttackWave()`, `Mission_Complete()`, `Mission_Fail()`
- `mon_chp2_kiev` → `DestroyGate_InitObjectives()`, `ForwardBase_InitObjectives()`, `DestroyKiev_InitObjectives()` (in respective objective files)
- `training_kiev` → `Kiev_InitializeArsenalTrainingHints()`, `Kiev_InitializeIncendiaryWeaponTrainingHints()`, `Kiev_InitializeLeaderTrainingHints()` called from core's `Kiev_InitializeTrainingHints()`

### MissionOMatic Module References
- `MissionOMatic_FindModule()`: Used to locate RovingArmy modules by descriptor string
- `RovingArmy_SetTargets()`, `RovingArmy_Init()`: Direct module manipulation
- `SpawnUnitsToModule()`, `SpawnGarrisonsIntoEGroup()`: MissionOMatic spawning utilities
- `Wave_New()`, `Wave_Prepare()`: Wave system for counter-attacks
- `Missionomatic_InitializeLeader()`: Leader system initialization
- `EventCues_CallToAction()`: UI cue system
- `TrackTradeCartsForPlayers()`: Trade tracking utility

### Blueprint References
- `SBP.MONGOL.UNIT_MONGKE_KHAN_CMP_MON`: Campaign Mongke Khan
- `SBP.MONGOL.BUILDING_*_MOVING_MON`: 5 mobile Mongol structures (TC, cavalry, infantry, house, Deer Stones)
- `EBP.RUS.BUILDING_DEFENSE_WALL_GATE_RUS`: Rus gate walls (tracked for destruction)
- `EBP.CAMPAIGN.BUILDING_DEFENSE_KIEVWALL_*`: Campaign-specific Kiev wall segments
- `UPG.MONGOL.UPGRADE_RANGED_INCENDIARY_MON`: Incendiary weapon upgrade (training target)
- `UPG.MONGOL.UPGRADE_BURN_BUILDING_BONUS_COOLDOWN_MON`: Prevents double raiding bonus
- `BP_GetAbilityBlueprint("leader_production_mon_activated")`: Mongke leader ability
