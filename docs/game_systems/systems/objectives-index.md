# Objectives Index

Cross-reference of all objectives across campaign missions, extracted from Phase 3 summaries.

## Summary Statistics
- Total objectives: ~731
- By type: Primary ~220, Secondary/Sub ~280, Battle ~65, Information ~55, Optional ~45, Bonus ~40, Tip ~55, Capture ~25, Debug ~20, Other ~26

## By Campaign

### Abbasid Dynasty

#### abb_bonus
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DestroyLandmarks | Primary | — | Destroy 2 Rival Crusader landmarks; completes mission (with holy orders) |
| OBJ_SubdueHolyOrders | Capture | — | Parent: subdue all 3 Holy Order keeps; completes mission (with landmarks) |
| SOBJ_CaptureTemplarKeep | Capture (sub) | — | Capture the Templar Keep; awards Templar units and production |
| SOBJ_DefeatTemplarResistance | Battle (sub) | — | Defeat Templar defenders; merges them into army after 10s |
| SOBJ_LocationTemplarKeep | Capture (sub) | — | UI location marker for Templar Keep |
| SOBJ_CaptureTeutonKeep | Capture (sub) | — | Capture the Teutonic Keep; awards Teutonic units and production |
| SOBJ_DefeatTeutonResistance | Battle (sub) | — | Defeat Teutonic defenders; merges them into army after 10s |
| SOBJ_LocationTeutonKeep | Capture (sub) | — | UI location marker for Teutonic Keep |
| SOBJ_CaptureHospitallerKeep | Capture (sub) | — | Capture the Hospitaller Keep; awards Hospitaller units and production |
| SOBJ_DefeatHospitallerResistance | Battle (sub) | — | Defeat Hospitaller defenders |
| SOBJ_LocationHospitallerKeep | Capture (sub) | — | UI location marker for Hospitaller Keep (triggers merge after 10s) |
| OBJ_DestroyDocks | Optional | — | Destroy 3 Byzantine docks; counter-tracked |
| OBJ_EstablishTrade | Optional | — | Send trade unit near allies; unlocks mercenary reinforcement panel |

**Win condition:** Both OBJ_DestroyLandmarks and OBJ_SubdueHolyOrders complete → `Mission_Complete()`. Either can finish first.
**Lose condition:** Player has zero active landmarks → `Mission_Fail()`.

#### abb_m1_tyre
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_HorseArchers | Information (fail) | — | Horse archers must survive; triggers Mission_Fail if all die |
| OBJ_DefendLandmarks | Information (fail) | — | Landmarks must survive; superseded by OBJ_DefendTyre later |
| OBJ_DefendTyre | Information (fail) | — | Tyre Town Center must survive during final phase |
| OBJ_ClearCamps | Primary | — | Clear 4 Frankish camps (counter 0/4) |
| SOBJ_EliminateGuardsAndGatherers | Primary (sub) | — | Sub-objective of ClearCamps — eliminate guards and gatherers |
| OBJ_FranksGathering | Information | — | Tracks enemy resource accumulation toward attack threshold |
| OBJ_AssaultCountdown | Information | — | 360-second countdown while Franks construct "The Beast" |
| TOBJ_EnemyConstructing | Tip | — | Tip displayed during assault countdown |
| OBJ_PauseMenu | Tip | — | Suggests viewing pause menu for mission info |
| OBJ_AgeUp | Primary | — | Advance to Feudal Age (requires HoW + Wing) |
| OBJ_HouseOfWisdom | Primary (sub) | — | Build a House of Wisdom |
| OBJ_Wing | Primary (sub) | — | Build a Wing on the House of Wisdom |
| OBJ_PrepareForAttack | Primary | — | Prepare defenses — complete via harvest OR unit production |
| OBJ_BuildUpStockpile | Primary (sub) | — | Harvest 6000 resources total |
| OBJ_ProduceUnits | Primary (sub) | — | Reach 80 population |
| OBJ_DestroyRam | Battle | — | Destroy "The Beast" siege engine to win |
| SOBJ_RamHP | Primary (sub) | — | Progress bar showing ram remaining health |
| OBJ_DefendMole | Primary | — | Position army at the mole to defend Tyre |

**Win condition:** Destroy "The Beast" (OBJ_DestroyRam complete) → `Mission_Complete()`.
**Lose condition:** Player horse archers all dead OR player landmarks destroyed OR Tyre TC destroyed → `Mission_Fail()`.

#### abb_m2_egypt
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Alexandria | Information | — | Fail-state guard — if control_balance ≤ 0, calls Mission_Fail() |
| OBJ_ControlPrimary | Primary | — | Root objective — hold area; completes when all sub-objectives done → Mission_Complete() |
| OBJ_Control | TugOfWar_WithVelocity | — | Sub-objective tracking control_balance; completes at ≥ 1.0; displays held point counts |
| OBJ_Reinforcements | Primary | — | 90-second countdown timer for reinforcement waves |
| TOBJ_ControlPointTip | Tip | — | UI hint explaining control point mechanics (child of OBJ_Control) |

**Win condition:** `control_balance` reaches ≥ 1.0 (OBJ_Control completes, then OBJ_ControlPrimary completes) → `Mission_Complete()`.
**Lose condition:** `control_balance` drops to ≤ 0 (OBJ_Alexandria triggers) → `Mission_Fail()`.

#### abb_m3_redsea
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_TutNaval | Primary | — | Tutorial wrapper: build ships, fish, trade, fight — timed on Hard+ (300s) |
| SOBJ_TutFishingBoats | Sub | — | Build 3 fishing boats |
| SOBJ_TutFishing | Sub | — | Assign 3 fishing boats to gather food |
| SOBJ_TutTradeShips | Sub | — | Build 5 trade ships |
| SOBJ_TutTrading | Sub | — | Assign 5 trade ships to trade with allied dock |
| SOBJ_TutWarships | Sub | — | Build 3 Baghlahs (warships) |
| SOBJ_TutNavalCombat | Battle (sub) | — | Destroy intro Crusader ships |
| OBJ_AllyGold | Primary | — | Accumulate gold threshold (30k–35k) with allies |
| SOBJ_GoldCounter | Sub | — | Tracks/displays team gold progress toward threshold |
| SOBJ_ClearRaiders | Sub | — | Clear remaining raiders after gold threshold reached |
| TOBJ_TradeTip | Tip | — | Trade guidance (Easy/Story only) |
| OBJ_UnrestMeter | Unrest | — | Civil Unrest progress bar — reaches 1.0 = mission fail |
| TOBJ_UnrestTip | Tip | — | Unrest explanation tooltip |
| OBJ_RaidWaveIncoming | Battle | — | Countdown timer to next Crusader raid wave |
| OBJ_DemoRaiders | Information | — | Tracks approaching demolition ships with UI indicator |
| SOBJ_PirateHunt | Optional | — | Destroy pirate camp on island — resets unrest to 0 |
| TOBJ_PirateTip | Tip | — | Pirate hunt guidance |
| OBJ_BufferFinalWave | Information | — | Prep timer before Reynald's final assault (60–300s by difficulty) |
| SOBJ_NavyConstruction | Sub | — | Guidance: build 40 warships before finale (Easy/Story) |
| OBJ_FinalWave | Information | — | Defend 3 allied docks from Reynald — victory/failure condition |
| SOBJ_DockCounter | Sub | — | Tracks remaining allied docks (all destroyed = fail) |

**Win condition:** OBJ_FinalWave completes (Reynald's final assault defeated, all allied docks survive).
**Lose condition:** Civil Unrest reaches 1.0 (OBJ_UnrestMeter) OR all 3 allied docks destroyed (SOBJ_DockCounter).

#### abb_m4_hattin
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Tutorial | Primary | — | Tutorial umbrella: complete the burn-fields tutorial |
| SOBJ_FirstTutorialCombat | Primary (child) | — | Defeat first scout group (optionally after burning field) |
| SOBJ_SecondTutorialBurn | Primary (child) | — | Burn the large tutorial field to ≥25% |
| SOBJ_SecondTutorialRetreat | Primary (child) | — | Retreat all units to the pass marker |
| SOBJ_SecondTutorialCombat | Primary (child) | — | Defeat second scout group using crossbowmen + fire |
| OBJ_Crusaders | Primary | — | Main objective: defeat all Crusader waves, prevent Tiberias breach |
| SOBJ_WaveCounter | Primary (child) | — | Tracks waves killed vs total; completes parent when all dead + Reynald defeated |
| SOBJ_DefeatReynald | Primary (child) | — | Kill Reynald (spawns in wave 8, mid path) |
| TOBJ_PrepareForCrusaders | Tip (child) | — | Countdown timer before first wave (180/120/90/90s by difficulty) |
| TOBJ_BurnableFields | Tip (child) | — | Reminds player about burnable fields |
| SOBJ_PlacementGuidance | Bonus (child) | — | Place ≥15 military units at preparation marker (easy/medium only) |
| SOBJ_BuildTroops | Primary (child) | — | Train 20 additional military units |
| OBJ_NextWaveTimer | Information | — | Countdown to next crusader wave |
| OBJ_ProductionQueueGuidance | Information | — | Warning when production queue < 5 for > 60s |
| OBJ_FieldScoutingGuidance | Tip | — | Pings on all burnable field locations until observed |

**Win condition:** All Crusader waves defeated including Reynald (OBJ_Crusaders / SOBJ_WaveCounter + SOBJ_DefeatReynald complete) → `Mission_Complete()`.
**Lose condition:** Crusaders reach Tiberias → `Mission_Fail()`.

#### abb_m5_mansurah
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DummyBattle | Battle (secret) | — | Hidden objective for UI element anchoring |
| OBJ_DummyPrimary | Primary (secret) | — | Hidden objective for UI element anchoring |
| OBJ_SendForHelp | Primary | Phase 1 | Phase 1 goal: bring spy to messenger (parent) |
| OBJ_BringSpy | Primary | Phase 1 | Sub-objective: move spy to signal trigger proximity |
| OBJ_DefendMansurah | Information | Phase 2 | Phase 2 fail condition: all landmarks destroyed |
| OBJ_DestroyTheHeadquarters | Primary | Phase 2 | Phase 2 win condition: destroy enemy leader tent |
| OBJ_EliminateTheLeaders | Optional | Phase 2 | Kill all 3 Grand Masters (counter-tracked) |
| OBJ_GrandMasterTip | Tip | Phase 2 | "A Holy Order will flee if their leader is eliminated" |
| OBJ_BaybarsArrivingSoon | Optional | Phase 2 | Countdown timer (1500s) until Baybars arrives |

**Win condition:** Destroy the enemy headquarters (OBJ_DestroyTheHeadquarters complete) → `Mission_Complete()`.
**Lose condition:** All player landmarks destroyed (OBJ_DefendMansurah triggers) → `Mission_Fail()`.

#### abb_m6_aynjalut
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Dummy | Primary | — | Placeholder for UI element anchoring |
| OBJ_DummyBattle | Battle | — | Placeholder battle objective |
| OBJ_DefendTheVanguard | Information | Phase 1 | Keep Mamluk vanguard alive; counter tracks survivors; fails mission if all die |
| OBJ_WeakenTheEnemy | Battle | Phase 1 | Phase 1: weaken Mongol army before main force arrives |
| OBJ_UnitsKilled | Battle (child) | Phase 1 | Counter of enemy units eliminated (child of WeakenTheEnemy) |
| OBJ_DefeatTheEnemy | Battle | Phase 2 | Phase 2: defeat all 5 Mongol waves |
| OBJ_Waves | Primary (child) | Phase 2 | Counter: waves defeated out of 5 (child of DefeatTheEnemy); completes mission |
| OBJ_DefendAfula | Information | Phase 2 | Protect Afula villagers; fails mission if all die |
| OBJ_DefendTheVillagers | Primary (child) | Phase 2 | Counter of remaining villagers (child of DefendAfula) |
| OBJ_Reinforcements | Primary | — | Countdown timer to next reinforcement wave |

**Win condition:** All 5 waves defeated (OBJ_Waves counter reaches 5/5, completing OBJ_DefeatTheEnemy) → `Mission_Complete()`.
**Lose condition:** All vanguard units die (OBJ_DefendTheVanguard) OR all Afula villagers die (OBJ_DefendAfula) → `Mission_Fail()`.

#### abb_m7_acre
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefendSiegeCamp | OT_Information | — | Protect the Siege Camp; failure = mission loss (Mission_Fail) |
| OBJ_DestroyCrusaders | ObjectiveType_Primary | — | Destroy all Frankish Keeps; completion = mission win (Mission_Complete); counter tracks destroyed/total |
| OBJ_Genoese | ObjectiveType_Battle | — | 1291-second countdown timer; on expiry spawns Genoese crossbowmen fleet; tracks remaining Genoese count |

**Win condition:** All Frankish Keeps destroyed (OBJ_DestroyCrusaders complete) → `Mission_Complete()`.
**Lose condition:** Siege Camp destroyed (OBJ_DefendSiegeCamp) → `Mission_Fail()`.

#### abb_m8_cyprus
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefendLandmarks | Information (fail) | — | Player TC + HoW must survive; fails mission if both destroyed |
| OBJ_CaptureLimassol | Primary/Capture | Phase 1 | Capture Limassol town as first base; fails if all land units die |
| SOBJ_DefeatLimassolRebels | Capture (child) | Phase 1 | Defeat Limassol's garrison defenders |
| SOBJ_LocationLimassol | Capture (child) | Phase 1 | Capture the Limassol location zone |
| TOBJ_AvoidDestruction | Tip (child) | Phase 1 | Hint: avoid destroying Limassol buildings |
| OBJ_DestroyNicosia | Primary | Phase 2 | Destroy Nicosia TC + 2 Keeps to win mission |
| SOBJ_DestroyNicosia_TC | Primary (child) | Phase 2 | Destroy Nicosia's Town Center |
| SOBJ_DestroyNicosia_Keeps | Primary (child) | Phase 2 | Destroy both Nicosia Keeps (counter: 0/2) |
| OBJ_HouseOfWisdom | Optional | Phase 2 | Build a House of Wisdom (auto-starts after 120s if not begun) |
| OBJ_DestroyFamagusta | Battle | Phase 2 | Destroy 3 Genoese docks to stop naval raids |
| OBJ_DestroyKyrenia | Battle | Phase 2 | Destroy Kyrenia to stop cavalry reinforcements |
| SOBJ_DestroyKyrenia_TC | Battle (child) | Phase 2 | Destroy Kyrenia's Town Center |
| OBJ_Prisoners | Optional | Phase 2 | Liberate 3 prison camps (counter: 0/3) |

**Win condition:** Nicosia TC and both Keeps destroyed (OBJ_DestroyNicosia complete) → `Mission_Complete()`.
**Lose condition:** Both player TC and House of Wisdom destroyed (OBJ_DefendLandmarks) → `Mission_Fail()`.

---

### The Normans (Angevin)

#### ang_chp0_intro
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DevelopEconomy | Primary | Dark Age | Dark Age economy: gather food, produce villagers, build econ buildings |
| SOBJ_GatherFood | Sub | Dark Age | Gather 50 additional food |
| SOBJ_ProduceVillagers | Sub | Dark Age | Produce 5 villagers |
| SOBJ_BuildMill | Sub | Dark Age | Build 1 mill |
| SOBJ_GatherWood | Sub | Dark Age | Gather 50 additional wood |
| SOBJ_BuildLumberCamp | Sub | Dark Age | Build 1 lumber camp |
| SOBJ_BuildHouses | Sub | Dark Age | Build 3 houses |
| SOBJ_BuildFarms | Sub | Dark Age | Build 3 farms |
| OBJ_ExploreTheMap | Primary | Dark Age | Exploration: produce scout, find/mine gold |
| SOBJ_ProduceScouts | Sub | Dark Age | Produce 1 scout |
| SOBJ_FindGoldDeposit | Sub | Dark Age | Scout near a gold deposit |
| SOBJ_BuildMine | Sub | Dark Age | Build 1 mining camp |
| SOBJ_GatherGold | Sub | Dark Age | Gather 50 additional gold |
| OBJ_ProgressFeudalAge | Primary | Dark→Feudal | Age up to Feudal via Abbey of Kings landmark |
| SOBJ_AgeUpFeudal | Sub | Dark→Feudal | Build and complete the landmark |
| OBJ_LearnSpearman | Primary | Feudal | Build barracks, produce spearmen, destroy palisade |
| SOBJ_BuildBarrack | Sub | Feudal | Build 1 barracks |
| SOBJ_ProduceSpearmen | Sub | Feudal | Produce 10 spearmen |
| SOBJ_DestroyThePallisade | Sub | Feudal | Destroy French palisade wall |
| OBJ_AttackCavalryEncampment | Primary | Feudal | Attack-move tutorial + destroy cavalry encampment |
| SOBJ_AttackMove | Sub | Feudal | Use attack-move on a roving horseman |
| SOBJ_KillHorsemen | Sub | Feudal | Kill 6 horsemen at cavalry village |
| SOBJ_DestroyTheStables | Sub | Feudal | Destroy all cavalry encampment buildings |
| OBJ_AttackArchersEncampment | Primary | Feudal | Build stables, produce horsemen, destroy archery encampment |
| SOBJ_BuildStables | Sub | Feudal | Build 2 stables near designated area |
| SOBJ_ProduceHorsemen | Sub | Feudal | Produce 15 horsemen |
| SOBJ_KillArchers | Sub | Feudal | Kill all archers (progress bar) |
| SOBJ_DestroyTheArcheryEncampment | Sub | Feudal | Destroy archery encampment buildings |
| OBJ_AttackInfantryEncampment | Primary | Feudal | Build archery ranges, produce longbowmen, defeat spearmen |
| SOBJ_BuildArcheryRange | Sub | Feudal | Build 3 archery ranges near designated area |
| SOBJ_ProduceArchers | Sub | Feudal | Produce 20 longbowmen |
| SOBJ_SetupLongbowmenOnCliff | Sub | Feudal | Position 18+ longbowmen on clifftop |
| SOBJ_KillSpearman | Sub | Feudal | Kill enemy spearmen (progress bar) |
| OBJ_ProgressCastleAge | Primary | Feudal→Castle | Build White Tower landmark to win |
| SOBJ_AgeUpCastle | Sub | Feudal→Castle | Construct Castle Age landmark |
| OBJ_Tip_GatherFood | Tip | Dark Age | Tip: gather food |
| OBJ_Tip_ProduceVillagers | Tip | Dark Age | Tip: produce villagers |
| OBJ_Tip_BuildMill | Tip | Dark Age | Tip: build mill |
| OBJ_Tip_GatherWood | Tip | Dark Age | Tip: gather wood |
| OBJ_Tip_BuildFarms | Tip | Dark Age | Tip: build farms |
| OBJ_Tip_BuildHouses | Tip | Dark Age | Tip: build houses |
| OBJ_Tip_BuildLumberCamp | Tip | Dark Age | Tip: build lumber camp |
| OBJ_Tip_ProduceScout | Tip | Dark Age | Tip: produce scout |
| OBJ_Tip_FindGoldDeposit | Tip | Dark Age | Tip: find gold deposit |
| OBJ_Tip_BuildMine | Tip | Dark Age | Tip: build mine |
| OBJ_Tip_GatherGold | Tip | Dark Age | Tip: gather gold |
| OBJ_Tip_AgeUpFeudal | Tip | Dark Age | Tip: age up to Feudal |
| OBJ_Tip_AgeUpFeudalMoreVillagers | Tip | Dark Age | Tip: produce more villagers before aging |
| OBJ_Tip_NotEnoughFood | Tip | Feudal | Tip: not enough food |
| OBJ_Tip_NotEnoughWood | Tip | Feudal | Tip: not enough wood |
| OBJ_Tip_MakeMoreVillagers | Tip | Feudal | Tip: make more villagers |
| OBJ_Tip_doubleclickunits | Tip | Feudal | Tip: double-click to select unit type |
| OBJ_Tip_Attack | Tip | Feudal | Tip: attack |
| OBJ_Tip_BuildBarracks | Tip | Feudal | Tip: build barracks |
| OBJ_Tip_ProduceSpearmen | Tip | Feudal | Tip: produce spearmen |
| OBJ_Tip_BuildMultipleStables | Tip | Feudal | Tip: build multiple stables |
| OBJ_Tip_AttackMove | Tip | Feudal | Tip: attack-move |
| OBJ_Tip_BuildStables | Tip | Feudal | Tip: build stables |
| OBJ_Tip_ProduceHorsemen | Tip | Feudal | Tip: produce horsemen |
| OBJ_Tip_CombatVsCavalry | Tip | Feudal | Tip: combat vs cavalry counter |
| OBJ_Tip_CombatVsArchery | Tip | Feudal | Tip: combat vs archery counter |
| OBJ_TipBuildArcheryRange | Tip | Feudal | Tip: build archery range |
| OBJ_Tip_ProduceArchers | Tip | Feudal | Tip: produce archers |
| OBJ_Tip_SetupArchers | Tip | Feudal | Tip: setup archers on cliff |
| OBJ_Tip_CombatVsInfantry | Tip | Feudal | Tip: combat vs infantry counter |
| OBJ_Tip_AgeUpCastle | Tip | Feudal | Tip: age up to Castle |

**Win condition:** Build the White Tower landmark (Castle Age) to complete the mission.
**Lose condition:** None explicitly defined — this is a fixed-difficulty tutorial mission with no fail state.

#### ang_chp1_hastings
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefeatSaxons | Primary | Phases 2–5 | "Attack Harold's Army" — umbrella objective for all battle phases |
| SOBJ_Phase2_KillFyrd | Sub | Phase 2 | Kill the Fyrd from the shield wall (post-feign melee) |
| SOBJ_Phase3_UseArchers | Sub | Phase 3 | Use archers against enemy spearmen |
| SOBJ_Phase4_KillSpearmen | Sub | Phase 4 | Kill enemy spearmen to allow cavalry |
| SOBJ_Phase5_UseCavalry | Sub | Phase 5 | Use cavalry against enemy archers |
| OBJ_Feign | Primary | Phase 1→2 | Feign a retreat to lure Saxons from shield wall |
| OBJ_KillHarold | Primary | Final | Defeat King Harold — final objective |
| OBJ_Reinforcements | Information | — | Remaining reinforcement waves counter (progress bar) |
| OBJ_DebugComplete | Debug | — | Force mission complete |

**Win condition:** Kill King Harold to complete the mission.
**Lose condition:** All player units eliminated after limited reinforcements are exhausted (Story mode has unlimited reinforcements).

#### ang_chp1_york
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_ReclaimYork | Primary | — | Top-level mission objective — reclaim the city of York |
| SOBJ_BreachGates | Primary (sub) | — | Destroy a city gate or wall section to enter York |
| SOBJ_DestroyKeep | Primary (sub) | — | Reduce the rebel keep to below 0.5% health |
| OBJ_CaptureMiddlethorpe | Capture | — | Capture the village of Middlethorpe (first objective) |
| SOBJ_DefeatMiddlethorpeRebels | Capture (sub) | — | Defeat Middlethorpe's rebel defenders |
| SOBJ_LocationMiddlethorpe | Capture (sub) | — | Middlethorpe location marker |
| OBJ_CaptureFulford | Capture | — | Capture the village of Fulford (second village) |
| SOBJ_DefeatFulfordRebels | Capture (sub) | — | Defeat Fulford's rebel defenders |
| SOBJ_LocationFulford | Capture (sub) | — | Fulford location marker |
| OBJ_DevelopEconomy | Build | — | Build up economy after capturing Middlethorpe |
| SOBJ_BuildFarms | Build (sub) | — | Build 4 additional farms |
| SOBJ_AssignToWood | Build (sub) | — | Assign 5 villagers to chop wood |
| SOBJ_BuildHouses | Build (sub) | — | Build 2 additional houses |
| OBJ_BuildSupport | Build | — | Build up support for your army (after Fulford) |
| SOBJ_GatherResourcesForLandmark | Build (sub) | — | Gather 400 Food and 200 Gold for landmark |
| SOBJ_BuildLandmark | Build (sub) | — | Construct a landmark to advance to Feudal Age |
| SOBJ_BuildStable | Build (sub) | — | Build a stable to produce horsemen |
| OBJ_RepelAttack | Battle | — | Repel the initial Danish raid (timed countdown) |
| OBJ_StopDaneRaids | Optional | — | Stop the Danish raids (parent for two alternatives) |
| SOBJ_PayTribute | Optional (sub) | — | Send gold tribute to Danes (amount = difficulty-scaled) |
| SOBJ_DestroyCamp | Optional (sub) | — | OR destroy the Dane camp (7 buildings) |
| OBJ_DestroyCampAlt | Optional | — | Standalone Dane camp destroy (if discovered before raid) |
| OBJ_DebugComplete | Primary | — | Debug cheat objective — instantly completes mission |

**Win condition:** Destroy the rebel keep (reduce to below 0.5% health) after breaching the city gates.
**Lose condition:** No Town Center remaining or no military units remaining.

#### ang_chp2_bayeux
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Destroy | Primary | Siege | Burn Bayeux — parent objective for the siege phase |
| OBJ_Rams | Primary | Siege | Build Rams — parent for blacksmith/siege/build chain |
| SOBJ_Blacksmith | Sub | Siege | Build a Blacksmith building |
| SOBJ_SiegeEngineer | Sub | Siege | Purchase the Siege Engineers upgrade |
| SOBJ_BuildSiege | Sub | Siege | Use infantry to construct 3 rams (counter: X/3) |
| SOBJ_Breach | Sub | Siege | Breach the walls of Bayeux |
| SOBJ_BurnBuildings | Sub | Siege | Destroy Bayeux buildings (progress bar, completes at 75% damage) |
| SOBJ_Defenders | Sub | Siege | Defeat the city defenders (progress bar) |
| OBJ_CaptureVillage | Primary | Pre-siege | Capture the Wood Mill — prerequisite to siege phase |
| SOBJ_DefeatHamletRebels | Sub | Pre-siege | Defeat defenders at the Wood Mill |
| SOBJ_LocationHamlet | Sub | Pre-siege | Wood Mill location capture marker |
| OBJ_ControlGroups | Optional | — | Create control groups using CTRL+0-9 |
| SOBJ_CGArchers | Sub | — | Group only archers into a control group |
| SOBJ_CGSpears | Sub | — | Group only spearmen into a control group |
| OBJ_DebugComplete | Debug | — | Cheat objective to skip to mission complete |
| OBJ_VideoCapture | Debug | — | Video capture mode with full base/army spawn |

**Win condition:** Burn Bayeux to 75% damage AND defeat all city defenders.
**Lose condition:** All non-Henry player units die (pre-capture phase) or player base buildings destroyed (post-capture phase).

#### ang_chp2_bremule
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_FrenchAdvance | Primary/Battle | Phase 1 | Hold off the French advance |
| SOBJ_HoldingFleury | Sub/Battle | Phase 1 | Hold Fleury until King Henry arrives |
| SOBJ_ClearFleury | Sub/Battle | Phase 1 | Push remaining French out of Fleury |
| OBJ_DefeatTheFrench | Primary/Battle | Phase 2 | Stop King Louis rallying troops (win when ≤20 remain) |
| SOBJ_BurningBarn | Secondary | Phase 1 | Investigate the smoke |
| SOBJ_KingLouis_Title | Secret/Battle | Phase 2 | King Louis banner UI container |
| OBJ_Recapture | Optional | Phase 1→2 | Parent wrapper for village recapture |
| SOBJ_CaptureCressenville | Capture | Phase 1→2 | Retake Cressenville from French |
| SOBJ_DefeatCressenvilleRebels | Sub/Capture | Phase 1→2 | Push French out of Cressenville |
| SOBJ_LocationCressenville | Sub/Capture | Phase 1→2 | Cressenville location marker |
| SOBJ_CaptureGrainville | Capture | Phase 1→2 | Retake Grainville from French |
| SOBJ_DefeatGrainvilleRebels | Sub/Capture | Phase 1→2 | Push French out of Grainville |
| SOBJ_LocationGrainville | Sub/Capture | Phase 1→2 | Grainville location marker |
| OBJ_FuncKeys | Optional | Phase 2 | Teach F1–F4 quick-select (Normal or below) |
| SOBJ_F1 | Sub/Optional | Phase 2 | Select military buildings |
| SOBJ_F2 | Sub/Optional | Phase 2 | Select economy buildings |
| SOBJ_F3 | Sub/Optional | Phase 2 | Select research buildings |
| SOBJ_F4 | Sub/Optional | Phase 2 | Select landmark buildings |
| OBJ_DebugComplete_Min | Debug | — | Cheat: skip to victory (min defenders) |
| OBJ_DebugComplete_Mid | Debug | — | Cheat: skip to victory (mid defenders) |
| OBJ_DebugComplete_Max | Debug | — | Cheat: skip to victory (max defenders) |

**Win condition:** Defeat King Louis's army (≤20 French units remaining).
**Lose condition:** No town center remains.

#### ang_chp2_tinchebray
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefeatArmy | Primary | — | Defeat Robert and his followers (completes on both sub-objectives) |
| OBJ_DestroyVillages | Primary | Phase 1 | Destroy villages to lure out Robert's army |
| SOBJ_DestroyMartigny | Sub | Phase 1 | Destroy all buildings in Martigny (counter-tracked) |
| SOBJ_DestroyFrenes | Sub | Phase 1 | Destroy all buildings in Frenes (counter-tracked) |
| SOBJ_EliminateReinforcements | Sub | Phase 2 | Destroy the enemy relief army before it reaches the castle |
| SOBJ_EliminateArmy | Sub | Phase 2 | Eliminate Robert's field army (progress bar tracked) |
| SOBJ_CaptureRobert | Sub | Phase 2 | Capture Duke Robert Curthose |
| OBJ_DebugComplete | Debug | — | Skips to outro cinematic |

**Win condition:** Eliminate Robert's field army AND capture Duke Robert Curthose.
**Lose condition:** Player has no non-villager squads remaining.

#### ang_chp3_lincoln
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_SetupAmbush | Primary | Phase 1 | Move all units to stealth forest and set stand ground |
| SOBJ_MoveAllUnits | Primary (sub) | Phase 1 | Track % of units in stealth forest |
| SOBJ_SetStandGround | Primary (sub) | Phase 1 | Track % of units on hold position |
| OBJ_DestroyReinforcementGroups | Primary | Phase 1 | Eliminate all 3 enemy reinforcement columns |
| SOBJ_DestroyReinforcementGroup1 | Primary (sub) | Phase 1 | Eliminate first column |
| SOBJ_DestroyReinforcementGroup2 | Primary (sub) | Phase 1 | Eliminate second column |
| SOBJ_DestroyReinforcementGroup3 | Primary (sub) | Phase 1 | Eliminate final column |
| OBJ_DestroyTradePost | Primary | Phase 2 | Destroy enemy market town buildings |
| OBJ_Rendezvous | Primary | Phase 2 | Meet Welsh allies at meeting point |
| OBJ_HelpWelsh | Primary | Phase 2 | Defeat flanking forces attacking Welsh |
| OBJ_GainEntry | Battle | Phase 3 | Umbrella objective for entering Lincoln |
| OBJ_RoutFieldArmy | Battle (sub) | Phase 3 | Break the blockade at castle gates |
| OBJ_TakeControl | Primary (sub) | Phase 3 | Enter Lincoln city gate trigger |
| OBJ_ClearCamps | Primary | Phase 4 | Defeat all 3 besieging siege camps |
| SOBJ_ClearLeftCamp | Primary (sub) | Phase 4 | Clear western siege camp |
| SOBJ_ClearMiddleCamp | Primary (sub) | Phase 4 | Clear central siege camp |
| SOBJ_ClearRightCamp | Primary (sub) | Phase 4 | Clear eastern siege camp |
| OBJ_DefeatStephen | Primary | Phase 5 | Capture/kill King Stephen |
| OBJ_DefendKeep | Information | Phase 4–5 | Lincoln Keep must not fall (fail condition) |

**Win condition:** Capture/kill King Stephen after clearing all siege camps.
**Lose condition:** Player has zero non-villager squads remaining, or Lincoln Keep is destroyed.

#### ang_chp3_wallingford
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Defend | Primary/Battle | All | Fail if all player landmarks destroyed → Mission_Fail() |
| OBJ_Survive | Information | Defense | Countdown timer (600s) until Henry's reinforcements arrive |
| OBJ_DestroyOutposts | Primary/Battle | Counter-attack | Destroy 4 enemy camps; counter tracks progress (0/4) |
| OBJ_Eliminate_Units | Primary/Battle | Final | Defeat all remaining enemy units (progress bar) |
| OBJ_DebugComplete | Debug | — | Cheat to instantly complete mission |

**Win condition:** Destroy all 4 enemy outpost camps, then defeat all remaining converging enemy units.
**Lose condition:** All player landmarks destroyed.

#### ang_chp4_dover
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_HoldOffSiege | Primary/Battle | All siege | Hold off the French siege (parent for all siege waves); counter 0–4 |
| SOBJ_DefeatFrenchUnits | Battle (child) | Initial | Defeat the first French attack (kill-count or wipe attackers) |
| OBJ_SiegeStrength | Information | Ongoing | Displays enemy reinforcement level for next attack (progress bar) |
| SOBJ_IncomingWave1 | Information (child) | Wave 2 | Countdown timer before second French attack |
| SOBJ_RepelSiege1 | Battle (child) | Wave 2 | Defeat the second French attack |
| SOBJ_IncomingWave2 | Tip (child) | Wave 3 | Countdown timer before third French attack |
| SOBJ_RepelSiege2 | Battle (child) | Wave 3 | Defeat the third French attack |
| SOBJ_IncomingWave3 | Tip (child) | Final wave | Countdown timer before final French attack |
| SOBJ_RepelFrenchSiege | Battle (child) | Final wave | Defeat the final French attack |
| OBJ_DisruptFrench | Primary | Guerrilla | Disrupt French forces with Willikin (parent for guerrilla phase) |
| SOBJ_GatherArchersDoverTown | Primary (child) | Guerrilla | Use Willikin to gather longbowmen from Dover town |
| SOBJ_GatherArchersVillages | Primary (child) | Guerrilla | Gather longbowmen from 2 nearby villages (counter 0/2) |
| SOBJ_AmbushSiege | Primary (child) | Guerrilla | Ambush French siege weapons to weaken attacks |
| SOBJ_RecruitForestAllies | Optional | Guerrilla | Use Willikin to gather additional forest camp allies |
| SOBJ_ProduceTraders | Optional | Guerrilla | Produce additional traders (counter 0/3) |
| OBJ_DestroySiegeCamp | Optional | — | Destroy 4 French siege camp production buildings |
| OBJ_DebugComplete | Debug | — | Kills all French, destroys gates, completes mission |

**Win condition:** Repel all four siege waves (completing OBJ_HoldOffSiege after the final wave).
**Lose condition:** Dover Keep is destroyed.

#### ang_chp4_lincoln
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Reinforce1 | Information | Defense | 360s countdown — defend castle until William Marshal arrives |
| OBJ_DefendKeep | Information | All | Activated on first keep damage; mission fails if keep destroyed |
| OBJ_DefeatRebels | Primary | Counter-attack | Destroy all 6 rebel military production buildings (counter 0/6) |
| OBJ_DefeatFrench | Primary | Counter-attack | Destroy both French forts; parent of two sub-objectives |
| SOBJ_DestroyFortWest | Primary (sub) | Counter-attack | Destroy all buildings/outposts in Fort A (west/south); counter tracked |
| SOBJ_DestroyFortEast | Primary (sub) | Counter-attack | Destroy all buildings/outposts in Fort B (east); counter tracked |
| OBJ_DebugComplete | Primary (cheat) | — | Debug-only; triggers instant outro |

**Win condition:** Destroy all 6 rebel military production buildings AND destroy both French forts (Fort A and Fort B).
**Lose condition:** Keep is destroyed.

#### ang_chp4_rochester
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_CaptureVillage | Primary | Phase 1 | Capture the village of Chatham from rebels |
| SOBJ_DefeatHamletRebels | Sub | Phase 1 | Defeat Chatham garrison defenders |
| SOBJ_LocationHamlet | Sub | Phase 1 | Location capture tracker for Chatham |
| OBJ_DestroyRochester | Primary | Phase 2 | Destroy Rochester Keep (health ≤ 15%) |
| OBJ_RochesterSupply | Optional | Phase 2 | Cut off Rochester's supply lines |
| SOBJ_FlamingFarms | Sub | Phase 2 | Burn all Rochester farms (counter-tracked) |
| SOBJ_TroubledTrade | Sub | Phase 2 | Destroy 6 enemy trade carts |
| OBJ_SiegeTut | Optional | Phase 2 | Build trebuchets to breach Rochester (Easy/Normal only) |
| SOBJ_AgeUp | Sub | Phase 2 | Build a Landmark to age up |
| SOBJ_SiegeWorkshop | Sub | Phase 2 | Build a Siege Workshop |
| SOBJ_Trebuchets | Sub | Phase 2 | Construct 3 trebuchets (counter: 0/3) |
| OBJ_DebugComplete | Debug | — | Kills outro entities and completes mission |

**Win condition:** Reduce Rochester Keep health to ≤ 15%.
**Lose condition:** Not explicitly defined in the summary (implied mission fail on total loss).

---

### Art of War Challenges

#### challenge_advancedcombat
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| _challenge.victory.objectiveVictory | OT_Primary | — | Defend camp against all 6 enemy attacks (counter: 0/6) |
| _challenge.victory.objectiveVictory2 | OT_Primary | — | Do not let the enemy burn down the village |
| _challenge.objective.surviveWave1 | OT_Bonus | — | Defeat approaching men-at-arms (wave 1) |
| _challenge.objective.surviveWave2 | OT_Bonus | — | Defeat approaching crossbowmen (wave 2) |
| _challenge.objective.surviveWave3 | OT_Bonus | — | Defeat approaching knights (wave 3) |
| _challenge.objective.surviveWave4 | OT_Bonus | — | Defeat approaching spearmen + crossbowmen (wave 4) |
| _challenge.objective.surviveWave5 | OT_Bonus | — | Defeat approaching men-at-arms + horsemen (wave 5) |
| _challenge.objective.surviveWave6 | OT_Bonus | — | Defeat approaching archers + knights (wave 6) |
| _challenge.objective.trainWave1–6 | ObjectiveType_Information | — | Prompt to train 1 or 2 unit groups |
| _challenge.objective.protectTown | OT_Bonus | — | Track buildings lost (counter: 0/7, fail at 7) |
| _challenge.benchmarks.gold.objective | OT_Bonus | — | Lose fewer than 15 units (18 on Xbox) |
| _challenge.benchmarks.silver.objective | OT_Bonus | — | Lose fewer than 30 units (35 on Xbox) |
| _challenge.benchmarks.bronze.objective | OT_Bonus | — | Lose fewer than 40 units (45 on Xbox) |
| _challenge.benchmarks.unplaced.objective | OT_Bonus | — | No medal — exceeds bronze threshold |

**Win condition:** All 6 enemy waves defeated (objectiveVictory counter reaches 6/6).
**Lose condition:** Village burns down — 7 buildings destroyed (objectiveVictory2 fails).

#### challenge_agincourt
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Victory | OT_Primary | — | Defeat all 3 French Divisions (count-up timer) |
| OBJ_Army | Sub-objective | — | French Strength tracker (not always started) |
| SOBJ_Defend | OT_Secondary | — | Defend Capital Town Center (failure = TC destroyed) |
| OBJ_ConquerorMedal | OT_Bonus | — | Defeat strengthened French army (conqueror mode) |
| OBJ_GoldMedal | OT_Bonus | — | Complete within 16 minutes |
| OBJ_SilverMedal | OT_Bonus | — | Complete within 20 minutes (registered after gold fails) |
| OBJ_BronzeMedal | OT_Bonus | — | Complete the challenge (registered after silver fails) |
| SOBJ_AttackWave1 | OT_Secondary | — | Attack the French Vanguard (8 min countdown) |
| SOBJ_AttackWave2 | OT_Secondary | — | Attack the Main French Division (8:30 countdown) |
| SOBJ_AttackWave3 | OT_Secondary | — | Defeat the Remaining French Army |
| SOBJ_AttackWave1Strength | OT_Information | — | Tug-of-war bar: player vs. Wave 1 resource cost |
| SOBJ_AttackWave2Strength | OT_Information | — | Tug-of-war bar: player vs. Wave 2 resource cost |
| SOBJ_AttackWave3Strength | OT_Information | — | Tug-of-war bar: player vs. Wave 3 resource cost |
| OBJ_Conqueror | OT_Bonus | — | Attack vanguard within 5 min for greater challenge |
| SOBJ_W1LeaderRally | OT_Information | — | Battlefield Promotion indicator (progress bar) |

**Win condition:** All 3 French Divisions (Vanguard, Main, Reserves) destroyed.
**Lose condition:** Capital Town Center is destroyed.

#### challenge_basiccombat
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| _challenge.victory.objectiveVictory | OT_Primary | — | Defend camp against all 5 enemy attacks (counter: 0/5) |
| _challenge.victory.objectiveVictory2 | OT_Primary | — | Do not let the enemy burn down the village |
| _challenge.objective.surviveWave1 | OT_Bonus | — | Defeat approaching horsemen (wave 1) |
| _challenge.objective.surviveWave2 | OT_Bonus | — | Defeat approaching spearmen (wave 2) |
| _challenge.objective.surviveWave3 | OT_Bonus | — | Defeat approaching archers (wave 3) |
| _challenge.objective.surviveWave4 | OT_Bonus | — | Defeat approaching spearmen + horsemen (wave 4) |
| _challenge.objective.surviveWave5 | OT_Bonus | — | Defeat approaching archers + horsemen (wave 5) |
| _challenge.objective.protectTown | OT_Bonus | — | Track buildings lost (counter: 0/7, fail at 7) |
| _challenge.benchmarks.gold.objective | OT_Bonus | — | Lose fewer than 16 units (19 on Xbox) |
| _challenge.benchmarks.silver.objective | OT_Bonus | — | Lose fewer than 21 units (26 on Xbox) |
| _challenge.benchmarks.bronze.objective | OT_Bonus | — | Lose fewer than 36 units (41 on Xbox) |
| _challenge.benchmarks.unplaced.objective | OT_Bonus | — | No medal — exceeds bronze threshold |

**Win condition:** All 5 enemy waves defeated (objectiveVictory counter reaches 5/5).
**Lose condition:** Village burns down — 7 buildings destroyed (objectiveVictory2 fails).

#### challenge_earlyeconomy
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| _challenge.victory.objectiveVictory | OT_Primary | — | Prepare to advance to the Feudal Age (parent objective) |
| _challenge.victory.objectiveVillagers | OT_Primary (sub) | — | Train additional villagers (counter: 0/21) |
| _challenge.victory.objectiveFood | OT_Primary (sub) | — | Gather food (counter: 0/landmark food cost) |
| _challenge.victory.objectiveGold | OT_Primary (sub) | — | Gather gold (counter: 0/landmark gold cost) |
| _challenge.victory.objectiveLandmark | OT_Primary (sub) | — | Begin construction of a Landmark |
| _challenge.secondary.objectiveVictory | OT_Secondary | — | Build up a base (parent for secondary subs) |
| _challenge.secondary.objectiveFirstHouse | OT_Secondary (sub) | — | Build a House (triggered at 8+ population) |
| _challenge.secondary.objectiveMill | OT_Secondary (sub) | — | Build a Mill (triggered at 12+ villagers) |
| _challenge.secondary.objectiveEcoTech | OT_Secondary (sub) | — | Research Survival Techniques (after first mill) |
| _challenge.secondary.objectiveMiningCamp | OT_Secondary (sub) | — | Build a Mining Camp (triggered at 9+ villagers) |
| _challenge.secondary.objectiveLumberCamp | OT_Secondary (sub) | — | Build a Lumber Camp (triggered at 10+ pop or wood < 100) |
| _challenge.benchmarks.gold.objective | OT_Bonus | — | Gold medal: complete within 5m10s (5m20s Xbox) |
| _challenge.benchmarks.silver.objective | OT_Bonus | — | Silver medal: complete within 6m00s (6m30s Xbox) |
| _challenge.benchmarks.bronze.objective | OT_Bonus | — | Bronze medal: complete within 7m30s (8m00s Xbox) |
| _challenge.benchmarks.unplaced.objective | OT_Bonus | — | No medal — time elapsed display only |

**Win condition:** All primary sub-objectives completed (21 villagers trained, food/gold gathered, landmark construction begun).
**Lose condition:** None explicit — pure economy tutorial with no fail state.

#### challenge_earlysiege
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| _challenge.victory.objectiveVictory | OT_Primary | — | Defeat the Rus (completes when both key buildings destroyed) |
| _challenge.victory.objectiveSub1 | OT_Secondary | — | Destroy the Rus Town Center |
| _challenge.victory.objectiveSub2 | OT_Secondary | — | Destroy the Kremlin Landmark |
| _challenge.benchmarks.gold.objective | OT_Bonus | — | Gold medal — complete within 6 min (7 min Xbox) |
| _challenge.benchmarks.silver.objective | OT_Bonus | — | Silver medal — complete within 10 min (12 min Xbox) |
| _challenge.benchmarks.bronze.objective | OT_Bonus | — | Bronze medal — complete within 20 min (both platforms) |
| _challenge.benchmarks.unplaced.objective | OT_Bonus | — | Time elapsed display — no medal tier |
| _challenge.victory.failedMedals | OT_Information | — | Shown when medals forfeited due to reinforcements |

**Win condition:** Both the Rus Town Center and Kremlin Landmark are destroyed.
**Lose condition:** No explicit defeat — if all player units lost and cannot produce more, reinforcements spawn (medals forfeited).

#### challenge_lateeconomy
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| _challenge.victory.objectiveVictory | OT_Primary | — | Build a booming economy (parent; completes when all subs done) |
| _challenge.victory.objectiveVillagers | OT_Secondary | — | Train 80 villagers (counter tracked, reverts if count drops) |
| _challenge.victory.objectiveTraders | OT_Secondary | — | Train 30 traders (counter tracked, reverts if count drops) |
| _challenge.victory.objectiveLandmark | OT_Secondary | — | Build Imperial Age landmark |
| _challenge.secondary.objectiveVictory | OT_Secondary | — | Expand your base (parent for secondary subs) |
| _challenge.secondary.objectiveSecondTownCenter | OT_Secondary (sub) | — | Build a second Town Center |
| _challenge.secondary.objectiveAddTownCenters | OT_Secondary (sub) | — | Build 4 total Town Centers |
| _challenge.secondary.objectiveAddMarkets | OT_Secondary (sub) | — | Build 4 total Markets |
| _challenge.secondary.objectiveAddHouses | OT_Secondary (sub) | — | Build houses until pop usage < 85% |
| _challenge.secondary.objectiveAddFarms | OT_Secondary (sub) | — | Build 20 total farms |
| _challenge.secondary.objectiveResearchTechs | OT_Secondary (sub) | — | Research 3 economic technologies |
| _challenge.benchmarks.gold.objective | OT_Bonus | — | Gold medal: complete within 10m30s (10m45s Xbox) |
| _challenge.benchmarks.silver.objective | OT_Bonus | — | Silver medal: complete within 15m30s (16m00s Xbox) |
| _challenge.benchmarks.bronze.objective | OT_Bonus | — | Bronze medal: complete within 19m30s (20m00s Xbox) |
| _challenge.benchmarks.unplaced.objective | OT_Bonus | — | No medal — no time limit |

**Win condition:** 80 villagers trained, 30 traders trained, and Imperial Age landmark constructed.
**Lose condition:** Player annihilation — no squads remaining and cannot produce more.

#### challenge_latesiege
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| objectiveVictory | OT_Primary | — | Defeat the Holy Roman Empire (all 3 buildings destroyed) |
| objectiveSub1 | OT_Secondary | — | Destroy HRE Town Center |
| objectiveSub2 | OT_Secondary | — | Destroy Aachen Chapel Landmark |
| objectiveSub3 | OT_Secondary | — | Destroy Regnitz Cathedral Landmark |
| benchmarks.gold.objective | OT_Bonus | — | Gold medal — complete within 6 min (7 Xbox) |
| benchmarks.silver.objective | OT_Bonus | — | Silver medal — complete within 9 min (10 Xbox) |
| benchmarks.bronze.objective | OT_Bonus | — | Bronze medal — complete within 15 min (16 Xbox) |
| benchmarks.unplaced.objective | OT_Bonus | — | Time Elapsed — no medal, count-up timer |
| failedMedals | OT_Information | — | Shown after reinforcements forfeit all medals |

**Win condition:** All 3 buildings destroyed (Town Center, Aachen Chapel, Regnitz Cathedral).
**Lose condition:** No explicit defeat — reinforcements spawn on total army loss (medals forfeited).

#### challenge_malian
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Victory | OT_Primary | — | Collect gold — ends when all mines destroyed |
| OBJ_AmbushWaves | OT_Battle | — | Ambush incoming enemy waves |
| OBJ_DefendMines | OT_Battle | — | Defend the three gold pit mines |
| OBJ_PrepareForAmbush | Capture | — | Pre-mission: capture 2 path positions to start waves |
| SOBJ_Path1 | Capture | — | Position units at path 1 capture point |
| SOBJ_Path2 | Capture | — | Position units at path 2 capture point |
| OBJ_Recruit | Optional | — | Use the reinforcement panel to purchase units |
| SOBJ_RecruitPanel | Optional | — | Open the diplomacy/reinforcement panel |
| benchmarks.unplaced.objective | OT_Bonus | — | No medal — collect 3000 gold (2500 Xbox) |
| benchmarks.bronze.objective | OT_Bonus | — | Bronze medal — collect 4500 gold (4000 Xbox) |
| benchmarks.silver.objective | OT_Bonus | — | Silver medal — collect 7000 gold (6500 Xbox) |
| benchmarks.gold.objective | OT_Bonus | — | Gold medal — collect 7000 gold (6500 Xbox); sends CE_MALIANSARTGOLD |

**Win condition:** Collect as much gold as possible; medals awarded based on total gold collected when all 3 pit mines are destroyed.
**Lose condition:** All 3 gold pit mines are destroyed (ends the mission; score determines medal).

#### challenge_montgisard
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_SacredSitesPrimary | OT_Primary | — | Capture all 4 Sacred Sites (counter: 0–4) |
| SOBJ_SacredSitesTip | Tip | — | UI hint about Sacred Sites mechanics |
| SOBJ_SacredSitesTip_Build | Tip | — | UI hint about building near sites |
| OBJ_DefendTC | OT_Information | — | Fail mission if starting TC is destroyed |
| OBJ_PointsOfInterest | Optional | — | Complete 6 POIs (counter 0–6) for ally army reward |
| OBJ_ConquerorMode | OT_Bonus | — | Two-phase conqueror unlock timer |
| OBJ_ConquerorMedal | OT_Bonus | — | Complete all sites within 25 min in Conqueror Mode |
| OBJ_GoldMedal | OT_Bonus | — | Capture all sites within 17 minutes (count-up timer) |
| OBJ_SilverMedal | OT_Bonus | — | Capture all sites within 25 minutes |
| OBJ_BronzeMedal | OT_Bonus | — | Capture all sites within 60 minutes |
| OBJ_ConquerorTip | OT_Battle | — | Placeholder for Conqueror Mode UI |

**Win condition:** All 4 Sacred Sites captured by the player.
**Lose condition:** Starting Town Center is destroyed.

#### challenge_ottoman
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_VizierBonus | OT_Primary | — | Choose a Vizier Bonus before waves begin |
| OBJ_Defend | OT_Primary | — | Defend your town center |
| OBJ_Survive | OT_Primary | — | Survive as long as you can (count-up timer) |
| SOBJ_AttackNotice | OT_Battle (secret) | — | Hidden objective for attack wave UI indicators |
| SOBJ_BronzeMedal | OT_Bonus | — | Survive 10 minutes (8 min Xbox); chains to Silver |
| SOBJ_SilverMedal | OT_Bonus | — | Survive 15 minutes (12 min Xbox); chains to Gold |
| SOBJ_GoldMedal | OT_Bonus | — | Survive 21 minutes (16 min Xbox); sends CE_OTTOMANSARTGOLD |

**Win condition:** Survive as long as possible; medals awarded at time thresholds (Bronze 10min, Silver 15min, Gold 21min).
**Lose condition:** Town Center landmark is destroyed.

#### challenge_safed
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_SaveFortressPrimary | OT_Primary | — | Save the Fortress of Safed from falling |
| OBJ_SaveFortressProgressBar | OT_Information | — | Displays fortress health percentage as a progress bar |
| OBJ_Tip_SaveVillagers | Tip | — | Reminder to protect villagers; disappears when all stone mined |
| OBJ_Bonus_ConqMode | OT_Bonus | — | Hints at conqueror mode; completes/updates when CM activates or fails |
| SOBJ_SecureStone | Capture (sub) | — | Mine stone at 4 deposits (counter: 0/4) |
| SOBJ_LocationSecureStone | Build (sub) | — | Stone Bounty UI marker on map for current mine location |
| SOBJ_StopBombardment | OT_Battle (sub) | — | Clear the enemy siege camp (triggered on all stone mined) |
| SOBJ_LocationStopBombardment | OT_Battle (sub) | — | Clear the siege camp location marker with progress bar |

**Win condition:** Mine all 4 stone deposits and clear the enemy siege camp to stop bombardment.
**Lose condition:** Fortress of Safed is destroyed, or all player villagers die.

#### challenge_towton
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Victory | OT_Battle | — | Defend against Yorkist attacks (countdown timer to final wave) |
| OBJ_Towns | OT_Battle | — | Allied Buildings Remaining (progress bar counter) |
| SOBJ_Defend | OT_Battle | — | Lancaster Stronghold (landmark) must survive |
| OBJ_ConquerorMedal | OT_Bonus | — | Conqueror Medal: survive all strengthened enemy waves |
| OBJ_GoldMedal | OT_Bonus | — | Gold Medal: save 35+ allied buildings |
| OBJ_SilverMedal | OT_Bonus | — | Silver Medal: save 20+ allied buildings |
| OBJ_BronzeMedal | OT_Bonus | — | Bronze Medal: survive all enemy waves |
| OBJ_Conqueror | OT_Bonus | — | Prove ability to defend allies for conqueror unlock |
| OBJ_InitialAttacks | OT_Battle | — | Yorkist scouting attacks testing defenses |
| SOBJ_AttackPhaseNW | OT_Battle | Phase 1 | Defend Northwest Town until reinforcements arrive |
| SOBJ_AttackPhaseSW | OT_Battle | Phase 2 | Defend Southwest Town until reinforcements arrive |
| SOBJ_AttackPhaseSE | OT_Battle | Phase 3 | Defend Southeast Town until reinforcements arrive |
| SOBJ_AttackPhaseNE | OT_Battle | Phase 4 | Defend Northeast Town until reinforcements arrive |
| SOBJ_ReinforcementsNW | OT_Information | — | NW naval reinforcements have arrived |
| SOBJ_ReinforcementsNE | OT_Information | — | NE naval reinforcements have arrived |
| SOBJ_ReinforcementsSE | OT_Information | — | SE cavalry reinforcements have arrived |
| SOBJ_ReinforcementsSW | OT_Information | — | SW cavalry reinforcements have arrived |
| SOBJ_ReinforcementsS | OT_Information | — | South beacon cavalry reinforcements have arrived |
| OBJ_Boss | OT_Battle | Final | Defeat the Duke of York's final attack |
| OBJ_AgeUpHint | Tip | — | Advance to Castle Age hint (at 7 min) |
| OBJ_ProductionHint | Tip | — | Build 4+ military production buildings hint (at 8 min) |

**Win condition:** Survive all enemy waves including the Duke of York's final boss attack; Lancaster Stronghold must remain standing.
**Lose condition:** Lancaster Stronghold (landmark) is destroyed.

#### challenge_walldefense
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_ConstructWonder | ObjectiveType_Battle | — | Build the Forbidden Palace Wonder before waves begin |
| SOBJ_SpendResources | ObjectiveType_Tip | — | Hint: spend resources on defenses before Wonder completes |
| SOBJ_QuickBuild | ObjectiveType_Tip | — | Hint: units and tech complete instantly until Wonder built |
| OBJ_Victory | ObjectiveType_Battle | — | Survive the 900s countdown; fails if Wonder destroyed |

**Win condition:** Survive the 900-second (15 minute) countdown timer after Wonder construction.
**Lose condition:** The Forbidden Palace Wonder is destroyed.

---

### Hundred Years War

#### hun_chp1_combat30
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_RecruitChampions | Primary | Approach | Recruit 2 of 4 champions before proceeding (counter 0/2) |
| SOBJ_Recruit1 | Battle (sub) | Approach | Kill wolves attacking villagers to recruit Olivier Arrel |
| SOBJ_Recruit2 | Battle (sub) | Approach | Defeat English raiders to recruit Guy de Rochefort |
| SOBJ_Recruit3 | Battle (sub) | Approach | Win a duel against Yves Charruel (reduce to <50% HP) |
| SOBJ_Recruit4 | Battle (sub) | Approach | Defeat English longbowmen + defend outpost 90s for Geoffroy du Bois |
| OBJ_Arrive | Primary | Approach | Travel to the Halfway Oak staging area |
| OBJ_RecruitChampions_Optional | Optional | Approach | Recruit remaining champions after first 2 collected |
| SOBJ_Recruit1_Optional | Battle (sub) | Approach | Optional version of Recruit 1 sub-objective |
| SOBJ_Recruit2_Optional | Battle (sub) | Approach | Optional version of Recruit 2 sub-objective |
| SOBJ_Recruit3_Optional | Battle (sub) | Approach | Optional version of Recruit 3 sub-objective |
| SOBJ_Recruit4_Optional | Battle (sub) | Approach | Optional version of Recruit 4 sub-objective |
| OBJ_BuildForce | Primary | Pre-Round | Select 2 champions from the diplomacy panel |
| SOBJ_RecruitInfantry | Secondary (sub) | Pre-Round | Counter tracks champion selections (0/2) |
| OBJ_TipEnglishForces | Tip | Pre-Round | Informational tip about English forces |
| OBJ_TipDiploController | Tip | Pre-Round | Xbox controller hint: open diplomacy panel |
| OBJ_Combat1 | Battle | Combat | Round 1 — defeat English soldiers (15 kills to win) |
| SOBJ_EngUnits1 | Battle (sub) | Combat | Remaining English units counter (x/30) |
| OBJ_Break1 | Primary | Combat | Reinforce units and research technology between rounds |
| SOBJ_Return | Secondary (sub) | Combat | Return to the field when prepared |
| OBJ_Combat2 | Battle | Combat | Round 2 — full elimination of English soldiers |
| SOBJ_EngUnits2 | Battle (sub) | Combat | Remaining English units counter (x/30) |
| OBJ_DebugComplete | Primary (debug) | — | Debug-only: skip to outro |

**Win condition:** Win both arena rounds (Round 1: reach 15 kills; Round 2: full elimination of English soldiers).
**Lose condition:** All player units lost.

#### hun_chp1_paris
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Defend | Primary (Battle) | — | Defend Paris — fails if all landmarks destroyed |
| OBJ_Defeat | Sub-objective (Battle) | Siege | Defeat all 8 English attack waves (progress bar tracks % killed) |
| OBJ_Prepare | Sub-objective (Info) | Transition | Prepare for siege — completes 25s after invasion ends |
| OBJ_Retreat | Optional | Invasion | Retreat outlying villagers to safety (counter tracks arrivals) |

**Win condition:** Kill all units across all 8 siege waves (OBJ_Defeat complete).
**Lose condition:** All player landmarks destroyed (OBJ_Defend fails).

#### hun_chp2_cocherel
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_StemRebel | Primary (Capture) | — | Parent: recapture all three French villages |
| SOBJ_CaptureJouy | Sub (Capture) | — | Recapture Jouy from peasant rebels |
| SOBJ_DefeatJouyRebels | Sub (Capture) | — | Defeat rebel garrison at Jouy |
| SOBJ_LocationJouy | Sub (Capture) | — | Location label for Jouy |
| SOBJ_CaptureCroisy | Sub (Capture) | — | Recapture Croisy from peasant rebels |
| SOBJ_DefeatCroisyRebels | Sub (Capture) | — | Defeat rebel garrison at Croisy |
| SOBJ_LocationCroisy | Sub (Capture) | — | Location label for Croisy |
| SOBJ_CaptureCocherel | Sub (Capture) | — | Recapture Cocherel (starts after Jouy + Croisy) |
| SOBJ_DefeatCocherelRebels | Sub (Capture) | — | Defeat rebel garrison at Cocherel |
| SOBJ_LocationCocherel | Sub (Capture) | — | Location label for Cocherel |
| OBJ_ProtectMonastery | Information | — | Protect monastery; failure = mission loss |
| OBJ_DefeatCharlesBadArmy | Primary (Battle) | — | Kill threshold of Charles's army at campsite |
| OBJ_DefeatRoutiers | Optional | — | Stop Routier raids (parent with two sub-paths) |
| SOBJ_PayTributeRoutiers | Optional Sub | — | Pay gold tribute to stop Routier attacks |
| SOBJ_DestroyRoutiersBuildings | Optional Sub | — | Destroy all Routier camp buildings |
| OBJ_RepelRoutiersAttack | Battle | — | Repel first Routier wave approaching player town |
| OBJ_DebugComplete1 | Debug | — | Debug-only mission completion shortcut |
| OBJ_DebugComplete2 | Debug | — | Debug-only mission completion shortcut |
| OBJ_increase_gold_income | Primary | — | Find relics parent (registered, not auto-started) |
| SOBJ_Findrelics | Secondary | — | Place relics in Holy Sites for gold income |

**Win condition:** Kill sufficient units of Charles's army (≤15 Navarre remaining + ≥20 player near camp).
**Lose condition:** Monastery destroyed OR player TC destroyed.

#### hun_chp2_pontvallain
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Protect | Primary | — | Town of Pontvallain must survive (fails if all buildings destroyed) |
| OBJ_Build | Optional | — | Construct 3 military production buildings (Easy/Normal only) |
| OBJ_DefeatEnglish | Battle (Parent) | — | Top-level: defeat all English forces |
| SOBJ_DefeatRaids | Battle (Sub) | — | Defeat all 3 raiding parties (counter: 0/3) |
| SOBJ_DefeatArmies | Battle (Sub) | — | Defeat all 3 English armies (counter: 0/3) |
| OBJ_Wait | Information | — | 15:00 countdown timer until English armies march |
| OBJ_Destroy | Primary | — | Template-based "Defeat the English army" (from obj_destroy.scar) |
| OBJ_DebugComplete | Primary (hidden) | — | Debug cheat: removes all rules and completes mission |

**Win condition:** Defeat all 3 raiding parties and all 3 English armies (OBJ_DefeatEnglish complete).
**Lose condition:** All Pontvallain buildings destroyed (OBJ_Protect fails).

#### hun_chp3_orleans
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Keep | Primary | — | Defend Orleans — fails if eg_landmarks count reaches 0 |
| OBJ_Les_Tourelles | Battle | — | Destroy the keep at Les Tourelles — completes mission |
| OBJ_Trade | Battle (Optional) | — | Protect supply convoy — repeating each trade cycle |
| SOBJ_NextConvoy | Information | — | Countdown timer (60s) until next trade ambush launches |
| OBJ_DebugComplete | Primary (hidden) | — | Debug cheat to force mission complete |

**Win condition:** Destroy the English keep at Les Tourelles (OBJ_Les_Tourelles complete).
**Lose condition:** All player landmarks destroyed (OBJ_Keep fails).

#### hun_chp3_patay
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefeatEnglish | Primary | — | Top-level: defeat the English on the road to Patay |
| OBJ_ClearRoad | Battle | — | Clear the blocked road (archer barricade with palings) |
| OBJ_ClearStSigmund | Battle | — | Clear English from St. Sigmund village |
| OBJ_DefeatArmy | Battle | — | Defeat the English blockade (main battle, progress-tracked) |
| OBJ_ClearRegiments | Battle | — | Eliminate 3 remaining English regiments (parent) |
| SOBJ_ClearRegiment1 | Battle (sub) | — | Eliminate the eastern regiment |
| SOBJ_ClearRegiment2 | Battle (sub) | — | Eliminate the central regiment |
| SOBJ_ClearRegiment3 | Battle (sub) | — | Eliminate the western regiment |
| OBJ_TakePatay | Optional | — | Take control of Patay (transfer buildings/villagers to player) |
| OBJ_DefendPatay | Information | — | Town Center in Patay must survive |
| OBJ_DebugComplete | Debug | — | Destroy all English and trigger outro |

**Win condition:** Defeat all English forces including the blockade and 3 fleeing regiments.
**Lose condition:** All player units lost OR Patay TC destroyed.

#### hun_chp4_formigny
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DefendCarentan | Primary (Battle) | Intro | Defend Carentan against Kyriell's advance |
| SOBJ_WeakenKyriell | Sub (Battle) | Intro | Track enemy kills during intro with progress bar/counter |
| OBJ_ClearNormandy | Primary | Main | Master objective: drive English from Normandy |
| SOBJ_findKyriell | Sub (Primary) | Main | March through Normandy to find Kyriell's main army |
| SOBJ_KillKyriellArmy | Sub (Battle) | Main | Destroy 85% of Kyriell's field army (progress bar) |
| OBJ_SaveValognes | Optional | Main | Save allied Valognes village from English attack |
| SOBJ_killEnemyValognes | Sub (Optional) | Main | Kill all English attackers at Valognes |
| SOBJ_CaptureFormigny | Sub (Capture) | Main | Capture the Formigny location (master) |
| SOBJ_DefeatFormignyUnits | Sub (Capture) | Main | Defeat Formigny garrison (secondary) |
| SOBJ_LocationFormigny | Sub (Capture) | Main | Location capture progress |
| OBJ_DebugComplete | Debug | — | Cheat objective to force mission complete |

**Win condition:** Destroy 85% of Kyriell's army, then capture the Formigny location.
**Lose condition:** All player units dead.

#### hun_chp4_rouen
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_RetakeNormandy | Primary/Battle | — | Top-level: retake Normandy from England |
| OBJ_CaptureUniTown | Primary/Capture | Phase 1 | Capture the university area |
| OBJ_ResearchCannons | Primary | Phase 2 | Research Chemistry upgrade |
| OBJ_BBSurvive | Information | Phase 2+ | Fail condition: Bureau Brothers' Workshop must survive |
| OBJ_AssistTheBrothers | Optional | Phase 2+ | Parent for 3 optional location captures |
| SOBJ_GetCannons | Sub/Build | Phase 2 | Build 4 cannons (culverin/ribauldequin/cannon types) |
| SOBJ_DestroyRouenWalls | Sub/Battle | Phase 3 | Breach Rouen's walls with siege |
| SOBJ_DestroyLandmarks | Sub/Battle | Phase 3 | Destroy 3 English landmarks to win |
| SOBJ_DefeatUniDefenders | Sub/Capture | Phase 1 | Clear English defenders from university |
| SOBJ_LocationUniTown | Sub/Capture | Phase 1 | Capture university location marker |
| SOBJ_EstablishTradeRoute_Optional | Optional | Phase 2+ | Capture trade route → assign 3 traders |
| SOBJ_RaidTheRiverPort_Optional | Optional | Phase 2+ | Raze all river port buildings |
| SOBJ_CaptureRouenMine_Optional | Optional/Capture | Phase 2+ | Capture the mine via Location system |
| SOBJ_BuildLandmark | Sub/Primary | Phase 2 | Advance to Imperial Age before chemistry |
| SOBJ_HoldTheUniversity | Sub/Primary | Phase 2 | Hold the university location |
| SOBJ_EstablishTradeRoute | Sub/Primary | Phase 2 | Primary version of trade route capture |
| SOBJ_RaidTheRiverPort | Sub/Battle | Phase 2 | Primary version of river port raze |

**Win condition:** Destroy all 3 English landmarks in Rouen.
**Lose condition:** Player landmarks destroyed OR Bureau Brothers' Workshop destroyed.

---

### Mongol Empire

#### mon_chp1_juyong
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Prepare | Primary | 1 | Plan attack — complete when scouts find forest post or keep |
| SOBJ_Scout | Primary (sub) | 1 | Scout the approach to Zhangjiakou |
| OBJ_Zhangjiakou | Battle | 2 | Destroy the keep at Zhangjiakou fortress |
| OBJ_Yanqing | Battle | 3 | Raze Yanqing — complete when all buildings destroyed |
| SOBJ_YanqingBuildings | Battle (sub) | 3 | Destroy buildings in Yanqing (progress bar) |
| OBJ_RaidBuildings | Optional | 3 | Collect 2000 resources by burning Jin buildings |
| OBJ_DestroyVillages | Optional | 3 | Destroy 3 outlying Jin villages (counter 0/3) |
| SOBJ_Village_1 | Optional (sub) | 3 | Destroy Western Village (6 buildings) |
| SOBJ_Village_2 | Optional (sub) | 3 | Destroy Southern Village (8 buildings) |
| SOBJ_Village_3 | Optional (sub) | 3 | Destroy Northern Village (9 buildings) |
| OBJ_Juyong | Primary | 4 | Breach the Great Wall |
| SOBJ_RazeKeepJuyong | Primary (sub) | 4 | Raze Juyong's keep to win the mission |
| SOBJ_BuildSiege | Primary (sub) | 4 | Construct 4 siege engines (rams or siege towers) |
| OBJ_DebugComplete | Primary | — | Debug: force-completes by destroying Great Wall gate |

**Win condition:** Raze Juyong keep → `Mission_Complete()`.
**Lose condition:** All non-scout units lost OR player TC destroyed.

#### mon_chp1_kalka_river
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_SetupTheRusAmbush | Primary | Setup | Prepare army at 3 ambush positions before timer expires |
| OBJ_RusTimer | Information | Setup | Countdown timer for Rus arrival (difficulty-scaled) |
| SOBJ_GetSquadToPositionA | Sub | Setup | Move 15 units to western ford |
| SOBJ_GetSquadToPositionB | Sub | Setup | Move 15 units to eastern ford |
| SOBJ_GetSquadToPositionC | Sub | Setup | Move 15 units to central woods |
| OBJ_DestroyTheRusUltimate | Primary | Combat | Parent: destroy the entire Rus army |
| SOBJ_MeetTheRus | Sub | Combat | Lure Rus cavalry across the river |
| SOBJ_GetRusToAmbushPt | Sub | Combat | Lead Rus army to the ambush point |
| SOBJ_KillAllRusAmbushPt | Sub/Battle | Combat | Eliminate all incoming Rus at ambush |
| SOBJ_KillAllEnclosedRus | Sub/Battle | Combat | Defeat enclosed Rus at cart stockade |
| OBJ_DebugComplete | Debug | — | Instant-win cheat objective |

**Win condition:** Destroy all Rus including enclosed defenders at cart stockade → `Mission_Complete()`.
**Lose condition:** All player squads dead.

#### mon_chp1_zhongdu
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Raid | Primary | 1 | Top-level Phase 1 wrapper; complete when SOBJ_HoardGold finishes |
| SOBJ_HoardGold | Optional (child) | 1 | Track gold earned; every 250/500 gold triggers reinforcement wave |
| OBJ_InfoSupply | Information | 1 | Display Zhongdu military supply bar; triggers counterattacks when full |
| SOBJ_InfoSupply_Explaination | Information (child) | 1 | UI text: "Eliminate traders to stop attacks" |
| OBJ_StarveCity | Battle | 1 | Phase 1 combat objective; complete when all traders stopped |
| SOBJ_SecretTraderPings | Optional (secret, child) | 1 | Hidden sub tracking trader status |
| SOBJ_StopTraders | Battle (child) | 1 | Destroy 4 village markets to reach 100% progress |
| OBJ_EasyHint | Optional | 1 | Easy/Normal mode hint for building placement |
| OBJ_PlunderCity | Primary | 2 | Phase 2: burn all 3 Zhongdu landmarks |
| SOBJ_Landmark_1 | Battle (child) | 2 | Burn Spirit Way landmark below 50% HP |
| SOBJ_Landmark_2 | Battle (child) | 2 | Burn Imperial Academy landmark below 50% HP |
| SOBJ_Landmark_3 | Battle (child) | 2 | Burn Imperial Palace landmark below 50% HP |
| OBJ_DebugComplete | Primary (hidden) | — | Debug cheat: instantly complete mission |

**Win condition:** Burn all 3 Zhongdu landmarks below 50% HP → `Mission_Complete()`.
**Lose condition:** Not explicitly stated; implied all units/buildings lost.

#### mon_chp2_kiev
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DestroyGate | Primary | 1 | Breach the main outer gate by destroying wall segments |
| OBJ_ForwardBase | Primary | 2 | Unpack at least one mobile Mongol structure |
| OBJ_DestroyKiev | Primary | 3 | Parent: destroy all buildings in 3 districts |
| SOBJ_DestroyIndustrial | Sub | 3 | Destroy all non-wall buildings in Industrial district |
| SOBJ_DestroyOuter | Sub | 3 | Destroy all non-wall buildings in Outer city |
| SOBJ_DestroyInner | Sub | 3 | Destroy all non-wall buildings in Inner city |
| OBJ_DebugComplete | Debug | — | Cheat objective: kill inner city and complete mission |

**Win condition:** Destroy all buildings across all 3 Kiev districts → `Mission_Complete()`.
**Lose condition:** Implied: all player units/buildings lost.

#### mon_chp2_liegnitz
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DestroyPolishArmy | Primary (Battle) | — | Destroy all Polish army groups across field, ridge, valley, templars |
| SOBJ_DefeatRemainingField | Sub (Battle) | — | Defeat field area defenders (4 modules) |
| SOBJ_DefeatRemainingRidge | Sub (Battle) | — | Defeat ridge area defenders (4 modules) |
| SOBJ_DefeatRemainingValley | Sub (Battle) | — | Defeat valley area defenders (6 modules) |
| SOBJ_DefeatRemainingPatrol | Sub (Battle) | — | Defeat roving templar knights (1 module) |
| SOBJ_RovingKnights | Sub (Battle) | — | Defeat the Elite Knights specifically |
| OBJ_BohemianTimer | Information | — | Countdown timer until Bohemian reinforcements arrive |
| OBJ_DestroyBohemianArmy | Primary (Battle) | — | Destroy Bohemian army (activates on timer expiry) |
| OBJ_RaidSettlements | Optional | — | Loot 2000 gold from raiding Polish settlements |
| OBJ_ArmySurvive | Information | — | Player army must not be fully destroyed (commented out) |
| OBJ_DebugComplete | Debug | — | Instantly complete mission |

**Win condition:** Destroy all Polish army groups (and Bohemian army if timer expires) → `Mission_Complete()`.
**Lose condition:** No units, no production buildings, and no resources.

#### mon_chp2_mohi
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_DestroyArmy | Primary | — | Top-level: destroy the Hungarian army; fail if economy locked |
| SOBJ_ScoutBridge | Primary | Scout | Scout across the bridge; triggers ambush on visibility |
| SOBJ_EscapeAmbush | Primary | Scout | Escape cavalry ambush; completes when pursuers killed or unseen 15s |
| SOBJ_SupportBatu | Primary | Buildup | Build army at flanks; completes when player attacks forward guards |
| SOBJ_OptRepairBridge | Optional | Buildup | Repair the destroyed western bridge for alternate route |
| SOBJ_OptMangonels | Optional | Buildup | Build 2 mangonels (Normal and below only) |
| SOBJ_BatuTimer | Primary | Buildup | Countdown timer until Batu attacks regardless of readiness |
| SOBJ_AttackBridge | Battle | Assault | Assault ambush positions with Batu; progress bar tracks kills |
| SOBJ_DriveArmyBack | Battle | Assault | Push through 2 defense lines; progress bar, rout on threshold |
| SOBJ_AssaultTheCamp | Battle | Assault | Destroy Hungarian camp defenders; rout at ~20 remaining |
| OBJ_DebugComplete | Primary | — | Debug cheat: instant mission complete |

**Win condition:** Destroy all Hungarian camp defenders → `Mission_Complete()`.
**Lose condition:** Player economy locked — no units, no buildings, no food.

#### mon_chp3_lumen_shan
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_ClaimArea | Primary | 1 | Destroy Song fort and claim Lumen area |
| SOBJ_DestroyFort | Battle (child) | 1 | Destroy all buildings in Song military camp |
| OBJ_Blockade | Build | 2 | Build walls to block all paths north |
| SOBJ_Walls | Build (child) | 2 | Evaluate blockade via cached path lengths (threshold: 15) |
| SOBJ_Towers | Build (child) | 2 | Build and upgrade a tower with springald/cannon (Easy/Normal only) |
| OBJ_Defense | Primary | 3 | Survive 8 wallbreaker waves |
| SOBJ_BlockadeSuccess | Battle (child) | 3 | Counter tracking defeated wallbreaker waves (target: 8) |
| SOBJ_BlockadeFailure | Tip (child) | 3 | Fail counter: mission fails if 20 Song units escape north |
| OBJ_Remedial | Primary | 4 | Phase 4 (on Phase 3 fail): stop the Song return sally |
| SOBJ_FinalChance | Battle (child) | 4 | Fail counter: mission fails if 20 Song units escape south |
| OBJ_Bohekou | Optional | — | Recruit Bohekou village by sending units nearby |
| SOBJ_GeneralToVillage | Optional (child) | — | Move any Mongol unit near Bohekou marker |
| OBJ_HintBridge | Optional (secret) | — | Hint to destroy a wooden bridge when spotted onscreen |
| OBJ_DebugComplete | Primary (hidden) | — | Debug: force mission complete |

**Win condition:** Survive all 8 wallbreaker waves without 20 Song escaping north; OR in Phase 4, stop Song sally before 20 escape south.
**Lose condition:** 20 Song units escape north (Phase 3) OR 20 escape south (Phase 4) OR all Chinese TCs and villagers lost.

#### mon_chp3_xiangyang_1267
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Advance | Primary | 1 | Phase 1 wrapper: advance through Song outer defenses |
| SOBJ_ClearApproach | Primary (child) | 1 | Clear initial Song watchpost or advance past it |
| SOBJ_BaitPlayer | Primary (child) | 1 | Rally to allied Mongol forces across the map |
| SOBJ_WoodenCamp | Battle (child) | 1 | Destroy all buildings in fortified wooden camp |
| SOBJ_DefendTrebs | Battle (child) | 1 | Protect 4 allied trebuchets during bridge assault |
| OBJ_CampUp | Primary | 2 | Phase 2 wrapper: surround Xiangyang at 3 positions |
| SOBJ_SurroundWest | Battle (child) | 2 | Station units at western bridgehead (ratio ≥ 55 pop) |
| SOBJ_SurroundNorth | Battle (child) | 2 | Station units at northern bridgehead (ratio ≥ 55 pop) |
| SOBJ_SurroundSouth | Battle (child) | 2 | Station units at southern bridgehead (ratio ≥ 55 pop) |
| OBJ_FinaleTimer | Information | 2 | 45-second countdown before final sally begins |
| OBJ_ContainFinalSally | Information | 2 | Survive 5 escalating Song counter-attack waves |
| OBJ_VisitPagoda | Optional | — | Visit pagoda to recruit neutral monks |
| OBJ_DebugComplete | Primary (hidden) | — | Debug: instantly complete mission |

**Win condition:** Surround Xiangyang at all 3 bridgeheads, then survive all 5 finale sally waves → `Mission_Complete()`.
**Lose condition:** Player loses all 3 bridgeheads (60s grace period per empty bridgehead before failure).

#### mon_chp3_xiangyang_1273
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Prepare | Primary | 1 | Phase 1: prepare siege by building a Huihui Pao |
| SOBJ_BuildTrebuchet | Sub (Build) | 1 | Build one Great Trebuchet (Huihui Pao) |
| SOBJ_OptUseSilkRoad | Sub (Optional) | 1 | Have 9 active traders on the Silk Road |
| OBJ_BreachCity | Primary | 2 | Phase 2: breach and capture Fancheng |
| SOBJ_OptUseFalcon | Sub (Optional) | 2 | Use falcon ability near two trigger markers |
| SOBJ_CrossMoat | Sub (Build) | 2 | Construct dirt bridges across the moat to 100% health |
| SOBJ_MoatHintpoints | Sub (Secret) | 2 | Hidden objective providing bridge UI hintpoints |
| SOBJ_EnterCity | Sub (Primary) | 2 | Move 6+ player units inside Fancheng walls |
| SOBJ_DefeatGarrison | Sub (Battle) | 2 | Kill all Fancheng garrison units (progress bar) |
| SOBJ_RazeLandmark | Sub (Battle) | 2 | Destroy Fancheng barbican landmark |
| OBJ_SackXiangyang | Primary | 3 | Phase 3: sack the city of Xiangyang |
| SOBJ_BombKeep | Sub (Battle) | 3 | Destroy the Xiangyang keep |
| SOBJ_RepairBridge | Sub (Build) | 3 | Repair the twin-city bridge to 100% |
| SOBJ_StormPalace | Sub (Battle) | 3 | Burn the Xiangyang palace below 50% health |
| OBJ_AlliedTradePartners | Information | — | Protect allied west and south trade markets |
| OBJ_DebugComplete | Debug | — | Cheat: burn palace and complete mission |

**Win condition:** Burn the Xiangyang palace below 50% HP → `Mission_Complete()`.
**Lose condition:** No military units + no villagers + no TC OR allied trade markets destroyed.

---

### Rise of Moscow

#### gdm_chp1_moscow
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_ProtectMoscow | Primary | 1 | Chase off Mongols and extinguish fires |
| SOBJ_ChaseOffMongols | Sub | 1 | Kill/rout all intro Mongol raiders (progress bar) |
| SOBJ_PutOutFires | Sub | 1 | Extinguish fires on inner city buildings (counter) |
| OBJ_RebuildMoscow | Primary | 2 | Gather resources and rebuild city |
| SOBJ_GatherWood | Sub | 2 | Gather 700 wood (counter) |
| SOBJ_GatherPeople | Sub | 2 | Produce/locate 8 additional villagers (counter) |
| SOBJ_RebuildStructures | Sub | 2 | Rebuild destroyed inner city structures (dynamic counter) |
| OBJ_ExpandMoscow | Primary | 3 | Construct expansion buildings |
| SOBJ_BuildLandmark | Sub | 3 | Build the Kremlin (Novgorod Kremlin landmark) |
| SOBJ_BuildMarket | Sub | 3 | Build the Market |
| SOBJ_BuildArchery | Sub | 3 | Build the Archery Range |
| OBJ_BuildDefences | Primary | 4 | Prepare for Mongol assault |
| SOBJ_BuildDefensiveStructures | Sub | 4 | Build Wooden Fortresses at preset locations (counter) |
| SOBJ_BuildMilitaryUnits | Sub | 4 | Produce 40 military units (counter) |
| OBJ_MongolCountdown | Info | 5 | Countdown timer before final attack; triggers weather change |
| OBJ_MongolAttacks | Primary | 5 | Survive all Mongol attack waves to win |
| OBJ_FindVillagers | Optional | — | Locate Hunting Cabins with scared villagers in forests |
| OBJ_DebugComplete | Debug | — | Cheat objective to skip to mission completion |

**Win condition:** Survive all four Mongol final assault waves.
**Lose condition:** TC and Kremlin both destroyed, OR fewer than 3 buildings remain during the fire phase.

#### gdm_chp2_kulikovo
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_PrepareArmy | Primary | Prep | Prepare to fight the Mongol threat (parent) |
| SOBJ_RecruitSoldiers | Secondary | Prep | Regroup with allied Rus armies |
| SOBJ_VisitVillages | Secondary | Prep | Visit 2 Rus villages with Dmitry to recruit soldiers |
| SOBJ_RallyFords | Secondary | Prep | Rally ≥10 player units at center ford; progress bar |
| OBJ_HiddenVillage | Primary (Secret) | Prep | Find hidden village for 18 bonus spearmen + blacksmith |
| OBJ_OptionalFindVillage | Optional | Prep | Find village to spend gold (Easy/Normal only) |
| OBJ_RepelMongols | Battle | Battle | Parent: Repel the Mongol Horde |
| SOBJ_Wave1 – SOBJ_Wave10 | Secondary | Battle | Individual wave sub-objectives under OBJ_RepelMongols |
| SOBJ_HoldFords | Battle | Battle | Defend Smolka River fords (waves 1–3) |
| SOBJ_HoldMainline | Battle | Battle | Defend central hill (waves 4–7) |
| SOBJ_HoldLast | Battle | Battle | Defend Don River crossing (waves 8–10) |
| OBJ_FordStrength_L/C/R | Secret Battle | Battle | Per-ford strength progress bars |
| OBJ_HoldDon | Information | Battle | Informational: Mongols must not cross the Don River |
| OBJ_SignalCavalry | Primary | Battle | Signal hidden cavalry to attack (one-time use) |

**Win condition:** Survive all 10 Mongol waves across three defense lines.
**Lose condition:** Mongols breach the Don River crossing, or the player army is entirely destroyed.

#### gdm_chp2_tribute
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_PayTheMongols | Primary | — | Pay gold tribute to Mongols within 7.5-minute timer |
| SOBJ_PayTheMongols_GoldAmount | Primary (sub) | — | Counter showing gold paid vs gold demanded |
| OBJ_CollectTaxes | Primary | — | Collect taxes from neighboring settlements via trade |
| SOBJ_MaintainTradeRoutes | Primary (sub) | — | Maintain trade routes with settlements |
| SOBJ_Bandits | Primary (sub) | — | Protect trade routes from bandits |
| OBJ_BuySettlements | Primary | — | Buy N settlements to expand Moscow (victory condition) |
| SOBJ_FindMoreSettlements | Primary (sub) | — | Find more settlements if all discovered ones are purchased |
| OBJ_BanditCamps | Optional | — | Destroy randomly-selected bandit camps (counter) |
| OBJ_BuildCabins | Optional | — | Build 3 Hunting Cabins near forests (Easy/Normal only) |
| OBJ_TipTradeRouteLengths | Tip | — | Longer trade routes generate more gold per trip |
| OBJ_TipManageGold | Tip | — | Manage gold for both settlements and Mongol payments |
| OBJ_DebugComplete | Primary (hidden) | — | Debug cheat: instantly complete mission |

**Win condition:** Purchase the required number of settlements (3 Easy/Normal, 4 Hard, 5 Expert).
**Lose condition:** Mongol tribute timer expires without payment (triggers punitive Mongol army then mission fails).

#### gdm_chp3_moscow
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_MoscowDefense | Information | — | Keep Mongols out of inner city; fails mission on countdown expiry |
| SOBJ_CountdownToFail | Secondary (child) | — | Visible countdown timer when Mongols breach inner walls |
| OBJ_Prepare | Primary | Prep | Timed preparation phase before Mongol assault begins |
| SOBJ_Attack | Secondary (child) | Prep | Countdown timer showing time until Mongol arrival |
| OBJ_HoldAgainstTheHorde | Primary | Battle | Survive finite Mongol waves; progress bar tracks remaining |
| OBJ_Refugees | Primary | Outro | Hold city while civilians evacuate; progress bar |
| SOBJ_MongolBlockade | Secondary (child) | Outro | Defeat Mongol blockade on escape route (commented-out) |
| OBJ_DebugComplete | Primary | — | Debug: skips to outro cinematic |

**Win condition:** Evacuate the required number of refugees (100/200/300 by difficulty).
**Lose condition:** Inner city breach failure countdown reaches zero (30–120s by difficulty).

#### gdm_chp3_novgorod
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_ConquerNovgorod | Master | — | Top-level primary: conquer Novgorod |
| OBJ_SettleBase | Primary | 1 | Capture outlying towns (Kuklino + Soltsy) |
| SOBJ_CaptureKuklino | Sub | 1 | Capture Kuklino village |
| SOBJ_DefeatkuklinoRebels | Sub | 1 | Defeat Kuklino defenders |
| SOBJ_Locationkuklino | Sub | 1 | Location capture tracking |
| SOBJ_CaptureSoltsy | Sub | 1 | Capture Soltsy village |
| SOBJ_DefeatsoltsyRebels | Sub | 1 | Defeat Soltsy defenders |
| SOBJ_Locationsoltsy | Sub | 1 | Location capture tracking |
| OBJ_OptionalHelp | Optional | 1 | Optional parent: economy guidance |
| SOBJ_BuildCabins | Sub (Optional) | 1 | Build 3 gold-generating Hunting Cabins |
| SOBJ_CaptureHolySites | Sub (Optional) | 1 | Capture 1 Holy Site |
| SOBJ_HuntGaia | Sub (Optional) | 1 | Hunt 5 animals for bounty |
| OBJ_MiddleBattle | Primary | 2 | Eliminate militia at Shelon River fort |
| SOBJ_KillUnitsAtFort | Sub | 2 | Defeat all militiamen (progress bar) |
| SOBJ_GetThroughNovgorod | Sub | 3 | Enter Novgorod (proximity check) |
| SOBJ_DestroyVecheBell | Sub | 4 | Destroy the Veche Bell to complete mission |
| OBJ_DebugComplete | Debug | — | Debug: instant mission complete cheat |

**Win condition:** Destroy the Veche Bell inside Novgorod.
**Lose condition:** Not explicitly defined (implied: player army destroyed).

#### gdm_chp3_ugra
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_FindMongols | Primary | Prep | Timed preparation phase — build forces before Mongols attack |
| OBJ_PrepareForMongols | Primary | Prep | Completes when prepare timer expires, triggers repel phase |
| OBJ_MoveUnitsToFords | Primary | Prep | Move units to fords |
| SOBJ_MoveToNorthFord | Sub (TugOfWar) | Prep | North ford force ratio progress indicator |
| SOBJ_MoveToSouthFord | Sub (TugOfWar) | Prep | South ford force ratio progress indicator |
| OBJ_RepelMongols | Battle | Battle | Repel two vanguard scout waves |
| SOBJ_RepelWave1 | Sub (Battle) | Battle | Repel 6 horsemen at south ford |
| SOBJ_RepelWave2 | Sub (Battle) | Battle | Repel 6 horsemen at north ford |
| OBJ_MaintainSuperiority | Information | Hold | Hold fords for 900s countdown timer |
| SOBJ_NorthFordRus | Sub (TugOfWar) | Hold | North ford force ratio during hold phase |
| SOBJ_SouthFordRus | Sub (TugOfWar) | Hold | South ford force ratio during hold phase |
| OBJ_SouthernReinforcements | Optional | Hold | Intercept southern Mongol reinforcement column |
| SOBJ_DestroyUnits | Sub (Optional) | Hold | Kill count tracker for reinforcement column |
| OBJ_AttackMongols | Battle | Attack | Destroy Mongol encampment (final phase) |
| SOBJ_DestroyTownCenter | Sub (Battle) | Attack | Destroy Mongol Town Center to win |
| OBJ_DebugComplete | Debug | — | Cheat objective to skip to victory |

**Win condition:** Destroy the Mongol Town Center.
**Lose condition:** Rus Town Center is destroyed.

#### gdm_chp4_kazan
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_SecureFort | Primary | 1 | Secure a foothold |
| SOBJ_KillWoodcutters | Battle | 1 | Destroy the Tatar woodcutter settlement |
| SOBJ_TatarBuildings | Battle | 1 | Dummy objective for remaining building UI hints |
| SOBJ_BuildFort | Primary | 1 | Construct a Town Center (free cost via modifier) |
| OBJ_SiegeKazan | Primary | 2 | Siege the city of Kazan |
| SOBJ_BreachOuter | Primary | 2 | Breach Kazan's outer stone wall |
| SOBJ_BreachInner | Primary | 2 | Breach Kazan's inner stone wall |
| SOBJ_KillKhanGuards | Primary | 2 | Defeat all Khan's elite guards (progress bar) |
| OBJ_ClearWestFord | Optional | — | Destroy west ford camp to stop flanking attacks |
| SOBJ_ClearWestFordBuildings | Optional | — | Destroy military buildings at west ford (counter) |
| OBJ_Failure | Primary | — | Failure/outro trigger wrapper |
| OBJ_DebugComplete | Primary | — | Debug: instant mission complete |

**Win condition:** Defeat all of the Khan's elite guards inside Kazan.
**Lose condition:** Player TC is destroyed, or the player has no remaining units.

#### gdm_chp4_smolensk
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_CaptureVillages | Primary | 1 | Capture all three surrounding villages |
| SOBJ_CaptureRoslavl | Sub (Capture) | 1 | Capture Roslavl — unlocks cavalry production |
| SOBJ_DefeatRoslavlResistance | Sub (Battle) | 1 | Defeat Roslavl garrison |
| SOBJ_LocationRoslavl | Sub (Capture) | 1 | Roslavl location marker |
| SOBJ_CaptureYelnya | Sub (Capture) | 1 | Capture Yelnya — unlocks archery production |
| SOBJ_DefeatYelnyaResistance | Sub (Battle) | 1 | Defeat Yelnya garrison |
| SOBJ_LocationYelnya | Sub (Capture) | 1 | Yelnya location marker |
| SOBJ_CaptureVyazma | Sub (Capture) | 1 | Capture Vyazma — unlocks infantry production |
| SOBJ_DefeatVyazmaResistance | Sub (Battle) | 1 | Defeat Vyazma garrison |
| SOBJ_LocationVyazma | Sub (Capture) | 1 | Vyazma location marker |
| OBJ_ProtectLandmarks | Information | — | Fail if all player-owned landmarks destroyed |
| OBJ_BesiegeSmolensk | Primary | 2 | Breach Smolensk's walls |
| OBJ_StopAttacks | Primary | 2 | Cut off supplies — stop Smolensk attacks |
| SOBJ_StopTraders | Sub (Battle) | 2 | Intercept traders from both caravan routes |
| OBJ_SmolenskSupply | Information | 2 | Supply progress bar for next Smolensk attack |
| OBJ_ForceSurrender | Primary | 3 | Capture Smolensk after wall breach |
| SOBJ_DefeatSmolenskResistance | Sub (Battle) | 3 | Defeat Smolensk's interior garrison |
| SOBJ_LocationSmolensk | Sub (Capture) | 3 | Smolensk location marker |
| OBJ_CaptureKrasny | Optional | — | Visit Krasny to receive 4 cannons |
| OBJ_DebugComplete | Debug | — | Instant mission complete cheat |

**Win condition:** Capture Smolensk (defeat interior garrison and capture the location).
**Lose condition:** All player-owned landmarks are destroyed.

---

### Rogue (Experimental)

#### rogue_maps

Rogue mode objectives are dynamically generated by the rogue system rather than defined as static constants. Only a few map-specific constants appear:

| Constant | Map | Purpose |
|----------|-----|---------|
| OBJ_DESTROY_BUILDINGS | japanese_daimyo | Destroy enemy structures |
| OBJ_DUMMY_INFORMATION | steppe_raiders | UI-only objective for raider camp location |
| OBJ_CaptureEnemiesTown | ugc_map | Capture the French city location |
| SOBJ_DefeatTownRebels | ugc_map | Defeat rebels at town |
| SOBJ_LocationTown | ugc_map | Capture the town location marker |
| OBJ_DestroyBuildings | ugc_map | Destroy all French city buildings |

Victory/failure is managed by the shared rogue system, not per-map scripts.

---

### The Normans (Salisbury Tutorial)

#### sal_chp1_rebellion
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_InvestigateSurroundings | Primary | 1 | Investigate the area — umbrella for 5 camera sub-objectives |
| SOBJ_MoveCameraToLumber | Sub | 1 | Move camera pivot over the lumber camp |
| SOBJ_MoveCameraToRocks | Sub | 1 | Move camera pivot over the large rocks |
| SOBJ_RotateCamera | Sub | 1 | Rotate camera orbit away from default angle |
| SOBJ_ZoomCamera | Sub | 1 | Zoom camera in while over rocks and rotated |
| SOBJ_ResetCamera | Sub | 1 | Reset camera zoom back to default |
| OBJ_Spearmen | Primary | 2 | Find Your Spearmen — unit-control sub-objectives |
| SOBJ_SelectWilliam | Sub | 2 | Select Guillaume |
| SOBJ_MoveWilliam | Sub | 2 | Move Guillaume to the indicated marker |
| SOBJ_FollowMarkers | Sub | 2 | Follow 3 waypoints to reach spearmen camp |

**Win condition:** Complete all camera and unit-control tutorial steps (reach the spearmen camp).
**Lose condition:** None — fixed tutorial with no combat.

#### sal_chp1_valesdun
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_OrganiseSpearmen | Primary | 1 | Organise the Spearmen — selection/move/control group |
| SOBJ_SelectSpearmen | Sub | 1 | Select all spearmen |
| SOBJ_MoveSpearmen | Sub | 1 | March spearmen to a marker |
| SOBJ_CreateRegiment | Sub | 1 | Create a control group for spearmen |
| OBJ_MusterForces | Primary | 2 | Command the Spearmen — search/destroy/attack-move/follow |
| SOBJ_SelectAll | Sub | 2 | Marquee-select Guillaume and all spearmen |
| SOBJ_Search | Sub | 2 | Follow 2 sequential waypoint markers |
| SOBJ_DestroyPalisade | Sub | 2 | Destroy an enemy palisade wall segment |
| SOBJ_DefeatHorseman | Sub | 2 | Defeat lone enemy horseman using attack-move |
| SOBJ_FollowMarkers | Sub | 2 | Follow markers to horsemen and enemy archers |
| OBJ_CommandHorsemen | Primary | 3 | Command the Horsemen — defeat enemy archers with cavalry |
| SOBJ_DefeatArchers | Sub | 3 | Kill all enemy archers with horsemen |
| OBJ_LocateArchers | Primary | 4 | Locate the Archers — find allied archers |
| SOBJ_SelectExpandedArmy | Sub | 4 | Select expanded army using add-to-selection |
| SOBJ_MoveAmbush | Sub | 4 | Follow marker to allied archer position |
| OBJ_CommandArchers | Primary | 5 | Command the Archers — ambush encounter |
| SOBJ_PositionAmbush | Sub | 5 | Move archers to ambush hill marker |
| SOBJ_AmbushSpearmen | Sub | 5 | Defeat all enemy spearmen from elevated position |
| OBJ_PrepareForBattle | Primary | 6 | Prepare for Battle — select army and march to Henri |
| SOBJ_SelectEntireArmy | Sub | 6 | Select entire army using D-pad |
| SOBJ_FollowToHenry | Sub | 6 | Follow 3 waypoints to King Henri |
| OBJ_DefeatGuy | Primary | 7 | Defeat Gui de Bourgogne — final pitched battle |
| SOBJ_DefeatGuyGetReady | Sub | 7 | Take Position — reach battlefield marker |
| SOBJ_DefeatGuyCavalry | Sub | 7 | Break Guy's cavalry (75% kill threshold) |
| SOBJ_DefeatGuyArchers | Sub | 7 | Break Guy's archers (75% kill threshold) |
| SOBJ_DefeatGuySpearmen | Sub | 7 | Break Guy's spearmen (75% kill threshold) |
| SOBJ_HeroAbility | Optional | 7 | Use Guillaume's leader_attack_speed_activated ability |

**Win condition:** Defeat Gui de Bourgogne by breaking 75% of his cavalry, archers, and spearmen.
**Lose condition:** None specified — tutorial with reinforcement safety nets.

#### sal_chp2_dinan
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_VillagerPriorities | Primary | 1 | Re-Prioritize the Villagers — set military preset |
| SOBJ_SetMilitaryPreset | Sub | 1 | Choose the Military Preset in villager priorities radial |
| OBJ_Spearmen | Primary | 2 | Recruit Spearmen — build and train |
| SOBJ_Build2Houses | Sub | 2 | Build 2 houses (counter 0/2) |
| SOBJ_BuildBarracks | Sub | 2 | Build a Barracks (counter 0/1) |
| SOBJ_SetRally | Sub | 2 | Set a Rally Point on the barracks |
| SOBJ_Make10Spearmen | Sub | 2 | Produce 10 Spearmen (counter 0/10) |
| OBJ_Cavalry | Primary | 3 | Recruit Horsemen — build stables and train |
| SOBJ_BuildStables | Sub | 3 | Build a Stable (counter 0/1) |
| SOBJ_HorsemenRaid | Sub | 3 | Defeat enemy horseman raid on player base |
| SOBJ_Make10Horsemen | Sub | 3 | Produce 10 Horsemen (counter 0/10) |
| OBJ_Archers | Primary | 4 | Recruit Archers — build archery range and train |
| SOBJ_BuildArchery | Sub | 4 | Build an Archery Range (counter 0/1) |
| SOBJ_ArchersRaid | Sub | 4 | Defeat enemy archer raid on player base |
| SOBJ_Make10Archers | Sub | 4 | Produce 10 Archers (counter 0/10) |
| OBJ_UpgradeUnits | Primary | 5 | Upgrade your Units — research at barracks and blacksmith |
| SOBJ_Hardened | Sub | 5 | Research Hardened (spearman tier 2) upgrade |
| SOBJ_BuildBlacksmith | Sub | 5 | Build a Blacksmith (counter 0/1) |
| SOBJ_Research | Sub | 5 | Research any technology at blacksmith |
| OBJ_Capture | Primary | 6 | Capture Chateau de Dinan — final assault |
| SOBJ_March | Sub | 6 | March army to the keep (proximity check) |
| SOBJ_Destroy | Sub | 6 | Destroy the enemy keep (health < 5%) |
| OBJ_HeroAbility | Optional | 6 | Use Guillaume's Hero Ability near outpost |

**Win condition:** Destroy the enemy keep at Chateau de Dinan (health < 5%).
**Lose condition:** None specified — tutorial with reinforcement safety nets.

#### sal_chp2_township
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_BuildLandmark | Primary | 1 | Build a Landmark & Advance to the Next Age |
| SOBJ_GatherFood | Sub | 1 | Gather 400 Food (progress bar) |
| SOBJ_GatherGold | Sub | 1 | Gather 200 Gold (progress bar) |
| SOBJ_PlaceLandmark | Sub | 1 | Place a Dark Age Landmark on the map |
| SOBJ_Make3Villagers | Sub | 1 | Make 3 Villagers (counter 0/3) |
| SOBJ_WaitFinish | Sub | 1 | Wait for the Landmark to finish construction |
| OBJ_ResearchTech | Primary | 2 | Research new Technology — final phase |
| SOBJ_Horticulture | Sub | 2 | Research Horticulture at a Mill |

**Win condition:** Research Horticulture at a Mill.
**Lose condition:** None — purely economic tutorial with no combat.

#### sal_chp2_womanswork
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_VillagersWork | Primary | 1 | Parent: complete all villager-work sub-objectives |
| SOBJ_SelectVillager | Sub | 1 | Select any villager from starting group |
| SOBJ_GatherFood | Sub | 1 | Gather 10 food (counter: 0/10) |
| SOBJ_VillagerCommand | Sub | 1 | Train 2 villagers from TC via radial menu |
| SOBJ_BuildMill | Sub | 1 | Build a Mill |
| SOBJ_BuildLumber | Sub | 1 | Build a Lumber Camp |
| SOBJ_Make5Villagers | Sub | 1 | Queue 5 villagers using LT modifier |
| SOBJ_BuildHouses | Sub | 1 | Build 2 houses (triggered when pop-capped) |
| OBJ_Scout | Primary | 2 | Parent: find, herd, harvest sheep |
| SOBJ_FindSheep | Sub | 2 | Scout locates sheep on map |
| SOBJ_HerdSheep | Sub | 2 | Bring sheep near TC (within 15 range) |
| SOBJ_HarvestSheep | Sub | 2 | Kill/harvest at least one sheep |
| OBJ_GrowTown | Primary | 3 | Parent: mine, farms, assign workers |
| SOBJ_BuildMine | Sub | 3 | Build a Mining Camp near gold |
| SOBJ_BuildFarms | Sub | 3 | Build 3 Farms near Mill (counter: 0/3) |
| SOBJ_AssignVillagers | Sub | 3 | Assign villagers to work 3 farms |
| OBJ_CommandOfficials | Primary | 4 | Parent: VPS and research |
| SOBJ_SetBalanced | Sub | 4 | Choose Economic VPS preset |
| SOBJ_Research | Sub | 4 | Research Wheelbarrow at Mill/TC |
| OBJ_BuildLandmark | Primary | 5 | Parent: place and finish landmark |
| SOBJ_PlaceLandmark | Sub | 5 | Place Casernes Centrales landmark |
| SOBJ_WaitFinish | Sub | 5 | Wait for landmark construction to complete |

**Win condition:** Build and complete the Dark Age Landmark (Casernes Centrales) to advance to Age II.
**Lose condition:** None — purely economic tutorial with no combat.

#### sal_chp3_brokenpromise
| Constant | Type | Phase | Purpose |
|----------|------|-------|---------|
| OBJ_Gather | Primary | 1 | Parent: gather resources for invasion |
| SOBJ_GatherFood | Sub | 1 | Gather 400 food (progress bar) |
| SOBJ_GatherWood | Sub | 1 | Gather 400 wood (progress bar) |
| SOBJ_GatherGold | Sub | 1 | Gather 200 gold (progress bar) |
| OBJ_AgeUp | Primary | 2 | Advance to Age II (Feudal) |
| OBJ_BuildInvasionForce | Primary | 3 | Parent: build military production buildings |
| SOBJ_Build2Barracks | Sub | 3 | Build 2 barracks (counter 0/2) |
| SOBJ_Build2Archery | Sub | 3 | Build 2 archery ranges (counter 0/2) |
| SOBJ_Build2Stables | Sub | 3 | Build 2 stables (counter 0/2) |
| OBJ_BuildInvasionArmy | Primary | 4 | Parent: train invasion force |
| SOBJ_Make40Spearmen | Sub | 4 | Train 40 spearmen (counter 0/40) |
| SOBJ_Make30Horsemen | Sub | 4 | Train 30 horsemen (counter 0/30) |
| SOBJ_Make30Archers | Sub | 4 | Train 30 archers (counter 0/30) |
| OBJ_BuildFleet | Primary | 5 | Parent: build naval fleet |
| SOBJ_Build2Docks | Sub | 5 | Build 2 docks (counter 0/2) |
| SOBJ_Build3TransportShips | Sub | 5 | Build 3 transport ships (counter 0/3) |
| OBJ_LoadTroops | Primary | 6 | Board 48+ troops onto transport ships |
| OBJ_BeginInvasion | Primary | 7 | Parent: execute invasion of England |
| SOBJ_SetSail | Sub | 7 | Sail ships to Pevensey landing marker |
| SOBJ_UnloadArmy | Sub | 7 | Disembark all troops (progress bar) |
| SOBJ_BeachAmbush | Sub | 7 | Repel 15 men-at-arms beach ambush |
| SOBJ_TakePevensey | Sub | 7 | Eliminate all Pevensey garrison defenders |
| OBJ_LocateHastings | Primary | 8 | Scout into fog of war to find Hastings |
| OBJ_TakeHastings | Primary | 9 | Parent: conquer Hastings |
| SOBJ_DestroyTC | Sub | 9 | Destroy the enemy Town Center |

**Win condition:** Destroy the Hastings Town Center.
**Lose condition:** None explicitly defined — tutorial mission with no stated failure condition.

---

## Shared Patterns

### Naming Conventions
- **OBJ_ prefix**: Used for all campaign missions (standard pattern)
- **SOBJ_ prefix**: Sub-objectives nested under parent OBJ_ objectives
- **TOBJ_ prefix**: Tip objectives (informational hints, used sparingly — mainly Abbasid)
- **Dot-path format** (`_challenge.victory.*`, `_challenge.benchmarks.*`): Used exclusively in Art of War challenges; namespaced by category (victory, secondary, benchmarks)
- **Bare names** (no prefix): Some challenge missions (challenge_latesiege) use unprefixed constants

### Common Objective Types
- **OBJ_Defend / OBJ_Protect**: Fail-state guard — mission fails if protected entity is destroyed (40+ missions)
- **OBJ_DebugComplete**: Debug/cheat objective that forces mission completion — present in nearly every mission
- **OBJ_Destroy***: Destruction target — destroying named entity completes the objective
- **OBJ_Capture***: Location capture using the Location system (Defeat rebels + capture zone)

### Objective Chaining Patterns
- **Phase progression**: Phase 1 objectives complete → unlock Phase 2 objectives (abb_m5_mansurah, abb_m8_cyprus, mon_chp3_xiangyang_1273)
- **Counter-tracked waves**: Wave counter sub-objective increments per wave defeated; parent completes when counter reaches target (abb_m4_hattin, abb_m6_aynjalut, challenge_advancedcombat)
- **Timed transitions**: Countdown timer objective completes → triggers next phase (hun_chp1_paris OBJ_Prepare, ang_chp3_wallingford OBJ_Survive)
- **Dual-path completion**: Two independent objectives both required for mission win (abb_bonus: landmarks + holy orders)
- **Optional → Primary conversion**: Optional objectives that become primary based on discovery (ang_chp1_york OBJ_DestroyCampAlt)
- **Medal cascading**: Gold timer fails → Silver timer starts → Bronze timer starts (all challenge missions)

### Location Capture Pattern
Standardized across campaigns using a 3-objective pattern:
1. `OBJ_Capture[Name]` — parent capture objective
2. `SOBJ_Defeat[Name]Rebels` — defeat garrison defenders
3. `SOBJ_Location[Name]` — capture the location zone

Used in: ang_chp1_york, ang_chp2_bayeux, ang_chp2_bremule, ang_chp4_rochester, hun_chp2_cocherel, hun_chp4_formigny, gdm_chp3_novgorod, gdm_chp4_smolensk, abb_bonus, abb_m8_cyprus, and others.
