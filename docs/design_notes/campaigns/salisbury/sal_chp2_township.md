# Salisbury Chapter 2: Township

## OVERVIEW

Salisbury Chapter 2: Township is a tutorial mission in the Salisbury (Norman) campaign that teaches age advancement and technology research. The player (player1, French civ) must gather food and gold, place and construct a Dark Age Landmark to advance to Age II, produce additional villagers to speed construction, and then research the Horticulture upgrade at a Mill. The mission uses MissionOMatic for intro NIS, a Training system for step-by-step controller prompts guiding each action, and extensive UI/building/unit restrictions to keep the player focused on the taught mechanics. Upon researching Horticulture, a closing intel event plays and the mission completes.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| sal_chp2_township.scar | core | Mission setup: players, restrictions, variables, resource grants, recipe, production tracker |
| obj_landmark.scar | objectives | Landmark-phase objectives: gather food/gold, place landmark, make villagers, wait for completion |
| obj_research.scar | objectives | Research-phase objectives: research Horticulture at a Mill (Broad Axe scrapped) |
| training_sal_chp2_township.scar | training | All Training goal sequences: landmark placement, faster construction, Mill research, lumber research |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_OnGameSetup | sal_chp2_township | Set player1 and player2 handles |
| Mission_OnInit | sal_chp2_township | Force training enabled, enable tutorialized HUD widgets |
| Mission_SetupVariables | sal_chp2_township | Init objectives, create landmark EGroup, grant starting resources |
| Mission_SetDifficulty | sal_chp2_township | Empty — fixed-difficulty tutorial mission |
| Mission_SetRestrictions | sal_chp2_township | Lock buildings/units/upgrades/abilities for tutorial scope |
| Mission_Preset | sal_chp2_township | Assign villagers to wood/gold/farms, lock music intensity |
| Mission_Start | sal_chp2_township | Wait for intro speech, then start OBJ_BuildLandmark |
| Mission_Start_WaitForSpeechToFinish | sal_chp2_township | Poll until intro NIS finishes, launch first objective |
| ProduceUnitsObjectiveTracker | sal_chp2_township | Snapshot current unit count, start production monitor |
| ProduceUnits_Monitor | sal_chp2_township | Poll unit count, increment counter, complete at target |
| GetRecipe | sal_chp2_township | Define intro NIS and title card for MissionOMatic |
| BuildLandmark_InitObjectives | obj_landmark | Register all landmark-phase objectives and sub-objectives |
| BuildLandmark_Start | obj_landmark | Check resources; skip gather or start gather objectives |
| StartGatherObjectives | obj_landmark | Start food and gold gather objectives, add monitor |
| HasResources_Monitor | obj_landmark | Complete gather phase when both resources met |
| GatherFood_UI | obj_landmark | Update food progress bar (current/400) |
| GatherFood_Start | obj_landmark | Add food gathering monitor rule |
| GatherFood_Monitor | obj_landmark | Complete when player food ≥ 400 |
| GatherGold_UI | obj_landmark | Update gold progress bar (current/200) |
| GatherGold_Start | obj_landmark | Add gold gathering monitor rule |
| GatherGold_Monitor | obj_landmark | Complete when player gold ≥ 200 |
| PlaceLandmark_Start | obj_landmark | Wait for speech, show landmark hint, add monitor |
| LandmarkHint_WaitForSpeechToFinish | obj_landmark | Poll until speech done, then call Goals_BuildLandmark |
| PlaceLandmark_Monitor | obj_landmark | Complete when wonder_dark_age entity placed |
| Make3Villagers_UI | obj_landmark | Set villager counter display (0/3) |
| Make3Villagers_Start | obj_landmark | Launch training, grant 150 food, track 3 villagers |
| WaitFinish_Start | obj_landmark | Add landmark completion monitor |
| WaitFinish_Monitor | obj_landmark | Complete when landmark no longer under construction |
| ResearchTech_InitObjectives | obj_research | Register research-phase objective and Horticulture sub |
| Horticulture_Start | obj_research | Unlock Horticulture upgrade, show training, add monitor |
| Horticulture_Monitor | obj_research | Complete when player has Horticulture upgrade |
| BroadAxe_Start | obj_research | (Scrapped) Unlock Broad Axe, add monitor |
| BroadAxe_Monitor | obj_research | (Scrapped) Complete when Broad Axe researched |
| Goals_BuildLandmark | training | Goal sequence: select villager, open landmark menu |
| Goals_FasterLandmark | training | Goal sequence: construction tip, make villagers, aging up |
| Goals_Research | training | Goal sequence: new tech info, select Mill, start Horticulture |
| Goals_ResearchLumber | training | (Scrapped) Goal sequence: select lumber camp, research Broad Axe |
| IdleVillager_CompletePredicate | training | Complete when any villager group selected |
| LandmarkSelected_CompletePredicate | training | Always false — dismissed by ignore predicate |
| BuildLandmark_IgnorePredicate | training | Remove sequence when SOBJ_PlaceLandmark complete |
| StartedConstruction_CompletePredicate | training | Complete after 5 seconds elapsed |
| MoreVillagers_CompletePredicate | training | Complete when SOBJ_Make3Villagers complete |
| AgingUp_CompletePredicate | training | Always false — dismissed by ignore predicate |
| FasterLandmark_IgnorePredicate | training | Remove sequence when SOBJ_WaitFinish complete |
| NewTech_CompletePredicate | training | Complete after 5 seconds elapsed |
| ResearchBonus_CompletePredicate | training | Complete after 5 seconds elapsed |
| SelectMill_CompletePredicate | training | Complete when eg_mill selected |
| StartResearch_CompletePredicate | training | Complete when Horticulture queued at Mill |
| Research_IgnorePredicate | training | Remove sequence when tech completed or objective done |
| SelectLumber_CompletePredicate | training | (Scrapped) Complete when lumber camp selected |
| StartLumberResearch_CompletePredicate | training | (Scrapped) Complete when Broad Axe queued |
| ResearchLumber_IgnorePredicate | training | (Scrapped) Remove when Broad Axe complete |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_BuildLandmark | Primary | "Build a Landmark & Advance to the Next Age" — main landmark phase |
| SOBJ_GatherFood | Sub | Gather 400 Food (progress bar) |
| SOBJ_GatherGold | Sub | Gather 200 Gold (progress bar) |
| SOBJ_PlaceLandmark | Sub | Place a Dark Age Landmark on the map |
| SOBJ_Make3Villagers | Sub | Make 3 Villagers to speed up construction (counter 0/3) |
| SOBJ_WaitFinish | Sub | Wait for the Landmark to finish construction |
| OBJ_ResearchTech | Primary | "Research new Technology" — final phase, completes mission |
| SOBJ_Horticulture | Sub | Research Horticulture at a Mill |
| SOBJ_BroadAxe | Sub (scrapped) | Research Broad Axe at Lumber Camp — commented out by design |

### Difficulty

No `Util_DifVar` calls — this is a fixed-difficulty tutorial mission. `Mission_SetDifficulty` is empty. All values are hardcoded.

### Spawns

**Player Setup (player1):**
- `sg_woodVillagers`, `sg_goldVillagers`, `sg_farmVillagers`: Pre-placed villager groups assigned to resources during `Mission_Preset`
- Starting resources: +200 Food, +100 Gold granted in `Mission_SetupVariables`
- +150 Food granted at `Make3Villagers_Start` for villager production
- Produced units: 3 villagers (player-built via Town Center)

**No Enemy Spawns:**
- `player2` exists but has no spawned units or combat role in this mission.

### AI

No `AI_Enable`, encounter plans, patrol logic, or enemy scripting. This is a purely economic tutorial with no combat.

### Timers & Rules

| Rule/Timer | Timing | Purpose |
|------------|--------|---------|
| Rule_AddInterval(Mission_Start_WaitForSpeechToFinish, 0.5) | 0.5s interval | Poll until intro NIS finishes, then start OBJ_BuildLandmark |
| Rule_AddOneShot(StartGatherObjectives) | one-shot | Start food and gold gather objectives if resources insufficient |
| Rule_Add(HasResources_Monitor) | per-frame | Check if both gather objectives complete, then start PlaceLandmark |
| Rule_Add(GatherFood_Monitor) | per-frame | Track food accumulation, update progress bar |
| Rule_Add(GatherGold_Monitor) | per-frame | Track gold accumulation, update progress bar |
| Rule_AddInterval(LandmarkHint_WaitForSpeechToFinish, 0.5) | 0.5s interval | Wait for speech to end before showing landmark build hint |
| Rule_Add(PlaceLandmark_Monitor) | per-frame | Detect when wonder_dark_age placed on map |
| Rule_AddOneShot(ProduceUnitsObjectiveTracker, 0) | one-shot | Snapshot villager count, begin production monitoring |
| Rule_Add(ProduceUnits_Monitor) | per-frame | Poll villager count delta, increment counter toward 3 |
| Rule_Add(WaitFinish_Monitor) | per-frame | Check landmark no longer under construction |
| Rule_Add(Horticulture_Monitor) | per-frame | Check if player has Horticulture upgrade |
| Timer (StartedConstruction goal) | 5s elapsed | Auto-advance construction training tip after 5 seconds |
| Timer (NewTech / ResearchBonus goals) | 5s elapsed | Auto-advance research info training tips after 5 seconds |

### Restrictions

Extensive lockdowns via `ITEM_REMOVED` to constrain the tutorial:
- **Buildings removed**: Age III/IV landmarks, Age II wonders, infantry/naval/outpost/palisade/palisade gate/ranged/blacksmith/market/TC/cavalry/tower/wall bastion/wall/wall gate
- **Units removed**: Scout
- **Upgrades removed**: Horticulture (initially; unlocked in research phase), Hunting Gear, Wheelbarrow, Forester, all wood/gold/stone harvest rate upgrades, villager health
- **Abilities removed**: Hold position, line/spread/wedge formations, unit death
- **Progressively unlocked**: Horticulture — unlocked via `Player_SetUpgradeAvailability` in `Horticulture_Start`

### Resource Grants

| Trigger | Resource | Amount | Purpose |
|---------|----------|--------|---------|
| Mission_SetupVariables | Food | 200 | Starting resources toward landmark cost |
| Mission_SetupVariables | Gold | 100 | Starting resources toward landmark cost |
| Make3Villagers_Start | Food | 150 | Fund 3 villager production |

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| sal_chp2_township.scar | MissionOMatic/MissionOMatic.scar, obj_landmark.scar, obj_research.scar, training_sal_chp2_township.scar |
| training_sal_chp2_township.scar | training.scar, cardinal.scar |

### Objective Chain

```
OBJ_BuildLandmark
  ├─ SOBJ_GatherFood (if food < 400)
  ├─ SOBJ_GatherGold (if gold < 200)
  ├─ SOBJ_PlaceLandmark (after resources met)
  │    → SOBJ_Make3Villagers (on PlaceLandmark complete)
  │         → SOBJ_WaitFinish (on Make3Villagers complete)
  └─ IsComplete: SOBJ_WaitFinish ALL
       → OBJ_ResearchTech
            └─ SOBJ_Horticulture (starts alongside parent)
                 → Mission_Complete() via MissionEnd intel
```

### Shared Globals

- `player1`, `player2`: Player handles used across all files
- `eg_landmark`: EGroup holding the placed Dark Age wonder, created in core, populated in obj_landmark, referenced in training
- `eg_player_tc`: Pre-placed Town Center EGroup, referenced in training goal targets
- `eg_mill`: Mill EGroup, referenced in training for research goal sequence
- `eg_lumber_camp`: Lumber camp EGroup, referenced in scrapped Broad Axe training sequence
- `sg_woodVillagers`, `sg_goldVillagers`, `sg_farmVillagers`: Villager groups assigned in core, referenced in training predicates
- `i_last_units`: Baseline unit count snapshot for production tracking, set in core
- `intro_skipped`: Flag set in core's `Mission_SetupVariables`
- `techCompleted`: Flag set in `StartResearch_CompletePredicate`, checked by `Research_IgnorePredicate`
- `lumberTechCompleted`: Flag set in scrapped `StartLumberResearch_CompletePredicate`
- `EVENTS.Township_Intro`: Intro NIS event for MissionOMatic recipe
- `EVENTS.GatherFoodStart`, `EVENTS.GatherGoldStart`, `EVENTS.PlaceLandmark`, `EVENTS.HorticultureStart`, `EVENTS.MissionEnd`: Intel event constants (some commented out)

### Campaign-Specific Blueprints

- `UPG.COMMON.UPGRADE_ECON_RESOURCE_FOOD_HARVEST_RATE_2` — Horticulture (food harvest rate upgrade, mission objective)
- `UPG.COMMON.UPGRADE_ECON_RESOURCE_WOOD_HARVEST_RATE_2` — Broad Axe (wood harvest rate, scrapped objective)
- `EBP.FRENCH.BUILDING_UNIT_INFANTRY_CONTROL_FRE` — Barracks (removed)
- `EBP.FRENCH.BUILDING_UNIT_RANGED_CONTROL_FRE` — Archery Range (removed)
- `EBP.FRENCH.BUILDING_UNIT_NAVAL_FRE` — Dock (removed)
- `EBP.FRENCH.BUILDING_UNIT_CAVALRY_CONTROL_FRE` — Stables (removed)
- `EBP.FRENCH.BUILDING_TECH_UNIT_INFANTRY_CONTROL_FRE` — Blacksmith (removed)
- `EBP.FRENCH.BUILDING_TECH_UNIT_RANGED_CONTROL_FRE` — University (removed)
- `EBP.FRENCH.BUILDING_ECON_MARKET_CONTROL_FRE` — Market (removed)
- `EBP.FRENCH.BUILDING_DEFENSE_OUTPOST_FRE` — Outpost (removed)
- `EBP.FRENCH.BUILDING_DEFENSE_PALISADE_FRE` — Palisade Wall (removed)
- `EBP.FRENCH.BUILDING_TOWN_CENTER_FRE` — Town Center (removed)
- `SBP.FRENCH.UNIT_SCOUT_1_FRE` — Scout (removed)
