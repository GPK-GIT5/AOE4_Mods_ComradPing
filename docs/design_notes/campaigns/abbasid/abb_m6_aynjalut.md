# Abbasid Mission 6: Ayn Jalut

## OVERVIEW

Ayn Jalut is a large-scale defensive battle where the player (Mamluks) must survive 5 timed waves of Mongol and Crusader forces advancing toward the town of Afula. The mission is split into two phases: an initial vanguard defense where the player must keep their vanguard alive while weakening the enemy, followed by a full battle phase where 5 rounds of enemy cohorts attack via road and flanking lanes while the player receives timed reinforcements. Enemy forces use a sophisticated order system that marches them through hill, field, and town phases with walk/run transitions. The mission fails if all Afula villagers or the vanguard are killed; it completes when all 5 rounds are defeated. Sultan Qutuz arrives with the final reinforcement wave carrying handcannoneers.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `abb_m6_aynjalut.scar` | core | Main mission script: player setup, preset, start, runtime logic, reinforcements, villager systems |
| `abb_m6_aynjalut_data.scar` | data | Defines all constants, army sizes, cohort/round definitions, lanes, slots, reinforcement schedules |
| `abb_m6_aynjalut_objectives.scar` | objectives | Registers and manages all OBJ_ objectives, fail/complete conditions |
| `abb_m6_aynjalut_forces.scar` | spawns | Force spawning engine: round/cohort/force init, rank-based spawning, order execution state machine |
| `abb_m6_aynjalut_automated.scar` | automated | Campaign autotest harness with checkpoint monitoring and AI-driven play |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | core | Init 4 players with alliances and shared vision |
| `Mission_SetupVariables` | core | Calls `AynJalut_InitData1` for variable setup |
| `Mission_Preset` | core | Upgrades, resources, building immunity, healer init |
| `Mission_PreStart` | core | Init objectives and spawn ally villagers |
| `Mission_Start` | core | Queue cohorts, start objectives, begin monitoring rules |
| `PerSecond` | core | Increment `mission_seconds` timer each second |
| `SpawnAllyVillagers` | core | Spawn villagers at farms, lumber, stone, gold camps |
| `ModifyVision` | core | Reduce ally sight radius, adjust outpost vision |
| `InitResources` | core | Set player1 resources to zero, disable pop cap UI |
| `SpawnEnemyScout` | core | Spawn single Mongol scout on road lane |
| `ScoutCTA` | core | Show call-to-action alert for Mongol arrival |
| `AdvanceScout` | core | Move scout further down the road at ~224s |
| `OnSquadDeath` | core | Track villager/vanguard/enemy kills globally |
| `OnEntityDamaged` | core | Detect villager damage, trigger flee behavior |
| `AfulaVillagerAttacked` | core | Create minimap blip and event cue on attack |
| `StartTrackingForwardVillagers` | core | Register outlying villagers for flee monitoring |
| `MonitorForwardVillagers` | core | Check proximity to enemies, trigger flee per villager |
| `VillagerFlee` | core | Move villager along waypoints to safe zone |
| `MonitorFleeingVillagers` | core | Check if fleeing villager reached safety |
| `VillagerStopFleeing` | core | Re-add arrived villager to Afula pool |
| `MakeAllyBuildingsAttackable` | core | Enable targeting on ally building groups |
| `MakeAllyBuildingsImmune` | core | Disable targeting on ally building groups |
| `Reinforcement_Init` | core | Calculate cost for each reinforcement battalion |
| `Reinforcement_Queue` | core | Spawn reinforcement battalions with ratio scaling |
| `Battalion_Queue` | core | Spawn units, play VO/CTA, trigger onComplete |
| `GetReinforcementRatio` | core | Scale reinforcements 0.4–1.0 based on player army cost |
| `MakeEGroupAttackable` | core | Toggle invulnerability and targeting on EGroup |
| `ShowMinimapPath` | core | Animate enemy approach arrows on minimap |
| `Minimap_AnimateArrowPath` | core | Set up blip animation along marker path |
| `Minimap_AnimateArrowPath_AddBlip` | core | Create directional arrow blip at path position |
| `Minimap_AnimateArrowPath_RemoveBlip` | core | Destroy arrow blip after duration |
| `Healers_Init` | core | Spawn monks at healer markers, start monitoring |
| `Healers_Monitor` | core | Keep healers facing their assigned marker direction |
| `PrintReport` | core | Log player military cost and count |
| `AynJalut_InitData1` | data | Define all constants, army sizes, lanes, slots, cohorts, reinforcements |
| `CreateLane` | data | Build ordered marker path for a named lane |
| `CreateSlots` | data | Build letter+number keyed marker lookup for area |
| `GetRecipe` | data | Return MissionOMatic recipe with intro/outro NIS |
| `Round_Init` | forces | Initialize round: assign IDs, init cohorts, sum costs |
| `Cohort_Init` | forces | Initialize cohort: assign IDs, init forces, sum costs |
| `Force_Init` | forces | Initialize force: resolve SBP, build ranks, set flags |
| `QueueCohorts` | forces | Schedule all cohort arrivals and signal timers |
| `Cohort_Arrives` | forces | Spawn all forces in cohort, call on_arrive callback |
| `Cohort_Signal` | forces | Execute signal orders for all forces in cohort |
| `Force_Spawn` | forces | Spawn force in ranks or as group, execute initial orders |
| `Force_SpawnInRank` | forces | Spawn single rank, walk down road lane |
| `Force_SpawnNotInRank` | forces | Spawn force as blob, optionally create Army |
| `Force_ExecuteOrders` | forces | State machine: dispatch order by type string |
| `Force_ExecuteOrderWaitForDuration` | forces | Delay then advance order index |
| `Force_ExecuteOrderWaitForArrival` | forces | Poll proximity to marker before advancing |
| `Force_ExecuteOrderRun` | forces | Remove walk speed modifier, set running |
| `Force_ExecuteOrderWalk` | forces | Apply walk speed modifier |
| `Force_ExecuteOrderAttackLane` | forces | Move force along lane markers with/without AI |
| `Force_ExecuteOrderAttackSlot` | forces | Move force to slot marker with/without AI |
| `Force_FinishAfula` | forces | Direct force to attack Afula targets |
| `Force_CreateArmy` | forces | Wrap force in Army_Init with combat params |
| `Force_ChooseAfulaTargets` | forces | Pick left/right Afula target based on villager positions |
| `AynJalut_InitObjectives` | objectives | Register all 10 objectives |
| `UpdateAfulaVillagerCount` | objectives | Update villager counter, fail if zero |
| `StartInitialObjectives` | objectives | Start vanguard defense and weaken objectives |
| `StartMainObjective` | objectives | Transition to defeat + defend Afula objectives |
| `AutoTest_OnInit` | automated | Detect autotest flag, register checkpoints |
| `AutomatedMission_Start` | automated | Reveal FOW, spawn knight armies on two lanes |
| `Automated_MonitorDefenders` | automated | Reinforce defender armies back to 50 knights |
| `Automated_Phase1_Monitor` | automated | Wait for vanguard objective completion |
| `Automated_Phase2_Monitor` | automated | Wait for defeat enemy objective completion |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_Dummy` | Primary | Placeholder for UI element anchoring |
| `OBJ_DummyBattle` | Battle | Placeholder battle objective |
| `OBJ_DefendTheVanguard` | Information | Keep Mamluk vanguard alive; counter tracks survivors; fails mission if all die |
| `OBJ_WeakenTheEnemy` | Battle | Phase 1: weaken Mongol army before main force arrives |
| `OBJ_UnitsKilled` | Battle (child) | Counter of enemy units eliminated (child of WeakenTheEnemy) |
| `OBJ_DefeatTheEnemy` | Battle | Phase 2: defeat all 5 Mongol waves |
| `OBJ_Waves` | Primary (child) | Counter: waves defeated out of 5 (child of DefeatTheEnemy); completes mission |
| `OBJ_DefendAfula` | Information | Protect Afula villagers; fails mission if all die |
| `OBJ_DefendTheVillagers` | Primary (child) | Counter of remaining villagers (child of DefendAfula) |
| `OBJ_Reinforcements` | Primary | Countdown timer to next reinforcement wave |

### Difficulty

All difficulty values use `Util_DifVar({easy, normal, hard, hardest})`:

| Parameter | Values | Effect |
|-----------|--------|--------|
| `player_prepare_time` | 60, 52, 46, 40 | Seconds of warning before each wave attack |
| `ARMY_SIZE_*` (8 tiers) | varies per tier | numRanks, numFiles, extra, numSquads — scales enemy force size |
| `ARMY_SIZE_*_SPECIAL` (3 tiers) | varies | Separate scaling for Crusader/special forces |
| Player upgrades (preset) | diff ≤ 2/1/0 | Extra ranged/melee damage upgrades on easier difficulties |
| `Player_ModifyAyyubidMilitaryBuildTimes` | 0.5, 0.75, 1, 1 | Faster military build on easier difficulties |

### Spawns

**Wave Structure:** 5 rounds, each composed of 2–3 cohorts (11 total). Each cohort has multiple forces.

| Round | Cohorts | Composition | Notes |
|-------|---------|-------------|-------|
| 1 | 1–3 | Horsemen, spearmen (sides); militia, archers (road) | Vanguard wave; walks in rank formation |
| 2 | 4–5 | Militia XXXL (sides); Mongol knights, horse archers (road) | Makes ally buildings attackable on arrive |
| 3 | 6–7 | Crusader Holy Order units (Teuton, Templar, Hospitaller masters + troops, crossbowmen) | `player3` forces; `is_crusader = true` |
| 4 | 8–9 | Mongol knights (left); archers XXL (right); spearmen XXL (road) | Mixed composition |
| 5 | 10–11 | Horse archers (left); Mongol knights (right); Kitbuqa hero + MAA + crossbowmen (road) | Final wave with named hero unit |

**Spawn Points:** `mkr_spawn_road`, `mkr_spawn_left`, `mkr_spawn_right`

**Movement Phases:** Forces advance through phases: hill → half → field → battle → town → finish_afula. Road forces march in rank formation (`is_in_rank=true`) with `RANK_INTERVAL=1.5s` between ranks. Side forces spawn as blobs with AI control.

**Player Reinforcements:** 5 timed reinforcement waves arrive before each enemy round:
1. Spearmen (20) + archers (20) + horsemen (20)
2. Men-at-arms (40) + crossbowmen (40)
3. Spearmen (40) + horse archers (20)
4. Archers (40) + knights (20)
5. Sultan Qutuz (hero) + men-at-arms (20) + handcannoneers (20) + horsemen (20)

Reinforcement counts are dynamically scaled by `GetReinforcementRatio()` (0.4–1.0) based on existing player military value (floor=8000, ceiling=20000 cost).

### AI

- `USE_AI_GLOBAL = true` — side cohorts and some road forces use Army system with AI control
- `Force_CreateArmy()` wraps forces in `Army_Init` with `combatRange = 35`
- Road forces in rank formation do NOT use AI initially; AI enabled via `enable_ai` flag at specific phases
- `AI_Enable(player1, true)` only used in autotest mode
- `Force_OnArmyComplete` switches completed armies to `TARGET_ORDER_PATROL` targeting Afula
- `Army_AddTargets` / `Army_SetTargets` used for dynamic target updates
- No encounter plans; uses custom cohort/force order system instead

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `PerSecond` | `Rule_AddInterval`, 1s | Global mission clock |
| `ROUNDS_BEGIN` | 20s | Base offset for wave scheduling |
| `ROUND_ATTACK_TIME_1` | 310s (~5:10) | First wave reaches town |
| `ROUND_INTERVAL` | 135s (2:15) | Gap between successive rounds |
| `ROUND_ATTACK_TIME_2–5` | +135s each | Rounds 2–5 attack times |
| `REINFORCE_TIME_1–5` | attack_time − prepare_time | Player reinforcements arrive before each wave |
| `FORCE_INTERVAL_LONG` | 15s | Delay between force spawns in a cohort (larger gaps) |
| `FORCE_INTERVAL_SHORT` | 10s | Delay between force spawns in a cohort (tighter gaps) |
| `RANK_INTERVAL` | 1.5s | Delay between rank spawns within a force |
| `SpawnEnemyScout` | `Rule_AddOneShot`, 7s | Scout spawns on road |
| `ScoutCTA` | `Rule_AddOneShot`, 25s | Call-to-action alert |
| `AdvanceScout` | `Rule_AddOneShot`, 244s | Scout advances further |
| `ShowMinimapPath` | `Rule_AddOneShot`, 15s | Animate enemy approach arrows |
| `RemoveAlert` | `Rule_AddOneShot`, 12s | Clear villager attack minimap blip |
| `Cohort arrival/signal` | `Rule_AddOneShot`, per cohort | Each cohort has `arrive_at`, `signal_field_at`, `signal_town_at` |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| `abb_m6_aynjalut.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar`, `missionomatic/missionomatic_upgrades.scar`, `abb_m6_aynjalut_data.scar`, `abb_m6_aynjalut_objectives.scar`, `abb_m6_aynjalut_forces.scar`, `abb_m6_aynjalut_automated.scar` |
| `abb_m6_aynjalut_data.scar` | `cardinal.scar`, `missionomatic/missionomatic.scar` |
| `abb_m6_aynjalut_forces.scar` | `MissionOMatic/MissionOMatic.scar`, `cardinal.scar` |
| `abb_m6_aynjalut_objectives.scar` | `cardinal.scar` |
| `abb_m6_aynjalut_automated.scar` | `cardinal.scar`, `MissionOMatic/MissionOMatic.scar`; conditionally: `test/common.scar`, `test/standard_test.scar`, `test/test_framework.scar` |

### Shared Globals

| Global | Defined In | Used In |
|--------|-----------|---------|
| `player1–player5` | core | all files |
| `cohorts`, `rounds`, `round_1–round_5` | data | forces, objectives |
| `cohort_1–cohort_11` | data | data (round grouping) |
| `ARMY_SIZE_*` constants | data | data (cohort definitions) |
| `ROUND_ATTACK_TIME_1–5`, `REINFORCE_TIME_1–5` | data | data, objectives |
| `reinforcements`, `reinforcement_index` | data | core, objectives |
| `forces_total`, `forces_spawned` | data | forces |
| `rounds_defeated`, `enemies_killed` | data | core, objectives |
| `sg_afula_villagers`, `sg_vanguard` | data/core | objectives, core |
| `sg_all_enemies`, `sg_healers`, `sg_qutuz` | data | core |
| `lanes`, `slots`, `slot_letters`, `slot_numbers` | data | forces |
| `WALK_SPEED`, `RANK_INTERVAL` | data | forces |
| `USE_AI_GLOBAL` | data | data (cohort definitions) |
| `mission_seconds` | data | core, objectives |
| `OBJ_DefendTheVanguard`, `OBJ_DefeatTheEnemy` | objectives | automated, core |
| `OBJ_Waves`, `OBJ_DefendAfula`, etc. | objectives | core |
| `EVENTS.*` | MissionOMatic (external) | core |
| `SBP.*`, `UPG.*`, `EBP.*` | cardinal (external) | data, core, forces |

### Inter-File Function Calls

| Caller File | Callee File | Functions Called |
|-------------|-------------|-----------------|
| core → data | `AynJalut_InitData1()`, `AynJalut_InitData2()`, `GetRecipe()` |
| core → objectives | `AynJalut_InitObjectives()`, `UpdateAfulaVillagerCount()`, `StartInitialObjectives()` |
| core → forces | `QueueCohorts()` |
| data → forces | `Round_Init()` (called during data init), `Reinforcement_Init()` |
| data → core | `StartMainObjective()` (via reinforcement onComplete callback), `MakeAllyBuildingsAttackable()`, `MakeAllyBuildingsImmune()`, `WaveAttack2–5` (via cohort on_signal_town callbacks) |
| forces → core | `Cardinal_ConvertTypeToSquadBlueprint()` (cardinal), `CreateUnits()`, `Army_Init()` |
| automated → objectives | `Objective_IsComplete(OBJ_DefendTheVanguard)`, `Objective_IsComplete(OBJ_DefeatTheEnemy)` |
