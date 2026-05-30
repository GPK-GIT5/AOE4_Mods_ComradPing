# Angevin Chapter 3: Lincoln

## OVERVIEW

The Battle of Lincoln (1141) is a multi-phase campaign mission in the Angevin storyline where the player controls Empress Matilda's forces against King Stephen's army besieging Lincoln Castle. The mission opens with a stealth ambush phase — the player must hide units in a stealth forest and intercept three enemy reinforcement columns marching along trade roads. After eliminating or failing to stop the columns, the player destroys an enemy market town, rendezvouses with Welsh allies under attack from flanking forces, then breaks through Stephen's field army blockade to enter the city. Once inside Lincoln, the player takes control of the garrison, clears three siege camps surrounding the keep, and ultimately captures King Stephen while defending the keep from escalating siege waves. An achievement rewards completing the mission without the keep taking any damage.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `ang_chp3_lincoln.scar` | core | Main mission script — player/relationship setup, difficulty, mission flow, spawning, combat logic, and phase transitions |
| `ang_chp3_lincoln_data.scar` | data | Initializes all global state variables, SGroups, EGroups, unit composition tables, waypoint lists, and siege data |
| `ang_chp3_lincoln_training.scar` | training | Defines tutorial goal sequences for scout selection, stealth forest movement, and allied unit awareness |
| `obj_defeat.scar` | objectives | All offensive objectives — ambush setup, reinforcement columns, trade post destruction, field army routing, camp clearing, and Stephen capture |
| `obj_defend.scar` | objectives | Defensive fail-condition objective for Lincoln Keep |
| `obj_welsh.scar` | objectives | Welsh rendezvous and help-Welsh objectives with flanking battle logic |

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Lincoln_Data_Init` | data | Initialize all globals, SGroups, unit tables, waypoint arrays |
| `GetRecipe` | data | Return MissionOMatic recipe with all modules and settings |
| `Lincoln_InitTraining` | training | Register scout-select, stealth-move, and allies training goals |
| `AlliesHaveArrived` | training | Trigger training when allied squads visible on screen |
| `HasScoutInSight` | training | Trigger training when idle scout visible to player |
| `Mission_SetupPlayers` | core | Configure 7 players, relationships, ages, colours, LOS |
| `Mission_SetDifficulty` | core | Set `t_difficulty` table via `Util_DifVar` for all scaling |
| `Mission_Preset` | core | Init training, upgrades, units, objectives, siege camps, besiegers |
| `Mission_Start` | core | Start ambush objective, enable rules, reset resources |
| `Lincoln_InitStartingUnits` | core | Deploy wall archers, villagers, player army, archer lines |
| `Lincoln_InitSiegeCamps` | core | Populate camp SGroups with defenders and archer lines |
| `Lincoln_InitBesiegers` | core | Build `t_besiegers` table linking 5 besieger modules |
| `Lincoln_InitFlankGuards` | core | Spawn flank guard units at 3 rear-line positions |
| `Lincoln_InitWallArchers` | core | Deploy 14 garrison archers along wall positions |
| `Lincoln_SpawnEnemyReinforcements` | core | Spawn reinforcement column (1-3) as RovingArmy modules |
| `Lincoln_CheckEnemyReinforcements` | core | Monitor all 3 erg groups for completion/failure/merging |
| `Lincoln_CheckEnemyReinforcementGroup` | core | Track kill progress on one column; fail if it reaches market |
| `Lincoln_MoveToMarket` | core | Move surviving column units to market perimeter defend |
| `Lincoln_SpawnWelsh` | core | Spawn 3 Welsh army groups (archers + spearmen) |
| `Lincoln_StartWelshPhase` | core | Trigger Welsh rendezvous and east patrol proximity checks |
| `Lincoln_StartRendezvous` | core | Spawn Welsh and start rendezvous objective |
| `Lincoln_ReinforceFlankAttackers` | core | Reinforce flank assault/guard modules every 10s if depleted |
| `Lincoln_SpawnFlankUnits` | core | Spawn hidden units to flank module via dynamic spawn |
| `Lincoln_PrepFieldArmy` | core | Count field army, start progress tracking, reveal FOW |
| `Lincoln_CheckFieldArmy` | core | Track field army destruction progress; complete when <5 remain |
| `Lincoln_CheckCityGateProx` | core | Transfer garrison to player, grant resources, start siege phase |
| `Lincoln_ReinforceAssault` | core | Periodically spawn besieger waves with escalating siege weapons |
| `Lincoln_AddSiegeWeapon` | core | Cycle through siege unit types for reinforcement waves |
| `Lincoln_LaunchFinalAttack` | core | Send FinalAttackers + RoyalGuard modules toward keep |
| `Lincoln_CheckRoyalGuard` | core | Remove Stephen's damage reduction when bodyguards depleted |
| `Lincoln_FinalAttackRetreat` | core | Force all final attackers to withdraw at threshold 2 |
| `Lincoln_BeginEndStage` | core | Make keep invulnerable, trigger mission complete |
| `Lincoln_TriggerBreachAlert` | core | Alert player when castle walls breached near keep |
| `Lincoln_CheckKeep` | core | Start DefendKeep objective when keep takes damage |
| `Lincoln_SetAdvanceWelshTargets` | core | Update Welsh armies to advance-phase waypoints |
| `Lincoln_SetFinalWelshTargets` | core | Update Welsh armies to final-phase waypoints |
| `Lincoln_DisbandWelsh` | core | Disband Welsh RovingArmy modules near castle |
| `Lincoln_GetWelshArchers` | core | Split Welsh into archers (walls) and spearmen (defenders) |
| `Lincoln_SpawnReinforcements1` | core | Spawn player reinforcements (archers, MaA, scouts) |
| `Lincoln_SpawnReinforcements2` | core | Spawn player cavalry reinforcements (26 knights) |
| `Lincoln_CheckMissionFail` | core | Fail mission if player has zero non-villager squads |
| `Lincoln_CheckStealthForestProx` | core | Track % of player units inside stealth forest |
| `Lincoln_CheckHoldPosition` | core | Track % of player units on hold/stand-ground stance |
| `Lincoln_SpawnContinuousUnitLine` | core | Spawn evenly-spaced units along a lerped line |
| `Lincoln_SpawnUnitLine` | core | Spawn units at numbered marker positions in a line |
| `Defeat_InitObjectives` | obj_defeat | Register all offensive objectives and sub-objectives |
| `DefeatArmy_StartCamps` | obj_defeat | Start camp clearing sub-objectives, init camp counts |
| `DefeatArmy_CheckCamps` | obj_defeat | Monitor all 3 camp populations; complete on empty |
| `DefeatArmy_CheckCamp` | obj_defeat | Progress bar + completion for a single camp |
| `DestroyTradePost_Check` | obj_defeat | Track trade post building destruction counter |
| `DefeatStephen_OnSquadKilled` | obj_defeat | Complete Stephen objective when his unit dies |
| `DefendKeep_Start` | obj_defend | Add hint point and start keep health check rule |
| `DefendKeep_Check` | obj_defend | Fail mission if keep entity count reaches 0 |
| `Welsh_InitObjectives` | obj_welsh | Register rendezvous and help-Welsh objectives |
| `Rendezvous_Check` | obj_welsh | Monitor player proximity to meeting point; detect Welsh under attack |
| `Rendezvous_HelpCheck` | obj_welsh | Track flank force kill progress; disband when <5 remain |
| `Rendezvous_SpawnWelshReinforcements` | obj_welsh | Reinforce Welsh army group if count drops below 15 |
| `Achievement_OnDamage` | core | Flag keep as damaged for achievement tracking |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_SetupAmbush` | Primary | Move all units to stealth forest and set stand ground |
| `SOBJ_MoveAllUnits` | Primary (sub) | Track % of units in stealth forest |
| `SOBJ_SetStandGround` | Primary (sub) | Track % of units on hold position |
| `OBJ_DestroyReinforcementGroups` | Primary | Eliminate all 3 enemy reinforcement columns |
| `SOBJ_DestroyReinforcementGroup1` | Primary (sub) | Eliminate first column |
| `SOBJ_DestroyReinforcementGroup2` | Primary (sub) | Eliminate second column |
| `SOBJ_DestroyReinforcementGroup3` | Primary (sub) | Eliminate final column |
| `OBJ_DestroyTradePost` | Primary | Destroy enemy market town buildings |
| `OBJ_Rendezvous` | Primary | Meet Welsh allies at meeting point |
| `OBJ_HelpWelsh` | Primary | Defeat flanking forces attacking Welsh |
| `OBJ_GainEntry` | Battle | Umbrella objective for entering Lincoln |
| `OBJ_RoutFieldArmy` | Battle (sub) | Break the blockade at castle gates |
| `OBJ_TakeControl` | Primary (sub) | Enter Lincoln city gate trigger |
| `OBJ_ClearCamps` | Primary | Defeat all 3 besieging siege camps |
| `SOBJ_ClearLeftCamp` | Primary (sub) | Clear western siege camp |
| `SOBJ_ClearMiddleCamp` | Primary (sub) | Clear central siege camp |
| `SOBJ_ClearRightCamp` | Primary (sub) | Clear eastern siege camp |
| `OBJ_DefeatStephen` | Primary | Capture/kill King Stephen |
| `OBJ_DefendKeep` | Information | Lincoln Keep must not fall (fail condition) |

### Difficulty

All values use `Util_DifVar({easy, normal, hard, hardest})`:

| Parameter | Easy | Normal | Hard | Hardest | Scales |
|-----------|------|--------|------|---------|--------|
| `enemy_bodyguardCount` | 5 | 5 | 8 | 12 | Horsemen guarding King Stephen |
| `enemy_siegeInterval` | 80 | 60 | 55 | 50 | Seconds between siege reinforcement waves |
| `enemy_fa_maa` | 6 | 8 | 12 | 15 | Men-at-arms per FinalAttacker module |
| `enemy_siege_max` | 1 | 2 | 3 | 4 | Max simultaneous siege engines across all besiegers |
| `enemy_besieger_count` | 5 | 6 | 8 | 10 | Base unit count per besieger wave |
| `enemy_siege_diff` | 1 | 1 | 2 | 3 | Index into `t_siege_distribution` (controls siege frequency) |
| `camp_defender_count` | 8 | 10 | 12 | 14 | Spearman/MaA defenders per siege camp position |

### Spawns

**Player Starting Forces:**
- 6 groups of 6 men-at-arms + 3 scouts, moved to stealth forest positions
- Garrison: 14 wall archers, ~23 villagers (farmers, miners, woodcutters)
- Archer lines: 2 continuous lines of 18 archers each with deployed palings

**Player Reinforcements:**
- `Lincoln_SpawnReinforcements1`: 10 archers + 5 MaA + 2 scouts, 20 MaA, 10 archers + 5 MaA (triggered by intel event)
- `Lincoln_SpawnReinforcements2`: 26 knights across 5 groups (triggered when trade post buildings < 3)

**Enemy Reinforcement Columns (ERG):**
- 3 columns of 4 sub-groups each, spawned sequentially during ambush phase
- Compositions escalate: Column 1 = mostly archers (4-5 per group); Column 2 = spearman+archer mixes; Column 3 = horseman+archer mixes
- Each sub-group marches along trade road waypoints; if reaching `mkr_trade_end`, column fails and merges into market defenders
- Speed modified to 0.8×

**Siege Camp Defenders:**
- Left camp: `camp_defender_count × 2` spearmen + `camp_defender_count × 2` MaA + 8 archer patrol + 16 line archers
- Middle camp: `camp_defender_count` spearmen + `camp_defender_count` MaA (×2 positions) + 16 line archers
- Right camp: `camp_defender_count × 2` spearmen (×2 positions) + 6 archer patrol + 16 line archers

**Besieger Waves:**
- 5 besieger modules cycle through `t_besiege_targets` attacking the keep
- Reinforced every `enemy_siegeInterval` seconds with escalating unit counts (`enemy_besieger_count + wave_count`, capped at 2×)
- Unit composition cycles: archer/archer → archer/spearman → archer/MaA → spearman/MaA
- Siege weapons cycle: ram → mangonel → siege_tower → mangonel → ram → mangonel → ram
- Distribution tables control siege spawn frequency per difficulty

**Final Attack:**
- 3 FinalAttacker modules: 5 archers + `enemy_fa_maa` MaA + 1 mangonel each
- 2 RoyalGuard modules: `enemy_bodyguardCount` horsemen each
- King Stephen (unique unit: `UNIT_KING_STEPHEN_CMP_ENG`) with 0.25× received damage until bodyguards drop below 50%

**Welsh Allies:**
- 3 RovingArmy modules (A/B/C): 10 archers + 15 spearmen each
- Reinforced with 4 archers + 6 spearmen if any group drops below 15
- Flank assault enemies: 3 groups of 8 archers each, reinforced every 10s

**Field Army:**
- 3 infantry lines of 20 spearmen each + 8 archer patrol + 1 springald
- Trade post guards: 2 groups of 10 spearmen + 8 archers each
- East patrol: 8 spearmen + 7 archers

### AI

- `AI_Enable(playerNeutral, false)` — disables AI for neutral citizens
- `PlayerUpgrades_Auto(player1, false)` — disables auto upgrades for player
- `PlayerUpgrades_Auto(playerStephen, false, {...})` — Stephen gets silk bowstring, spearman 3, archer 3 upgrades
- Garrison and Welsh learn all Feudal-age research/units
- All combat players get incendiary arrows upgrade
- Stephen also gets horseman 3 upgrade

**MissionOMatic Modules:**
- `GeneralGroup` (RovingArmy): King Stephen with 15 scan/combat/leash range
- `Besiegers1-5` (RovingArmy): Cycle-targeting, attack-everything toward keep
- `RoyalGuard1-2` (RovingArmy): Bodyguard horsemen with fallback retreat
- `FinalAttackers1-3` (RovingArmy): Archers+MaA+mangonel with fallback retreat
- `CampLeftDefend1`, `CampMiddleDefend1-2`, `CampRightDefend1-2` (Defend): Static camp defenders
- `LeftPatrol`, `RightPatrol` (RovingArmy): Archer patrols between camp waypoints
- `FieldPatrol` (RovingArmy): 8 archers patrolling field line
- `LineInfantry1-3` (Defend): 20 spearmen each in field army lines
- `FieldSiege` (Defend): 1 springald
- `TradePostGuards1-2` (Defend): Guard the market area
- `MarketPerimeter1-3` (Defend): Absorb surviving erg columns
- `FlankGuards1-3` (Defend): Block Welsh approach with infantry
- `FlankAssault1-3` (RovingArmy): Archers attacking Welsh, withdrawThreshold=0.2
- `EastPatrol` (RovingArmy): Spearman+archer patrol on east road
- `WelshArmyA-C` (RovingArmy): Allied Welsh columns, TARGETING_DISCARD
- `WelshDefenders` (Defend): Absorbs Welsh spearmen after disband
- `ERG1-3_1-4` (RovingArmy): Dynamically created reinforcement column sub-groups

### Timers

| Rule | Interval/Delay | Purpose |
|------|----------------|---------|
| `Lincoln_CheckEnemyReinforcements` | 1s interval | Monitor erg group progress, trigger spawns |
| `Lincoln_CheckTradePostProx` | 1s interval | Reveal FOW when player nears trade post |
| `Lincoln_CheckBridgeTrigger` | 2s interval | Start Welsh phase when player crosses bridge |
| `Lincoln_CheckStealthForestProx` | 1s interval | Track stealth forest unit placement |
| `Lincoln_CheckHoldPosition` | 1s interval | Track hold-position stance compliance |
| `Lincoln_CheckMissionFail` | 1s interval | Check for total player army loss |
| `Lincoln_ReinforceAssault` | `enemy_siegeInterval` (50-80s) | Spawn escalating besieger waves |
| `Lincoln_ReinforceFlankAttackers` | 10s interval | Reinforce flank forces attacking Welsh |
| `Lincoln_CheckFinalAttackTrigger` | 2s interval | Launch final attack when player nears trigger |
| `Lincoln_CheckKeep` | 2s interval | Start defend objective when keep damaged |
| `Lincoln_CheckFieldArmy` | 2s interval | Track field army destruction progress |
| `Lincoln_CheckFieldTriggerFinal` | 2s interval | Set final Welsh targets on field approach |
| `Lincoln_CheckCityGateProx` | 1s interval | Transfer garrison on city gate arrival |
| `Lincoln_CheckEastPatrolProx` | 2s interval | Redirect east patrol toward player |
| `DefeatArmy_CheckCamps` | 1s interval | Monitor all 3 siege camp populations |
| `DestroyTradePost_Check` | 1s interval | Track trade post building destroy counter |
| `DefendKeep_Check` | 1s interval | Fail if keep entity destroyed |
| `Rendezvous_Check` | 1s interval | Monitor Welsh proximity and under-attack state |
| `Rendezvous_HelpCheck` | 1s interval | Track flank force kill progress |
| `Lincoln_CheckWelshCastleTrigger` | 2s interval | Disband Welsh when near castle |
| `Lincoln_DisbandWelsh` | 25s one-shot | Disband Welsh army modules |
| `Lincoln_SetErgTargets1-3` | 0.5s one-shot | Set trade road waypoints for erg columns |
| `Lincoln_StartRendezvous` | 2s one-shot | Spawn Welsh and start rendezvous |
| `Lincoln_BeginEndStage → Lincoln_Complete` | 5s one-shot | Trigger mission victory |
| `Lincoln_StartDefendKeep` | 3s one-shot | Start defend keep objective after breach |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — core module system (RovingArmy, Defend, UnitSpawner, Prefab_DoAction)
- `training/campaigntraininggoals.scar` — shared campaign training predicates (`CampaignTraining_TimeoutIgnorePredicate`)
- `obj_defeat.scar`, `obj_welsh.scar`, `obj_defend.scar` — local objective files
- `ang_chp3_lincoln_data.scar`, `ang_chp3_lincoln_training.scar` — local data and training files

### Shared Globals / Systems
- `Util_DifVar` — difficulty scaling utility
- `Util_StartIntel` / `EVENTS` table — Intel/narrative event system
- `EventCues_CallToAction` — CTA notification system
- `SpawnUnitsToModule` — spawn units directly into a MissionOMatic module
- `RovingArmy_*` / `Defend_*` / `Prefab_DoAction` — MissionOMatic module APIs
- `UnitEntry_DeploySquads` with `dynamicSpawnType = DST_FURTHEST_HIDDEN` — hidden spawn system
- `PlayerUpgrades_Auto` / `PlayerUpgrades_LearnAllResearch` — shared upgrade utilities
- `Cardinal_EnablePartialXboxUI` — console UI management
- `SendReinforceNotification` — shared reinforcement notification helper
- `Music_*` / `Sound_*` — shared audio intensity and stinger system
- `SBP.ENGLISH.UNIT_KING_STEPHEN_CMP_ENG` — Stephen's unique blueprint
- `UPG.COMMON.*`, `UPG.ENGLISH.*` — shared upgrade blueprint constants

### Inter-File Function Calls
- `ang_chp3_lincoln.scar` calls `Lincoln_Data_Init()` (data), `Lincoln_InitTraining()` (training), `Defeat_InitObjectives()` (obj_defeat), `Welsh_InitObjectives()` (obj_welsh), `Defend_InitObjectives()` (obj_defend)
- `obj_defeat.scar` calls `Lincoln_BeginEndStage()`, `Lincoln_LaunchFinalAttack()`, `Lincoln_FinalAttackRetreat()`, `Lincoln_SpawnEnemyReinforcements()`, `Lincoln_ReinforceAssault()`, `Lincoln_StartWelshPhase()`, `Lincoln_PrepFieldArmy()`, `Lincoln_CheckCityGateProx()`, `Lincoln_Fail()`, `Lincoln_PlayWallaAtPosition()` (all in core)
- `obj_welsh.scar` calls `Lincoln_SetAdvanceWelshTargets()`, `Lincoln_ReinforceFlankAttackers()` (core)
- `obj_defend.scar` calls `Lincoln_Fail()` (core)

### Achievement
- `CE_ACHIEVDEFEATSIEGEOFLINCOLNEARLY` — unlocked if `defenseKeepDamaged == false` at mission end (keep never took damage)
