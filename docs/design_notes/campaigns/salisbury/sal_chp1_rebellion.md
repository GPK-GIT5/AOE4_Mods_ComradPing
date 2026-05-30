# Salisbury Chapter 1: Rebellion

## OVERVIEW

Salisbury Chapter 1: Rebellion is a tutorial mission that teaches players fundamental camera and unit controls. The mission progresses through two sequential primary objectives: first, an investigation phase where the player learns to pan, rotate, zoom, and reset the camera by navigating to landmarks (lumber camp, large rocks); then a unit-control phase where the player selects Duke Guillaume (William), moves him to a marker, and follows a trail of waypoints through fog of war to reach allied spearmen. There is no combat, AI opposition, or difficulty scaling — the mission relies entirely on the Training goal-sequence system for step-by-step input prompts. An intro NIS parade spawns Guillaume along a spline path before handing control to the player.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| sal_chp1_rebellion.scar | core | Mission setup: players, variables, restrictions, recipe, intro NIS support |
| obj_investigate.scar | objectives | Camera-tutorial objectives: pan to lumber, pan to rocks, rotate, zoom, reset |
| obj_spearmen.scar | objectives | Unit-control objectives: select Guillaume, move him, follow markers to spearmen |
| training_sal_chp1_rebellion.scar | training | Training goal sequences for every tutorial step with input prompts |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|----------------------|
| Mission_OnGameSetup | sal_chp1_rebellion | Configure player1/player3, set player names, marker aura size |
| Mission_OnInit | sal_chp1_rebellion | Force-enable training, set ally relationships, disable shared LOS |
| Mission_SetupVariables | sal_chp1_rebellion | Init objectives, create sg_william, store camera start zoom |
| Mission_SetRestrictions | sal_chp1_rebellion | Remove hold-position, leader ability, formations, death abilities |
| Mission_Preset | sal_chp1_rebellion | Reveal start area, set invulnerable buildings, lock explore music |
| Mission_Start | sal_chp1_rebellion | Wait for intro speech, then start investigation objective |
| Mission_Start_WaitForSpeechToFinish | sal_chp1_rebellion | Poll until intro event ends, launch OBJ_InvestigateSurroundings |
| GetRecipe | sal_chp1_rebellion | Define intro NIS and title card for MissionOMatic |
| WilliamIntroMove | sal_chp1_rebellion | Spawn Guillaume along 6-marker parade spline at 0.6× speed |
| Intro_WilliamResetSpeed | sal_chp1_rebellion | Reset Guillaume speed to 1.66× after intro |
| Investigate_InitObjectives | obj_investigate | Register OBJ_InvestigateSurroundings and 5 camera sub-objectives |
| MoveCameraToLumber_Start | obj_investigate | Activate lumber-pan training, start proximity monitor |
| MoveCameraToLumber_Monitor | obj_investigate | Complete when camera pivot within 5m of lumber camp |
| MoveCameraToRocks_Start | obj_investigate | Activate rock-pan training, start proximity monitor |
| MoveCameraToRocks_Monitor | obj_investigate | Complete when camera pivot within 7m of large rocks |
| IsOverRocks | obj_investigate | Check camera distance to rocks marker < 7 |
| RotateCamera_Start | obj_investigate | Activate rotate training, start orbit monitor |
| RotateCamera_Monitor | obj_investigate | Complete when over rocks and orbit outside 130°–285° |
| HasRotatedCamera | obj_investigate | Check camera orbit angle outside default range |
| ZoomCamera_Start | obj_investigate | Activate zoom training, start zoom monitor |
| ZoomCamera_Monitor | obj_investigate | Complete when over rocks, rotated, and zoom > 0.8 |
| HasZoomedCamera | obj_investigate | Check camera zoom distance > 0.8 |
| ResetCamera_Start | obj_investigate | Activate reset training, start zoom-reset monitor |
| ResetCamera_Monitor | obj_investigate | Complete when camera zoom < 0.2 |
| Spearmen_InitObjectives | obj_spearmen | Register OBJ_Spearmen and 3 unit-control sub-objectives |
| SelectWilliam_Start | obj_spearmen | Enable Guillaume selectable, start selection monitor |
| SelectWilliam_Monitor | obj_spearmen | Complete when player selects sg_william |
| MoveWilliam_UI | obj_spearmen | Add ground reticule and UI marker at move destination |
| MoveWilliam_Start | obj_spearmen | Activate move training, start proximity monitor |
| MoveWilliam_Monitor | obj_spearmen | Complete when Guillaume near move marker or first gate |
| FollowMarkers_Start | obj_spearmen | Add waypoint UI; skip first marker if already there |
| FollowMarkersA_Monitor | obj_spearmen | Advance UI from marker A to marker B on arrival |
| FollowMarkersB_Monitor | obj_spearmen | Advance UI from marker B to marker C on arrival |
| FollowMarkersC_Monitor | obj_spearmen | Transfer camp/spearmen to player1, complete objective |
| Goals_PanCameraLumber | training | Goal sequence: pan camera to lumber camp |
| Goals_PanCameraRock | training | Goal sequence: pan camera to large rocks |
| Goals_RotateCamera | training | Goal sequence: rotate camera with RS left/right |
| Goals_ZoomCamera | training | Goal sequence: zoom in/out with RS up/down |
| Goals_ResetCamera | training | Goal sequence: press RS to reset camera |
| Goals_SelectWilliam | training | Goal sequence: pan to Guillaume, press A to select |
| Goals_MoveWilliam | training | Two-step goal: select Guillaume then move to marker |
| Goals_FOW | training | Goal sequence: explain fog-of-war mechanic |
| SelectWilliam_CompletePredicate2 | training | Complete when sg_william is selected (move sequence) |
| MoveWilliam_IgnorePredicate | training | Ignore hint while Guillaume is moving |
| FOW_IgnorePredicate | training | Remove FOW hint when Guillaume reaches marker A |

## KEY SYSTEMS

### Objectives

| Constant | Purpose |
|----------|---------|
| OBJ_InvestigateSurroundings | Primary: "Investigate the area" — umbrella for 5 camera sub-objectives |
| SOBJ_MoveCameraToLumber | Sub: Move camera pivot over the lumber camp |
| SOBJ_MoveCameraToRocks | Sub: Move camera pivot over the large rocks |
| SOBJ_RotateCamera | Sub: Rotate camera orbit away from default angle while over rocks |
| SOBJ_ZoomCamera | Sub: Zoom camera in (zoom > 0.8) while over rocks and rotated |
| SOBJ_ResetCamera | Sub: Reset camera zoom back to default (zoom < 0.2) |
| OBJ_Spearmen | Primary: "Find Your Spearmen" — umbrella for 3 unit-control sub-objectives |
| SOBJ_SelectWilliam | Sub: Select Guillaume |
| SOBJ_MoveWilliam | Sub: Move Guillaume to the indicated marker |
| SOBJ_FollowMarkers | Sub: Follow 3 waypoints (A → B → C) to reach spearmen camp |

### Difficulty

No difficulty scaling (`Util_DifVar` not used). This is a fixed tutorial with no combat.

### Spawns

**Guillaume (William):**
- Spawned via `Util_UnitParade` along 6 parade markers during intro NIS using `UNIT_DUKE_WILLIAM_CMP_SAL` blueprint
- Speed reduced to 0.6× during parade, reset to 1.66× after intro

**Spearmen:**
- Pre-placed as `sg_spearmen` owned by player3; transferred to player1 when Guillaume reaches marker C
- Spearmen enable cheering on transfer; made non-selectable to prevent accidental orders

**Camp/Buildings:**
- `eg_lumberCamp` and `eg_campTents` set invulnerable and non-selectable during preset
- `eg_campTents` ownership transferred to player1 at marker C alongside spearmen

No wave spawns, reinforcement systems, or enemy units.

### AI

No AI systems. Player3 is used as a holding player for entities transferred to player1 during gameplay:
- Allied relationship set between player1 and player3
- Shared line-of-sight explicitly disabled between them
- No `AI_Enable` calls, no encounters, no patrol logic

### Timers

| Timer | Type | Delay/Interval | Purpose |
|-------|------|----------------|---------|
| Mission_Start_WaitForSpeechToFinish | Interval | 0.5s | Poll until intro NIS finishes, then start first objective |
| MoveCameraToLumber_Monitor | Rule_Add | per-frame | Check camera proximity to lumber camp marker |
| MoveCameraToRocks_Monitor | Rule_Add | per-frame | Check camera proximity to large rocks marker |
| RotateCamera_Monitor | Rule_Add | per-frame | Check camera orbit angle and position |
| ZoomCamera_Monitor | Rule_Add | per-frame | Check camera zoom level, position, and rotation |
| ResetCamera_Monitor | Rule_Add | per-frame | Check camera zoom reset to default |
| SelectWilliam_Monitor | Rule_Add | per-frame | Check if player has selected Guillaume |
| MoveWilliam_Monitor | Rule_Add | per-frame | Check if Guillaume reached move marker or first gate |
| FollowMarkersA/B/C_Monitor | Rule_Add | per-frame | Check waypoint proximity for each follow marker |

### Interaction Stages

- `World_SetInteractionStage(0)` — Set during preset; limits available UI/interactions
- `World_SetInteractionStage(1)` — Set when Guillaume reaches the move marker; unlocks next interaction tier

### Training System

All training goals use the `GenericTrainingDataTemplate` with localized controller-specific messages (LS for pan, RS for rotate/zoom, A for select). Each goal sequence:
- Triggers immediately (`_Trigger` returns `true`)
- Never self-completes (`_CompletePredicate` returns `false`)
- Is removed via `_IgnorePredicate` when the corresponding sub-objective completes
- The Move William sequence is a two-step chain: select Guillaume → move to marker, with a mid-chain predicate (`SelectWilliam_CompletePredicate2`) that gates on `Misc_IsSGroupSelected`

### Music

- `Music_LockIntensity(MUSIC_EXPLORE)` — Locked to exploration music for the entire mission
- `Sound_SetForceMusic` toggled based on `Music_UnlockIntensity` availability
- `sfx_campaign_scripted_ui_objective_counter_update` stinger played on each sub-objective completion

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Mission framework (Cardinal scripts)
- `cardinal.scar` — Core SCAR utilities (imported by obj_spearmen, training)
- `training.scar` — Base training system (Training_Goal, Training_GoalSequence, etc.)
- `training_sal_chp1_rebellion.scar` — Imported by both objective files and core
- `obj_investigate.scar` — Imported by core
- `obj_spearmen.scar` — Imported by core and obj_investigate

### Shared Globals
- `player1`, `player3` — Player handles; player1 is the human player, player3 holds transferable entities
- `sg_william` — Guillaume's squad group, referenced by all 4 files
- `sg_spearmen` — Allied spearmen transferred at mission end
- `eg_lumberCamp`, `eg_campTents` — Entity groups for buildings
- `marker_aura_size` — Ground reticule radius (5), set in core, used in obj_spearmen
- `camera_start_zoom` — Stored initial zoom level
- `intro_skipped` — Tracks whether intro NIS was skipped
- `OBJ_InvestigateSurroundings`, `SOBJ_*` — Objective tables shared between objective and training files
- `OBJ_Spearmen`, `SOBJ_SelectWilliam`, `SOBJ_MoveWilliam`, `SOBJ_FollowMarkers` — Unit-control objective tables
- `EVENTS.*` — Intel/NIS event table (Rebellion_Intro, RotatingStart, ZoomingStart, ResetStart, MoveStart, FollowStart, MissionEnd)
- `first_marker_ui`, `first_marker_aura`, `second_marker_ui`, `second_marker_aura` — UI element handles for dynamic waypoint swapping

### Inter-File Function Calls
- `sal_chp1_rebellion` → `Investigate_InitObjectives()`, `Spearmen_InitObjectives()` (from Mission_SetupVariables)
- `obj_investigate` → `Objective_Start(OBJ_Spearmen)` (after camera tutorial completes, via SOBJ_ResetCamera.OnComplete)
- `obj_investigate` → `Goals_PanCameraLumber()`, `Goals_PanCameraRock()`, `Goals_RotateCamera()`, `Goals_ZoomCamera()`, `Goals_ResetCamera()` (training activations)
- `obj_spearmen` → `Goals_SelectWilliam()`, `Goals_MoveWilliam()`, `Goals_FOW()` (training activations)
- `obj_spearmen` → `Mission_Complete()` (via OBJ_Spearmen.OnComplete after MissionEnd intel)
- Training predicates reference objective states: `Objective_IsComplete(SOBJ_*)` for ignore predicates
