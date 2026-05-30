# Mongol Chapter 3: Xiangyang 1267

## OVERVIEW

The Siege of Xiangyang (1267) is a two-phase campaign mission where the player commands Mongol forces (Castle age) against Song Dynasty defenders at the twin cities of Fancheng and Xiangyang. Phase 1 flows through clearing an initial Song watchpost, destroying a fortified wooden camp (with a flanking detection system that repositions defenders based on player approach), then linking up with allied reinforcements to escort traction trebuchets in a bridge assault. Phase 2 shifts to surrounding Xiangyang by stationing units at three bridgehead zones (west, north, south), triggering a 45-second countdown, and surviving a five-wave escalating Song counter-attack sally totaling 250–325 units depending on difficulty. Supporting systems include a Raiding module for horseman/knight/firelancer raids, scout-based threat arrow detection, villager fear walla audio, bridge destruction/repair mechanics, resource pickups, and an optional pagoda visit for monk allies.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp3_xiangyang_1267.scar | core | Main mission script: 4 players, restrictions, recipe with 20+ modules, patrol/bridge/scout/audio rules, outro |
| obj_xiangyang1_phase1.scar | objectives | Phase 1 objectives: clear approach, wooden camp flanking, ally rally, trebuchet defense |
| obj_xiangyang1_phase2.scar | objectives | Phase 2 objectives: 3 bridgehead surround zones, finale timer, final sally wave system |
| obj_xiangyang1_secondary.scar | objectives | Optional objective: visit pagoda to leash neutral monks for healing |
| training_xiangyang1.scar | training | Tutorial hint for Mongol outpost speed bonus mechanic |
| gathering_utility.scar | other | Imported utility for villager gathering commands (external) |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | core | Configure 4 players: Mongol, Song, Civilians, Allies |
| Mission_SetupVariables | core | Init SGroups, EGroups, difficulty vars, raiding, objectives |
| Mission_SetRestrictions | core | Lock siege engineers, gate locks, boost defences, upgrades |
| Mission_Preset | core | Global events, patrol/bridge/scout rules, audio, bridge inventory |
| Mission_Start | core | Set resources to 0, start OBJ_Advance, init tutorial |
| GetRecipe | core | Define recipe: intro units, Defend/RovingArmy/UnitSpawner modules |
| Xiangyang1267_SpawnPickups | core | Spawn 11 resource pickups (food/wood/gold) at markers |
| Xiangyang1267_OnSquadKilled | core | GE_SquadKilled handler tracking Song unit deaths |
| Xiangyang1267_RunOutro | core | Spawn outro armies, cut tower range, catapult bridge |
| Xiangyang_BoostDefences | core | Apply 15x health, 4x damage, 1.5x range to Song walls/towers |
| Xiangyang1267_SpawnRoadPatrol | core | Spawn militia/archer RovingArmy patrols every 90s (max 4) |
| Xiangyang1267_WaitForRefugees | core | Send refugee supply cart fleeing when player approaches |
| Xiangyang1267_WaitForBribe | core | Send civilian lumberjack to chop trees near pickup |
| Xiangyang1267_SpawnAllies | core | Deploy 96 horsemen + 48 knights + 4 trebs as allies |
| Xiangyang1267_ScoutSpotting | core | Create threat arrows when scouts detect Song modules |
| Xiangyang1267_CheatDeleteOutlyingUnits | core | Stage-based cleanup of Song units for cheat skipping |
| Xiangyang1267_WatchSallyBridge | core | Monitor player near bridge, trigger Nest of Bees destruction |
| Xiangyang1267_BlastSallyBridge | core | Order bridgeblaster Nest of Bees to destroy sally bridge |
| Xiangyang1267_OnBreachFirst | core | Play charge walla on first palisade wall breach |
| Xiangyang1267_OnBreachSecond | core | Play charge walla on second palisade breach at camp |
| Xiangyang1267_VillagerFearWallas | core | Trigger fear audio when civilian workers attacked |
| Xiangyang1267_OnDamageReceived | core | Warn player when attacking invulnerable stone walls |
| Xiangyang1267_InitObjectives_Phase1 | phase1 | Register OBJ_Advance and 4 sub-objectives |
| Xiangyang_WatchForTemple | phase1 | Start pagoda objective when player spots temple |
| Xiangyang_WatchForCamp | phase1 | Reveal wooden camp and start VO when spotted |
| Xiangyang1267_CheckMongolAdvance_Logic | phase1 | Check if Song post defeated or player advanced |
| Xiangyang1267_WatchRiverPostVO | phase1 | Play VO only if player fought (not bypassed) river post |
| Xiangyang_SpawnNorthernArmy | phase1 | Deploy western army: 16 knights, 24 horse archers, 2 scouts |
| Xiangyang1267_TopUpWithAllies | phase1 | Transfer allied reinforcement group to player control |
| Xiangyang_CampFlanks | phase1 | Detect north/east flanking, reposition Song defenders |
| Xiangyang1267_WithdrawOutlyingSoldiers | phase1 | Retreat barricade defenders after wooden camp destroyed |
| Xiangyang1267_AlliedAttackWavePeelOff | phase1 | Split allied force into RovingArmy waves at Fancheng gate |
| Xiangyang_HandleLeftovers | phase1 | Disband ally armies, split into 3 defend modules at bridgeheads |
| Xiangyang1267_LaunchAlliedAttack | phase1 | Send allies in 40-unit waves toward Fancheng gate |
| Xiangyang1267_LaunchBreadcrumbers | phase1 | Spawn Song breadcrumb units to lure player south |
| Xiangyang1267_LaunchSwarmerArmy | phase1 | Spawn escalating Song swarmers from Xiangyang direction |
| Xiangyang1267_IsBridgeDestroyed | phase1 | Check sally bridge health below 5% threshold |
| Xiangyang1267_WatchAfterWoodenPost | phase1 | Spawn allies when player crosses wooden post area |
| Xiangyang1267_InitObjectives_Phase2 | phase2 | Register OBJ_CampUp, 3 surround subs, finale, sally |
| Xiangyang1267_MonitorBridgeheadVO | phase2 | Play VO when bridgehead zones first reach 100% |
| Xiangyang1267_SpawnAllCamps | phase2 | Deploy 3 Mongol camps with buildings + mixed units |
| Xiangyang1267_CalcSpawns | phase2 | Calculate safe spawn count within population cap |
| Xiangyang1267_SmallPokeAttack | phase2 | Trigger raiding system sally every 180s (Normal+) |
| Xiangyang1267_RevealWoods | phase2 | Reveal forest path when lumbermill visible on screen |
| Xiangyang1267_BridgeheadRatioWest | phase2 | Calculate player unit ratio at western bridgehead |
| Xiangyang1267_BridgeheadRatioNorth | phase2 | Calculate player unit ratio at northern bridgehead |
| Xiangyang1267_BridgeheadRatioSouth | phase2 | Calculate player unit ratio at southern bridgehead |
| Xiangyang1267_TriggerWarningSally | phase2 | Launch initial warning wave and start bridge repair |
| Xiangyang1267_InitFinalSally | phase2 | Configure 5 wave structures and sally directions |
| Xiangyang1267_LaunchFinaleWave | phase2 | Spawn and dispatch finale wave in random directions |
| Xiangyang1267_FinalWaveAreaComplete | phase2 | Retarget RovingArmy to nearby player units on victory |
| Xiangyang1267_FinalWaveDeath | phase2 | Increment wave counter and update progress bar |
| Xiangyang1267_CheckPlayerDefeat | phase2 | Grace period failure check across 3 bridgeheads |
| Xiangyang1267_StartBridgeRepair | phase2 | Spawn invulnerable Song villagers to repair bridges |
| Xiangyang1267_WarnAboutBridgehead | phase2 | Flash UI warning when bridgehead ratio drops below 50% |
| VisitPagoda_InitObjectives | secondary | Register optional pagoda visit objective |
| Xiangyang1267_MonkLeashing | secondary | Keep neutral monks within 45 range of temple |
| MissionTutorial_Init | training | Initialize training system (mostly disabled) |
| MissionTutorial_AddHintToOutposts | training | Register outpost speed bonus training hint |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_Advance | Primary | Phase 1 wrapper: advance through Song outer defenses |
| SOBJ_ClearApproach | Primary (child) | Clear initial Song watchpost or advance past it |
| SOBJ_BaitPlayer | Primary (child) | Rally to allied Mongol forces across the map |
| SOBJ_WoodenCamp | Battle (child) | Destroy all buildings in fortified wooden camp |
| SOBJ_DefendTrebs | Battle (child) | Protect 4 allied trebuchets during bridge assault |
| OBJ_CampUp | Primary | Phase 2 wrapper: surround Xiangyang at 3 positions |
| SOBJ_SurroundWest | Battle (child) | Station units at western bridgehead (ratio ≥ 55 pop) |
| SOBJ_SurroundNorth | Battle (child) | Station units at northern bridgehead (ratio ≥ 55 pop) |
| SOBJ_SurroundSouth | Battle (child) | Station units at southern bridgehead (ratio ≥ 55 pop) |
| OBJ_FinaleTimer | Information | 45-second countdown before final sally begins |
| OBJ_ContainFinalSally | Information | Survive 5 escalating Song counter-attack waves |
| OBJ_VisitPagoda | Optional | Visit pagoda to recruit neutral monks |
| OBJ_DebugComplete | Primary (hidden) | Debug: instantly complete mission |

### Difficulty

| Parameter | Values {Easy, Normal, Hard, Expert} | What it scales |
|-----------|-------------------------------------|----------------|
| g_finalWaveTiming | {40, 40, 35, 30} | Seconds between finale sally waves |
| g_sizeWoodenPost | {6, 8, 12, 18} | Garrison size at wooden camp defend modules |
| g_sizeBarricades | {2, 3, 4, 5} | Unit count per barricade position (Posts 6/7) |
| g_sizeSiegeAttackers | {12, 16, 20, 26} | Song siege attacker RovingArmy size |
| g_finalWaveTotalSize | {250, 275, 300, 325} | Total units across all 5 finale waves |
| Raiding partySize | {12, 12, 14, 16} | Horseman/knight/firelancer raid party count |
| Raiding raidTiming | {40, 40, 30, 20} | Seconds between raid launches |
| Road patrol archers | {2, 4, 5, 6} | Archer count in road patrol groups |
| Breadcrumber squads | {4, 6, 8, 10} | Spearmen and archers per breadcrumb wave |
| SongPost1 archers | {4, 4, 6, 8} | Initial Song watchpost ranged garrison |
| SongPost1 MAA | {0, 0, 2, 2} | Men-at-arms at initial watchpost |
| Camp springalds | {0, 0, 1, 2} | Springalds at wooden camp southwest |
| Finale ranged types | varies | Grenadiers/repeater crossbows on Hard/Expert |

### Spawns

- **Player start**: 14 knights + 14 horsemen + 28 horse archers + 2 scouts at eastern map edge
- **Western army**: 16 knights + 24 horse archers + 2 scouts spawned mid-phase as reinforcements
- **Allied force**: 3 groups of 32 horsemen + 16 knights each, plus 4 traction trebuchets
- **Allied reinforcements**: 15–50 mixed cavalry, scaled to keep player above 80 total units
- **Song wooden camp**: 4 Defend modules (north/east/southwest + buffer), difficulty-scaled
- **Song barricades**: Posts 6 (5 groups) and Post 7 (3 groups) of spearmen/archers/militia
- **Siege attackers**: RovingArmy of MAA/spearmen/archers targeting trebuchets
- **Road patrols**: Militia + archers in RovingArmy, spawned every 90s (max 4 patrols)
- **Breadcrumber waves**: Spearmen + archers spawned from Fancheng side, max 8 waves
- **Swarmer armies**: Escalating RovingArmies (MAA/spearmen/crossbow), capped at 150 active
- **Phase 2 camps**: 3 Mongol camps (east/north/west) with mixed infantry + cavalry + mobile buildings
- **Raiding system**: Horseman 60% / Knight 20% / Fire Lancer 20%, 2 parties max, 60s spacing
- **Final sally**: 5 waves escalating from 2/20 to 6/20 of total (250–325), distributed across occupied bridgeheads
- **Finale unit types**: Spearman, MAA, archer, repeater crossbow (+ grenadier on Hard/Expert)
- **Bridge blasters**: 4 Nest of Bees positioned to destroy sally bridge on player approach

### AI

- **Defend modules**: SongPost1, SongPost4North/East/NorthBuff/EastBuff/Southwest — static position defense
- **RovingArmy modules**: SongSiegeAttackers (target trebuchets), road patrols (cycle waypoints), swarmer armies (attack-move to player rally points)
- **Flanking AI**: `Xiangyang_CampFlanks` detects player approach direction (FLANK_NONE/NORTH/EAST/FULL) and dynamically repositions all 4 wooden camp Defend modules via `Defend_UpdateTargetLocation`
- **Raiding system**: `Raiding_Init` with 5 village scout targets, inactive scouting, 2-party limit
- **Final sally RovingArmies**: ARMY_TARGETING_PROX with combatRange=50, leashRange=60, `preVictoryFunction` retargets to nearby player squads
- **Allied AI**: Allied cavalry split into 40-unit RovingArmy waves attacking Fancheng gate, then converted to 3 Defend modules at bridgeheads post-Phase 1
- **Mop-up system**: After Phase 1, Song spawns infantry to attack-move remaining player units near Xiangyang, then retreats
- **Gate control**: Song city gates locked/unlocked at phase transitions; palisade gates unlocked for unit flow
- **Withdraw behavior**: SongRunners, BaitScout1/2 flee when sighted or reduced, dissolving into other modules
- **Bridgeblasters**: Nest of Bees on hold position with boosted weapon damage, fire on sally bridge when player approaches

### Timers

| Rule | Interval | Purpose |
|------|----------|---------|
| Xiangyang1267_SpawnRoadPatrol | 90s | Spawn Song road patrols (max 4 total) |
| Xiangyang1267_WatchSallyBridge | 1s | Monitor player proximity to trigger bridge destruction |
| Xiangyang1267_WaitForRefugees | 1s | Detect player near refugees, send them fleeing |
| Xiangyang1267_WaitForBribe | 1s | Detect player near lumberyard pickup point |
| Xiangyang1267_VillagerFearWallas | 1s | Trigger fear audio when villagers attacked |
| Xiangyang1267_ScoutSpotting | 1s | Create threat arrows for scout-spotted enemies |
| Xiangyang_WatchForTemple | 0.5s | Start pagoda objective when temple visible |
| Xiangyang_WatchForCamp | 0.5s | Reveal wooden camp and trigger VO |
| Xiangyang_CampFlanks | 0.5s | Detect and respond to player flanking approach |
| Xiangyang1267_SmallPokeAttack | 180s | Trigger raid attacks on player buildings (Normal+) |
| Xiangyang1267_MonitorBridgeheadVO | 3s | Play VO for bridgehead zone completion |
| Xiangyang1267_LaunchFinaleWave | g_finalWaveTiming | Launch escalating finale waves (30–40s) |
| Xiangyang1267_LaunchBreadcrumbers | 12s (24s delay) | Spawn breadcrumb units to lure player south |
| Xiangyang1267_LaunchAlliedAttack | OneShot 5s | Begin allied assault on Fancheng after treb deployment |
| Xiangyang1267_WithdrawOutlyingSoldiers_Retry | 5s (15s delay) | Re-issue retreat orders to stuck Song units |
| Xiangyang1267_NudgeAlliesAway | 3s | Push allied stragglers away from Fancheng gate |
| Xiangyang1267_RevealWoods | 1s | Reveal forest path when lumbermill on screen |
| Xiangyang1267_DelayedAutoSave | OneShot 20s | Autosave after Phase 2 starts |
| OBJ_FinaleTimer | 45s countdown | Countdown before final sally begins |
| g_failGracePeriod | 60s | Grace period before mission failure at empty bridgehead |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core mission framework (Defend, RovingArmy, UnitSpawner, recipe system)
- `obj_xiangyang1_phase1.scar` → imports `obj_xiangyang1_phase2.scar` (chained import)
- `obj_xiangyang1_secondary.scar` — optional pagoda objective
- `training_xiangyang1.scar` → imports `training/campaigntraininggoals.scar`
- `gathering_utility.scar` — villager gathering commands (used for lumberyard bribe)

### Shared Globals
- `g_playerMongol`, `g_playerSong`, `g_playerCivilians`, `g_playerAllies` — player handles used across all files
- `sg_allies`, `sg_allied_trebuchets`, `sg_all_intro_units` — shared SGroups across objectives
- `sg_second_army` — western army SGroup referenced in flanking logic
- `g_SongFortressStarted` — flag set in Mission_Start
- `g_breadcrumbersLaunched`, `g_breadcrumbMax` — breadcrumb wave tracking
- `g_finalWaveInitialized`, `g_finalWavesStarted` — finale state flags
- `g_stopAttackingGate` — stops allied gate assault on treb objective completion
- `g_stopSpawingRaiders` — disables raid spawning
- `g_bridgeheadDenominator` (55) — population threshold for bridgehead completion
- `g_failGracePeriod` (60) — seconds before failure when bridgehead lost
- `eg_song_invulnerable_walls` — made invulnerable after Phase 1 completion
- `eg_sally_bridge`, `eg_southern_bridges` — bridge EGroups shared across phases

### Inter-File Function Calls
- Core → Phase 1: `Xiangyang1267_InitObjectives_Phase1()`, `Xiangyang1267_InitObjectives_Phase2()`
- Core → Secondary: `VisitPagoda_InitObjectives()`
- Core → Training: `MissionTutorial_Init()`
- Phase 1 → Core: `Xiangyang1267_SpawnAllies()`, `Xiangyang1267_CheatDeleteOutlyingUnits()`, `Xiangyang1267_TopUpWithAllies()`
- Phase 1 → Phase 2: imported directly via `import("obj_xiangyang1_phase2.scar")`
- Phase 2 → Core: `Xiangyang1267_SmallPokeAttack()`, `Xiangyang_HandleLeftovers()`, `Xiangyang1267_SpawnAllCamps()`
- Phase 2 → Phase 1: `Xiangyang1267_CheckPlayerDefeat()` references bridgehead ratio functions

### MissionOMatic Framework Usage
- `MissionOMatic_FindModule()` — locates Defend/RovingArmy modules by descriptor string
- `Defend_IsDefeated()`, `Defend_UpdateTargetLocation()`, `Defend_Init()` — defend module lifecycle
- `RovingArmy_Init()`, `RovingArmy_AddTarget()`, `RovingArmy_Disband()` — roving army lifecycle
- `Raiding_Init()`, `Raiding_TriggerRaid()` — raiding subsystem
- `Missionomatic_SetGateLock()` — gate lock/unlock control
- `Missionomatic_SpawnPickup()` — resource pickup spawning
- `MissionOMatic_RevealMovingSGroup()` — fog of war reveal for moving units
- `MissionOMatic_HintOnSquadSelect()` — conditional squad-selection hints
- `MissionOMatic_SGroupCommandDelayed()` — delayed movement commands
