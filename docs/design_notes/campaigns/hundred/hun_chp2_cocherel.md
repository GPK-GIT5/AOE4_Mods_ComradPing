# Hundred Years War Chapter 2: Cocherel

## OVERVIEW

"France in Chaos 1364" casts the player as Bertrand du Guesclin (player1, French) who must reunify three rebellious peasant villages — Jouy, Croisy, and Cocherel — while managing two enemy factions: English Routiers (player3) and Charles of Navarre (player4). The mission progresses through three phases: capture the rebel towns, protect the Cocherel monastery, and defeat Charles's army at his campsite. A diplomacy/tribute system lets the player optionally pay gold to the Routiers to stop their raids, or alternatively destroy their camp. Difficulty scales starting resources, attack frequencies, wave sizes, and kill thresholds across four tiers (Easy → Expert). The mission uses MissionOMatic with RovingArmy/Defend modules, Wave-based spawn pipelines, and a custom Diplomacy UI repurposed as a tribute menu.

---

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp2_cocherel.scar` | core | Main mission script: player/difficulty setup, recipe definition, wave infrastructure, inter-village attack logic, intro sequence, and global monitors. |
| `diplomacy_chp2_cocherel.scar` | other | Diplomacy & tribute UI system reused as a gold-tribute menu for paying off the Routiers. |
| `obj_capture_frenchtowns.scar` | objectives | Objective logic for capturing Jouy, Croisy, and Cocherel from peasant rebels. |
| `obj_kill_charlesarmy.scar` | objectives | Final objective: defeat Charles of Navarre's army at his encampment via kill-count progress bar. |
| `obj_optional_killroutiers.scar` | objectives | Optional objective: stop Routier raids by paying tribute OR destroying their buildings. |
| `obj_protect_monastery.scar` | objectives | Information objective: protect the Cocherel monastery from Routier/Navarre attacks; failure = mission loss. |
| `obj_find_relics.scar` | objectives | Optional objective: place relics in Holy Sites for gold income (registered but not started in main flow). |

---

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_OnGameSetup` | hun_chp2_cocherel | Assigns 4 players with named factions |
| `Mission_SetupPlayers` | hun_chp2_cocherel | Sets ages, relationships, colours for all players |
| `Mission_SetDifficulty` | hun_chp2_cocherel | Defines `t_difficulty` table via `Util_DifVar` |
| `Mission_SetRestrictions` | hun_chp2_cocherel | Reduces player1 max pop cap by 15 |
| `Mission_Preset` | hun_chp2_cocherel | Applies upgrades, building locks, initialises all objectives |
| `Mission_Start` | hun_chp2_cocherel | Sets resources, starts stem-rebel objective, sets up timers |
| `GetRecipe` | hun_chp2_cocherel | Returns MissionOMatic recipe with locations/modules/playbill |
| `SetupAttackWaves` | hun_chp2_cocherel | Creates all Wave objects and path tables |
| `FranceChaos_MoveStartingUnits` | hun_chp2_cocherel | Spawns intro army parade via `Util_UnitParade` |
| `Routiers_ShowTributeMenu` | hun_chp2_cocherel | Configures diplomacy UI to show only Routier gold |
| `Routiers_HideTributeMenu` | hun_chp2_cocherel | Disables diplomacy UI entirely |
| `RebuildTC_Villagers` | hun_chp2_cocherel | Damages player buildings, sends villagers to repair |
| `Mission_CheckTC` | hun_chp2_cocherel | Fails mission if player TC destroyed |
| `CounterMonks` | hun_chp2_cocherel | Spawns peasant monk+army to recapture holy sites |
| `MoveJouyUnit01/02` | hun_chp2_cocherel | Shuffles Jouy garrison between defend modules |
| `MoveCroisyUnit01/02` | hun_chp2_cocherel | Shuffles Croisy garrison between defend modules |
| `MoveCocherelUnits01` | hun_chp2_cocherel | Shuffles Cocherel garrison between defend modules |
| `MoveRoutiersKnights` | hun_chp2_cocherel | Rotates Routier knight garrison between positions |
| `Monitor_PlayerFoundSecret` | hun_chp2_cocherel | Creates minimap blips when player nears holy sites |
| `CheckRoutierslooted` | hun_chp2_cocherel | Awards achievement when Routier gold crates taken |
| `Cocherel_Mainloop` | hun_chp2_cocherel | Increments `cocherel_seconds` timer each second |
| `FoundRoutiersCamp` | hun_chp2_cocherel | Starts defeat-routiers objective on discovery |
| `FoundCocherelCamp` | hun_chp2_cocherel | Starts capture-Cocherel sub-objective on discovery |
| `FoundCroisyCamp` | hun_chp2_cocherel | Triggers gold-hint intel on Croisy discovery |
| `CleanIntroSkipped` | hun_chp2_cocherel | Respawns intro army at final positions if NIS skipped |
| `CaptureFrenchVillages_InitStemRebel` | obj_capture_frenchtowns | Registers parent OBJ_StemRebel objective |
| `CaptureFrenchVillages_InitJouy` | obj_capture_frenchtowns | Registers SOBJ_CaptureJouy with location binding |
| `CaptureFrenchVillages_InitCroisy` | obj_capture_frenchtowns | Registers SOBJ_CaptureCroisy with location binding |
| `CaptureFrenchVillages_InitCocherel` | obj_capture_frenchtowns | Registers SOBJ_CaptureCocherel with location binding |
| `CaptureJouy_OnComplete` | obj_capture_frenchtowns | Triggers Cocherel objective start, starts inter-village attacks |
| `CaptureCroisy_OnComplete` | obj_capture_frenchtowns | Triggers Cocherel objective start, starts inter-village attacks |
| `CaptureCocherel_OnComplete` | obj_capture_frenchtowns | Ages up player, starts Charles/Routier attacks, starts monastery protection |
| `PrepareWave_CocherelToJouyOrCroisy` | obj_capture_frenchtowns | Escalating peasant waves from Cocherel to captured towns |
| `PrepareWave_JouyOrCroisyToCocherel` | obj_capture_frenchtowns | Reverse peasant waves toward Cocherel |
| `DestroyWallCocherel_EntityKill` | obj_capture_frenchtowns | Plays celebration on palisade destruction at Cocherel |
| `DefeatCharlesBadArmy_InitObjectives` | obj_kill_charlesarmy | Registers OBJ_DefeatCharlesBadArmy + debug completes |
| `DefeatCharlesBadArmy_OnStart` | obj_kill_charlesarmy | Spawns all Navarre garrison units at camp |
| `PrepareCharlesWaveToCocherel` | obj_kill_charlesarmy | Escalating knight waves from Navarre to Cocherel |
| `EnemyKilledCharlesEvent` | obj_kill_charlesarmy | Tracks kills vs progress bar threshold |
| `DefeatCharlesBadArmy_IsComplete` | obj_kill_charlesarmy | Checks ≤15 Navarre + ≥20 player near camp, sets ending |
| `DiscoverCharlesCamp_Monitor` | obj_kill_charlesarmy | Detects front/back approach to Navarre camp |
| `SendOutroCharlesArmy` | obj_kill_charlesarmy | Spawns outro retreat/celebration units |
| `DefeatRoutiers_InitObjectives` | obj_optional_killroutiers | Registers OBJ_DefeatRoutiers with two sub-paths |
| `Routiers_AttackInit` | obj_optional_killroutiers | Sets unit type tables, schedules first attack |
| `PrepareWave_RoutiersToPlayerBase` | obj_optional_killroutiers | Escalating Routier waves to player base |
| `PrepareWave_RoutiersToCocherel` | obj_optional_killroutiers | Routier mixed-unit waves against Cocherel |
| `PayTributeRoutiers_Complete` | obj_optional_killroutiers | Dissolves Routier attack modules on tribute paid |
| `DestroyRoutiersBuildings_Start` | obj_optional_killroutiers | Monitors building kills via EGroup event |
| `Mission_OnTributeSent` | obj_optional_killroutiers | Callback: increments tribute counter toward goal |
| `ProtectMonastery_InitObjectives` | obj_protect_monastery | Registers OBJ_ProtectMonastery (fail = mission loss) |
| `CheckMonasteryIsAttacked` | obj_protect_monastery | Triggers intel when monastery under attack |
| `ProtectMonastery_IsFailed` | obj_protect_monastery | Returns true if monastery EGroup empty |
| `Diplomacy_DiplomacyEnabled` | diplomacy_chp2_cocherel | Initialises full `_diplomacy` data structure |
| `Diplomacy_CreateUI` | diplomacy_chp2_cocherel | Creates WPF XAML tribute panel in HUD |
| `Diplomacy_SendTributeNtw` | diplomacy_chp2_cocherel | Network callback: transfers resources between players |
| `Diplomacy_OverridePlayerSettings` | diplomacy_chp2_cocherel | Per-player visibility/resource enable overrides |
| `Diplomacy_OverrideSettings` | diplomacy_chp2_cocherel | Global tribute UI behaviour overrides |

---

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_StemRebel` | Primary (Capture) | Parent: recapture all three French villages |
| `SOBJ_CaptureJouy` | Sub (Capture) | Recapture Jouy from peasant rebels |
| `SOBJ_DefeatJouyRebels` | Sub (Capture) | Defeat rebel garrison at Jouy |
| `SOBJ_LocationJouy` | Sub (Capture) | Location label for Jouy |
| `SOBJ_CaptureCroisy` | Sub (Capture) | Recapture Croisy from peasant rebels |
| `SOBJ_DefeatCroisyRebels` | Sub (Capture) | Defeat rebel garrison at Croisy |
| `SOBJ_LocationCroisy` | Sub (Capture) | Location label for Croisy |
| `SOBJ_CaptureCocherel` | Sub (Capture) | Recapture Cocherel (starts after Jouy + Croisy) |
| `SOBJ_DefeatCocherelRebels` | Sub (Capture) | Defeat rebel garrison at Cocherel |
| `SOBJ_LocationCocherel` | Sub (Capture) | Location label for Cocherel |
| `OBJ_ProtectMonastery` | Information | Protect monastery; failure = mission loss |
| `OBJ_DefeatCharlesBadArmy` | Primary (Battle) | Kill threshold of Charles's army at campsite |
| `OBJ_DefeatRoutiers` | Optional | Stop Routier raids (parent with two sub-paths) |
| `SOBJ_PayTributeRoutiers` | Optional Sub | Pay gold tribute to stop Routier attacks |
| `SOBJ_DestroyRoutiersBuildings` | Optional Sub | Destroy all Routier camp buildings |
| `OBJ_RepelRoutiersAttack` | Battle | Repel first Routier wave approaching player town |
| `OBJ_DebugComplete1/2` | Debug | Debug-only mission completion shortcuts |
| `OBJ_increase_gold_income` | Primary | Find relics parent (registered, not auto-started) |
| `SOBJ_Findrelics` | Secondary | Place relics in Holy Sites for gold income |

### Difficulty

All values use `Util_DifVar({Easy, Normal, Hard, Expert})`:

| Parameter | Easy | Normal | Hard | Expert | Scales |
|-----------|------|--------|------|--------|--------|
| `given_resources_gold` | 500 | 400 | 300 | 200 | Starting gold |
| `given_resources_wood` | 1000 | 800 | 600 | 400 | Starting wood |
| `given_resources_food` | 1000 | 800 | 600 | 400 | Starting food |
| `given_resources_stone` | 250 | 200 | 150 | 100 | Starting stone |
| `i_numberUnitsToKillCharles` | 83 | 97 | 124 | 159 | Kill threshold for final objective |
| `findHolySite_NearbyDistance` | 140 | 110 | 80 | 50 | Proximity hint range for holy sites |
| `routiers_goldDemanded` | 800 | 800 | 1000 | 1400 | Gold required to pay off Routiers |
| `routiers_firstAttackDelay` | 90 | 90 | 60 | 30 | Seconds before first Routier base attack |
| `routiers_attackFrequency` | 180 | 180 | 150 | 120 | Interval between Routier base attacks |
| `cocherel_firstAttackDelay` | 50 | 50 | 30 | 10 | Delay before inter-village attacks |
| `cocherel_attackFrequency` | 180 | 180 | 150 | 120 | Interval between inter-village attacks |
| `routier_attackCocherelDelay` | 120 | 120 | 100 | 80 | Delay before Routiers attack Cocherel |
| `routier_attackCocherelInterval` | 180 | 180 | 150 | 120 | Interval of Routier-Cocherel attacks |
| `charles_firstAttackDelay` | 70 | 70 | 50 | 30 | Delay before Charles attacks Cocherel |
| `charles_attackInterval` | 180 | 180 | 150 | 120 | Interval of Charles's knight waves |

Additional per-unit scaling via `Util_DifVar` in spawn definitions (villagers: 4/3/3/3, garrison shield villagers: 6-20 range, Navarre archers: 14-25, etc.). Player pop cap reduced by 15. Pop cap increases +5 per village captured. Village capture rewards scale with difficulty (200-500 resources). Gold pickup amounts at Routier camp: 1000/800/600/400. Holy site blip hints disabled on Expert.

### Spawns

**Player starting army:** 2 scouts, 2 knights, 8 spearmen, 9 archers — deployed via `Util_UnitParade` during intro. Villagers: 13/9/9/9 across three spawn groups.

**Peasant rebel garrisons (player2):**
- Jouy: ~3 Defend modules of shield villagers (6-14 per group), with units shuffling between positions on 12-16s intervals
- Croisy: ~3 Defend modules of shield villagers (8-20 per group), similar rotation
- Cocherel: Archers (5-12) + shield villagers (8-20) + spearmen (6-12), strongest garrison with walls

**Inter-village attack waves (player2):** Cocherel sends escalating waves to Jouy/Croisy after capture (triggered on Normal+ only). Phase <4: shield villagers only. Phase 4-7: shield villagers + archers. Phase 8+: adds spearmen. Reverse waves (Jouy/Croisy → Cocherel) follow similar escalation.

**Routier waves (player3):**
- To player base: Phase 1 = 3-6 horsemen. Phases 2-3 = 5-10 horsemen. Phases 4-7 = 7-15 mixed (horseman/spearman). Phases 8-14 = 8-20 mixed (adds MaA on Hard+). Phase 15+ = capped at 25 + difficulty offset with knights.
- To Cocherel: 2-5 each of knights, horsemen, MaA per wave.
- Routier camp garrison: 2 Defend modules (MaA + spearmen), 2 roving horseman patrols (3-6), 1 knight Defend (3-6).

**Navarre forces (player4):**
- Camp garrison (spawned on objective start): 3× archer groups (14-25 each), 2× patrol groups (spearmen/MaA 7-15 each), 3× garrison groups (knights 3-7 + spearmen 6-11 each)
- Attack waves to Cocherel: knights only, phase <4 = 6-14, phase 4+ = phase_number + 3-11 offset. Two paths alternate.

**Counter-monk system:** Every 340s, player2 spawns a roving army (4 spearmen + 1 MaA + 1 monk) targeting uncaptured holy sites.

### AI

No `AI_Enable` calls — all enemy behaviour is scripted via MissionOMatic modules:
- **Defend modules:** Used for all garrisons (peasant, Routier, Navarre) with `combatRange`/`leashRange` parameters (35-90 range)
- **RovingArmy modules:** Used for all attack paths — peasant inter-village attacks, Routier raids (3 paths to player base: direct, west, east), Routier monastery attacks, Navarre attacks to Cocherel (2 paths), Routier horseman patrols (cycling between waypoints)
- **Garrison rotation:** Interval rules shuttle units between paired Defend modules to create patrol-like movement at Jouy, Croisy, Cocherel, and Routier camp
- **Wave system:** All attack waves use `Wave_New`/`Wave_Prepare`/`Wave_SetUnits` pipeline with 5s build time overrides and auto-launch after 15s staging delay

### Timers

| Rule | Type | Interval/Delay | Purpose |
|------|------|----------------|---------|
| `Cocherel_Mainloop` | Interval | 1s | Global second counter |
| `Mission_CheckTC` | Interval | 10s | Check player TC exists |
| `MoveRoutiersKnights` | Interval | 15s | Rotate Routier knight garrison |
| `MoveJouyUnit01` | Interval | 15s | Shuffle Jouy garrison A |
| `MoveJouyUnit02` | Interval | 12s | Shuffle Jouy garrison B |
| `MoveCroisyUnit01` | Interval | 16s | Shuffle Croisy garrison A |
| `MoveCroisyUnit02` | Interval | 13s | Shuffle Croisy garrison B |
| `MoveCocherelUnits01` | Interval | 8s | Shuffle Cocherel garrison |
| `CheckRoutierslooted` | Interval | 3s | Check if gold crates collected |
| `CounterMonks` | Interval | 340s | Spawn peasant monk recapture squads |
| `Monitor_PlayerFoundSecret` | Interval | 1s | Holy site proximity blip creation |
| `StartRoutiers` | OneShot | 30-90s (diff) | First Routier attack on base |
| `PrepareWave_RoutiersToPlayerBase` | Interval | 120-180s (diff) | Recurring Routier base attacks |
| `StartAttacks_CocherelToJouyOrCroisy` | OneShot | 10-50s (diff) | First inter-village attack wave |
| `PrepareWave_CocherelToJouyOrCroisy` | Interval | 120-180s (diff) | Recurring inter-village attacks |
| `StartRoutierAttacksOnCocherel` | OneShot | 80-120s (diff) | First Routier attack on Cocherel |
| `PrepareWave_RoutiersToCocherel` | Interval | 120-180s (diff) | Recurring Routier-Cocherel attacks |
| `StartCharlesAttacks` | OneShot | 30-70s (diff) | First Charles wave to Cocherel |
| `PrepareCharlesWaveToCocherel` | Interval | 120-180s (diff) | Recurring Charles attack waves |
| `DiscoverCharlesCamp_Monitor` | Interval | 1s | Detect player approach to Navarre camp |
| `RebuildTC_Villagers` | OneShot | 0.125s | Kick off village repair sequence |
| `CheckRepairStatusTC` | Interval | 10s | Monitor TC repair completion |
| `CheckRepairStatusHouse` | Interval | 12s | Monitor house repair completion |
| `SendNavarreArchersFormation` | OneShot | 2s | Move Navarre archers to position |
| `DefeatCharlesBad_MusicChange` | OneShot | 120s | Unlock music intensity after tension |
| `CheckRoutiersSquadSent` | Interval | 1s | Start/complete repel-routiers battle objective |

---

## CROSS-REFERENCES

### Imports
- `MissionOMatic/MissionOMatic.scar` — framework for locations, modules, playbill, waves
- `obj_capture_frenchtowns.scar` — village capture objectives
- `obj_kill_charlesarmy.scar` — final battle objective
- `obj_optional_killroutiers.scar` — optional Routier objective
- `obj_protect_monastery.scar` — monastery protection
- `diplomacy_chp2_cocherel.scar` — tribute/diplomacy UI
- `gameplay/xbox_diplomacy_menus.scar` — Xbox-specific diplomacy (conditional)

### Shared Globals
- `player1`–`player4`: global player references used across all files
- `t_difficulty`: difficulty parameter table created in core, read everywhere
- `difficulty`: raw `Game_GetSPDifficulty()` value
- `cocherel_seconds`: global second counter read for debug prints
- `sg_CharlesArmy`: shared SGroup for Navarre kill tracking
- `routierspaidordestroyed`, `routiers_destroyed`, `cocherel_captured`, `jouy_captured`, `croisy_capture`: global state flags
- `i_which_ending`: determines outro variant (1 = surrender, 2 = annihilated)
- `givenGold`, `i_amount_gold_given`: track tribute gold for gold-chest spawning
- `_diplomacy`: global diplomacy state table

### Inter-File Function Calls
- Core → `ProtectMonastery_InitObjectives()`, `CaptureFrenchVillages_Init*()`, `DefeatCharlesBadArmy_InitObjectives()`, `DefeatRoutiers_InitObjectives()` (called from `Mission_Preset`)
- Core → `Routiers_AttackInit()` (called via recipe `preStart` action)
- Core → `Routiers_ShowTributeMenu()` / `Routiers_HideTributeMenu()` (wraps `Diplomacy_*` calls)
- `obj_capture_frenchtowns` → `StartCharlesAttacks()`, `StartRoutierAttacksOnCocherel()` (from `CaptureCocherel_OnComplete`)
- `obj_kill_charlesarmy` → `Mission_Complete()` (on final objective complete)
- `obj_kill_charlesarmy` → `CaptureCocherel_OnComplete()` (from cheat function)
- `obj_optional_killroutiers` → `Mission_OnTributeSent()` (delegate callback from diplomacy system via `Core_CallDelegateFunctions("OnTributeSent")`)
- `obj_optional_killroutiers` → `Routiers_HideTributeMenu()` (on tribute paid or buildings destroyed)
- `obj_protect_monastery` → `Mission_Fail()` (on monastery destruction)
- Diplomacy → `Core_CallDelegateFunctions("OnTributeSent")` triggers `Mission_OnTributeSent` in kill-routiers

### Constants & Blueprints Referenced
- `EBP.FRENCH.*`: Town centers, market, religious, landmarks, palisades (locked/filtered)
- `EBP.ENGLISH.BUILDING_DEFENSE_OUTPOST_ENG`: Routier outposts
- `SBP.FRENCH.*`, `SBP.HRE.*`: Outro unit spawning
- `UPG.COMMON.UPGRADE_*`: Armor upgrades applied to player3/player4
- `EVENTS.HUN_FRANCEINCHAOS_*`: Intel/NIS event constants
- `LINE_FORMATION`: `core_formation_line` ability blueprint
- `CE_ROUTIERSLOOTED`: Custom challenge event for achievement
