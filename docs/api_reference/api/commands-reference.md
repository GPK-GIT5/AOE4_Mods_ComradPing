# AoE4 Command Types — Complete Reference

Last Updated: 2026-02-23

All entity, squad, and player command type constants.

---

## Entity Commands (CMD_)
Commands issued to individual entities.

| Constant | Value | Description |
|----------|-------|-------------|
| `CMD_DefaultAction` | 0 | Context-dependent default action |
| `CMD_Stop` | 1 | Stop current action |
| `CMD_Destroy` | 2 | Self-destruct |
| `CMD_BuildSquad` | 3 | Produce a squad |
| `CMD_InstantBuildSquad` | 4 | Instantly produce a squad |
| `CMD_CancelProduction` | 5 | Cancel production queue item |
| `CMD_BuildStructure` | 6 | Construct a building |
| `CMD_Move` | 7 | Move to position |
| `CMD_FlightMove` | 8 | Aerial movement |
| `CMD_Face` | 9 | Face a direction |
| `CMD_Attack` | 10 | Attack target |
| `CMD_AttackMove` | 11 | Move and attack enemies en route |
| `CMD_RallyPoint` | 12 | Set rally point |
| `CMD_Capture` | 13 | Capture strategic point |
| `CMD_Ability` | 14 | Use ability |
| `CMD_Evacuate` | 15 | Evacuate garrison |
| `CMD_Upgrade` | 16 | Research upgrade |
| `CMD_InstantUpgrade` | 17 | Instantly complete upgrade |
| `CMD_Load` | 18 | Load into transport/garrison |
| `CMD_Unload` | 19 | Unload from transport |
| `CMD_UnloadSquads` | 20 | Unload specific squads |
| `CMD_AttackStop` | 21 | Stop attacking |
| `CMD_AttackForced` | 22 | Force attack (friendly fire) |
| `CMD_SetHoldHeading` | 23 | Lock facing direction |
| `CMD_Halt` | 24 | Hard stop |
| `CMD_Paradrop` | 25 | Paradrop |
| `CMD_DefuseMine` | 26 | Defuse mine |
| `CMD_Casualty` | 27 | Become casualty |
| `CMD_Death` | 28 | Die |
| `CMD_InstantDeath` | 29 | Die instantly |
| `CMD_Projectile` | 30 | Fire projectile |
| `CMD_PlaceCharge` | 31 | Place demolition charge |
| `CMD_BuildEntity` | 32 | Build entity |
| `CMD_RescueCasualty` | 33 | Rescue casualty |
| `CMD_AttackFromHold` | 34 | Attack from garrison |
| `CMD_Vault` | 35 | Vault over obstacle |
| `CMD_KnockedBack` | 36 | Knockback reaction |
| `CMD_Teardown` | 37 | Tear down structure |
| `CMD_Melee` | 38 | Melee attack |
| `CMD_ResolveOverlap` | 39 | Resolve position overlap |
| `CMD_Stun` | 40 | Stun reaction |
| `CMD_InstantSetupTeamWeapon` | 41 | Instant team weapon setup |
| `CMD_SetupTeamWeapon` | 42 | Setup team weapon |
| `CMD_MoveToCover` | 43 | Move to cover |
| `CMD_Taunted` | 44 | Taunt reaction |
| `CMD_Trade` | 45 | Trade route |
| `CMD_Brace` | 46 | Brace for impact |
| `CMD_Gather` | 47 | Gather resource |
| `CMD_PickUpSimItem` | 48 | Pick up item |
| `CMD_ChangeCombatSlot` | 49 | Change combat slot |
| `CMD_RetreatMove` | 50 | Retreat move |
| `CMD_StopAbility` | 51 | Stop ability |
| `CMD_InstantLoad` | 52 | Instant garrison |
| `CMD_FieldSupportConvert` | 53 | Field support conversion |
| `CMD_Disable` | 54 | Disable |
| `CMD_Enable` | 55 | Enable |
| `CMD_CancelConstruction` | 56 | Cancel building construction |
| `CMD_HoldPositionOn` | 57 | Enable hold position |
| `CMD_HoldPositionOff` | 58 | Disable hold position |
| `CMD_Teleport` | 59 | Teleport |
| `CMD_Patrol` | 60 | Patrol route |

---

## Squad Commands (SCMD_)
Commands issued to squads (groups of entities).

| Constant | Value | Description |
|----------|-------|-------------|
| `SCMD_DefaultAction` | 0 | Context-dependent default |
| `SCMD_Move` | 62 | Move to position |
| `SCMD_Stop` | 63 | Stop |
| `SCMD_Destroy` | 64 | Self-destruct |
| `SCMD_BuildStructure` | 65 | Build structure |
| `SCMD_Capture` | 66 | Capture point |
| `SCMD_Attack` | 67 | Attack |
| `SCMD_ReinforceUnit` | 68 | Reinforce |
| `SCMD_Upgrade` | 69 | Research |
| `SCMD_CancelProduction` | 70 | Cancel production |
| `SCMD_AttackMove` | 71 | Attack-move |
| `SCMD_Ability` | 72 | Use ability |
| `SCMD_Load` | 73 | Load/garrison |
| `SCMD_InstantLoad` | 74 | Instant load |
| `SCMD_UnloadSquads` | 75 | Unload squads |
| `SCMD_Unload` | 76 | Unload |
| `SCMD_SlotItemRemove` | 77 | Remove slot item |
| `SCMD_Retreat` | 78 | Retreat |
| `SCMD_CaptureTeamWeapon` | 79 | Capture team weapon |
| `SCMD_SetMoveType` | 80 | Set movement type |
| `SCMD_InstantReinforceUnit` | 81 | Instant reinforce |
| `SCMD_InstantUpgrade` | 82 | Instant upgrade |
| `SCMD_PlaceCharge` | 83 | Place charge |
| `SCMD_DefuseCharge` | 84 | Defuse charge |
| `SCMD_PickUpSlotItem` | 85 | Pick up slot item |
| `SCMD_PickUpSimItem` | 86 | Pick up sim item |
| `SCMD_DefuseMine` | 87 | Defuse mine |
| `SCMD_DoPlan` | 88 | Execute AI plan |
| `SCMD_Patrol` | 89 | Patrol |
| `SCMD_Surprise` | 90 | Surprise/ambush |
| `SCMD_InstantSetupTeamWeapon` | 91 | Instant team weapon |
| `SCMD_SetupTeamWeapon` | 92 | Setup team weapon |
| `SCMD_AbandonTeamWeapon` | 93 | Abandon team weapon |
| `SCMD_StationaryAttack` | 94 | Stationary attack |
| `SCMD_RevertFieldSupport` | 95 | Revert field support |
| `SCMD_Face` | 96 | Face direction |
| `SCMD_BuildSquad` | 97 | Produce squad |
| `SCMD_RallyPoint` | 98 | Set rally |
| `SCMD_RescueCasualty` | 99 | Rescue casualty |
| `SCMD_Recrew` | 100 | Recrew vehicle |
| `SCMD_Merge` | 101 | Merge squads |
| `SCMD_WeaponPreference` | 102 | Set weapon preference |
| `SCMD_CombatStance` | 103 | Set combat stance |
| `SCMD_MoveToCover` | 104 | Move to cover |
| `SCMD_Gather` | 105 | Gather resource |
| `SCMD_AttackWithinLeashArea` | 106 | Attack within leash |
| `SCMD_JoinFormationSquadGroup` | 107 | Join formation |
| `SCMD_Trade` | 108 | Trade |
| `SCMD_HoldPosition` | 109 | Hold position |
| `SCMD_Evacuate` | 110 | Evacuate |
| `SCMD_Vault` | 111 | Vault |
| `SCMD_CancelQueuedCommand` | 112 | Cancel queued command |
| `SCMD_RespondToBeingBreached` | 113 | Respond to breach |
| `SCMD_StopAbility` | 114 | Stop ability |
| `SCMD_Teleport` | 115 | Teleport |
| `SCMD_AddPatrolPoint` | 116 | Add patrol point |

---

## Player Commands (PCMD_)
Commands issued at the player level.

| Constant | Value | Description |
|----------|-------|-------------|
| `PCMD_PlaceAndConstructEntities` | 123 | Place & build structures |
| `PCMD_ResourceDonation` | 124 | Tribute resources |
| `PCMD_CheatResources` | 125 | Cheat: add resources |
| `PCMD_CheatRevealAll` | 126 | Cheat: reveal map |
| `PCMD_Ability` | 127 | Player ability |
| `PCMD_CheatBuildTime` | 128 | Cheat: instant build |
| `PCMD_CheatIgnoreCosts` | 129 | Cheat: free costs |
| `PCMD_Upgrade` | 130 | Research upgrade |
| `PCMD_InstantUpgrade` | 131 | Instant upgrade |
| `PCMD_UpgradeRemove` | 134 | Remove upgrade |
| `PCMD_SlotItemRemove` | 136 | Remove slot item |
| `PCMD_CancelProduction` | 137 | Cancel production |
| `PCMD_DetonateCharges` | 138 | Detonate placed charges |
| `PCMD_AIPlayer` | 139 | AI player command |
| `PCMD_AIPlayer_EncounterNotification` | 140 | AI encounter notification |
| `PCMD_Surrender` | 141 | Surrender |
| `PCMD_AIPlayer_EncounterSniped` | 144 | AI encounter sniped |
| `PCMD_AIPlayer_ResourceBonus` | 145 | AI resource bonus |
| `PCMD_FormationSquadGroupCreateBegin` | 146 | Start formation group |
| `PCMD_FormationSquadGroupAddSquad` | 147 | Add squad to formation |
| `PCMD_FormationSquadGroupCreateEnd` | 148 | Finalize formation group |
| `PCMD_StopAbility` | 150 | Stop ability |

---

## AI Task Types (TASK_)

### Squad Tasks
| Constant | Value | Description |
|----------|-------|-------------|
| `TASK_SquadSimpleMoveState` | 0 | Simple move |
| `TASK_SquadMoveState` | 1 | Complex move |
| `TASK_SquadCombatState` | 2 | Combat |
| `TASK_SquadTacticState` | 3 | Tactic execution |
| `TASK_SquadFallbackState` | 4 | Fallback behavior |
| `TASK_SquadRetreatState` | 5 | Retreat |
| `TASK_SquadCapture` | 21 | Capture point |
| `TASK_SquadCombat` | 22 | Squad combat |
| `TASK_SquadImmobileCombat` | 23 | Stationary combat |
| `TASK_SquadConstruction` | 24 | Building |
| `TASK_SquadProduction` | 25 | Producing |
| `TASK_SquadPickUp` | 26 | Pick up item |
| `TASK_SquadPatrol` | 27 | Patrolling |
| `TASK_SquadHold` | 28 | Holding position |
| `TASK_SquadLeader` | 29 | Leading |
| `TASK_SquadFollow` | 30 | Following |
| `TASK_SquadAbility` | 31 | Using ability |
| `TASK_SquadForwardBase` | 32 | Forward base |
| `TASK_SquadGather` | 33 | Gathering |

### Formation Tasks
| Constant | Value | Description |
|----------|-------|-------------|
| `TASK_FormationMoveState` | 6 | Formation move |
| `TASK_FormationMinRangeState` | 7 | Min range |
| `TASK_FormationUnitTypeAttackState` | 8 | Unit-type attack |
| `TASK_FormationProtectState` | 9 | Protect |
| `TASK_FormationSimpleMeleeAttackState` | 10 | Melee attack |
| `TASK_FormationSetupRangedAttackState` | 11 | Ranged attack |
| `TASK_FormationLoadToHoldState` | 12 | Load to hold |
| `TASK_FormationTransportMoveState` | 13 | Transport move |
| `TASK_FormationTargetedAbilityState` | 14 | Targeted ability |
| `TASK_FormationPathToMeleeState` | 15 | Path to melee |
| `TASK_FormationIdleState` | 16 | Idle |
| `TASK_FormationHoldableUnloadState` | 17 | Holdable unload |
| `TASK_FormationFleeState` | 18 | Flee |
| `TASK_FormationTargetedConstructState` | 19 | Construction |
| `TASK_FormationAutoHealState` | 20 | Auto heal |

### Entity/Player Tasks
| Constant | Value |
|----------|-------|
| `TASK_EntityAbility` | 34 |
| `TASK_PlayerAbility` | 35 |

### Encounter Tasks
| Constant | Value |
|----------|-------|
| `TASK_AttackEncounter` | 36 |
| `TASK_DefendEncounter` | 37 |
| `TASK_MoveEncounter` | 38 |
| `TASK_AbilityEncounter` | 39 |
| `TASK_ScoutEncounter` | 40 |
| `TASK_FormationMoveEncounter` | 41 |
| `TASK_FormationAttackMoveEncounter` | 42 |
| `TASK_FormationPhaseEncounter` | 43 |
| `TASK_TownLifeEncounter` | 44 |
| `TASK_GatherEncounter` | 45 |
| `TASK_FormationDefendAreaEncounter` | 46 |

---

## Extension IDs (EXTID_)
Extension type identifiers for entity capability checks.

| Constant | String Value | Purpose |
|----------|-------------|---------|
| `EXTID_Ability` | `"ability_ext"` | Ability system |
| `EXTID_ActionApply` | `"action_apply_ext"` | Action application |
| `EXTID_Burn` | `"burn_ext"` | Fire/burning |
| `EXTID_Combat` | `"combat_ext"` | Combat system |
| `EXTID_Construction` | `"construction_ext"` | Building construction |
| `EXTID_Cost` | `"cost_ext"` | Resource costs |
| `EXTID_Health` | `"health_ext"` | Health system |
| `EXTID_Hold` | `"hold_ext"` | Garrison (building) |
| `EXTID_Holdable` | `"holdable_ext"` | Can be garrisoned |
| `EXTID_Market` | `"market_ext"` | Market trading |
| `EXTID_Modifier` | `"modifier_ext"` | Modifiers |
| `EXTID_Moving` | `"moving_ext"` | Movement |
| `EXTID_ProductionQueue` | `"production_queue_ext"` | Production |
| `EXTID_Resource` | `"resource_ext"` | Resource node |
| `EXTID_Sight` | `"sight_ext"` | Vision |
| `EXTID_StrategicPoint` | `"strategic_point_ext"` | Strategic point |
| `EXTID_Territory` | `"territory_ext"` | Territory |
| `EXTID_Upgrade` | `"upgrade_ext"` | Upgrades |
| `EXTID_Wall` | `"wall_ext"` | Walls |
| `EXTID_Weapon` | `"weapon_ext"` | Weapons |
| `EXTID_WalkableSurface` | `"walkable_surface_ext"` | Wall walking |

*Plus 39 additional extensions: Attention, AttentionGen, AideStation, AttachmentChild, Camouflage, Casualty, Cover, Crew, Crush, Crushee, Demolishable, DemolitionCharge, Element, Explosion, FieldSupport, Flight, InteractiveObject, Medic, Mine, MineClearer, ModifierApply, MoveType, MovementBlocker, MultiControlTerritoryController, OOCTarget, ObjCover, Paradrop, Posture, Projectile, Recrewable, RepairEngineer, RepairStation, Road, StimulusEmission, StimulusPerception, Supply, SupplyRoad, TeamWeaponUser, UI*

---

## AI Build Styles (BS_)

| Constant | Value | Description |
|----------|-------|-------------|
| `BS_Secure` | 0 | Build in safe area |
| `BS_NearAnchor` | 1 | Near anchor point |
| `BS_FinishIncompleteStructure` | 2 | Complete unfinished building |
| `BS_ForwardDefense` | 3 | Forward defense position |
| `BS_Walls` | 4 | Wall placement |
| `BS_Gates` | 5 | Gate placement |
| `BS_NearResources` | 6 | Near resource deposits |
| `BS_NearResourceDropoff` | 7 | Near drop-off buildings |
| `BS_AwayFromResources` | 8 | Away from resources |
| `BS_NearSameBlueprint` | 9 | Near same building type |
| `BS_NearBlueprint` | 10 | Near specific blueprint |
| `BS_ProductionBuilding` | 11 | Production building |
| `BS_ExpansionBase` | 12 | Expansion base |
| `BS_Tower` | 13 | Tower placement |
| `BS_TargetedRequest` | 14 | At specific location |
| `BS_Outpost` | 15 | Outpost |
| `BS_Keep` | 16 | Keep |
| `BS_WallEmplacement` | 17 | Emplacement on wall |
| `BS_Siege` | 18 | Siege workshop/weapon |
| `BS_Dock` | 19 | Dock |
| `BS_Wonder` | 20 | Wonder |
| `BS_Landmark` | 21 | Landmark |

---

## Hint Point Types (HPAT_)

| Constant | Value | Description |
|----------|-------|-------------|
| `HPAT_Objective` | 0 | Objective marker |
| `HPAT_Hint` | 1 | Hint marker |
| `HPAT_Critical` | 2 | Critical marker |
| `HPAT_Movement` | 3 | Movement marker |
| `HPAT_Attack` | 4 | Attack marker |
| `HPAT_FormationSetup` | 5 | Formation setup |
| `HPAT_RallyPoint` | 6 | Rally point |
| `HPAT_DeepSnow` | 7 | Deep snow |
| `HPAT_Artillery` | 8 | Artillery |
| `HPAT_CoverGreen` | 9 | Good cover |
| `HPAT_CoverYellow` | 10 | Medium cover |
| `HPAT_CoverRed` | 11 | Bad cover |
| `HPAT_Detonation` | 12 | Detonation |
| `HPAT_Vaulting` | 13 | Vault point |
| `HPAT_Bonus` | 14 | Bonus |
| `HPAT_MovementLooping` | 15 | Looping movement |
| `HPAT_AttackLooping` | 16 | Looping attack |

---

## AI Tactic Types (TACTIC_)

| Constant | Value |
|----------|-------|
| `TACTIC_Ability` | 0 |
| `TACTIC_Cover` | 1 |
| `TACTIC_Hold` | 2 |
| `TACTIC_Avoid` | 3 |
| `TACTIC_Vehicle` | 4 |
| `TACTIC_ForceAttack` | 5 |
| `TACTIC_Pickup` | 6 |
| `TACTIC_CaptureTeamWeapon` | 7 |
| `TACTIC_Recrew` | 8 |
| `TACTIC_ProvideReinforcementPoint` | 9 |
| `TACTIC_FinishHealing` | 10 |
| `TACTIC_CapturePoint` | 11 |
| `TACTIC_MinRange` | 12 |
| `TACTIC_VehicleDecrew` | 13 |
| `TACTIC_Sequence` | 14 |
| `TACTIC_Lua` | 15 |
