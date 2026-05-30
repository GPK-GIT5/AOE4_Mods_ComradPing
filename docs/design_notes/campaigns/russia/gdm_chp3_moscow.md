# Russia Chapter 3: Moscow

## OVERVIEW

Russia Chapter 3 ("Hold Against the Horde," 1382) is a multi-phase siege defense mission where the player (Muscovites) must prepare defenses, survive escalating Mongol attack waves, and then evacuate civilians from Moscow. The mission features a customized diplomacy/tribute UI repurposed as a "Request Aid" panel, allowing the player to call in vassal reinforcements from seven surrounding settlements. Gameplay progresses through a timed preparation phase, a finite wave-based Mongol assault tracked by a progress bar, a climactic Khan's Army arrival, and a final refugee evacuation objective. A failure countdown triggers whenever Mongol units penetrate the inner city walls, creating constant defensive pressure.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| gdm_chp3_moscow.scar | core | Main mission script: player setup, difficulty, variables, recipe, imports, gold trickle, Mongol wave generation, and resource-raider armies |
| diplomacy_chp3_moscow.scar | other | Customized diplomacy/tribute UI system adapted for the Request Aid vassal reinforcement panel |
| obj_mongolattacks.scar | objectives | OBJ_HoldAgainstTheHorde: manages Mongol invasion waves, progress tracking, outer city breach detection, and final Khan's Army |
| obj_moscowdefense.scar | objectives | OBJ_MoscowDefense: inner city breach detection with failure countdown timer |
| obj_prepare.scar | objectives | OBJ_Prepare: preparation timer, vassal reinforcement UI data and purchase callbacks |
| obj_refugees.scar | objectives | OBJ_Refugees: spawns fleeing civilians (intro and outro phases), tracks evacuation progress for mission completion |
| training_moscow3.scar | training | Tutorial hints for the diplomacy/reinforcement menu and wooden fortress garrisoning |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| Mission_SetupPlayers | gdm_chp3_moscow | Sets up 4 players, ages, relationships, colors |
| Mission_SetupVariables | gdm_chp3_moscow | Creates SGroups, leader, booleans, aid amounts, trickle vars |
| Mission_SetDifficulty | gdm_chp3_moscow | Defines t_difficulty table with Util_DifVar scaling |
| Mission_PreInit | gdm_chp3_moscow | Enables diplomacy/tribute panel before mission start |
| Mission_SetRestrictions | gdm_chp3_moscow | Removes monk conversion, relics, trade carts; upgrades Mongols |
| Mission_Preset | gdm_chp3_moscow | Registers all objectives, configures music intensity mapping |
| Mission_Start | gdm_chp3_moscow | Starts defense/prepare objectives, gold trickle, villagers, tutorials |
| GetRecipe | gdm_chp3_moscow | Returns MissionOMatic recipe with spawners and presentation |
| Mission_TrickleResources | gdm_chp3_moscow | Periodic gold income based on GOLD_TRICKLE_AMOUNT |
| Mission_VillagerSetup | gdm_chp3_moscow | Spawns and assigns villagers to farms/stone/wood |
| Init_MongolInvasion | gdm_chp3_moscow | Creates initial RovingArmy modules for first wave and raiders |
| NewMongolArmy | gdm_chp3_moscow | Spawns new Mongol wave with contextual unit comp |
| Get_MongolUnits | gdm_chp3_moscow | Generates normal-difficulty wave compositions by phase |
| Get_MongolUnitsStory | gdm_chp3_moscow | Generates simplified story-mode wave compositions |
| Emergency_Cleanup | gdm_chp3_moscow | Destroys unseen leftover Mongols after final wave |
| GetOutsideTarget | gdm_chp3_moscow | Finds nearest player entity/squad outside Moscow |
| UpdateWoodArmy | gdm_chp3_moscow | Retargets wood-raider army to nearest exterior target |
| UpdateStoneArmy | gdm_chp3_moscow | Retargets stone-raider army to nearest exterior target |
| NewWoodArmy | gdm_chp3_moscow | Respawns wood-raiding force after death (60s delay) |
| MongolAttack_FleeingCitizens | gdm_chp3_moscow | Spawns 3 blockade RovingArmies on escape route |
| PositionArchers | gdm_chp3_moscow | Distributes player archers across wall positions |
| Wispness | gdm_chp3_moscow | Random decorative wisp entity visibility toggle |
| Trebuchet_Intel | gdm_chp3_moscow | One-shot intel event for siege escalation |
| Tribute_Intel | gdm_chp3_moscow | One-shot intel event for tribute menu hint |
| Reinforcement_Intel | gdm_chp3_moscow | One-shot intel for vassal support with 300s cooldown |
| Diplomacy_DiplomacyEnabled | diplomacy_chp3_moscow | Initializes _diplomacy state table and data context |
| Diplomacy_Start | diplomacy_chp3_moscow | Registers network events, sets initial ages, creates UI |
| Diplomacy_SendTribute | diplomacy_chp3_moscow | Validates and sends tribute via network event |
| Diplomacy_SendTributeNtw | diplomacy_chp3_moscow | Processes tribute transfer, applies tax, fires callbacks |
| Diplomacy_OverrideSettings | diplomacy_chp3_moscow | Overrides tribute enabled/visible/score/team settings |
| Diplomacy_OverridePlayerSettings | diplomacy_chp3_moscow | Overrides per-player tribute visibility and resource toggles |
| Diplomacy_ShowDiplomacyUI | diplomacy_chp3_moscow | Forces diplomacy panel open or closed |
| Diplomacy_CreateUI | diplomacy_chp3_moscow | Builds XAML-based diplomacy/Request Aid panel |
| Diplomacy_UpdateDataContext | diplomacy_chp3_moscow | Refreshes all tribute enabled states and requirements |
| Diplomacy_GetTaxRate | diplomacy_chp3_moscow | Returns fixed 30% tax rate for tribute |
| MongolAttacks_InitializeObjectives | obj_mongolattacks | Registers OBJ_HoldAgainstTheHorde objective |
| MongolAttacks_OnStart | obj_mongolattacks | Starts invasion, wave timer, breach/progress checks |
| MongolAttacks_OuterCityBreached | obj_mongolattacks | Detects Mongols in outer city via metadata layer |
| MongolAttacks_OuterCityDestroyed | obj_mongolattacks | Triggers when 40% of outer buildings destroyed |
| MongolAttacks_CheckLastWaveFinished | obj_mongolattacks | Tracks progress bar; completes objective when all dead |
| MongolAttacks_HalfwayThere | obj_mongolattacks | Fires halfway intel event |
| Mongols_CTA | obj_mongolattacks | Call-to-action when player first sees Mongol army |
| DeclareFinalMongols | obj_mongolattacks | Defines random unit tables for final endless spawns |
| FinalMongols | obj_mongolattacks | Loop spawning infinite Mongol skirmish forces |
| Infinite_Mongols | obj_mongolattacks | Spawns one RovingArmy from random final compositions |
| BeginTheEnd | obj_mongolattacks | Deploys Khan's Army, starts final Mongol spawner |
| Init_KhansArmy | obj_mongolattacks | Spawns massive doom army (~196 squads) at spawn6 |
| Sgroup_FilterUnfinishedRams | obj_mongolattacks | Removes incomplete rams from squad group |
| Dip_Remind | obj_mongolattacks | Reminds player about diplomacy if army < 80 |
| MoscowDefense_InitializeObjectives | obj_moscowdefense | Registers OBJ_MoscowDefense and SOBJ_CountdownToFail |
| MoscowDefense_OnStart | obj_moscowdefense | Starts inner-city breach detection interval |
| MongolAttacks_BreachedUnits | obj_moscowdefense | Checks for Mongols inside inner city via metadata layer |
| MongolAttacks_StartCountdownToFailure | obj_moscowdefense | Starts failure countdown timer and CTA |
| MongolAttacks_CountdownToFailure | obj_moscowdefense | Fails mission if countdown reaches zero |
| MongolAttacks_StopCountdownToFailure | obj_moscowdefense | Cancels failure timer when breach cleared |
| MongolsInsideCTA | obj_moscowdefense | Call-to-action with cooldown for inner breach |
| MongolAttacks_CountBuildingsInOuterCity | obj_moscowdefense | Counts non-wall player buildings in outer city |
| Prepare_InitObjectives | obj_prepare | Registers OBJ_Prepare, SOBJ_Attack, reinforcement data |
| Attack_OnStart | obj_prepare | Starts preparation countdown; schedules refugees and attack |
| UI_ReinforcePanel_UpdateData | obj_prepare | Builds settlement data for Request Aid panel |
| UI_RequestAid_ButtonCallback | obj_prepare | Spawns purchased vassal units and triggers CTA |
| Start_CTACooldown | obj_prepare | Manages reinforcement arrival CTA with cooldown |
| Refugees_InitObjectives | obj_refugees | Registers OBJ_Refugees and SOBJ_MongolBlockade |
| Refugees_OnStart | obj_refugees | Begins outro refugee evacuation spawning |
| RefugeesIntro | obj_refugees | Spawns fleeing villagers entering Moscow (up to 50) |
| RefugeesOutro | obj_refugees | Spawns villagers fleeing out of Moscow to escape point |
| Track_RefugeeCount | obj_refugees | Tracks evacuation progress; completes mission when done |
| RefugeesRemaining | obj_refugees | Decrements count when refugee killed; respawns replacement |
| RampUpEndingDanger | obj_refugees | Releases Khan's Army restraints at 75% refugee spawn |
| EnsureFleeing | obj_refugees | Forces stopped refugees to resume moving |
| Refugee_FearWalla | obj_refugees | Plays panic SFX on random refugee at scaled intervals |
| Moscow3_Tutorials_Init | training_moscow3 | Activates reinforcement and wooden tower tutorials |
| MissionTutorial_Reinforce | training_moscow3 | Training goal sequence for diplomacy menu usage |
| MissionTutorial_WoodTower | training_moscow3 | Training goal sequence for garrisoning wooden fortresses |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| OBJ_MoscowDefense | Information | Keep Mongols out of inner city; fails mission on countdown expiry |
| SOBJ_CountdownToFail | Secondary (child) | Visible countdown timer when Mongols breach inner walls |
| OBJ_Prepare | Primary | Timed preparation phase before Mongol assault begins |
| SOBJ_Attack | Secondary (child) | Countdown timer showing time until Mongol arrival |
| OBJ_HoldAgainstTheHorde | Primary | Survive finite Mongol waves; progress bar tracks remaining |
| OBJ_Refugees | Primary | Hold city while civilians evacuate; progress bar tracks escaped count |
| SOBJ_MongolBlockade | Secondary (child) | Defeat Mongol blockade on escape route (commented-out logic) |
| OBJ_DebugComplete | Primary | Debug: skips to outro cinematic |

### Difficulty

All values indexed as `{Story, Easy, Intermediate, Hard}`:

| Parameter | Values | Scales |
|-----------|--------|--------|
| totalMongols | {300, 300, 400, 500} | Total Mongol squads across all waves |
| maxMongols | {60, 80, 120, 200} | Max simultaneous Mongol squads on field |
| mongolFrequency | {120, 120, 120, 90} | Seconds between wave spawn attempts |
| mongolMaxRams | {0, 3, 5, 8} | Max rams in wave compositions |
| timeTillFailure | {120, 60, 30, 30} | Seconds before inner breach causes failure |
| siegeWaves | {120, 120, 200, 240} | Threshold where siege units begin appearing |
| preperationTime | {420, 420, 300, 300} | Seconds of preparation before attack |
| escapingVillagers | {100, 100, 200, 300} | Number of refugees needed for evacuation victory |
| Starting resources | Gold: {1500,1000,500,0}, Wood: {5000,3000,2000,1000}, Food: {3000,2400,1200,600}, Stone: {1000,600,300,100} | Player starting economy |
| Villager count | {9, 8, 8, 8} | Villagers per resource gathering group |

### Spawns

**Preparation Phase:**
- Player starts with: Prince Dmitry, 10 monks, 20 MAA + 30 spearmen (infantry), 50 archers
- 4 groups of 8-9 villagers assigned to farms/stone/wood

**Mongol Main Waves (10 squads each, recurring):**
- Early (pre-siege threshold): 6 horse archers + 4 knights (or with khan); rams introduced after outer city breach
- Mid-siege: 6 horse archers + 3 knights + 1 mangonel
- Late-siege: 6 archers + 3 MAA + 1 traction trebuchet
- Story mode: simplified compositions (horsemen instead of knights, no siege)
- Resource raiders: 6 horse archers + 4 knights targeting wood/stone areas (disabled on Story)

**Khan's Army (final battle):**
- 50 MAA, 65 horse archers, 55 knights, 1 khan, 10 mangonels, 4 rams, 7 trebuchets, 4 siege towers
- Spawned at mkr_enemyspawn6 with 0.33x speed modifier, gradually released

**Final Infinite Mongols:**
- Random from: khan group (8 HA + 2 knights + 1 khan), mangonel group (6 HA + 4 knights + 2 mangonels), treb group (6 archers + 4 MAA + 1 treb)
- Cap: 20 + (refugeesSpawned/10), delay: 5 × (1 - refugeesSpawned/500) seconds
- Story mode: capped at 20, 15s delay

**Vassal Reinforcements (7 settlements via Request Aid):**
- Clin: 20 horsemen (+30 gold/min)
- Troitskoy: 30 archers (+40 gold/min)
- Pereslaw: 10 MAA + 30 spearmen (+50 gold/min)
- Susdal: 10 monks (+30 gold/min)
- Wlodimer: 30 spearmen (+35 gold/min)
- Kerisler: 15 knights (+55 gold/min)
- Colunma: 15 Streltsy (+60 gold/min)

**Refugees:**
- Intro: up to 50 villagers spawning at random exterior markers, moving into city
- Outro: up to `escapingVillagers` count spawning inside, fleeing to mkr_outro_departure
- 2% chance of trade cart instead of villager; random speed modifier (1.0x-2.0x)

### AI

- `AI_Enable(player4, false)` — Dmitry's downed-state player has no AI
- All Mongol armies use `RovingArmy` modules via MissionOMatic system
- `ARMY_TARGETING_DISCARD` — armies abandon targets once reached
- Resource raiders use `attackMoveStyle_ignoreEverything` en route, `attackMoveStyle_attackEverything` at target
- Wood/stone armies retarget to nearest exterior player assets via `GetOutsideTarget()`
- Khan's Army starts at 0.33x speed; constraint removed at 75% refugee evacuation via `RampUpEndingDanger()`
- Blockade armies (3 groups) positioned on escape route (CitizenBlockade1/2/3, partially commented out)

### Timers

| Timer/Rule | Timing | Purpose |
|------------|--------|---------|
| `Rule_AddInterval(NewMongolArmy, mongolFrequency)` | 90-120s | Spawns new Mongol attack wave |
| `Rule_AddOneShot(StartMongols, preperationTime)` | 300-420s | Ends preparation, starts Mongol assault |
| `Rule_AddOneShot(StartRefugees, prep-180)` | 120-240s | Begins intro refugee spawning before attack |
| `Rule_AddOneShot(Mission_TrickleResources, 5)` | 5s recurring | Gold trickle to player (GOLD_TRICKLE_AMOUNT/min) |
| `Objective_StartTimer(SOBJ_Attack, COUNT_DOWN, prep)` | 300-420s | Visible preparation countdown |
| `Objective_StartTimer(SOBJ_CountdownToFail, COUNT_DOWN, timeTillFailure, 15)` | 30-120s, warn at 15 | Failure countdown on inner breach |
| `Rule_AddInterval(MongolAttacks_BreachedUnits, 1)` | 1s | Monitors inner city for Mongol intrusion |
| `Rule_AddInterval(MongolAttacks_OuterCityBreached, 1)` | 1s | Monitors outer city breach via metadata layer |
| `Rule_AddInterval(MongolAttacks_CheckLastWaveFinished, 1)` | 1s | Updates progress bar; checks wave completion |
| `Rule_AddInterval(Track_RefugeeCount, 1)` | 1s | Tracks refugee evacuation progress |
| `Rule_AddOneShot(Dip_Remind, 20)` | 20s after breach | Reminds player about diplomacy/reinforcements |
| `Rule_AddOneShot(OnWoodArmyDeath → NewWoodArmy, 60)` | 60s | Respawns wood-raider army |
| `Rule_AddOneShot(ResetMongolsInsideCTA, 10)` | 10s | CTA cooldown for inner breach alarm |
| `Rule_AddOneShot(Reinforcement_Intel_Cooldown, 300)` | 300s | Allows reinforcement intel to replay |
| `Rule_AddInterval(Wispness, 4)` | 4s | Decorative wisp effect |
| `Rule_AddInterval(UI_ReinforcePanel_UpdateData, 1)` | 1s | Refreshes vassal reinforcement panel |
| `Rule_Diplomacy_UpdateUI` | 0.125s one-shot | Batched UI data context update |

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — provides RovingArmy_Init, MissionOMatic_InitializeModule, MissionOMatic_FindModule, SpawnUnitsToModule, Missionomatic_InitializeLeader
- `obj_moscowdefense.scar` — inner city defense objective
- `obj_mongolattacks.scar` — Mongol wave assault objective
- `obj_prepare.scar` — preparation phase and reinforcement UI
- `obj_refugees.scar` — refugee evacuation objective
- `diplomacy_chp3_moscow.scar` — customized tribute/diplomacy system
- `training_moscow3.scar` → `training/campaigntraininggoals.scar` — tutorial goal framework
- `gameplay/xbox_diplomacy_menus.scar` — conditional Xbox UI import

### Shared Globals
- `_diplomacy` — diplomacy state table shared between diplomacy_chp3_moscow and obj_prepare (buySettlements panel data injected into _diplomacy.data_context)
- `t_difficulty` — difficulty parameters accessed across all objective files
- `player1`–`player4` — player handles used in all files
- `GOLD_TRICKLE_AMOUNT` — updated by UI_ReinforcePanel_UpdateData when settlements are purchased
- `b_outerCityBreached`, `b_outerCity_Destroyed`, `b_innerwallBreached` — breach state flags read across obj_mongolattacks, obj_moscowdefense, gdm_chp3_moscow
- `b_endofMission`, `b_EndingComplete` — ending state flags
- `refugeesSpawned` — refugee count shared between obj_refugees and obj_mongolattacks (FinalMongols scaling)
- `maxTotalMongols` — total wave count set in gdm_chp3_moscow, read in obj_mongolattacks
- `sg_refugees`, `sg_khansarmy` — squad groups shared across files
- `EVENTS.*` — intel event constants (MongolDrums, OuterCityBreached, Halfway, MongolFinalFight_Part1/2/3, etc.)
- `g_leaderDmitry` — leader data struct (Missionomatic_InitializeLeader) for Prince Dmitry

### Inter-file Function Calls
- gdm_chp3_moscow calls: `MoscowDefense_InitializeObjectives()`, `Prepare_InitObjectives()`, `MongolAttacks_InitializeObjectives()`, `Refugees_InitObjectives()`, `Moscow3_Tutorials_Init()`, `Diplomacy_ShowUI()`, `Core_CallDelegateFunctions("DiplomacyEnabled")`
- obj_mongolattacks calls: `Init_MongolInvasion()` (in gdm_chp3_moscow), `MongolAttacks_CountBuildingsInOuterCity()` (in obj_moscowdefense), `Tribute_Intel()` (in gdm_chp3_moscow), `Diplomacy_ShowDiplomacyUI()` (in diplomacy)
- obj_prepare calls: `Diplomacy_ShowDiplomacyUI()`, `Diplomacy_UpdateUI()`, `UI_ReinforcePanel_UpdateData()` writes to `_diplomacy.data_context.buySettlements`
- obj_prepare calls: `RefugeesIntro()` (in obj_refugees) via `StartRefugees()`
- obj_refugees calls: `MongolAttacks_StopCountdownToFailure()`, `MongolAttacks_BreachedUnits` removal (from obj_moscowdefense)
- training_moscow3 reads: `_diplomacy.data_context.is_ui_expanded` for tutorial predicate
- `Core_RegisterModule("Diplomacy")` — hooks diplomacy lifecycle into Core framework callbacks
