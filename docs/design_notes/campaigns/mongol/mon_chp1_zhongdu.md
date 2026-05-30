# Mongol Chapter 1: Zhongdu

## OVERVIEW

Zhongdu (1215) is a two-phase Mongol campaign mission where the player controls Genghis Khan's forces besieging the Jin Dynasty capital. In Phase 1, the player must raid surrounding villages (Shunyi, Tongzhou, Daxing, Fangshan), destroy their markets to cut off supply caravans feeding Zhongdu's military strength, and accumulate gold to trigger reinforcement waves. In Phase 2, once supply lines are severed, Zhongdu's tower defenses are disabled and the player must breach the city walls and burn three landmarks (Spirit Way, Imperial Academy, Imperial Palace) to complete the mission. The mission features a dynamic raiding AI system that retaliates against the player, a supply caravan economy that fuels Jin counterattacks, a gold-based reinforcement mechanic that grants the player new units and buildings, and extensive tutorial/training elements for Genghis Khan's abilities and siege engineering.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| mon_chp1_zhongdu.scar | core | Main mission script: player setup, variables, restrictions, recipe, event handlers, raiding logic, intro/outro cinematics |
| obj_zhongdu_phase1.scar | objectives | Phase 1 objectives: supply tracking (OBJ_InfoSupply), trade route interdiction (SOBJ_StopTraders), city defense scaling |
| obj_zhongdu_phase2.scar | objectives | Phase 2 objectives: breach Zhongdu and burn three landmarks (SOBJ_Landmark_1/2/3), skirmisher AI monitoring |
| obj_zhongdu_secondary.scar | objectives | Secondary gold-hoarding objective (SOBJ_HoardGold) and reinforcement spawning system |
| training_zhongdu.scar | training | Tutorial sequences: sheep rally point hint, Genghis Khan fire arrow ability, siege engineers upgrade |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | mon_chp1_zhongdu | Initialize 3 players: Mongol, Jin, Neutral |
| Mission_SetupVariables | mon_chp1_zhongdu | Create groups, set difficulty vars, init raiding system |
| Mission_SetRestrictions | mon_chp1_zhongdu | Lock techs, remove outposts on easy, boost fire rates |
| Mission_Preset | mon_chp1_zhongdu | Register event rules, audio triggers, move intro units |
| Mission_Start | mon_chp1_zhongdu | Start OBJ_Raid, zero resources, setup wall archers |
| GetRecipe | mon_chp1_zhongdu | Define mission recipe with modules, garrisons, locations |
| Zhongdu_Intro_Parade | mon_chp1_zhongdu | Spawn and animate intro cavalry parade sequence |
| Zhongdu_OutroParade | mon_chp1_zhongdu | Spawn outro cinematic units and gold trade carts |
| Zhongdu_OnAbilityExecuted | mon_chp1_zhongdu | Track relic deposit events, ping minimap |
| Zhongdu_OnSquadKilled | mon_chp1_zhongdu | Trigger revenge raids on Jin squad deaths |
| Zhongdu_OnEntityKilled | mon_chp1_zhongdu | Trigger revenge raids on building destruction |
| Zhongdu_OnPlayerBreach | mon_chp1_zhongdu | Detect player entering Zhongdu, deactivate raiding |
| Zhongdu_AttackPlayerBase | mon_chp1_zhongdu | Periodically raid player villagers/traders on Hard+ |
| Zhongdu_OnIdleRaiders | mon_chp1_zhongdu | Redirect idle raid parties to player military |
| Zhongdu_GrowRaidSize | mon_chp1_zhongdu | Increment raid party size every 180s |
| Zhongdu_DelayScouting | mon_chp1_zhongdu | Enable raid scouting after 90s delay |
| Zhongdu_WarnAgainstCity | mon_chp1_zhongdu | Warn player approaching Zhongdu too early |
| Zhongdu_WatchForAgeUp | mon_chp1_zhongdu | Trigger Genghis Khan ability hint on age-up |
| Zhongdu_WatchForBlacksmith | mon_chp1_zhongdu | Trigger siege engineers hint on blacksmith built |
| Zhongdu_UpdateDefences | mon_chp1_zhongdu | Scale Zhongdu tower modifiers (damage, fire, armor) |
| Zhongdu_OnVillageDestroyed | mon_chp1_zhongdu | Escalate raids, boost party limit, play VO |
| Zhongdu_OnmapCaravan | mon_chp1_zhongdu | Spawn Jin supply caravans with escorts from villages |
| Zhongdu_TickSupplyCaravans | mon_chp1_zhongdu | Track caravan arrival, increment supply counter |
| Zhongdu_ExtraCleanup | mon_chp1_zhongdu | Remove excess supply units near Zhongdu center |
| Zhongdu_SetupMinimapPath | mon_chp1_zhongdu | Display trade route paths on minimap |
| Zhongdu_MonitorSkirmishers | obj_zhongdu_phase2 | Dissolve skirmish patrols into landmark defenders |
| Zhongdu_StagedVoLandmarks | obj_zhongdu_phase2 | Play sequential VO on landmark destruction |
| Zhongdu_InitObjectives_Phase1 | obj_zhongdu_phase1 | Register Phase 1 objectives and supply tracking |
| Zhongdu_InitObjectives_Phase2 | obj_zhongdu_phase2 | Register Phase 2 landmark objectives |
| ZhongduRaid_InitObjectives | obj_zhongdu_secondary | Register gold-hoarding and reinforcement objectives |
| Zhongdu_SpawnReinforcements | obj_zhongdu_secondary | Spawn villagers, buildings, and military as reward |
| MissionTutorial_Init | training_zhongdu | Initialize tutorial modal hover callback |
| Zhongdu_SetupSheepRallyHint | training_zhongdu | Create training sequence for pasture rally points |
| Zhongdu_TriggerGenghisHint | training_zhongdu | Detect Genghis Khan on-screen for ability hint |
| Zhongdu_TriggerSiegeEngineersHint | training_zhongdu | Detect blacksmith on-screen for siege upgrade hint |
| Predicate_UserHasSelectedGenghis | training_zhongdu | Check if player selected Genghis Khan |
| Predicate_UserHasLookedAtGenghisAbility | training_zhongdu | Check if player hovered over incendiary ability |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_Raid | Primary | Top-level Phase 1 wrapper; complete when SOBJ_HoardGold finishes |
| SOBJ_HoardGold | Optional (child of OBJ_Raid) | Track gold earned; every 250/500 gold triggers a reinforcement wave (4 stages total) |
| OBJ_InfoSupply | Information | Display Zhongdu military supply bar; triggers counterattacks when full |
| SOBJ_InfoSupply_Explaination | Information (child) | UI text: "Eliminate traders to stop attacks" |
| OBJ_StarveCity | Battle | Phase 1 combat objective; complete when all traders stopped |
| SOBJ_SecretTraderPings | Optional (secret, child) | Hidden sub-objective tracking trader status |
| SOBJ_StopTraders | Battle (child of OBJ_StarveCity) | Destroy 4 village markets to reach 100% progress |
| OBJ_EasyHint | Optional | Easy/Normal mode hint to place buildings near suggested locations |
| OBJ_PlunderCity | Primary | Phase 2: burn all 3 Zhongdu landmarks |
| SOBJ_Landmark_1 | Battle (child of OBJ_PlunderCity) | Burn Spirit Way landmark below 50% HP |
| SOBJ_Landmark_2 | Battle (child of OBJ_PlunderCity) | Burn Imperial Academy landmark below 50% HP |
| SOBJ_Landmark_3 | Battle (child of OBJ_PlunderCity) | Burn Imperial Palace landmark below 50% HP |
| OBJ_DebugComplete | Primary (hidden) | Debug cheat: instantly complete mission |

### Difficulty

| Parameter | Values (Easy/Normal/Hard/Expert) | Scales |
|-----------|----------------------------------|--------|
| g_guardsPrimary | 8 / 9 / 18 / 27 | Zhongdu main garrison squad count |
| g_guardsLandmarks | 5 / 6 / 12 / 18 | Landmark defender squad count |
| g_guardsSkirmish | 2 / 3 / 6 / 9 | Roving skirmisher patrol squad count |
| g_guardsWalls | 6 / 8 / 12 / 16 | Wall archer squad count |
| g_guardsTowns | 4 / 6 / 12 / 18 | Village garrison squad count |
| scoutTiming | 330 / 300 / 270 / 210 | Seconds before first raid scout |
| partySize | 4 / 4 / 6 / 9 | Initial raiding party squad count |
| raidTiming | 480 / 360 / 240 / 120 | Seconds between raid launches |
| escortHorsemen (scaling) | +2 / +2 / +4 / +7 | Convoy horseman escorts (scaled by progress ratio) |
| escortSpearmen (scaling) | +3 / +4 / +6 / +10 | Convoy spearman escorts (scaled by progress ratio) |
| escortArchers (scaling) | +5 / +6 / +9 / +12 | Convoy archer escorts (scaled by progress ratio) |
| Base hunt reset timer | 360 / 360 / 300 / 210 | Seconds between attacks on player base (Hard+ only) |

**Easy/Normal-specific adjustments:**
- All village outposts (BUILDING_DEFENSE_OUTPOST_CHI) removed
- Bridge at riverbend destroyed to limit attack angles
- OBJ_EasyHint shown after first reinforcement wave

**Expert-specific adjustments:**
- All outposts upgraded to Stone Outposts (UPGRADE_OUTPOST_STONE)

### Spawns

**Jin Supply Caravans:** Four trade routes originate from village markets (Shunyi, Tongzhou, Daxing, Fangshan), each spawning caravans at staggered intervals (g_supplyCartFrequency = 120s, spaced by 30s offsets). Each caravan consists of 1 supply cart + scaling military escort (horsemen, spearmen, archers). Caravans follow marker paths to Zhongdu; on arrival, they increment OBJ_InfoSupply.supplyCurrent. When supply reaches 100, a counterattack force (horsemen 50%, knights 30%, fire lancers 20%) raids the player.

**Player Reinforcements (SOBJ_HoardGold):** Triggered when gold threshold is met. Stage 1 (250 gold): 6 villagers + TC + pasture + house + up to 20 random military (3 compositions: horseman/spear/archer, MAA/crossbow, or knight/horse archer). Stages 2-4 (500 gold each): 6 villagers + 1 random production building + up to 20 military. Pop cap check prevents spawning if under 10 pop remaining.

**Enemy Garrisons (Recipe Modules):**
- GuardsZhongdu: Defend module at main garrison (spearmen 40%, archers 60%)
- GuardsLandmark1/2/3: Defend modules (MAA/ranged 45% each, monks 10%) with paired RovingArmy skirmisher patrols
- WallArchers1-6: UnitSpawner modules on walls (grenadiers/repeater crossbows/crossbowmen mix)
- Village guards: Militia + archers/repeater crossbows per village
- Road posts: Runners1 with withdraw-on-sight behavior, 3 WarningPosts, 1 WarningPatrol

### AI

- `AI_Enable(g_playerNeutral, false)` — Neutral player AI disabled
- **Raiding System** (`Raiding_Init`): Jin raids spawned from mkr_zhongdu_raid_spawn, despawn at mkr_scout_despawn. Composition: spearmen 40%, archers 60%. Features: probe scouting (sendProbes=true), party limit starts at 1, grows with village destruction (+1 per 2 villages). Idle raiders redirected via `Zhongdu_OnIdleRaiders`.
- **Revenge Raids**: Triggered on GE_SquadKilled and GE_EntityKilled events — raid sent to death location targeting nearby player units
- **Village Revenge**: Additional raid triggered when a village market is destroyed
- **Base Hunting** (Hard+ only): `Zhongdu_AttackPlayerBase` targets player villagers/trade carts periodically; timer resets after successful raid launch
- **Supply Counterattacks**: When OBJ_InfoSupply reaches 100%, a raid with horsemen/knights/fire lancers launches against the Khan's position
- **Skirmisher Reinforcement**: `Zhongdu_MonitorSkirmishers` dissolves roving patrols into landmark defenders when guards take casualties (<=90% ratio)
- **Wall Archers**: Hold position commands issued to 6 WallArcher modules at mission start

### Timers

| Rule | Timing | Purpose |
|------|--------|---------|
| Rule_AddInterval(Zhongdu_OnPlayerBreach) | 1s | Detect player entry into Zhongdu |
| Rule_AddInterval(Zhongdu_MonitorSkirmishers) | 1s | Check if landmark defenders need skirmisher support |
| Rule_AddInterval(Zhongdu_WatchForAgeUp) | 1s | Detect age-up to show Genghis ability hint |
| Rule_AddInterval(Zhongdu_WatchForBlacksmith) | 1s | Detect blacksmith to show siege engineers hint |
| Rule_AddInterval(Zhongdu_GrowRaidSize) | 180s | Increment raid party size (+1, up to 8 times) |
| Rule_AddOneShot(Zhongdu_DelayScouting) | 90s | Enable raid scouting after initial delay |
| Rule_AddInterval(Zhongdu_WarnAgainstCity) | 1s | Warn player if >2 units near Zhongdu perimeter |
| Rule_AddInterval(Zhongdu_AttackPlayerBase) | 1s | Countdown-based player base raids (Hard+, starts on first village destroyed) |
| Rule_AddInterval(Zhongdu_OnmapCaravan) — Shunyi | delay=0, interval=120s | Spawn Shunyi supply caravans |
| Rule_AddInterval(Zhongdu_OnmapCaravan) — Tongzhou | delay=60s, interval=120s | Spawn Tongzhou supply caravans |
| Rule_AddInterval(Zhongdu_OnmapCaravan) — Daxing | delay=90s, interval=120s | Spawn Daxing supply caravans |
| Rule_AddInterval(Zhongdu_OnmapCaravan) — Fangshan | delay=30s, interval=120s | Spawn Fangshan supply caravans |
| Rule_AddInterval(Zhongdu_EntryVO) | 1s | Detect player leaving start zone for VO trigger |
| Rule_AddOneShot(GenghisMove_Intro) | 12s | Move Genghis Khan to start position in intro |
| GE_AbilityExecuted | event | Track relic deposits |
| GE_SquadKilled | event | Track Jin squad kills for revenge raids + trader progress |
| GE_EntityKilled | event | Track Jin building kills for revenge raids |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — Core campaign framework (objective system, modules, leader system, recipe)
- `obj_zhongdu_secondary.scar` — Imported by main script for gold/reinforcement objectives
- `obj_zhongdu_phase1.scar` — Imported by main script for Phase 1 supply/trader objectives
- `obj_zhongdu_phase2.scar` — Imported by obj_zhongdu_phase1 for Phase 2 landmark objectives
- `training_zhongdu.scar` — Imported by main script for tutorial sequences
- `training.scar` — Base training framework (imported by training_zhongdu)
- `training/campaigntraininggoals.scar` — Campaign training goal definitions

### Shared Globals
- `g_playerMongol`, `g_playerJin`, `g_playerNeutral` — Player handles used across all files
- `g_leaderGenghisKhan` — Leader object initialized via `Missionomatic_InitializeLeader`, used in training and objectives
- `g_raidSystem` — Raiding system state, referenced in event handlers and village destruction
- `g_villagesDestroyed` — Counter incremented in Phase 1, affects supply cart strength and raid scaling
- `g_zhongduModifierList` — Tower modifier tracking for defense scaling
- `g_supplyCartStrength` — Supply value per caravan arrival, incremented on village loss
- `g_baseHuntingTimer` — Countdown timer for base hunting raids, modified by multiple events

### Inter-File Function Calls
- Main script calls `Zhongdu_InitObjectives_Phase1()`, `Zhongdu_InitObjectives_Phase2()`, `ZhongduRaid_InitObjectives()` during setup
- `SOBJ_HoardGold.IsComplete` calls `Zhongdu_SpawnReinforcements()` (obj_zhongdu_secondary)
- `SOBJ_StopTraders.IsComplete` calls `Zhongdu_OnVillageDestroyed()` (mon_chp1_zhongdu)
- `OBJ_StarveCity.OnComplete` starts `OBJ_PlunderCity` (cross-phase transition)
- `SOBJ_HoardGold.OnComplete` starts `OBJ_StarveCity` if not already started
- `Zhongdu_OnPlayerBreach` calls `Raiding_Dectivate()` and completes `OBJ_StarveCity`
- Training functions reference `g_leaderGenghisKhan.sgroup` from main script

### MissionOMatic Framework References
- `MissionOMatic_InitializeLeader` — Leader hero setup
- `MissionOMatic_FindModule` — Retrieve named recipe modules (GuardsLandmark, WallArchers, ZhongduSkirmish)
- `MissionOMatic_SGroupCommandDelayed` — Delayed move/attack-move commands
- `MissionOMatic_HintOnHover` / `MissionOMatic_HintOnHover_Xbox` — Training hint display
- `MissionOMatic_RevealMovingSGroup` — Fog-of-war reveal for caravans
- `MissionOMatic_SquadHasTag` — Tag-based squad filtering
- `Raiding_Init`, `Raiding_TriggerRaid`, `Raiding_SetScouting`, `Raiding_SetPartyLimit`, `Raiding_Dectivate`, `Raiding_ExtractAllSquads` — Raiding subsystem
- `DissolveModuleIntoModule` — Merge one module's units into another
- `RovingArmy_GetRemainingUnitRatio` — Check patrol unit losses
- `TrackTradeCartsForPlayers` — Enable trade cart monitoring
- `AudioTrigger_InitAreaTrigger` — Proximity-based music triggers
- `Training_Goal`, `Training_GoalSequence`, `Training_AddGoalSequence`, `Training_EnableGoalSequenceByID` — Tutorial framework
