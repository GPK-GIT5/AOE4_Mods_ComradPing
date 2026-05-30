# Hundred Years War Chapter 1: Combat30

## OVERVIEW

The "Combat of the Thirty" is a Hundred Years War campaign mission where the player controls Jean de Beaumanoir (French) in a staged melee tournament against the English. The mission flows through three phases: an **Approach** phase where the player recruits up to 4 French champion heroes via side-quests (killing wolves, defeating raiders, winning a duel, defending an outpost); a **Pre-Round** phase where the player selects 2 of the recruited champions via a custom diplomacy/tribute UI panel to compose their army; and a **Combat** phase consisting of two arena rounds (15 kills each in Round 1, full elimination in Round 2) with a break interval for reinforcement and blacksmith research. An achievement tracks whether the player loses ≤10 units across both rounds.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| `hun_chp1_combat30.scar` | core | Main mission script: imports all sub-files, defines variables, player setup, restrictions, recipe/modules, intro/outro sequences, and shared helper functions. |
| `diplomacy_hun_chp1_combat30.scar` | other (UI) | Customized diplomacy/tribute panel repurposed as the champion selection UI during pre-round phase. |
| `obj_approach.scar` | objectives | Defines approach-phase objectives: recruit 4 champions (primary requires 2, optional for remaining), arrive at Halfway Oak. |
| `obj_preround.scar` | objectives | Defines pre-round objectives: select champions from panel, spawn English army, trigger combat start. |
| `obj_combat.scar` | objectives | Defines combat-phase objectives: Round 1, break, Round 2, unit counters, elimination checks, gate locking, outro. |
| `training_combat30.scar` | training | Tutorial goal sequences teaching leader aura abilities for Beaumanoir, Arrel, Rochefort, Charruel, and Blois; plus blacksmith hint. |

## FUNCTION INDEX

| Function | File | Purpose (10 words max) |
|----------|------|------------------------|
| `Mission_SetupVariables` | hun_chp1_combat30 | Initializes all globals, SGroups, recruit data, unit compositions |
| `Mission_SetupPlayers` | hun_chp1_combat30 | Configures 8 players, relationships, colors, ages, AI |
| `Mission_SetRestrictions` | hun_chp1_combat30 | Sets pop caps, resources, build times, invulnerable buildings |
| `Mission_Preset` | hun_chp1_combat30 | Applies upgrades, spawns champions, initializes intro units |
| `Mission_Start` | hun_chp1_combat30 | Starts recruit modules and OBJ_RecruitChampions |
| `GetRecipe` | hun_chp1_combat30 | Returns MissionOMatic recipe with modules and playbill |
| `Combat30_SpawnChampions` | obj_approach | Deploys all 4 champion heroes and escorts at map locations |
| `Approach_InitObjectives` | obj_approach | Registers all approach-phase objectives and sub-objectives |
| `Recruit1_Trigger` | obj_approach | Proximity check to start wolf-killing sub-objective |
| `Recruit1_SpawnWolves` | obj_approach | Spawns 5 wolves and fleeing villagers for Recruit 1 |
| `Recruit2_SpawnEnglishRaid1` | obj_approach | Spawns 8 horsemen raiders for Recruit 2 encounter |
| `Recruit2_SpawnEnglishRaid2` | obj_approach | Spawns 6 spearmen + 2 MAA second raider wave |
| `Recruit3_SpawnDuel` | obj_approach | Spawns Yves Charruel and villager audience for duel |
| `Recruit3_CheckDuelComplete` | obj_approach | Completes Recruit 3 when Charruel health < 50% |
| `Recruit4_SpawnEnglishArchers` | obj_approach | Spawns difficulty-scaled archers for Recruit 4 |
| `Recruit4_SpawnEnglishWaves` | obj_approach | Starts 90s tower-defend timer with 6 attack waves |
| `Recruit4_SpawnRandomWave` | obj_approach | Spawns random wave from horsemen/spearmen/MAA compositions |
| `Combat30_Recruit_BoundaryCheck` | obj_approach | Fails objective if player leaves recruitment boundary |
| `Combat30_IncrementChampionCounter` | obj_approach | Tracks recruited champion count, updates objective counter |
| `Combat30_AddOptionToRecruitPanel` | obj_approach | Adds recruited champion to diplomacy selection panel |
| `Combat30_SpawnChampionsAtBase` | obj_approach | Warps recruited champions to staging base markers |
| `Combat30_StartTravellers` | obj_approach | Sends ambient traveller groups along main path every 25s |
| `Combat30_ToggleBeaumanoirSlow` | obj_approach | Toggles 0.615x speed modifier on leader Beaumanoir |
| `Combat30_FailCheck` | obj_approach | Fails mission if player has no remaining squads |
| `PreRound_InitObjectives` | obj_preround | Registers pre-round build/select objectives |
| `PreRound_SpawnEnglish` | obj_preround | Spawns difficulty-scaled English army with hint points |
| `BuffLandsknecht` | obj_preround | Applies 1.9x health modifier to Landsknecht units |
| `Combat30_ShowTributeMenu` | obj_preround | Opens champion selection UI via diplomacy panel |
| `UI_ReinforcePanel_UpdateData` | obj_preround | Updates champion panel data context for each recruit |
| `UI_RequestAid_ButtonCallback` | obj_preround | Handles champion selection button, spawns player units |
| `Combat30_SpawnPlayerUnitsFromSelection` | obj_preround | Deploys selected champion's unit composition at base |
| `Start_CTACooldown` | obj_preround | Shows reinforcement CTA, plays stinger, 20s cooldown |
| `Combat_InitObjectives` | obj_combat | Registers Round 1, Break, Round 2, and debug objectives |
| `Combat30_CombatStart` | obj_combat | Starts OBJ_Combat1 after 18s delay |
| `Combat1_EnteredArena` | obj_combat | Detects player entering arena, transfers English to attack |
| `Combat_LockGate` | obj_combat | Locks arena gates when all squads inside |
| `Combat30_TransferEnglishToAttack` | obj_combat | Transfers English from passive player5 to aggressive player2 |
| `Combat30_UnitCountUpdate` | obj_combat | Updates English kill counter (out of 30) on UI |
| `Combat30_FirstRoundComplete` | obj_combat | Ends Round 1 when either side reaches 15 kills |
| `Combat30_ChooseBreakVO` | obj_combat | Selects break VO based on kill differential |
| `Combat30_ReturnToBase` | obj_combat | Sends armies back to bases after Round 1 |
| `Combat30_ReturnToField` | obj_combat | Sends English back to arena for Round 2 |
| `Combat30_EliminationCheck` | obj_combat | Checks full elimination to end Round 2 |
| `Combat30_RebuildToCounter` | obj_combat | Rebuilds English army to counter player's unit kills |
| `Combat30_AchievementTracker` | obj_combat | Tracks player unit losses for achievement (≤10) |
| `Combat30_GrantAchievement` | obj_combat | Grants "Du Bois Are Back In Town" achievement |
| `Combat30_OnSquadKilled` | obj_combat | Tracks kills per side, triggers cheering and UI update |
| `MissionTutorial_BeaumanoirAura` | training_combat30 | Tutorial: select Beaumanoir, view attack speed ability |
| `MissionTutorial_ArrelAura` | training_combat30 | Tutorial: select Arrel, view healing ability |
| `MissionTutorial_RochefortAura` | training_combat30 | Tutorial: select Rochefort, view reduce armor ability |
| `MissionTutorial_CharruelAura` | training_combat30 | Tutorial: select Charruel, view armor boost ability |
| `MissionTutorial_BloisAura` | training_combat30 | Tutorial: select Blois, view movement speed ability |
| `MissionTutorial_Combat30Blacksmith` | training_combat30 | Tutorial: highlights blacksmith during break phase |
| `Diplomacy_DiplomacyEnabled` | diplomacy | Initializes diplomacy data context and state |
| `Diplomacy_CreateUI` | diplomacy | Creates XAML-based champion selection panel UI |
| `Diplomacy_UpdateDataContext` | diplomacy | Updates tribute-enabled state and per-player visibility |

## KEY SYSTEMS

### Objectives

| Constant | Type | Purpose |
|----------|------|---------|
| `OBJ_RecruitChampions` | Primary | Recruit 2 of 4 champions before proceeding (counter 0/2) |
| `SOBJ_Recruit1` | Battle (sub) | Kill wolves attacking villagers to recruit Olivier Arrel |
| `SOBJ_Recruit2` | Battle (sub) | Defeat English raiders to recruit Guy de Rochefort |
| `SOBJ_Recruit3` | Battle (sub) | Win a duel against Yves Charruel (reduce to <50% HP) |
| `SOBJ_Recruit4` | Battle (sub) | Defeat English longbowmen + defend outpost 90s for Geoffroy du Bois |
| `OBJ_Arrive` | Primary | Travel to the Halfway Oak staging area |
| `OBJ_RecruitChampions_Optional` | Optional | Recruit remaining champions after first 2 collected |
| `SOBJ_Recruit1_Optional` – `SOBJ_Recruit4_Optional` | Battle (sub) | Optional versions of each recruit sub-objective |
| `OBJ_BuildForce` | Primary | Select 2 champions from the diplomacy panel |
| `SOBJ_RecruitInfantry` | Secondary (sub) | Counter tracks champion selections (0/2) |
| `OBJ_TipEnglishForces` | Tip | Informational tip about English forces |
| `OBJ_TipDiploController` | Tip | Xbox controller hint: open diplomacy panel |
| `OBJ_Combat1` | Battle | Round 1 — defeat English soldiers (15 kills to win) |
| `SOBJ_EngUnits1` | Battle (sub) | Remaining English units counter (x/30) |
| `OBJ_Break1` | Primary | Reinforce units and research technology between rounds |
| `SOBJ_Return` | Secondary (sub) | Return to the field when prepared |
| `OBJ_Combat2` | Battle | Round 2 — full elimination of English soldiers |
| `SOBJ_EngUnits2` | Battle (sub) | Remaining English units counter (x/30) |
| `OBJ_DebugComplete` | Primary (debug) | Debug-only: skip to outro |

### Difficulty

| Parameter | Values (Story/Easy/Normal/Hard) | What it scales |
|-----------|---------------------------------|----------------|
| `combat30_unitCompositions_*` | 4 tables | English army composition — Landsknecht count (4/6/4+4/4+5), cavalry mix |
| `Recruit4 archer count` | 9 / 10 / 11 / 12 | Number of archers in Recruit 4 initial wave |
| `Recruit4 wave horsemen` | 4/4/5/5 | Horsemen per tower-defense wave |
| `Recruit4 wave spearmen` | 3/4/5/6 | Spearmen per tower-defense wave |
| `Recruit4 wave MAA` | 3/4/4/5 | Men-at-arms per tower-defense wave |
| `Recruit4 wave knight` | 1/1/1/2 | Knights per tower-defense wave |
| Starting gold | 750/750/450/150 | Player starting gold resources |
| Hard-only upgrades | — | player2/5 get Melee Armor III + Damage III on Expert |

### Spawns

- **Recruit 1 (Wolves):** 5 wolves at fixed markers, 2 fleeing villagers as bait. Wolves dealt 0.66x damage modifier.
- **Recruit 2 (Raiders):** Wave 1 at 3s — 8 horsemen. Wave 2 at 5s — 6 spearmen + 2 MAA. Both via RovingArmy modules.
- **Recruit 3 (Duel):** 1 Yves Charruel spawned at duel marker, villager audience at surrounding positions.
- **Recruit 4 (Tower Defense):** Initial wave of difficulty-scaled archers. Then 6 timed waves at 0s/18s/34s/48s/60s/70s with random spawn points (west/east/south). Composition randomized from 5 unit mixes.
- **Pre-Round English Army:** Randomly selected from 2 compositions (MAA/Spear or MAA/Cavalry), spread across 6 spawn markers. Landsknecht units buffed with 1.9x health.
- **Pre-Round French Army:** 4 spearmen + 5 MAA deployed as baseline, plus selected champion's unit package (e.g., 9 spearmen + Arrel, or 4 lancers + 5 horsemen + Blois).
- **Crowd:** 8 villagers per side at 2 markers each (French + English spectators), weapon range set to 0.01, untargetable.
- **Travellers:** Ambient villagers/spearmen/trade carts spawned every 25s along a 20-waypoint path.
- **Round 2 Rebuild:** English can be rebuilt to counter player's most-killed unit type (on Normal/Hard).

### AI

- `AI_Enable(player6, false)` — Downed leader holder player has AI disabled.
- **RovingArmy modules:** `Attack1` (aggressive attack-move to combat field), `EnglishRaid1`/`EnglishRaid2` (leashed to recruit 2 boundary), `EnglishArchers1`–`EnglishArchers7` (leashed to recruit 4 boundary).
- **Defend modules:** `DefendEngBase`, `DefendRecruit1`, `DefendRecruit2` — static formation spawners.
- English army transferred from passive `player5` to aggressive `player2` via `Combat30_TransferEnglishToAttack()` when combat begins.
- No traditional AI plans — all behavior is module/script-driven.

### Timers

| Timer/Rule | Delay | Purpose |
|------------|-------|---------|
| `Recruit1_Trigger` – `Recruit4_Trigger` | 1s interval | Proximity checks to start recruit sub-objectives |
| `Recruit2_MidBanner1` | 3s one-shot | Spawn first English raid wave |
| `Recruit2_MidBanner2` | 5s one-shot | Transfer recruit 2 to player, enable movement |
| `Recruit4_MidBanner` | 8s one-shot | Transfer recruit 4 to player ownership |
| `Recruit4_SpawnEnglishWaves` timers | 0/18/34/48/60/70s | 6 timed tower-defense attack waves |
| `Recruit4_TowerDefended` | 90s (`defendTimer`) | Marks tower as successfully defended |
| `Combat30_CombatStart` | 18s one-shot | Starts OBJ_Combat1 after pre-round intel |
| `Combat30_CompleteBreak` | 18s one-shot | Completes OBJ_Break1 after returning to field |
| `Combat30_BeaumanoirLowHealth` | 1s interval | Plays injured VO if Beaumanoir downed (45s cooldown) |
| `Combat30_FailCheck` | 1s interval | Checks if player has lost all units |
| `Combat30_SendTraveller` | 25s interval | Spawns ambient traveller groups |
| `UI_ReinforcePanel_UpdateData` | 1s interval | Refreshes champion selection panel data |
| `ReinforceCTA_Cooldown` | 20s one-shot | Resets reinforcement CTA cooldown flag |
| `Combat30_FirstRoundComplete` | 1s interval | Checks if either side reached 15 kills (Round 1) |
| `Combat30_OnSeeEnglishAudioStinger` | 2s interval | Plays music stinger when English first visible |
| `Combat1_ReturnedToBase` | 4s interval | Checks if all French returned to base after Round 1 |
| `Combat1_ReturnedToField` | 2s interval | Detects player re-entering arena for Round 2 |

## CROSS-REFERENCES

### Imports
- `hun_chp1_combat30.scar` imports: `MissionOMatic/MissionOMatic.scar`, `obj_approach.scar`, `obj_preround.scar`, `obj_combat.scar`, `diplomacy_hun_chp1_combat30.scar`, `training_combat30.scar`
- `diplomacy_hun_chp1_combat30.scar` imports: `gameplay/xbox_diplomacy_menus.scar` (conditional on Xbox UI)
- `training_combat30.scar` imports: `training/campaigntraininggoals.scar`
- `obj_preround.scar` imports: `cardinal.scar`

### Shared Globals
- `g_leaderBeaumanoir` — leader table initialized via `Missionomatic_InitializeLeader`, used across all files
- `player1`–`player8` — 8 player handles used extensively across all files
- `sg_recruit1`–`sg_recruit4`, `sg_recruit*_escort` — champion SGroups shared between approach/preround/combat
- `sg_eng_army`, `sg_fre_army` — army SGroups shared between preround and combat
- `t_recruitData`, `t_availableRecruitData` — champion data tables shared between core and preround
- `recruitedChampions`, `recruitFailedCount` — counters shared between approach objectives
- `damageScale` — 0.75 damage modifier applied to both armies in arena
- `freKills`, `engKills` — kill counters shared between combat objectives and break VO selection
- `_diplomacy` — diplomacy state table shared between diplomacy file and preround show/hide calls
- `EVENTS.*` — intel event table referenced across all objective files

### Inter-File Function Calls
- `obj_approach.scar` calls `PreRound_SpawnEnglish()`, `Combat30_ShowTributeMenu()`, `Combat30_HideTributeMenu()`
- `obj_preround.scar` calls `Diplomacy_ShowDiplomacyUI()`, `Diplomacy_ShowUI()`, `Combat30_RetreatRecruitSGroup()`, `MoveToAndRespectFacing()` (from obj_approach)
- `obj_combat.scar` calls `Combat30_RemoveProduction()`, `Combat30_ReaddProduction()`, `Combat30_RetreatAllUnselectedChampions()`, `MissionTutorial_Combat30Blacksmith()`
- `training_combat30.scar` functions called by `obj_approach.scar` recruit PreStart/PreComplete handlers (e.g., `MissionTutorial_BeaumanoirAura()`, `MissionTutorial_ArrelAura()`)
- `Diplomacy_*` functions from diplomacy file called by preround and core files for UI management

### Blueprint References
- `SBP.FRENCH.UNIT_JEAN_DE_BEAUMANOIR_CMP_FRE` — leader hero
- `SBP.FRENCH.UNIT_OLIVIER_ARREL_CMP_FRE` — champion 1 (healing aura)
- `SBP.FRENCH.UNIT_GUY_DE_ROCHEFORT_CMP_FRE` — champion 2 (reduce armor aura)
- `SBP.FRENCH.UNIT_YVES_CHARRUEL_CMP_FRE` — champion 3 (armor aura)
- `SBP.FRENCH.UNIT_GEOFFROY_DU_BLOIS_CMP_FRE` — champion 4 (movement speed aura)
- `unit_landsknecht_mercenary_3_hre_cmp` — English Landsknecht (buffed 1.9x HP)
- Ability BPs: `leader_attack_speed_activated_lowcd`, `leader_healing_activated_lowcd`, `leader_reduce_armor_activated_lowcd`, `leader_decay_armor_activated_lowcd`, `leader_move_speed_activated_lowcd`

### Achievement
- **"Du Bois Are Back In Town"** (Achievement #13): Win both arena rounds with ≤10 player units lost. Tracked via `CE_ACHIEVNODEATHSINCOMBAT30ARENA`.
