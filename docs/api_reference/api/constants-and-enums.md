# AoE4 Constants & Enums — Complete Reference

Last Updated: 2026-03-18

All typed constants extracted from the Lua runtime dump.
Categories marked *(scardocs)* were added from `Essence_Constants.api` (Game v15.4.8719.0) — names only, no numeric values.

---

## Resource Types (RT_)

| Constant | Value | Description |
|----------|-------|-------------|
| `RT_Begin` / `RT_Action` | 0 | Action points |
| `RT_Command` | 1 | Command resource |
| `RT_Food` | 2 | Food |
| `RT_Gold` | 3 | Gold |
| `RT_Militia_HRE` | 4 | HRE militia resource |
| `RT_Popcap` | 5 | Population capacity |
| `RT_Stone` | 6 | Stone |
| `RT_Wood` | 7 | Wood |
| `RT_Count` | 8 | Total resource types |

---

## Ages (AGE_)

| Constant | Value |
|----------|-------|
| `AGE_NONE` | 0 |
| `AGE_DARK` | 1 |
| `AGE_FEUDAL` | 2 |
| `AGE_CASTLE` | 3 |
| `AGE_IMPERIAL` | 4 |

---

## Stances (STANCE_)

| Constant | Type | Value |
|----------|------|-------|
| `STANCE_CeaseFire` | StanceType | 0 — No combat |
| `STANCE_StandGround` | StanceType | 1 — Defend only |
| `STANCE_Attack` | StanceType | 2 — Aggressive |

---

## Relationships (R_)

| Constant | Type | Value |
|----------|------|-------|
| `R_UNDEFINED` | Relationship | 0 |
| `R_ENEMY` | Relationship | 1 |
| `R_ALLY` | Relationship | 2 |
| `R_NEUTRAL` | Relationship | 3 |

---

## SCAR Types (ST_)

| Constant | Type | Value | Description |
|----------|------|-------|-------------|
| `ST_NIL` | ScarType | 0 | Nil/null |
| `ST_BOOLEAN` | ScarType | 1 | Boolean |
| `ST_NUMBER` | ScarType | 2 | Number |
| `ST_STRING` | ScarType | 4 | String |
| `ST_TABLE` | ScarType | 5 | Table |
| `ST_FUNCTION` | ScarType | 7 | Function |
| `ST_ENUM` | ScarType | 8 | Enum |
| `ST_SCARPOS` | ScarType | 9 | Position |
| `ST_EGROUP` | ScarType | 10 | Entity Group |
| `ST_ENTITY` | ScarType | 11 | Entity |
| `ST_CONSTENTITY` | ScarType | 12 | Const Entity |
| `ST_SGROUP` | ScarType | 13 | Squad Group |
| `ST_SQUAD` | ScarType | 14 | Squad |
| `ST_CONSTSQUAD` | ScarType | 15 | Const Squad |
| `ST_PLAYER` | ScarType | 16 | Player |
| `ST_CONSTPLAYER` | ScarType | 17 | Const Player |
| `ST_MARKER` | ScarType | 18 | Marker |
| `ST_PBG` | ScarType | 19 | Property Bag Group |
| `ST_AIPLAYER` | ScarType | 20 | AI Player |
| `ST_AISQUAD` | ScarType | 21 | AI Squad |
| `ST_AIENTITY` | ScarType | 22 | AI Entity |
| `ST_AIENCOUNTER` | ScarType | 23 | AI Encounter |
| `ST_LOCSTRING` | ScarType | 24 | Localized String |
| `ST_MODIFIER` | ScarType | 25 | Modifier |
| `ST_RESOURCEAMOUNT` | ScarType | 26 | Resource Amount |
| `ST_UIGAMEITEMINFO` | ScarType | 27 | UI Game Item |
| `ST_PREFAB` | ScarType | 28 | Prefab |
| `ST_SPLAT` | ScarType | 29 | Splat/Decal |
| `ST_UNKNOWN` | ScarType | 30 | Unknown |

---

## Modifier Usage Types (MUT_)

| Constant | Value | Description |
|----------|-------|-------------|
| `MUT_Addition` | 0 | Add flat value |
| `MUT_Multiplication` | 1 | Multiply by value |
| `MUT_MultiplyAdd` | 2 | Multiply then add |
| `MUT_Enable` | 3 | Enable/disable toggle |
| `MUT_MultiplicationAddition` | 4 | Multiplication + addition |
| `MUT_Set` | 5 | Set absolute value |

---

## Modifier Application Types (MAT_)

| Constant | Value | Target |
|----------|-------|--------|
| `MAT_EntityType` | 0 | Entity blueprint type |
| `MAT_Entity` | 1 | Specific entity |
| `MAT_Player` | 2 | Player |
| `MAT_Squad` | 3 | Specific squad |
| `MAT_SquadType` | 4 | Squad blueprint type |
| `MAT_Weapon` | 5 | Specific weapon |
| `MAT_WeaponType` | 6 | Weapon type |
| `MAT_Upgrade` | 7 | Upgrade |
| `MAT_Ability` | 8 | Ability |
| `MAT_EntityTypeAndDescendants` | 9 | Entity type + subtypes |
| `MAT_SquadTypeAndDescendants` | 10 | Squad type + subtypes |
| `MAT_UpgradeTypeAndDescendants` | 12 | Upgrade type + subtypes |
| `MAT_AbilityTypeAndDescendants` | 13 | Ability type + subtypes |
| `MAT_WeaponTypeAndDescendants` | 14 | Weapon type + subtypes |

---

## Player States

| Constant | Value |
|----------|-------|
| `ABORTED` | PlayerState(1) |
| `KILLED` | PlayerState(3) |
| `KICKED` | PlayerState(4) |
| `WON` | PlayerState(5) |
| `PLAYING` | PlayerState(6) |
| `SURRENDERED` | PlayerState(7) |
| `INVALID` | PlayerState(9) |
| `COUNT` | PlayerState(10) |

---

## Win Reasons (WR_)

| Constant | Value | Condition |
|----------|-------|-----------|
| `WR_ANNIHILATION` | 0 | All units/buildings destroyed |
| `WR_CONQUEST` | 1 | Landmarks destroyed |
| `WR_ELIMINATION` | 2 | Player eliminated |
| `WR_KEEPRUSH` | 3 | Keep rush |
| `WR_NONE` | 4 | No win condition |
| `WR_OBJECTIVECOMPLETE` | 5 | Campaign objective |
| `WR_OBJECTIVEFAILED` | 6 | Campaign failure |
| `WR_REGICIDE` | 7 | King killed |
| `WR_RELICHUNT` | 8 | Sacred Sites |
| `WR_RELIGIOUS` | 9 | Religious victory |
| `WR_SETTLEMENTS` | 10 | Settlement control |
| `WR_SIEGE` | 11 | Siege victory |
| `WR_SURRENDER` | 12 | Player surrendered |
| `WR_WONDER` | 13 | Wonder victory |

---

## Counter Types (COUNTER_)

| Constant | Value | Description |
|----------|-------|-------------|
| `COUNTER_None` | -1 | No counter |
| `COUNTER_TimerDecreasing` | 0 | Countdown timer |
| `COUNTER_TimerIncreasing` | 1 | Counting up timer |
| `COUNTER_Count` | 2 | Numeric count |
| `COUNTER_CountUpTo` | 3 | Count toward target |
| `COUNTER_TurnsDecreasing` | 4 | Turn countdown |
| `COUNTER_TurnsIncreasing` | 5 | Turn count up |

---

## Objective Types (OT_)

| Constant | Value | Description |
|----------|-------|-------------|
| `OT_Primary` | ObjectiveType(0) | Primary objective |
| `OT_Secondary` | ObjectiveType(1) | Secondary objective |
| `OT_Bonus` | ObjectiveType(2) | Bonus objective |
| `OT_Information` / `OT_Warning` | ObjectiveType(3) | Info/warning |

---

## Objective States (OS_)

| Constant | Value |
|----------|-------|
| `OS_Off` | ObjectiveState(0) |
| `OS_Incomplete` | ObjectiveState(1) |
| `OS_Complete` | ObjectiveState(2) |
| `OS_Failed` | ObjectiveState(3) |

---

## Objective Data Templates (DT_)

| Constant | Value |
|----------|-------|
| `DT_PRIMARY_DEFAULT` | `"PrimaryObjectiveDataTemplate"` |
| `DT_PRIMARY_OR` | `"PrimaryOrObjectiveDataTemplate"` |
| `DT_SECONDARY_DEFAULT` | `"SecondaryObjectiveDataTemplate"` |
| `DT_BONUS_DEFAULT` | `"BonusObjectiveDataTemplate"` |
| `DT_INFO_DEFAULT` | `"InfoObjectiveDataTemplate"` |

---

## Objective Functions (FN_)

| Constant | Value |
|----------|-------|
| `FN_OnShow` | ObjectiveFunction(0) |
| `FN_OnSelect` | ObjectiveFunction(1) |
| `FN_OnActivate` | ObjectiveFunction(2) |
| `FN_LuaTableQuery` | ObjectiveFunction(3) |

---

## Dialog Buttons (DB_)

| Constant | Value |
|----------|-------|
| `DB_Close` | DialogButton(0) |
| `DB_Button1` | DialogButton(1) |
| `DB_Button2` | DialogButton(2) |
| `DB_Button3` | DialogButton(3) |

---

## Dialog Classes (DC_)

| Constant | Value |
|----------|-------|
| `DC_Default` | DialogClass(0) |
| `DC_Iconographic` | DialogClass(1) |

---

## Preset Colours

| Constant | Value |
|----------|-------|
| `Colour_Local` | PresetColour(0) |
| `Colour_Ally` | PresetColour(1) |
| `Colour_Enemy` | PresetColour(2) |
| `Colour_Neutral` | PresetColour(3) |

---

## Input Enabled Flags (IEF_)

| Constant | Value | Description |
|----------|-------|-------------|
| `IEF_None` | 0 | No input |
| `IEF_Camera` | 1 | Camera only |
| `IEF_Selection` | 2 | Selection only |
| `IEF_Command` | 4 | Commands only |
| `IEF_Default` / `IEF_All` | 7 | All input |

---

## HUD Feature Types (HUDF_)

| Constant | Value |
|----------|-------|
| `HUDF_AbilityCard` | HUDFeatureType(0) |
| `HUDF_MiniMap` | HUDFeatureType(1) |
| `HUDF_Upgrades` | HUDFeatureType(2) |
| `HUDF_CommandCard` | HUDFeatureType(3) |
| `HUDF_None` | HUDFeatureType(4) |

---

## Targeting Types

| Constant | Value |
|----------|-------|
| `Targeting_Automatic` | TargetingType(0) |
| `Targeting_Manual` | TargetingType(1) |
| `Targeting_None` | TargetingType(2) |

---

## Weapon Preferences (WP_)

| Constant | Value |
|----------|-------|
| `WP_Melee` | WeaponPreference(0) |
| `WP_Ranged` | WeaponPreference(1) |

---

## Mood Modes (MM_)

| Constant | Value |
|----------|-------|
| `MM_Auto` | MoodMode(0) |
| `MM_ForceTense` | MoodMode(1) |
| `MM_ForceCalm` | MoodMode(2) |

---

## Population Cap Types (CT_)

| Constant | Value |
|----------|-------|
| `CT_Personnel` | CapType(0) |
| `CT_Vehicle` | CapType(1) |
| `CT_Medic` | CapType(2) |

---

## Kill Player Reasons (KPR_)

| Constant | Value |
|----------|-------|
| `KPR_Endgame` | KillPlayerReason(1) |
| `KPR_NetworkAbort` | KillPlayerReason(3) |
| `KPR_NetworkDisconnected` | KillPlayerReason(4) |
| `KPR_NetworkKickedOut` | KillPlayerReason(5) |
| `KPR_Lost` | KillPlayerReason(7) |

---

## Death Reasons (DEATHREASON_)

| Constant | Value |
|----------|-------|
| `DEATHREASON_NORMAL` | DeathReason(0) |
| `DEATHREASON_OUTOFCONTROL` | DeathReason(1) |
| `DEATHREASON_CASUALTY` | DeathReason(2) |
| `DEATHREASON_WALKABLE_SURFACE` | DeathReason(3) |
| `DEATHREASON_SUBMERGE` | DeathReason(4) |
| `DEATHREASON_DEATH_AS_DRIVER` | DeathReason(5) |
| `DEATHREASON_SYNC_KILL` | DeathReason(6) |
| `DEATHREASON_ON_BLUEPRINT_CONVERT` | DeathReason(7) |

---

## Crush Modes

| Constant | Value |
|----------|-------|
| `Heavy` | CrushMode(0) |
| `Medium` | CrushMode(1) |
| `Light` | CrushMode(2) |
| `Off` | CrushMode(3) |

---

## Production Item Types (PITEM_)

| Constant | Value |
|----------|-------|
| `PITEM_Upgrade` | ProductionItemType(0) |
| `PITEM_SquadUpgrade` | ProductionItemType(2) |
| `PITEM_SquadReinforce` | ProductionItemType(3) |
| `PITEM_PlayerUpgrade` | ProductionItemType(4) |

---

## Can Produce Results (CANPRODUCE_)

| Constant | Value | Meaning |
|----------|-------|---------|
| `CANPRODUCE_NoItem` | 1 | Item doesn't exist |
| `CANPRODUCE_PrerequisitesProducer` | 2 | Producer prereqs not met |
| `CANPRODUCE_PrerequisitesItem` | 4 | Item prereqs not met |
| `CANPRODUCE_NoResources` | 8 | Insufficient resources |
| `CANPRODUCE_PopulationCapFull` | 16 | Pop cap reached |
| `CANPRODUCE_ProductionItemFull` | 128 | Queue full |
| `CANPRODUCE_OutOfTerritory` | 512 | Outside territory |
| `CANPRODUCE_Error` | 4096 | Generic error |

---

## Availability / Item States

| Constant | Value |
|----------|-------|
| `ITEM_LOCKED` | Availability(0) |
| `ITEM_REMOVED` | Availability(2) |
| `ITEM_DEFAULT` | Availability(3) |

---

## Decorator Visibility (DV_)

| Constant | Value |
|----------|-------|
| `DV_Hidden` | DecoratorVisibility(0) |
| `DV_MouseOver` | DecoratorVisibility(1) |
| `DV_Default` | DecoratorVisibility(2) |
| `DV_Visible` | DecoratorVisibility(3) |
| `DV_EnemyOnly` | DecoratorVisibility(4) |
| `DV_MouseOverOrDamagedEnemy` | DecoratorVisibility(5) |

---

## UI Combine Types

| Constant | Value |
|----------|-------|
| `UI_DoNotCombine` | UICombineType(0) |
| `UI_Intersection` | UICombineType(1) |
| `UI_Union` | UICombineType(2) |

---

## Area Types (AT_)

| Constant | Value |
|----------|-------|
| `AT_CIRCLE` | `"icons/minimap/area_circle"` |
| `AT_SQUARE` | `"icons/minimap/area_square"` |

---

## Game Over Constants

| Constant | Value |
|----------|-------|
| `GAMEOVER_OBJECTIVE_TIME` | 6.5 (seconds) |
| `GAMEOVER_PRESENTATION_TIME` | 20.0 (seconds) |

---

## Army Constants (ARMY_)

### Status
| Constant | Value |
|----------|-------|
| `ARMY_STATUS_ATTACKING` | `"Attacking"` |
| `ARMY_STATUS_DEFENDING` | `"Defending"` |
| `ARMY_STATUS_DISSOLVED` | `"Dissolved"` |
| `ARMY_STATUS_DISSOLVING_INTO_MODULE` | `"Dissolving into module"` |
| `ARMY_STATUS_EMPTY` | `"Empty"` |

### Defend Types
| Constant | Value |
|----------|-------|
| `ARMY_DEFEND_TYPE_CURRENT_POSITION` | `"Current Position"` |
| `ARMY_DEFEND_TYPE_FALLBACK` | `"Fallback"` |
| `ARMY_DEFEND_TYPE_SPAWN` | `"Spawn"` |
| `ARMY_DEFEND_TYPE_TARGET` | `"Target"` |

### Targeting Order
| Constant | Value |
|----------|-------|
| `ARMY_TARGETING_CYCLE` | `"Cycle"` |
| `ARMY_TARGETING_DISCARD` | `"Discard"` |
| `ARMY_TARGETING_PROX` | `"Proximity"` |
| `ARMY_TARGETING_RANDOM` | `"Random"` |
| `ARMY_TARGETING_RANDOM_MEANDERING` | `"RandomMeandering"` |
| `ARMY_TARGETING_REVERSE` | `"Reverse"` |

---

## AI Module Constants

| Constant | Value |
|----------|-------|
| `AI_MODULE_LEASH_BUFFER` | 20 |
| `AI_MODULE_COMBAT_RANGE` | 40 |

---

## NIS/Cutscene Types (NISLET_)

| Constant | Value |
|----------|-------|
| `NISLET_BLACK2GAME` | 1 |
| `NISLET_TIME` | 1 |
| `NISLET_VO` | 2 |
| `NISLET_GAME2GAME` | 2 |
| `NISLET_GAME2BLACK` | 3 |
| `NISLET_GAME2LETTER` | 4 |

---

## PropertyBagGroup Types (PBGTYPE_)

| Constant | Value |
|----------|-------|
| `PBGTYPE_Entity` | 1245184 |
| `PBGTYPE_Squad` | 3014656 |
| `PBGTYPE_Upgrade` | 3407872 |

---

## Comparison Operators

| Constant | Value |
|----------|-------|
| `IS_EQUAL` | RuleComparison(0) |
| `IS_LESS_THAN` | RuleComparison(2) |
| `IS_LESS_THAN_OR_EQUAL` | RuleComparison(3) |
| `IS_GREATER_THAN` | RuleComparison(4) |
| `IS_GREATER_THAN_OR_EQUAL` | RuleComparison(5) |

---

## AI Encounter Types (AIEncounterType_)

| Constant | Value |
|----------|-------|
| `AIEncounterType_AttackArea` | 1 |
| `AIEncounterType_FormationMove` | 4 |
| `AIEncounterType_FormationAttackMove` | 5 |

---

## AI Build Styles (BS_) *(scardocs)*

AI building placement strategy types. Used by `AI_*` functions for construction decisions.

| Constant | Description |
|----------|-------------|
| `BS_AwayFromResources` | Build away from resource deposits |
| `BS_Capital` | Capital/TC placement |
| `BS_Cistern` | Cistern placement (Byzantines) |
| `BS_COUNT` | Enum count sentinel |
| `BS_Dock` | Dock placement |
| `BS_ExpansionBase` | Expansion base location |
| `BS_Farm` | Farm placement |
| `BS_FinishIncompleteStructure` | Complete unfinished buildings |
| `BS_ForwardDefense` | Forward defensive structure |
| `BS_Gates` | Gate placement |
| `BS_Keep` | Keep/Donjon/Castle placement |
| `BS_LandAndNavalProductionBuilding` | Combined land/naval production |
| `BS_Landmark` | Landmark placement |
| `BS_Market` | Market placement |
| `BS_MercenaryHouse` | Mercenary house (Byzantines) |
| `BS_Mill` | Mill placement |
| `BS_NearAnchor` | Build near anchor point |
| `BS_NearBlueprint` | Build near specific blueprint |
| `BS_NearHomeBase` | Build near home base |
| `BS_NearResourceDropoff` | Build near resource drop-off |
| `BS_NearResources` | Build near resources |
| `BS_NearSameBlueprint` | Build near same type building |
| `BS_Outpost` | Outpost/tower placement |
| `BS_ProductionBuilding` | Production building placement |
| `BS_Secure` | Secure/strategic position |
| `BS_Siege` | Siege workshop placement |
| `BS_Storehouse` | Storehouse placement |
| `BS_TargetedRequest` | AI-targeted build request |
| `BS_Tower` | Tower placement |
| `BS_WallEmplacement` | Wall emplacement |
| `BS_Walls` | Wall segment placement |
| `BS_Wonder` | Wonder placement |
| `BS_WoodenFortress` | Wooden fortress (Rus) |

---

## AI Tactic Types (TACTIC_) *(scardocs)*

AI squad tactic behavior types. Used with `AITactic_*` and encounter tactic filter functions.

| Constant |
|----------|
| `TACTIC_Ability` |
| `TACTIC_Avoid` |
| `TACTIC_CapturePoint` |
| `TACTIC_CaptureTeamWeapon` |
| `TACTIC_COUNT` |
| `TACTIC_Cover` |
| `TACTIC_FinishHealing` |
| `TACTIC_ForceAttack` |
| `TACTIC_Hold` |
| `TACTIC_Lua` |
| `TACTIC_MinRange` |
| `TACTIC_Pickup` |
| `TACTIC_ProvideReinforcementPoint` |
| `TACTIC_Recrew` |
| `TACTIC_Sequence` |
| `TACTIC_Vehicle` |
| `TACTIC_VehicleDecrew` |

---

## AI Tactic Target Preferences (TacticTargetPreference_) *(scardocs)*

| Constant |
|----------|
| `TacticTargetPreference_Best` |
| `TacticTargetPreference_COUNT` |
| `TacticTargetPreference_HighDamage` |
| `TacticTargetPreference_LowHealth` |
| `TacticTargetPreference_Near` |
| `TacticTargetPreference_NearAndBest` |
| `TacticTargetPreference_None` |
| `TacticTargetPreference_Support` |

---

## AI Task Types (TASK_) *(scardocs)*

AI encounter task types. Used with `AIEncounter_*` functions for task identification.

| Constant |
|----------|
| `TASK_AbilityEncounter` |
| `TASK_AttackEncounter` |
| `TASK_COUNT` |
| `TASK_DefendEncounter` |
| `TASK_ENCOUNTERS_END` |
| `TASK_ENCOUNTERS_START` |
| `TASK_EntityAbility` |
| `TASK_FormationAbilityState` |
| `TASK_FormationAttackMoveEncounter` |
| `TASK_FormationAutoHealState` |
| `TASK_FormationDefendAreaEncounter` |
| `TASK_FormationFleeState` |
| `TASK_FormationHoldableUnloadState` |
| `TASK_FormationIdleState` |
| `TASK_FormationLoadToHoldState` |
| `TASK_FormationMinRangeState` |
| `TASK_FormationMoveEncounter` |
| `TASK_FormationMoveState` |
| `TASK_FormationPathToMeleeState` |
| `TASK_FormationPhaseEncounter` |
| `TASK_FormationProtectState` |
| `TASK_FormationSetupRangedAttackState` |
| `TASK_FormationSimpleMeleeAttackState` |
| `TASK_FormationTargetedAbilityState` |
| `TASK_FormationTargetedConstructState` |
| `TASK_FormationTransportMoveState` |
| `TASK_FormationUnitTypeAttackState` |
| `TASK_GatherEncounter` |
| `TASK_MoveEncounter` |
| `TASK_PlayerAbility` |
| `TASK_ScoutEncounter` |
| `TASK_SquadAbility` |
| `TASK_SquadCapture` |
| `TASK_SquadCombat` |
| `TASK_SquadCombatState` |
| `TASK_SquadConstruction` |
| `TASK_SquadFallbackState` |
| `TASK_SquadFollow` |
| `TASK_SquadForwardBase` |
| `TASK_SquadGather` |
| `TASK_SquadHold` |
| `TASK_SquadImmobileCombat` |
| `TASK_SquadLeader` |
| `TASK_SquadMoveState` |
| `TASK_SquadPatrol` |
| `TASK_SquadPickUp` |
| `TASK_SquadProduction` |
| `TASK_SquadRetreatState` |
| `TASK_SquadSimpleMoveState` |
| `TASK_SquadTacticState` |
| `TASK_TownLifeEncounter` |

---

## Combat Range Policies (CombatRangePolicy_) *(scardocs)*

Used with `AIEncounter_CombatGuidance_SetCombatRangePolicy`.

| Constant |
|----------|
| `CombatRangePolicy_Count` |
| `CombatRangePolicy_Default` |
| `CombatRangePolicy_INVALID` |
| `CombatRangePolicy_MeleeRange` |
| `CombatRangePolicy_Ranged_MaxRange` |
| `CombatRangePolicy_Ranged_MinRange` |

---

## AI Combat Types (COMBAT_) *(scardocs)*

| Constant |
|----------|
| `COMBAT_Attack` |
| `COMBAT_COUNT` |
| `COMBAT_Default` |
| `COMBAT_Defend` |

---

## AI Count Types (ACT_) *(scardocs)*

| Constant |
|----------|
| `ACT_Count` |
| `ACT_Current` |
| `ACT_CurrentTeam` |
| `ACT_Invalid` |
| `ACT_Produced` |
| `ACT_ProducedTeam` |

---

## Camera Tuning Values (TV_) *(scardocs)*

Camera system tuning parameters. Used by the game camera system.

| Constant |
|----------|
| `TV_CameraMode` |
| `TV_ClipFar` |
| `TV_ClipNear` |
| `TV_Count` |
| `TV_DeclAbove` |
| `TV_DeclBelow` |
| `TV_DeclBelowClose` |
| `TV_DeclinationEnabled` |
| `TV_DeclRateMouse` |
| `TV_DefaultAngle` |
| `TV_DefaultDeclination` |
| `TV_DefaultFOV` |
| `TV_DefaultHeight` |
| `TV_DistExp` |
| `TV_DistExpMouse` |
| `TV_DistExpWheel` |
| `TV_DistGroundMin` |
| `TV_DistGroundTargetHeight` |
| `TV_DistMax` |
| `TV_DistMaxDead` |
| `TV_DistMin` |
| `TV_DistMinDead` |
| `TV_DistMinGround` |
| `TV_DistRateMouse` |
| `TV_DistRateWheelZoomIn` |
| `TV_DistRateWheelZoomOut` |
| `TV_DistScale` |
| `TV_EntityMinViewAngle` |
| `TV_FieldOfView` |
| `TV_NearPlaneShifter` |
| `TV_NonPlayableAreaBuffer` |
| `TV_OrbitRateMouse` |
| `TV_PanAccelerate` |
| `TV_PanMaxSpeedScalar` |
| `TV_PanScaleKeyboardDefZ` |
| `TV_PanScaleKeyboardMinZ` |
| `TV_PanScaleMouseDefZ` |
| `TV_PanScaleMouseMinZ` |
| `TV_PanScaleScreenDefZ` |
| `TV_PanScaleScreenMinZ` |
| `TV_PanStartSpeedScalar` |
| `TV_RotationEnabled` |
| `TV_ScreenObjectCullingAreaSize` |
| `TV_ScreenObjectCullingDistanceStart` |
| `TV_SlideDeclBase` |
| `TV_SlideDeclRate` |
| `TV_SlideDeclThreshold` |
| `TV_SlideDistBase` |
| `TV_SlideDistRate` |
| `TV_SlideDistThreshold` |
| `TV_SlideOrbitBase` |
| `TV_SlideOrbitRate` |
| `TV_SlideOrbitThreshold` |
| `TV_SlideTargetBase` |
| `TV_SlideTargetRate` |
| `TV_SlideTargetThreshold` |
| `TV_TrackBoundScale` |
| `TV_TrackElastic` |
| `TV_ZoomLocked` |

---

## Visibility Flags (VF_) *(scardocs)*

HUD component and visual visibility flags. Used with `Game_SetVisibility` and UI systems.

| Constant |
|----------|
| `VF_All` |
| `VF_AllNoXbox` |
| `VF_ComponentChatControl` |
| `VF_ComponentDecorators` |
| `VF_ComponentHintPoint` |
| `VF_ComponentKickers` |
| `VF_ComponentReplayControls` |
| `VF_ComponentReplayTaskbar` |
| `VF_Components` |
| `VF_ComponentSimulation` |
| `VF_ComponentTaskbar` |
| `VF_ComponentTitles` |
| `VF_Default` |
| `VF_MiscPaused` |
| `VF_None` |
| `VF_VisualArcs` |
| `VF_VisualCoverPreview` |
| `VF_VisualDistricts` |
| `VF_VisualEntityColors` |
| `VF_VisualMissionArea` |
| `VF_VisualModals` |
| `VF_VisualPathPreview` |
| `VF_Visuals` |
| `VF_VisualSelectionSilhouettes` |
| `VF_VisualTerritoryCapturePoint` |
| `VF_VisualTerritoryOutOfBoundsBorders` |
| `VF_VisualTerritorySectors` |
| `VF_XboxUI` |
| `VF_XboxUIBuildQueue` |
| `VF_XboxUIContextualRadial` |
| `VF_XboxUIControlGroups` |
| `VF_XboxUIFindMenu` |
| `VF_XboxUIMinimapFocus` |
| `VF_XboxUIQueueModifier` |
| `VF_XboxUIQuickCommands` |
| `VF_XboxUIQuickFind` |
| `VF_XboxUIResourceCard` |
| `VF_XboxUISelectAllOnScreen` |
| `VF_XboxUISiteMenu` |
| `VF_XboxUIVillagerPriorities` |

---

## Front-End Layers (FEL_) *(scardocs)*

UI layer ordering.

| Constant |
|----------|
| `FEL_Dialog` |
| `FEL_FullscreenModal` |
| `FEL_Hud` |
| `FEL_Modal` |
| `FEL_Modal2` |
| `FEL_Notification` |
| `FEL_Screen` |
| `FEL_SemiModal` |
| `FEL_Video` |
| `FEL_VideoBackground` |
| `FEL_Widget` |

---

## HUD Ping Anim Types (HPAT_) *(scardocs)*

| Constant |
|----------|
| `HPAT_Artillery` |
| `HPAT_Attack` |
| `HPAT_AttackLooping` |
| `HPAT_Bonus` |
| `HPAT_Count` |
| `HPAT_CoverGreen` |
| `HPAT_CoverRed` |
| `HPAT_CoverYellow` |
| `HPAT_Critical` |
| `HPAT_DeepSnow` |
| `HPAT_Detonation` |
| `HPAT_FormationSetup` |
| `HPAT_Hint` |
| `HPAT_Movement` |
| `HPAT_MovementLooping` |
| `HPAT_Objective` |
| `HPAT_RallyPoint` |
| `HPAT_Vaulting` |

---

## Save Types (STT_) *(scardocs)*

| Constant |
|----------|
| `STT_Auto` |
| `STT_Count` |
| `STT_Dev` |
| `STT_Quick` |
| `STT_Standard` |

---

## Entity State IDs (STATEID_) *(scardocs)*

| Constant |
|----------|
| `STATEID_Count` |
| `STATEID_Dead` |
| `STATEID_Idle` |
| `STATEID_Invalid` |
| `STATEID_Projectile` |

---

## Loop Types (LOOP_) *(scardocs)*

| Constant |
|----------|
| `LOOP_INVALID` |
| `LOOP_NONE` |
| `LOOP_NORMAL` |
| `LOOP_TOGGLE_DIRECTION` |

---

## Targeting Phases (TP_) *(scardocs)*

| Constant |
|----------|
| `TP_Cancelled` |
| `TP_Count` |
| `TP_Facing` |
| `TP_Issued` |
| `TP_None` |
| `TP_Position` |

---

## Unit Owner Types (UOT_) *(scardocs)*

| Constant |
|----------|
| `UOT_COUNT` |
| `UOT_EntityInSquad` |
| `UOT_None` |
| `UOT_Player` |
| `UOT_Self` |

---

## Availability States *(scardocs)*

| Constant |
|----------|
| `eAvailablityCOUNT` |
| `eDefault` |
| `eLocked` |
| `eRemoved` |
| `eUnlocked` |

---

## Billboard Icon States (BIS_) *(scardocs)*

| Constant |
|----------|
| `BIS_Count` |
| `BIS_Icon` |
| `BIS_IconState` |

---

## FOW Check Types (CHECK_) *(scardocs)*

| Constant |
|----------|
| `CHECK_BOTH` |
| `CHECK_COUNT` |
| `CHECK_IN_FOW` |
| `CHECK_OFFCAMERA` |

---

## Presentation Events (PE_) *(scardocs)*

| Constant |
|----------|
| `PE_AgeUpResourceLoaded` |
| `PE_ControlGroupChanged` |
| `PE_MultiplayerPauseChangeEvent` |
| `PE_PlayerWinOrLose` |
| `PE_Taunt` |
| `PE_TownGenFailedBuilding` |
