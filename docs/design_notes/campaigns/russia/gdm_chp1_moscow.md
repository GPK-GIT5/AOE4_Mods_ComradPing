# Russia Chapter 1: Moscow

## OVERVIEW

This mission depicts the 1238 Mongol siege of Moscow from the Russian campaign. The player (Muscovites, Rus civilization) must first defend Moscow from raiding Mongol horsemen who set buildings ablaze, then rebuild the devastated city, expand by constructing the Kremlin landmark and supporting structures, and finally withstand a multi-wave Mongol assault. The mission progresses through a linear objective chain: Protect Moscow → Rebuild Moscow → Expand Moscow → Build Defences → Defend Against Mongol Attacks. Gameplay spans Dark Age to Feudal Age, with environmental hazards (wolves, fires) and an optional objective to locate scattered villagers sheltering in forest Hunting Cabins.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `gdm_chp1_moscow.scar` | core | Main mission setup: players, variables, difficulty, recipe, intro fire sequence, wolf spawning, outro |
| `obj_protectmoscow.scar` | objectives | Phase 1: Chase off Mongol raiders and extinguish building fires |
| `obj_rebuildmoscow.scar` | objectives | Phase 2: Gather wood, recruit villagers, rebuild destroyed structures with ghost-building system |
| `obj_expandmoscow.scar` | objectives | Phase 3: Build Kremlin landmark, Market, and Archery Range |
| `obj_builddefences.scar` | objectives | Phase 4: Construct defensive Wooden Fortresses and train 40 military units |
| `obj_findvillagers.scar` | objectives | Optional: Locate Hunting Cabins with scared villagers in forests |
| `obj_mongolattacks.scar` | objectives | Phase 5: Countdown timer then multi-wave final Mongol attack; win/loss condition |
| `training_moscow.scar` | training | Tutorial hints for fire repair, Hunting Cabin mechanics, bounties, garrison, scouts |

---

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupPlayers` | gdm_chp1_moscow | Configure 3 players: Muscovites, Golden Horde, Villagers |
| `Mission_SetupVariables` | gdm_chp1_moscow | Create SGroups/EGroups for attackers, buildings, wolves |
| `Mission_SetDifficulty` | gdm_chp1_moscow | Define difficulty table for wolves, fire, attacks |
| `Mission_SetRestrictions` | gdm_chp1_moscow | Remove trade cart production |
| `Mission_Preset` | gdm_chp1_moscow | Init all objectives, set fires, configure music |
| `GetRecipe` | gdm_chp1_moscow | Define MissionOMatic recipe with units and RovingArmy modules |
| `Mission_Start` | gdm_chp1_moscow | Start ProtectMoscow, remove invulnerability, spawn wolves |
| `MissionStart_SetMoscowOnFire` | gdm_chp1_moscow | Set buildings on fire, destroy wall sections during intro |
| `MissionStart_SetMoscowOnFire_PartB` | gdm_chp1_moscow | Kill walls, apply zero fire damage modifier during intro |
| `MissionStart_SetMoscowOnFire_PartC` | gdm_chp1_moscow | Apply real fire damage rate after intro ends |
| `Mission_AddMoreWolves` | gdm_chp1_moscow | Periodically spawn wolves in forests up to max |
| `Mission_AdjustPlayerMaxPopCap` | gdm_chp1_moscow | Dynamically modify player pop cap via modifiers |
| `Mission_CheckForFail` | gdm_chp1_moscow | Fail mission if TC and Kremlin both destroyed |
| `Mission_PrepareForOutro` | gdm_chp1_moscow | Delete all units, spawn outro scene around Kremlin |
| `ProtectMoscow_InitObjectives` | obj_protectmoscow | Register OBJ_ProtectMoscow, SOBJ_ChaseOffMongols, SOBJ_PutOutFires |
| `ChaseOffMongols_Init` | obj_protectmoscow | Assign Mongol raiders to attack random buildings |
| `ChaseOffMongols_Monitor` | obj_protectmoscow | Track Mongol health; trigger flee/retarget/retaliate AI |
| `ChaseOffMongols_RunAway` | obj_protectmoscow | Make damaged Mongol flee toward exit marker |
| `ChaseOffMongols_ChangeTarget` | obj_protectmoscow | Redirect idle Mongol to new building target |
| `ChaseOffMongols_Retaliate` | obj_protectmoscow | Make Mongol counter-attack nearby player units |
| `ChaseOffMongols_ChooseBuildingToAttack` | obj_protectmoscow | Pick non-burning building as Mongol target |
| `PutOutFires_SetupUI` | obj_protectmoscow | Count burning buildings, set objective counter |
| `PutOutFires_Monitor` | obj_protectmoscow | Track fires extinguished; fail if <3 buildings remain |
| `PutOutFires_Complete` | obj_protectmoscow | Extinguish remaining fires, remove modifiers, start fail rule |
| `Villager_FearWalla` | obj_protectmoscow | Play periodic villager panic sounds during fires |
| `RebuildMoscow_InitObjectives` | obj_rebuildmoscow | Register rebuild obj with wood/people/structures sub-objs |
| `RebuildMoscow_TriggerObjective` | obj_rebuildmoscow | Start rebuild after ProtectMoscow completes |
| `RebuildStructures_SetupUI` | obj_rebuildmoscow | Place ghost palisades and buildings, track construction |
| `RebuildStructures_CheckRebuildingFinished` | obj_rebuildmoscow | Complete sub-obj when all structures rebuilt |
| `RebuildStructure_OnConstructionComplete` | obj_rebuildmoscow | Auto-assign villagers to next wall segment |
| `BuildStructures_RememberPositionsOfBuildings` | obj_rebuildmoscow | Record EBP/position/heading for ghost placement |
| `BuildStructures_MonitorConstructionProgress` | obj_rebuildmoscow | Match ghosts to manifest, add hintpoints, track progress |
| `BuildStructures_MonitorConstructionProgress_Check` | obj_rebuildmoscow | Poll construction progress, update counters/hintpoints |
| `BuildStructures_FilterManifest` | obj_rebuildmoscow | Remove already-built entries from manifest |
| `BuildStructures_IsManifestComplete` | obj_rebuildmoscow | Return true if all manifest buildings constructed |
| `GatherWood_Start` | obj_rebuildmoscow | Begin wood gathering monitor rule |
| `GatherWood_Monitor` | obj_rebuildmoscow | Track wood gathered, complete at 700 |
| `GatherWood_PlayerVenturedIntoForest` | obj_rebuildmoscow | Trigger wolf warning intel after 10s in forest |
| `GatherPeople_Monitor` | obj_rebuildmoscow | Track new villagers, complete at 8 |
| `RebuildMoscow_OnComplete` | obj_rebuildmoscow | Trigger ExpandMoscow on rebuild completion |
| `RebuildMoscow_GetConstructionHintPointText` | obj_rebuildmoscow | Return localized hint text per building type |
| `RebuildMoscow_GetBuildingHeightOffset` | obj_rebuildmoscow | Return UI hintpoint height offset per building |
| `ExpandMoscow_InitObjectives` | obj_expandmoscow | Register Kremlin, Market, Archery sub-objectives |
| `ExpandMoscow_TriggerObjective` | obj_expandmoscow | Start expand phase after rebuild completes |
| `BuildLandmark_SetupUI` | obj_expandmoscow | Place ghost Kremlin, unlock production |
| `BuildLandmark_CheckBuildingFinished` | obj_expandmoscow | On Kremlin done: start Market/Archery, trigger defences |
| `BuildMarket_SetupUI` | obj_expandmoscow | Place ghost Market building |
| `BuildArchery_SetupUI` | obj_expandmoscow | Place ghost Archery Range building |
| `BuildDefences_InitObjectives` | obj_builddefences | Register defence obj with structures/military sub-objs |
| `BuildDefences_TriggerObjective` | obj_builddefences | Start defence phase, show garrison hint |
| `BuildDefences_Start` | obj_builddefences | Schedule Mongol countdown 60s after defences start |
| `BuildDefensiveStructures_SetupUI` | obj_builddefences | Remove blockers, place ghost defensive structures |
| `BuildMilitaryUnits_SetupUI` | obj_builddefences | Set military counter, adjust for existing units |
| `BuildMilitaryUnits_Monitor` | obj_builddefences | Track military production, complete at 40 |
| `FindVillagers_InitObjectives` | obj_findvillagers | Register optional obj, set villager spawn table |
| `FindVillagers_MakeVillagersRunAway` | obj_findvillagers | Scatter villagers to forest Hunting Cabins |
| `FindVillagers_Monitor` | obj_findvillagers | Detect player proximity to cabins, transfer villagers |
| `FindVillagers_StartIfNotAlreadyStarted` | obj_findvillagers | Fallback trigger 5 min after rebuild starts |
| `MongolCountdown_InitObjectives` | obj_mongolattacks | Register countdown timer objective |
| `MongolCountdown_SetupUI` | obj_mongolattacks | Start countdown timer, trigger weather transition |
| `MongolCountdown_StartProbingAttacks` | obj_mongolattacks | Begin probing attacks (skipped on Easy) |
| `MongolCountdown_CreateProbingAttack` | obj_mongolattacks | Spawn escalating probe waves on interval |
| `MongolCountdown_CreateProbingAttack_Delayed` | obj_mongolattacks | Determine probe composition by escalation level |
| `MongolCountdown_MonitorProbingAttacks` | obj_mongolattacks | Track probing units for threat arrows |
| `MongolAttacks_Start` | obj_mongolattacks | Upgrade Mongols to Age II, begin final assault |
| `MongolAttacks_StartAttacks_PartB` | obj_mongolattacks | Define 4 spawn locations, launch wave 1, schedule waves 2-4 |
| `MongolAttacks_Monitor` | obj_mongolattacks | Monitor wave progression, check fail condition |
| `MongolAttacks_SpawnUnits` | obj_mongolattacks | Spawn wave units, assign to RovingArmy module |
| `MongolAttacks_Complete` | obj_mongolattacks | Destroy threat arrows, complete mission |
| `MissionTutorial_Init` | training_moscow | Start fire and fortress tutorial hints |
| `MissionTutorial_AddHintToPutOutFire` | training_moscow | Training goal: right-click burning building |
| `MissionTutorial_AddHintToHuntingBounties` | training_moscow | Training goal: hunt wolves for gold bounty |
| `MissionTutorial_AddHintForWoodenFortressLumberCampBonus` | training_moscow | Training goal: build fortress near lumber camp |
| `MissionTutorial_AddHintToDropoffHuntingCabins` | training_moscow | Training goal: Hunting Cabins as food drop-off |
| `MissionTutorial_AddHintToGoldGenHuntingCabins` | training_moscow | Training goal: Hunting Cabins generate gold near trees |
| `MissionTutorial_AddHintToBuildScouts` | training_moscow | Training goal: build scouts from TC or cabin |
| `MissionTutorial_AddHintToGarrisonOutposts` | training_moscow | Training goal: garrison units in Wooden Fortress |

---

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_ProtectMoscow` | Primary | Phase 1 parent: chase off Mongols and extinguish fires |
| `SOBJ_ChaseOffMongols` | Sub | Kill/rout all intro Mongol raiders (progress bar) |
| `SOBJ_PutOutFires` | Sub | Extinguish fires on inner city buildings (counter) |
| `OBJ_RebuildMoscow` | Primary | Phase 2 parent: gather resources and rebuild city |
| `SOBJ_GatherWood` | Sub | Gather 700 wood (counter) |
| `SOBJ_GatherPeople` | Sub | Produce/locate 8 additional villagers (counter) |
| `SOBJ_RebuildStructures` | Sub | Rebuild destroyed inner city structures (dynamic counter) |
| `OBJ_ExpandMoscow` | Primary | Phase 3 parent: construct expansion buildings |
| `SOBJ_BuildLandmark` | Sub | Build the Kremlin (Novgorod Kremlin landmark) |
| `SOBJ_BuildMarket` | Sub | Build the Market |
| `SOBJ_BuildArchery` | Sub | Build the Archery Range |
| `OBJ_BuildDefences` | Primary | Phase 4 parent: prepare for Mongol assault |
| `SOBJ_BuildDefensiveStructures` | Sub | Build Wooden Fortresses at preset locations (counter) |
| `SOBJ_BuildMilitaryUnits` | Sub | Produce 40 military units (counter, adjusted for existing) |
| `OBJ_MongolCountdown` | Info | Countdown timer before final attack; triggers weather change |
| `OBJ_MongolAttacks` | Primary | Phase 5: survive all Mongol attack waves to win |
| `OBJ_FindVillagers` | Optional | Locate Hunting Cabins with scared villagers in forests |
| `OBJ_DebugComplete` | Debug | Cheat objective to skip to mission completion |

### Difficulty

All values indexed by `{Easy, Normal, Hard, Expert}` via `Util_DifVar`:

| Parameter | Values | Scales |
|-----------|--------|--------|
| `maximumNumberOfWolves` | 10 / 15 / 20 / 30 | Max wolf count on map |
| `findVillagers_NearbyDistance` | 75 / 75 / 50 / 0 | Proximity for cabin hint ping (0 = no hint) |
| `fireDamageRate` | 0.35 / 0.4 / 0.7 / 1.0 | Fire damage multiplier on buildings |
| `fireThreshold` | 0.5 / 0.5 / 0.55 / 0.6 | Health % at which buildings catch fire |
| `numberOfScaredVillagers` | 6 / 6 / 5 / 3 | Number of findable villager groups |
| `mongolAttackDelay` | 10 / 10 / 8 / 5 | Minutes before final Mongol attack |
| `probingAttackFrequency` | 2 / 2 / 1.6 / 1.2 | Minutes between probing attacks |
| `probingAttackLevelAdjustment` | 0 / 0 / 1 / 2 | Offset added to probing attack escalation level |

Additional difficulty scaling:
- Intro Mongol horseman counts scale with `Util_DifVar` (1-2 squads per spawn point)
- Intro spearman groups restricted by difficulty flags (`GD_EASY`, `GD_NORMAL`, `GD_HARD`)
- Final attack wave 4 is Hard/Expert only; Expert gets extra units in every wave
- Probing attacks disabled entirely on Easy (`GD_EASY`)

### Spawns

**Intro Mongol Raiders:** 5-9 horsemen + 1 Khan spawned at `mkr_intro_mongol1-9` markers inside the city. Attack buildings, flee when damaged or Khan leaves.

**Probing Attacks (during countdown):** Escalating waves via `RovingArmy` module "ProbingMongolAttacks":
- Level 1-2: 1 scout
- Level 3-4: 1 scout + 2 spearmen
- Level 5: 2 horsemen + 2 spearmen
- Level 6: 3 horse archers
- Level 7+: 4 horse archers
- Spawn from `mkr_mongol_spawn1/2/4`, attack OuterCity/InnerCity

**Final Assault (4 waves):**
- **Wave 1:** 3 sub-waves of horsemen (3-5 each) + horse archers (Hard/Expert) + Khan. Single spawn direction.
- **Wave 2:** 5 sub-waves of spearmen (3-5 each), split across 2 spawn locations. Triggers at 30s or ≤15 Mongols remaining.
- **Wave 3:** 5 sub-waves of horse archers (3-4 each), multi-directional (adds spawn4 on Hard/Expert). Triggers at 60s or ≤15 remaining.
- **Wave 4 (Hard/Expert only):** 5 sub-waves of horse archers (2-6 each), 3 spawn directions. Triggers at 60s or ≤15 remaining.

Mongols upgraded to Age II (horseman_2, spearman_2) before final assault.

**Wolves:** Spawned every 30s up to difficulty max. Placed at hidden fog-of-war positions near forest markers.

**Scared Villagers:** 3-6 groups (2-3 villagers each) flee to forest Hunting Cabins at mission start. Transfer to player on proximity discovery.

### AI

- **No formal AI_Enable calls** — enemy behavior is entirely scripted
- **Intro raiders:** Custom state machine in `ChaseOffMongols_Monitor` — Mongols attack buildings, switch targets when building burns/dies, retaliate against attackers (Hard: prefer spearmen, Expert: prefer villagers), flee at ≤20% HP or when Khan leaves
- **Khan special behavior:** Flees when heavily damaged or ≤3 raiders remain; other raiders flee probabilistically after Khan departs
- **Probing attacks:** Use `RovingArmy` module with random spawn location selection and `attackMoveStyle_normal`
- **Final assault:** Uses 18 `RovingArmy` modules (MongolAttackers1a-4e), all targeting "InnerCity", staggered 2s apart within each wave
- **Threat arrows:** Created per spawn location for probing and final attacks via `ThreatArrow_CreateGroup`

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `Rule_AddInterval(Mission_AddMoreWolves, 30)` | Every 30s | Restock wolves in forests |
| `Rule_AddInterval(RebuildMoscow_TriggerObjective, 1)` | Every 1s | Poll for ProtectMoscow completion to start rebuild |
| `Rule_AddOneShot(FindVillagers_StartIfNotAlreadyStarted, 300)` | 5 min after rebuild | Fallback start for optional objective |
| `Rule_AddOneShot(BuildDefences_TriggerObjective, 20)` | 20s after Kremlin done | Start defence phase |
| `Rule_AddOneShot(MongolCountdown_TriggerObjective, 60)` | 60s after defences start | Begin Mongol countdown |
| `Objective_StartTimer(OBJ_MongolCountdown, COUNT_DOWN, ...)` | 5-10 min (difficulty) | Visible countdown to final attack |
| `Rule_AddInterval(MongolCountdown_CreateProbingAttack, ...)` | 1.2-2 min (difficulty) | Probing attack frequency |
| `Game_TransitionToState("taiga_winter_sunset", ...)` | Over countdown | Weather transition for atmosphere |
| `Rule_AddInterval(ChaseOffMongols_Monitor, 0.5)` | Every 0.5s | Mongol raider AI state updates |
| `Rule_AddInterval(PutOutFires_Monitor, 0.5)` | Every 0.5s | Track fire extinguishing progress |
| `Rule_AddInterval(GatherWood_Monitor)` | Every frame | Track wood income |
| `Rule_AddInterval(GatherPeople_Monitor, 0.5)` | Every 0.5s | Track new villager count |
| `Rule_AddInterval(FindVillagers_Monitor, 0.5)` | Every 0.5s | Detect player near scared villagers |
| `Rule_AddInterval(BuildMilitaryUnits_Monitor, 0.5)` | Every 0.5s | Track military production count |
| `Rule_AddInterval(MongolAttacks_Monitor, 0.5)` | Every 0.5s | Wave progression and fail check |
| `Rule_AddInterval(Villager_FearWalla, 1)` | Every 1s | Play panic sounds during fires |
| `Rule_AddOneShot(RebuildMoscow_AddDropoffHint, 10)` | 10s after rebuild | Show Hunting Cabin drop-off tutorial |
| `Rule_AddInterval(GatherWood_PlayerVenturedIntoForest, 2)` | Every 2s | Detect player in forest for wolf warning |

---

## CROSS-REFERENCES

### Imports

| Import | File |
|--------|------|
| `MissionOMatic/MissionOMatic.scar` | gdm_chp1_moscow (also imports Cardinal scripts) |
| `training/campaigntraininggoals.scar` | training_moscow |

### Inter-File Function Calls

| Caller File | Calls Into | Function |
|-------------|-----------|----------|
| gdm_chp1_moscow | obj_protectmoscow | `ProtectMoscow_InitObjectives()` |
| gdm_chp1_moscow | obj_rebuildmoscow | `RebuildMoscow_InitObjectives()` |
| gdm_chp1_moscow | obj_expandmoscow | `ExpandMoscow_InitObjectives()` |
| gdm_chp1_moscow | obj_builddefences | `BuildDefences_InitObjectives()` |
| gdm_chp1_moscow | obj_mongolattacks | `MongolCountdown_InitObjectives()`, `MongolAttacks_InitObjectives()` |
| gdm_chp1_moscow | obj_findvillagers | `FindVillagers_InitObjectives()` |
| gdm_chp1_moscow | training_moscow | `MissionTutorial_Init()` |
| obj_rebuildmoscow | obj_findvillagers | `FindVillagers_StartIfNotAlreadyStarted()` |
| obj_rebuildmoscow | obj_expandmoscow | `ExpandMoscow_TriggerObjective()` |
| obj_rebuildmoscow | training_moscow | `MissionTutorial_AddHintToDropoffHuntingCabins()`, `MissionTutorial_AddHintToHuntingBounties()` |
| obj_expandmoscow | obj_builddefences | `BuildDefences_TriggerObjective()` |
| obj_expandmoscow | obj_rebuildmoscow | `BuildStructures_RememberPositionsOfBuildings()`, `BuildStructures_FilterManifest()`, `BuildStructures_MonitorConstructionProgress()`, `BuildStructures_IsManifestComplete()` |
| obj_builddefences | obj_mongolattacks | `MongolCountdown_TriggerObjective()` |
| obj_builddefences | obj_rebuildmoscow | `BuildStructures_*` family (shared construction system) |
| obj_builddefences | training_moscow | `MissionTutorial_AddHintToGarrisonOutposts()` |
| obj_findvillagers | training_moscow | `MissionTutorial_AddHintToBuildScouts()`, `MissionTutorial_AddHintToGoldGenHuntingCabins()` |
| obj_mongolattacks | gdm_chp1_moscow | `Mission_Complete()`, `Mission_Fail()` |
| obj_protectmoscow | gdm_chp1_moscow | `Mission_Fail()` |

### Shared Globals

- **Player handles:** `player1` (Muscovites), `player2` (Golden Horde), `player3` (Villagers)
- **Difficulty table:** `t_difficulty` — accessed by all objective files
- **Resource goals:** `i_desiredWoodAmount` (700), `i_desiredVillagerAmount` (8), `i_desiredMilitaryAmount` (40)
- **SGroups:** `sg_start_mongols`, `sg_start_mongols_khan`, `sg_end_mongols`, `sg_wolves`, `sg_gaia`, `sg_probing_mongol_attacks`
- **EGroups:** `eg_importantBuildings`, `eg_gradBuildings_onFire`, `eg_gradBuildings_notOnFire`, `eg_allPlannedBuildings`
- **Construction manifests:** `t_buildingsToConstruct_Age1`, `t_buildingsToConstruct_Landmark`, `t_buildingsToConstruct_Defences`
- **Forest/wolf markers:** `t_forestMarkers`, `t_wolfSpawnMarkers`, `t_wolfDestinationMarkers`
- **Mongol spawn markers:** `mkr_mongol_spawn1-4`, `mkr_mongol_exit`
- **Location descriptors:** "InnerCity", "OuterCity" (via `LOCATION()`)
- **Fire modifiers:** `modid_fireDamageRate`, `modid_fireThreshold`
