# Salisbury Chapter 1: Valesdun

## OVERVIEW

Salisbury Chapter 1: Valesdun is a tutorial-combat mission in the Salisbury (Norman) campaign that teaches unit selection, movement, control groups, attack-move, and counter-unit tactics before culminating in a pitched battle. The player controls Guillaume de Normandie (Duke William) through seven sequential primary objectives: organising spearmen, mustering forces through waypoints, commanding horsemen against archers, locating and commanding archers for an ambush, selecting the full army, marching to King Henri, and finally defeating Gui de Bourgogne's rebel army. A four-player setup uses player4 as a greyed-out holder for temporarily locked units, while player3 (Henri) provides allied reinforcements for the final battle. The Training goal-sequence system drives step-by-step input prompts throughout, and the mission uses Mission-o-Matic for intro/outro NIS and mission completion.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| sal_chp1_valesdun.scar | core | Mission setup: players, relationships, variables, restrictions, spawn helpers, recipe, outro staging |
| obj_organise.scar | objectives | First objectives: select spearmen, move them to marker, create a control group |
| obj_muster.scar | objectives | Second objectives: marquee-select all, search waypoints, destroy palisade, defeat horseman, follow markers |
| obj_horsemen.scar | objectives | Third objective: command horsemen to defeat enemy archers |
| obj_locate.scar | objectives | Fourth objectives: select expanded army, follow markers to find allied archers, spawn enemy spearmen |
| obj_archers.scar | objectives | Fifth objectives: position archers for ambush, defeat enemy spearmen from high ground |
| obj_prepare.scar | objectives | Sixth objectives: select entire army via D-pad, follow waypoints to King Henri, spawn allied/enemy armies |
| obj_defeat.scar | objectives | Final objectives: reach battlefield, break Guy's cavalry/archers/spearmen, use hero ability |
| training_sal_chp1_valesdun.scar | training | All Training goal sequences: selection, movement, control groups, marquee, attack-move, terrain advantage, D-pad, hero ability |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_OnGameSetup | sal_chp1_valesdun | Set player1–4 names, marker_aura_size |
| Mission_OnInit | sal_chp1_valesdun | Force training, set relationships, configure player4 neutral/grey |
| Mission_SetupVariables | sal_chp1_valesdun | Init all 7 objective sets, define encounter unit counts |
| Mission_SetRestrictions | sal_chp1_valesdun | Remove abilities, formations, siege; set William invulnerable min cap |
| Mission_Preset | sal_chp1_valesdun | Set buildings invulnerable/unselectable, configure music intensity map |
| Mission_Start | sal_chp1_valesdun | Wait for intro NIS, reveal FOW, start OBJ_OrganiseSpearmen |
| GetRecipe | sal_chp1_valesdun | Define intro/outro NIS and title card for MissionOMatic |
| SpawnGuyArmy | sal_chp1_valesdun | Deploy Guy + spearmen/archers/cavalry at battlefield markers |
| SpawnOutro | sal_chp1_valesdun | Spawn outro scene enemies, William, archers, corpse field |
| InitOutro | sal_chp1_valesdun | Order enemies to flee, archers to chase and hold |
| OutroPart2 | sal_chp1_valesdun | Spawn Henri, allied units, horsemen; enable cheering |
| RecordControlGroups | sal_chp1_valesdun | Save current control group assignments to SGroups |
| RestoreControlGroups | sal_chp1_valesdun | Restore saved control groups; assign new group to first empty |
| SetSquadControlGroup | sal_chp1_valesdun | Assign all squads in SGroup to given control group index |
| OrganiseSpearmen_InitObjectives | obj_organise | Register OBJ_OrganiseSpearmen + 3 sub-objectives |
| SelectSpearmen_Start | obj_organise | Launch select-all-spearmen training, add monitor |
| SelectSpearmen_Monitor | obj_organise | Complete when all spearmen selected |
| MoveSpearmen_Start | obj_organise | Launch move-spearmen training, add proximity monitor |
| MoveSpearmen_Monitor | obj_organise | Complete when spearmen near move marker |
| CreateRegiment_Start | obj_organise | Show control group UI, launch training, add monitor |
| CreateRegiment_Monitor | obj_organise | Complete when all spearmen in a control group |
| MusterForces_InitObjectives | obj_muster | Register OBJ_MusterForces + 5 sub-objectives |
| SelectAll_Start | obj_muster | Launch marquee-select training |
| SelectAll_Monitor | obj_muster | Complete when spearmen + William both selected |
| Search_Start | obj_muster | Add waypoint UI, launch snap-to training |
| Search1_Monitor | obj_muster | Advance UI from first to second waypoint |
| Search2_Monitor | obj_muster | Complete search on reaching second waypoint |
| DestroyPalisade_PreStart | obj_muster | Make palisade attackable, add entity-killed listener |
| DestroyPalisade_Monitor | obj_muster | Complete when any wall segment destroyed |
| DefeatHorseman_PreStart | obj_muster | Enable quick commands, spawn lone enemy horseman |
| DefeatHorseman_Start | obj_muster | Reveal FOW, add attack-move and proximity monitors |
| DefeatHorseman_Monitor | obj_muster | Complete when horseman killed after player attack-moved |
| SpawnAnotherLonelyUnit | obj_muster | Respawn enemy horseman if killed without attack-move |
| FollowMarkers_Start | obj_muster | Spawn enemy archers + allied horsemen, add waypoint UI |
| FollowMarkers1_Monitor | obj_muster | On proximity: reveal FOW, trigger intel, transfer horsemen |
| MoveToHorsemenAfterAudio | obj_muster | Give horsemen to player, grey out other units |
| CommandHorsemen_InitObjectives | obj_horsemen | Register OBJ_CommandHorsemen + SOBJ_DefeatArchers |
| DefeatArchers_PreStart | obj_horsemen | Set counter to enemy archer count, add kill tracker |
| DefeatArchers_Start | obj_horsemen | Launch cavalry-vs-archers training, add proximity monitor |
| ArcherDefeatedTracker | obj_horsemen | Track archer kills; respawn player horsemen if depleted |
| DefeatArchers_Complete | obj_horsemen | Return units to player, restore control groups, start OBJ_LocateArchers |
| LocateArchers_InitObjectives | obj_locate | Register OBJ_LocateArchers + 2 sub-objectives |
| SelectExpandedArmy_Start | obj_locate | Launch selection-exploration training |
| MoveAmbush_Start | obj_locate | Spawn allied archers (player4), add proximity monitor |
| MoveAmbush_Monitor | obj_locate | Transfer archers to player, spawn enemy spearmen (2× damage) |
| CommandArchers_InitObjectives | obj_archers | Register OBJ_CommandArchers + 2 sub-objectives |
| PositionAmbush_Start | obj_archers | Move William/spearmen/horsemen aside, add proximity monitor |
| PositionAmbush_Monitor | obj_archers | Complete when all archers near ambush marker |
| AmbushSpearmen_Start | obj_archers | Launch terrain-advantage training, send enemy spearmen |
| SpearmanDefeatedTracker | obj_archers | Track spearman kills; respawn archers if player loses them |
| CommandArchers_PreComplete | obj_archers | Return units to player, un-reveal FOW, restore control groups |
| PrepareForBattle_InitObjectives | obj_prepare | Register OBJ_PrepareForBattle + 2 sub-objectives |
| SelectEntireArmy_Start | obj_prepare | Show quick-find UI, launch D-pad training |
| SelectEntireArmy_Monitor | obj_prepare | Complete when all player units selected |
| FollowToHenry_UI | obj_prepare | Spawn King Henri + full allied army + player reinforcements |
| FollowToHenry_Start | obj_prepare | Add waypoint UI with up to 3 waypoints |
| FollowToHenry_Monitor | obj_prepare | Track army proximity to Henri; complete when all arrive |
| PrepareForBattle_PreComplete | obj_prepare | Give reinforcements to player, share LOS with Henri, spawn Guy's army |
| DefeatGuy_InitObjectives | obj_defeat | Register OBJ_DefeatGuy + 4 sub-objectives |
| DefeatGuy_Start | obj_defeat | Init kill counters, add global kill tracker, launch battle help |
| HenryMove_Monitor | obj_defeat | Trigger Henri's army march when player reaches bridge |
| DefeatGuyGetReady_Start | obj_defeat | Add proximity monitor for reaching battlefield position |
| ReachedBattle_Monitor | obj_defeat | Complete get-ready on reaching battlefield marker |
| StartBattle_Monitor | obj_defeat | Launch battle: order Henri's army to attack, start hero ability objective |
| EnemyDefeatedTracker | obj_defeat | Track kills per unit type; trigger retreat at 75% threshold |
| UnitHighlight_Monitor | obj_defeat | Show counter-unit hints when player selects specific troops |
| Reinforcement_Monitor | obj_defeat | Respawn player horsemen/spearmen/archers if any group emptied |
| HeroAbility_Start | obj_defeat | Unlock leader ability, launch hero-ability training |
| HeroAbility_Monitor | obj_defeat | Complete when player uses Guillaume's ability |
| Cheat_DefeatGuy | obj_defeat | Debug skip: spawn all armies, jump to final battle |
| Cheat_CommandHorsemen | obj_horsemen | Debug skip: spawn horsemen/archers, jump to horsemen objective |
| Goals_SelectAllSpearmen | training | Goal sequence: double-press A to select all spearmen |
| Goals_MoveSpearmen | training | Goal sequence: select spearmen, move to marker |
| Goals_CreateRegiment | training | Goal sequence: open control group menu, add units, close |
| Goals_UseMarquee | training | Goal sequence: hold LT to marquee over spearmen + Guillaume |
| Goals_SnapTo | training | Goal sequence: press LS to snap camera to selected units |
| Goals_AttackStructure | training | Goal sequence: select palisade, press A to attack |
| Goals_AttackMove | training | Goal sequence: press X for attack-move, explain counter-units |
| Goals_CavalryVSArchers | training | Goal sequence: select horsemen, attack-move into archers |
| Goals_ExploreSelection | training | Goal sequence: use LT+A/B to add/subtract from selection |
| Goals_TerrainAdvantage | training | Goal sequence: explain ranged height advantage |
| Goals_DPadUse | training | Goal sequence: D-pad left to select military units |
| Goals_DPadUseReminder | training | Reminder: hold D-pad left to select all — 2 min timeout |
| Goals_BattleHelp | training | Goal sequence: counter-unit reminder before final battle |
| Goals_HeroAbility | training | Goal sequence: D-pad right to select hero, Y to activate ability |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_OrganiseSpearmen | Primary | "Organise the Spearmen" — umbrella for selection/move/control group |
| SOBJ_SelectSpearmen | Sub | Select all spearmen (double-press A) |
| SOBJ_MoveSpearmen | Sub | March spearmen to a marker |
| SOBJ_CreateRegiment | Sub | Create a control group for spearmen |
| OBJ_MusterForces | Primary | "Command the Spearmen" — umbrella for search/destroy/attack-move/follow |
| SOBJ_SelectAll | Sub | Marquee-select Guillaume and all spearmen |
| SOBJ_Search | Sub | Follow 2 sequential waypoint markers |
| SOBJ_DestroyPalisade | Sub | Destroy an enemy palisade wall segment |
| SOBJ_DefeatHorseman | Sub | Defeat lone enemy horseman using attack-move |
| SOBJ_FollowMarkers | Sub | Follow markers to discover horsemen and enemy archers |
| OBJ_CommandHorsemen | Primary | "Command the Horsemen" — defeat enemy archers with cavalry |
| SOBJ_DefeatArchers | Sub | Kill all enemy archers with horsemen (kill counter) |
| OBJ_LocateArchers | Primary | "Locate the Archers" — find allied archers |
| SOBJ_SelectExpandedArmy | Sub | Select entire expanded army using add-to-selection |
| SOBJ_MoveAmbush | Sub | Follow marker to allied archer position |
| OBJ_CommandArchers | Primary | "Command the Archers" — ambush encounter |
| SOBJ_PositionAmbush | Sub | Move archers to ambush hill marker |
| SOBJ_AmbushSpearmen | Sub | Defeat all enemy spearmen from elevated position (kill counter) |
| OBJ_PrepareForBattle | Primary | "Prepare for Battle" — select army and march to Henri |
| SOBJ_SelectEntireArmy | Sub | Select entire army using D-pad |
| SOBJ_FollowToHenry | Sub | Follow 3 waypoints to King Henri; progress bar by unit count |
| OBJ_DefeatGuy | Primary | "Defeat Gui de Bourgogne" — final pitched battle |
| SOBJ_DefeatGuyGetReady | Sub | "Take Position" — reach battlefield marker |
| SOBJ_DefeatGuyCavalry | Sub | Break Guy's cavalry (progress bar, 75% kill threshold) |
| SOBJ_DefeatGuyArchers | Sub | Break Guy's archers (progress bar, 75% kill threshold) |
| SOBJ_DefeatGuySpearmen | Sub | Break Guy's spearmen (progress bar, 75% kill threshold) |
| SOBJ_HeroAbility | Optional | Use Guillaume's leader_attack_speed_activated ability |

### Difficulty

No `Util_DifVar` calls — this is a fixed-difficulty tutorial mission. All unit counts are hardcoded constants.

### Spawns

**Player Units (player1):**
- `sg_william`: Duke William (UNIT_DUKE_WILLIAM_CMP_SAL), invulnerable min cap 0.75
- `sg_starting_spearmen`: Pre-placed on map; count stored in `target_spearmen`
- `sg_horsemen`: 4 groups × `num_allied_horsemen_per_marker` (2) = 8 horsemen, spawned at cavalry markers
- `sg_archers`: 4 groups × `num_allied_archers_per_marker` (3) = 12 archers, spawned at archery markers

**Enemy Units (player2):**
- `sg_enemy_archers`: `num_archers_encounter` (8) archers at one marker
- `sg_enemy_spearmen`: 3 groups × `num_enemy_spearmen_per_marker` (2) = 6 spearmen; receive `Modify_ReceivedDamage(2)` (double damage taken)
- `sg_attackMove_scout`: Single horseman respawned if killed without attack-move
- `sg_guy`: Gui de Bourgogne hero (UNIT_GUYBURGUNDY_CMP_SAL)
- `sg_guy_spearmen`: 2 markers × `num_guy_spearmen_per_marker` (6) = 12 spearmen, SPREAD_FORMATION
- `sg_guy_archers`: 3 markers × `num_guy_archers_per_marker` (6) = 18 archers, SPREAD_FORMATION
- `sg_guy_cavalry`: 2 markers × `num_guy_cavalry_per_marker` (5) = 10 horsemen, SPREAD_FORMATION

**Allied Units (player3 — Henri):**
- `sg_henry`: King Henri (UNIT_KING_HENRY_CMP_SAL), invulnerable min cap 0.75
- `sg_henry_spearmen`: 2 markers × `num_henry_spearmen_per_marker` (7) = 14 spearmen
- `sg_henry_archers`: 3 markers × `num_henry_archers_per_marker` (4) = 12 archers
- `sg_henry_cavalry`: 3 markers × `num_henry_cavalry_per_marker` (3) = 9 horsemen

**Reinforcement Safety Nets:**
- During horseman encounter: respawn horsemen if count ≤ `num_allied_horsemen_per_marker`
- During ambush: respawn archers if count ≤ `num_allied_archers_per_marker`
- During final battle: respawn spearmen/horsemen/archers if any group reaches 0

**Outro staging** spawns individual squads of enemies (Modify_ReceivedDamage 20× for instant death), archers, spearmen, William, Henri, corpse field (15 × 2 infinite corpse squads), and horsemen for cinematic choreography.

### AI

No AI_Enable, encounter plans, or patrol logic. Enemy units use scripted `Cmd_AttackMove`, `Cmd_Move`, and `Cmd_Attack` commands. Henri's army is ordered to attack specific enemy groups when the player reaches the battlefield. Enemy units in the final battle retreat at 75% casualties using `Modify_UnitSpeed(1.2)` + `Cmd_Move` to retreat marker.

### Timers & Rules

| Rule/Timer | Timing | Purpose |
|------------|--------|---------|
| Rule_AddInterval(ArcherProx_Monitor, 1) | 1s interval | Check horsemen proximity to archers |
| Rule_AddInterval(DefeatHorseman_Monitor, 1) | 1s interval | Check if horseman killed after attack-move |
| Rule_AddOneShot(RemoveHintTimer, 3) | 3s one-shot | Remove counter-unit UI highlights |
| Rule_AddOneShot(MoveToHorsemenAfterAudio, 5.5) | 5.5s one-shot | Transfer horsemen to player after intel audio |
| Rule_AddOneShot(MoveUnitAttackMove, 1) | 1s one-shot | Move spawned horseman to hold position |
| Rule_AddInterval(Mission_Start_WaitForSpeechToFinish, 0.5) | 0.5s interval | Poll until intro NIS finishes |
| DPadUseReminder timeout | 120s (2 min) | Auto-dismiss D-pad reminder if player ignores it |

### World Interaction Stages

Stages are unlocked progressively as the player advances:
- Stage 0: Initial locked state
- Stages 1–9: Sequentially opened to expand available map areas and UI features

### Player4 Grey-Out System

Player4 is a neutral, grey-colored slot (colour index 9) used to temporarily hold player units during focused objectives. Units are transferred to player4 with `SGroup_SetSelectable(false)` and shared LOS is enabled so the player can still see them. Control groups are recorded before transfer and restored after.

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| sal_chp1_valesdun.scar | cardinal.scar, obj_organise.scar, obj_muster.scar, obj_horsemen.scar, obj_locate.scar, obj_archers.scar, obj_prepare.scar, obj_defeat.scar, training_sal_chp1_valesdun.scar, MissionOMatic/MissionOMatic.scar |
| obj_organise.scar | obj_muster.scar |
| obj_muster.scar | cardinal.scar, MissionOMatic/MissionOMatic.scar, obj_horsemen.scar, sal_chp1_valesdun.scar |
| obj_horsemen.scar | cardinal.scar, MissionOMatic/MissionOMatic.scar, obj_locate.scar |
| obj_locate.scar | cardinal.scar, MissionOMatic/MissionOMatic.scar, obj_archers.scar |
| obj_archers.scar | obj_prepare.scar, sal_chp1_valesdun.scar |
| obj_prepare.scar | cardinal.scar, MissionOMatic/MissionOMatic.scar, obj_defeat.scar |
| obj_defeat.scar | cardinal.scar, MissionOMatic/MissionOMatic.scar, obj_prepare.scar |
| training_sal_chp1_valesdun.scar | training.scar, cardinal.scar, sal_chp1_valesdun.scar |

### Objective Chain

```
OBJ_OrganiseSpearmen → OBJ_MusterForces → OBJ_CommandHorsemen → OBJ_LocateArchers → OBJ_CommandArchers → OBJ_PrepareForBattle → OBJ_DefeatGuy → Mission_Complete()
```

### Shared Globals

- `sg_william`, `sg_starting_spearmen`, `sg_horsemen`, `sg_archers`, `sg_player_units`: Core SGroups referenced across all objective files
- `sg_henry`, `sg_henry_spearmen/archers/cavalry`: Allied army groups shared between obj_prepare and obj_defeat
- `sg_guy`, `sg_guy_spearmen/archers/cavalry`: Enemy army groups spawned by sal_chp1_valesdun, used in obj_defeat
- `num_*_per_marker`, `target_*`: Encounter sizing variables set in Mission_SetupVariables, consumed by objective files
- `EVENTS.*`: Intel event constants (AmbushStart, AmbushEnd, SelectSpearmenStart, etc.) used across objective files for narrative beats
- `Training_*` functions: Called from objective files into training_sal_chp1_valesdun.scar for tutorial prompts
- `RecordControlGroups()` / `RestoreControlGroups()`: Called from obj_horsemen, obj_archers when temporarily transferring units to player4

### Campaign-Specific Blueprints

- `SBP.CAMPAIGN.UNIT_DUKE_WILLIAM_CMP_SAL` — Guillaume de Normandie hero unit
- `SBP.CAMPAIGN.UNIT_KING_HENRY_CMP_SAL` — King Henri hero unit
- `SBP.CAMPAIGN.UNIT_GUYBURGUNDY_CMP_SAL` — Gui de Bourgogne hero unit
- `BP_GetAbilityBlueprint("leader_attack_speed_activated")` — Guillaume's hero ability (attack speed boost)
- `EBP.FRENCH.BUILDING_DEFENSE_PALISADE_BASTION_FRE` — Filtered out of destroyable palisade group
