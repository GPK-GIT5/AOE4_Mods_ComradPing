# Salisbury Chapter 2: Dinan

## OVERVIEW

Salisbury Chapter 2: Dinan is a tutorial mission in the Salisbury (Norman) campaign that teaches base-building, military production, unit upgrades, and siege assault. The player controls Mathilde (player1, French civ) in the Feudal Age, progressing through four sequential objective phases: setting villager priorities and building military infrastructure (barracks, stables, archery range), recruiting spearmen/horsemen/archers, researching upgrades at a blacksmith, and finally marching an assembled army to capture Chateau de Dinan by destroying its keep. Two scripted enemy raids — horsemen after building stables and archers after building an archery range — teach counter-unit matchups mid-build. The mission uses MissionOMatic for intro/outro NIS, Training goal sequences for step-by-step controller input prompts, and a reinforcement safety net during the final assault.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| sal_chp2_dinan.scar | core | Mission setup: players, relationships, ages, restrictions, variables, production helpers, recipe, outro staging |
| obj_expand.scar | objectives | Expand-phase objectives: villager priorities, build houses/barracks/stables/archery, recruit 10 each of spearmen/horsemen/archers, handle raids |
| obj_upgrade.scar | objectives | Upgrade-phase objectives: research Hardened spearman upgrade, build blacksmith, research technology |
| obj_capture.scar | objectives | Capture-phase objectives: march army to Chateau de Dinan, destroy the enemy keep, hero ability optional |
| training_sal_chp2_dinan.scar | training | All Training goal sequences: villager priorities, building placement, rally points, unit production, counter-unit raids, find menu, D-pad selection, hero ability |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_OnGameSetup | sal_chp2_dinan | Set player1–3 names (Mathilde, Brittany, Neutral) |
| Mission_OnInit | sal_chp2_dinan | Force training, set ages, configure player3 neutral |
| Mission_SetupVariables | sal_chp2_dinan | Init objectives, define enemy/raid/patrol unit counts |
| Mission_SetDifficulty | sal_chp2_dinan | Empty — fixed-difficulty tutorial mission |
| Mission_SetRestrictions | sal_chp2_dinan | Lock most buildings/units/upgrades, remove abilities |
| Mission_Preset | sal_chp2_dinan | Assign villagers to resources, complete harvest upgrade |
| Mission_PreStart | sal_chp2_dinan | Spawn 3 starting villagers, set buildings invulnerable |
| Mission_Start | sal_chp2_dinan | Enable HUD widgets, start OBJ_VillagerPriorities |
| GetRecipe | sal_chp2_dinan | Define intro/outro NIS and title card for MissionOMatic |
| GivePlayerRequired | sal_chp2_dinan | Calculate and grant resources for unit production |
| ProduceBuildingsObjectiveTracker | sal_chp2_dinan | Track building construction count toward objective |
| ProduceBuildings_Monitor | sal_chp2_dinan | Poll building count, complete objective when target met |
| ProduceUnitsObjectiveTracker | sal_chp2_dinan | Track unit production count toward objective |
| ProduceUnits_Monitor | sal_chp2_dinan | Poll unit count + queue, complete objective at target |
| Spawn_Corpses | sal_chp2_dinan | Spawn 10 corpse fields for outro cinematic |
| Destroy_Buildings | sal_chp2_dinan | Set Dinan buildings on fire for outro |
| Shot_01 | sal_chp2_dinan | Outro shot 1: spawn cheering soldiers |
| Shot_02 | sal_chp2_dinan | Outro shot 2: spawn William, Harold, gift escorts |
| Shot_03 | sal_chp2_dinan | Outro shot 3: warp Harold's gifts, march them out |
| SpawnDinanCheatArmy | sal_chp2_dinan | Debug: spawn 10 of each unit type for testing |
| Expand_InitObjectives | obj_expand | Register all expand-phase objectives |
| SetMilitaryPreset_Start | obj_expand | Launch villager priorities training, add monitor |
| SetMilitaryPreset_Monitor | obj_expand | Complete when any resource weight is set |
| HandleBuildHousesObjective | obj_expand | Check existing houses; start houses or skip to barracks |
| Build2Houses_PreStart | obj_expand | Grant 100 wood, track house construction starts |
| BuildBarracks_PreStart | obj_expand | Grant 150 wood, unlock barracks, track construction |
| SetRally_Start | obj_expand | Find barracks, set invulnerable, add rally event listener |
| OnRallyPoint | obj_expand | Complete SOBJ_SetRally on CMD_RallyPoint issued |
| Make10Spearmen_PreStart | obj_expand | Unlock spearman production, set counter to 10 |
| BuildStables_PreStart | obj_expand | Grant 150 wood, unlock stables, track construction |
| HorsemenRaid_Start | obj_expand | Spawn raid horsemen, slow speed, set waypoints to TC |
| HorsemenRaid_Monitor | obj_expand | Complete when all raid horsemen killed |
| Make10Horsemen_PreStart | obj_expand | Unlock horseman production, set counter to 10 |
| BuildArchery_PreStart | obj_expand | Grant 150 wood, unlock archery range, track construction |
| ArchersRaid_Start | obj_expand | Spawn raid archers, set waypoints to TC |
| ArchersRaid_Monitor | obj_expand | Complete when all raid archers killed |
| Make10Archers_PreStart | obj_expand | Unlock archer production, set counter to 10 |
| HorsemenRaid_UI | obj_expand | Collect stables + landmark into eg_stables group |
| ArchersRaid_UI | obj_expand | Collect archery ranges into eg_archeryranges group |
| UpgradeUnits_InitObjectives | obj_upgrade | Register all upgrade-phase objectives |
| Hardened_Start | obj_upgrade | Unlock spearman upgrade, find barracks, add monitor |
| Hardened_Monitor | obj_upgrade | Complete when Hardened queued or already researched |
| BuildBlacksmith_Start | obj_upgrade | Unlock blacksmith, track construction |
| Research_Start | obj_upgrade | Find blacksmith, launch training, add monitor |
| Research_Monitor | obj_upgrade | Complete when any research queued at blacksmith |
| Capture_InitObjectives | obj_capture | Register capture-phase + hero ability objectives |
| March_Start | obj_capture | Collect army, launch D-pad training, add monitor |
| March_Monitor | obj_capture | Complete when army reaches mkr_chateau_dinan |
| SpawnEnemies | obj_capture | Deploy all enemy defenders across Dinan zones |
| StartPatrols | obj_capture | Init 2 RovingArmy patrol modules for enemy patrols |
| HeroAbility_StartMonitor | obj_capture | Start hero ability objective near outpost proximity |
| HeroAbility_Start | obj_capture | Launch hero ability training, add event listener |
| HeroAbility_Monitor | obj_capture | Complete when ability executed |
| HeroAbilityFail_Monitor | obj_capture | Fail hero objective if outpost enemies all dead |
| Destroy_Start | obj_capture | Add keep monitor, setup reinforcements, set keep min cap |
| Destroy_Monitor | obj_capture | Complete when keep health < 5% or destroyed |
| KeepAttacked | obj_capture | Send all enemies to keep when player approaches |
| Reinforcement_Setup | obj_capture | Track player army by type for reinforcement system |
| Reinforcement_Monitor | obj_capture | Respawn 7–10 units of any type that drops to ≤ 2 |
| SelectAll_Monitor | obj_capture | Trigger intel when whole army selected |
| Goals_VillagerPriorities | training | Goal sequence: open menu, set military preset, close |
| Goals_Build2Houses | training | Goal sequence: select villager, choose house, place 2 |
| Goals_BuildBarracks | training | Goal sequence: open radial, military page, select barracks |
| Goals_RallyPoint | training | Goal sequence: select barracks, set rally point |
| Goals_Make10Spearmen | training | Goal sequence: open barracks radial, queue 10 spearmen |
| Goals_BuildStables | training | Goal sequence: open radial, military page, select stables |
| Goals_HorsemenRaid | training | Goal sequence: hold LT, select infantry, attack-move |
| Goals_ProduceMultipleSources | training | Goal sequence: double-select stables, queue horsemen ×5 |
| Goals_BuildArchery | training | Goal sequence: open radial, military page, select archery range |
| Goals_ArchersRaid | training | Goal sequence: hold LT, select cavalry, attack-move |
| Goals_Make10Archers | training | Goal sequence: find menu, locate archery, queue archers |
| Goals_SelectDPad | training | Goal sequence: D-pad left for army, attack-move |
| Goals_HeroAbility | training | Goal sequence: D-pad right for hero, Y to activate |
| Goals_UpgradeUnits | training | (Referenced) Goal sequence for research at barracks |
| Goals_BuildBlacksmiths | training | (Referenced) Goal sequence for blacksmith construction |
| Goals_Research | training | (Referenced) Goal sequence for blacksmith research |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_VillagerPriorities | Primary | "Re-Prioritize the Villagers" — set military production preset |
| SOBJ_SetMilitaryPreset | Sub | Choose the Military Preset in villager priorities radial |
| OBJ_Spearmen | Primary | "Recruit Spearmen" — build infrastructure and train spearmen |
| SOBJ_Build2Houses | Sub/Build | Build 2 houses (counter 0/2) |
| SOBJ_BuildBarracks | Sub/Build | Build a Barracks (counter 0/1) |
| SOBJ_SetRally | Sub | Set a Rally Point on the barracks |
| SOBJ_Make10Spearmen | Sub | Produce 10 Spearmen (counter 0/10) |
| OBJ_Cavalry | Primary | "Recruit Horsemen" — build stables, survive raid, train horsemen |
| SOBJ_BuildStables | Sub/Build | Build a Stable (counter 0/1) |
| SOBJ_HorsemenRaid | Sub/Battle | Defeat enemy horseman raid on player base |
| SOBJ_Make10Horsemen | Sub | Produce 10 Horsemen (counter 0/10) |
| OBJ_Archers | Primary | "Recruit Archers" — build archery range, survive raid, train archers |
| SOBJ_BuildArchery | Sub/Build | Build an Archery Range (counter 0/1) |
| SOBJ_ArchersRaid | Sub/Battle | Defeat enemy archer raid on player base |
| SOBJ_Make10Archers | Sub | Produce 10 Archers (counter 0/10) |
| OBJ_UpgradeUnits | Primary | "Upgrade your Units" — research at barracks and blacksmith |
| SOBJ_Hardened | Sub | Research Hardened (spearman tier 2) upgrade at barracks |
| SOBJ_BuildBlacksmith | Sub | Build a Blacksmith (counter 0/1) |
| SOBJ_Research | Sub | Research any technology at blacksmith |
| OBJ_Capture | Primary | "Capture Chateau de Dinan" — final assault |
| SOBJ_March | Sub | March army to the keep (proximity check) |
| SOBJ_Destroy | Sub/Battle | Destroy the enemy keep (health < 5%) |
| OBJ_HeroAbility | Optional | Use Guillaume's Hero Ability near outpost |

### Difficulty

No `Util_DifVar` calls — this is a fixed-difficulty tutorial mission. All unit counts are hardcoded constants in `Mission_SetupVariables`. Production rate is tripled (`Modify_PlayerProductionRate(player1, 3)`) and construction time is halved (`construction_rate_multiplier = 0.5`) to accelerate the tutorial pace.

### Spawns

**Player Units (player1):**
- `sg_startVillagers`: 3 villagers at `mkr_starting_villagerse`
- `sg_woodVillagers`, `sg_goldVillagers`, `sg_farmVillagers`: Pre-placed villagers assigned to resources
- `sg_william`: Guillaume/Duke William hero unit (pre-placed in map)
- Produced units: 10 spearmen, 10 horsemen, 10 archers (player-built)

**Enemy Defenders (player2) — spawned by `SpawnEnemies()` on capture phase:**
- Outpost: `num_spear_outpost` (4) spearmen + `num_archers_outpost` (4) archers
- Garrison: `num_garrison` (3) villagers, garrisoned via `Util_FallBackToGarrisonBuilding`
- Exterior: 3 spearmen + 6 archers (2 markers × 3)
- Front gate: 8 spearmen (2 markers × 4)
- Docks: 4 spearmen
- Town Center: 3 spearmen + 4 horsemen + 4 archers + 4 horsemen (rear)
- Keep: 5 spearmen + 4 horsemen + 6 archers (2 markers × 3)
- **Total defenders: ~53 units**

**Enemy Patrols (player2):**
- Patrol 01: 3 spearmen + 3 archers, 4-waypoint cycle (`ARMY_TARGETING_CYCLE`)
- Patrol 02: 3 spearmen + 3 archers, 3-waypoint reverse (`ARMY_TARGETING_REVERSE`)

**Enemy Raids (player2):**
- Horsemen raid: `num_raid_horsemen` (4) horsemen from `mkr_raid_spawn_a`, speed reduced to 0.8×, pathed through 4 waypoints to TC
- Archer raid: `num_raid_archers` (6) archers from `mkr_raid_spawn_a`, pathed through 4 waypoints to TC

**Reinforcement Safety Net (capture phase):**
- Monitored every 5 seconds via `Reinforcement_Monitor`
- If spearmen ≤ 2: spawn 7 spearmen at `mkr_reinforcements_spear_spawn`
- If archers ≤ 2: spawn 10 archers at `mkr_reinforcements_cav_spawn`
- If horsemen ≤ 2: spawn 10 horsemen at `mkr_reinforcements_archer_spawn`
- First reinforcement triggers a Call-to-Action event cue; subsequent ones are silent
- Reinforcements attack-move through 4 waypoints to the battlefield

**Outro Staging:**
- Cheering soldiers: 7 spearmen + 10 archers + 5 horsemen across 8 markers
- Duke William + Earl Harold (English hero) spawned for narrative scene
- Harold's gift escorts (3 groups × 1 spearman), slow-marched then warped for final shot
- Corpse field: 10 markers × 3 corpse squads (`unit_spearman_2_eng_infinite_corpse`)
- Dinan buildings set on fire with random 25–60% health

### AI

No `AI_Enable` or encounter plan usage. All enemy behavior is scripted:
- **Patrols**: Two `RovingArmy_Init` modules with cycling/reversing waypoint patterns
- **Raids**: Scripted `Cmd_Move` + `Cmd_AttackMove` waypoint chains toward player TC
- **Defenders**: Static until player approaches keep, then `Cmd_AttackMove(sg_enemies, mkr_dinan_keep)` rallies all defenders
- **Garrison**: Villagers auto-garrison via `Util_FallBackToGarrisonBuilding`
- **Keep**: `Entity_SetInvulnerableMinCap(0.01, 0)` prevents instant destruction; completion at < 5% health

### Timers & Rules

| Rule/Timer | Timing | Purpose |
|------------|--------|---------|
| Rule_AddInterval(Mission_Start_WaitForSpeechToFinish, 0.5) | 0.5s interval | Poll until intro NIS finishes, then start first objective |
| Rule_Add(SetMilitaryPreset_Monitor) | per-frame | Check if villager priority weights are set |
| Rule_Add(March_Monitor) | per-frame | Check army proximity to Chateau de Dinan marker |
| Rule_Add(HeroAbility_StartMonitor) | per-frame | Start hero ability objective near outpost (radius 50) |
| Rule_Add(SelectAll_Monitor) | per-frame | Trigger intel when whole army selected |
| Rule_Add(HorsemenRaid_Monitor) | per-frame | Check if all raid horsemen killed |
| Rule_Add(ArchersRaid_Monitor) | per-frame | Check if all raid archers killed |
| Rule_Add(Destroy_Monitor) | per-frame | Check keep health for mission completion |
| Rule_AddInterval(KeepAttacked, 5) | 5s interval | Rally defenders when player enters keep radius (20) |
| Rule_AddInterval(Reinforcement_Monitor, 5) | 5s interval | Check player unit counts, spawn reinforcements if low |
| Rule_AddSGroupEvent(HeroAbility_Monitor) | event | Complete hero objective on GE_AbilityExecuted |
| Rule_AddEGroupEvent(OnRallyPoint) | event | Complete rally objective on CMD_RallyPoint |
| Rule_AddGlobalEvent(BuildHousesStart_Monitor) | event | Track GE_ConstructionStart for house placement |
| UI_SetModalConstructionPhaseCallback | callback | Track building placement for training hint advancement |
| ShowMoreVillagers timer | 10s elapsed | Dismiss villager reminder after 10 seconds |

### Resource Grants

Resources are granted at objective pre-start to ensure the player can always progress:
- Build 2 Houses: +100 wood
- Build Barracks: +150 wood
- Build Stables: +150 wood
- Build Archery Range: +150 wood
- Unit production: `GivePlayerRequired` calculates and grants exact cost for desired unit count

### Restrictions

Extensive lockdowns via `ITEM_REMOVED` to guide the tutorial:
- **Age**: Locked to Feudal (player1), Dark (player2)
- **Buildings removed**: Naval, outpost, palisade, TC, market, towers, walls, wall gates, age-up landmarks
- **Units removed**: Scout, man-at-arms, knight, crossbowman, handcannoneer, siege tower, ram
- **Upgrades removed**: Most economy/military upgrades beyond what the tutorial teaches
- **Abilities removed**: Unit death, building scuttle, auto-train villager
- **Progressively unlocked**: Barracks → Spearman → Stables → Horseman → Archery Range → Archer → Hardened upgrade → Blacksmith

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| sal_chp2_dinan.scar | MissionOMatic/MissionOMatic.scar, obj_expand.scar, obj_upgrade.scar, obj_capture.scar, training_sal_chp2_dinan.scar |
| obj_capture.scar | sal_chp2_dinan.scar, sal_chp2_dinan.events, training_sal_chp2_dinan.scar |
| training_sal_chp2_dinan.scar | training.scar, cardinal.scar, sal_chp2_dinan.events |

### Objective Chain

```
OBJ_VillagerPriorities (SOBJ_SetMilitaryPreset)
  → OBJ_Spearmen (SOBJ_Build2Houses → SOBJ_BuildBarracks → SOBJ_SetRally → SOBJ_Make10Spearmen)
    → OBJ_Cavalry (SOBJ_BuildStables → SOBJ_HorsemenRaid → SOBJ_Make10Horsemen)
      → OBJ_Archers (SOBJ_BuildArchery → SOBJ_ArchersRaid → SOBJ_Make10Archers)
        → OBJ_UpgradeUnits (SOBJ_Hardened → SOBJ_BuildBlacksmith → SOBJ_Research)
          → OBJ_Capture (SOBJ_March → SOBJ_Destroy) → Mission_Complete()
```

Optional: `OBJ_HeroAbility` — triggered by proximity during capture phase, independent of main chain.

### Shared Globals

- `player1` (Mathilde), `player2` (Brittany/enemy), `player3` (Neutral): Player handles used across all files
- `sg_william`: Guillaume hero SGroup, referenced in obj_capture and training for hero ability
- `sg_army`: Combined army SGroup built in March_Start, used for march monitoring and selection checks
- `sg_enemies`, `sg_outpost_enemies`: Enemy defender groups spawned in obj_capture, rallied on keep attack
- `sg_spearmen`, `sg_horsemen`: Unit-type SGroups built during raids, reused in training and capture
- `sg_raid_horsemen`, `sg_raid_archers`: Raid enemy groups spawned in obj_expand, monitored for kill completion
- `sg_startVillagers`, `sg_goldVillagers`: Villager groups referenced in training goals
- `eg_barracks`, `eg_stables`, `eg_archeryranges`, `eg_blacksmith`: Building EGroups shared between objective and training files
- `eg_player_tc`, `eg_player_landmark`, `eg_player_start_buildings`: Pre-placed map EGroups
- `eg_enemy_keep`, `eg_dinan_buildings`, `eg_enemy_tc`: Enemy structure groups for objectives and outro
- `num_*` variables: All enemy/patrol/raid unit counts set in Mission_SetupVariables, consumed by obj_expand and obj_capture
- `training_*` flags: `training_placing_houses`, `training_placing_barracks`, `training_placing_stables`, `training_placing_archery`, `training_units_queued`, `training_spearmen_attacked`, `training_ranges_selected`, `training_showMoreVillagersTimer` — state flags shared between objective and training files
- `EVENTS.*`: Intel event constants (CaptureStart, MarchStart, DestroyStart, BuildBarracksStart, BuildStablesStart, BuildArcheryStart, HardenedStart, BuildBlacksmithStart, etc.)
- `starting_houses_count`: Captured in PreStart, used by HandleBuildHousesObjective to calculate new houses built

### Campaign-Specific Blueprints

- `SBP.CAMPAIGN.UNIT_DUKE_WILLIAM_CMP_SAL` — Duke William / Guillaume hero unit (outro)
- `SBP.ENGLISH.UNIT_EARL_HAROLD_CMP_ENG` — Earl Harold hero unit (outro)
- `SBP.FRENCH.UNIT_SPEARMAN_1_FRE` — Spearman (progressively unlocked)
- `SBP.FRENCH.UNIT_HORSEMAN_2_FRE` — Horseman (progressively unlocked)
- `SBP.FRENCH.UNIT_ARCHER_2_FRE` — Archer (progressively unlocked)
- `UPG.COMMON.UPGRADE_UNIT_SPEARMAN_2` — Hardened spearman upgrade (unlocked in upgrade phase)
- `EBP.FRENCH.BUILDING_UNIT_INFANTRY_CONTROL_FRE` — Barracks
- `EBP.FRENCH.BUILDING_UNIT_CAVALRY_CONTROL_FRE` — Stables
- `EBP.FRENCH.BUILDING_UNIT_RANGED_CONTROL_FRE` — Archery Range
- `EBP.FRENCH.BUILDING_TECH_UNIT_INFANTRY_CONTROL_FRE` — Blacksmith
- `EBP.FRENCH.BUILDING_HOUSE_CONTROL_FRE` — House
