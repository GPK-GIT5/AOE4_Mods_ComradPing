# Gameplay: Win Conditions

## OVERVIEW

The Win Conditions system defines how multiplayer and skirmish matches in Age of Empires IV determine winners and losers. It comprises eight independent SCAR modules — **Annihilation**, **Conquest**, **Religious**, **Wonder**, **Regicide**, **Elimination**, **Surrender**, and **Empire Wars** — each registered via `Core_RegisterModule()` and following the Core lifecycle callbacks (`OnInit`, `Start`, `OnGameOver`, `OnPlayerDefeated`). Each condition monitors game state through global events (`GE_EntityKilled`, `GE_StrategicPointChanged`, `GE_ConstructionComplete`, etc.) and interval rules, invoking `Core_SetPlayerDefeated()` or `Core_SetPlayerVictorious()` when conditions are met, then calling `Core_OnGameOver()` to end the match. All modules support team-based play (default) and free-for-all diplomacy mode via a `DiplomacyEnabled` callback. Empire Wars is a game mode modifier that layers on top of standard mode rather than being a win condition itself.

## FILE ROLES

| File | Role | Purpose |
|------|------|---------|
| annihilation.scar | core/wincondition | Eliminates a player when they have no units and cannot produce more (no buildings/resources/allies with tribute) |
| conquest.scar | core/wincondition | Eliminates a player/team when all their Landmarks (including capital Town Center) are destroyed |
| religious.scar | core/wincondition | Awards victory to whichever team captures all Holy Sites and holds them through a 10-minute countdown |
| wonder.scar | core/wincondition | Awards victory to a player who builds a Wonder and defends it through a 15-minute countdown |
| regicide.scar | core/wincondition | Eliminates a player when their King unit is killed; last King standing wins |
| elimination.scar | core/wincondition | Eliminates a player when they quit or disconnect; last remaining player/team wins |
| surrender.scar | core/wincondition | Eliminates a player when they press the Surrender button; last remaining player/team wins |
| empirewars.scar | gamemode/setup | Empire Wars game mode — spawns Age II economy (buildings, villagers, resources) at match start for all civilizations |

## FUNCTION INDEX

### Annihilation (annihilation.scar)

| Function | Purpose |
|----------|---------|
| `Annihilation_OnInit` | Caches cheapest squad cost per building type per player |
| `Annihilation_Start` | Registers GE_EntityKilled, GE_EntityLandmarkDestroyed, GE_ConstructionComplete events |
| `Annihilation_OnEntityKilled` | On unit/building death, checks if owner is annihilated |
| `Annihilation_OnLandmarkDestroyed` | On landmark destruction, checks annihilation condition |
| `Annihilation_CheckAnnihilationCondition` | Core logic: evaluates squads, production queues, resources, allied tribute |
| `Annihilation_OnConstructionComplete` | Tracks which players have built markets for tribute check |
| `Annihilation_PlayerCanReceiveTribute` | Returns true if player has an ally with a market |
| `Annihilation_CheckVictory` | Determines if last team standing; calls Core_SetPlayerVictorious |
| `Annihilation_GetActiveEnemyCount` | Returns count of non-eliminated enemies for a player |
| `Annihilation_WinnerPresentation` | Triggers victory stinger/video for local player |
| `Annihilation_LoserPresentation` | Triggers defeat/eliminated stinger/video for local player |
| `Annihilation_DiplomacyEnabled` | Toggles team vs free-for-all mode |

### Conquest (conquest.scar)

| Function | Purpose |
|----------|---------|
| `Conquest_OnInit` | Tracks all player Landmarks/capitals; registers damage/construction events |
| `Conquest_Start` | Adds objectives; starts 1s interval elimination check |
| `Conquest_CheckElimination` | Interval rule: eliminates players whose team has 0 active Landmarks |
| `Conquest_PostConstructionComplete` | Delayed handler: tracks newly constructed Landmarks |
| `Conquest_OnDamageReceived` | Shows damage notification cues with cooldown timer |
| `Conquest_CheckVictory` | Determines if last team standing; awards victory |
| `Conquest_GetPlayerLandmarkCount` | Returns built/remaining Landmark counts for a player |
| `Conquest_GetAllyLandmarkCount` | Returns combined allied Landmark counts |
| `Conquest_GetEnemyLandmarkCount` | Returns enemy Landmark counts for objective display |
| `Conquest_DestroyLandmarks` | Kills all player Landmarks on elimination to prevent ally repair |
| `Conquest_IsACapital` | Checks entity state model for capital Town Center |
| `Conquest_IsALandmark` | Checks entity type is "wonder" but not "wonder_imperial_age" |
| `Conquest_AddObjective` | Creates primary "Destroy all enemy landmarks" objective |
| `Conquest_UpdateObjective` | Updates objective counter with destroyed/total enemy Landmarks |
| `Conquest_WinnerPresentation` | Delayed victory stinger with objective popup |
| `Conquest_LoserPresentation` | Delayed defeat/eliminated stinger with team check |

### Religious (religious.scar)

| Function | Purpose |
|----------|---------|
| `Religious_OnInit` | Finds all "special_beacon" Holy Site entities; stores positions/IDs |
| `Religious_Start` | Creates objectives; starts 0.125s update interval; registers GE_StrategicPointChanged |
| `Religious_Update` | Per-site progress polling; updates UI colours/progress bars |
| `Religious_OnHolySiteChange` | Handles 12 change types (CT_Captured through CT_CapturedContestedEnded) |
| `Religious_UpdateObjectiveState` | Manages victory countdown timer start/pause/resume/cancel |
| `Religious_AllSitesControlled` | Returns true if one alliance controls all Holy Sites |
| `Religious_SitesOwnedByPlayer` | Returns count of sites owned by a specific player |
| `Religious_AddObjective` | Creates primary + per-site secondary objectives |
| `Religious_UpdateObjectiveCounter` | Updates controlled site count on primary objective |
| `Religious_ToggleCountdownObjective` | Switches objective between counter mode and timer mode |
| `Religious_HolySiteMinimapBlips` | Interval rule: pings all Holy Sites during countdown |
| `Religious_FlashAllHolySites` | Interval rule: flashes site icons during enemy countdown |
| `Religious_WinnerPresentation` | Victory stinger with objective popup |
| `Religious_LoserPresentation` | Defeat stinger with "Neutralize a Holy Site" popup |
| `Religious_UpdatePlayerStats` | Replay stat callback: reports sites owned per player |

### Wonder (wonder.scar)

| Function | Purpose |
|----------|---------|
| `Wonder_OnInit` | Scales Wonder cost by map size (1.2x/1.4x/1.6x); inits per-player timer data |
| `Wonder_Start` | Creates "Build a Wonder" objectives; registers construction/kill/damage events |
| `Wonder_OnConstructionStart` | Stores Wonder entity ID; shows "building a Wonder" cue to opponents |
| `Wonder_OnConstructionComplete` | Starts deterministic victory timer; reveals FOW; creates defend/destroy objectives |
| `Wonder_OnConstructionCancelled` | Unreveals FOW around cancelled Wonder |
| `Wonder_OnEntityKilled` | On Wonder destruction: ends timer, removes objective, notifies players |
| `Wonder_OnDamageReceived` | Shows "Wonder under attack" cue with 30s cooldown |
| `Wonder_Update` | 1s interval: updates timer display, triggers countdown notifications at thresholds |
| `Wonder_CheckVictory` | 1s interval: checks if any player's timer reached 0; awards victory |
| `Wonder_AddObjective1` | Creates "Build a Wonder" primary objective |
| `Wonder_AddObjective2` | Converts to "Defend/Destroy Wonder" with countdown timer |
| `Wonder_RemoveObjective2` | Removes defend/destroy objective when Wonder is destroyed |
| `Wonder_EndWonderVictoryTimer` | Ends victory timer and resets state model (used by Salisbury campaign) |
| `Wonder_WinnerPresentation` | Victory stinger with "Defend your Wonder" popup |
| `Wonder_LoserPresentation` | Defeat stinger with "Destroy %PLAYER%'s Wonder" popup |
| `Wonder_UpdatePlayerStats` | Replay stat callback: reports timer remaining or construction status |

### Regicide (regicide.scar)

| Function | Purpose |
|----------|---------|
| `Regicide_OnInit` | Validates player count; spawns Kings; registers entity/player killed events |
| `Regicide_Start` | Creates objective UI with enemy King counter and population display |
| `Regicide_SpawnKings` | Spawns civ-specific King unit near each player's Town Center |
| `Regicide_UpdateEntityKilled` | On King death: eliminates owner, grants killer +50 pop bonus |
| `Regicide_CheckWinner` | If a player has 0 enemy Kings alive, award victory to their team |
| `Regicide_KilledKingBonus` | Applies +50 max population modifier to killing player |
| `Regicide_GetEnemyKingCount` | Counts living enemy Kings via SGroup_IsAlive checks |
| `Regicide_GetSquad` | Maps civ name to King unit blueprint (all 22 civs including variants) |
| `Regicide_SetupObjective` | Creates primary objective with King counter + population sub-objective |
| `Regicide_UpdateObjective` | Refreshes enemy King count and population cap display |
| `Regicide_OnPlayerDefeated` | Kills all player squads and Landmarks on Regicide defeat |

### Elimination (elimination.scar)

| Function | Purpose |
|----------|---------|
| `Elimination_OnPlayerAITakeover` | Handles player disconnect: shows notification, defeats player |
| `Elimination_OnPlayerDefeated` | Kills all Landmarks, kills player, checks victory |
| `Elimination_CheckVictory` | Last-team-standing check with winnerless fallback |
| `Elimination_GetActiveEnemyCount` | Returns count of non-eliminated enemies |

### Surrender (surrender.scar)

| Function | Purpose |
|----------|---------|
| `Surrender_Start` | Registers "Surrender_Notify" network event |
| `Surrender_OnSurrenderMatchRequested` | Broadcasts surrender to all peers via Network_CallEvent |
| `Surrender_Notify` | Network callback: receives surrender, shows cue, defeats player |
| `Surrender_OnPlayerDefeated` | Kills Landmarks + player; checks victory; reveals FOW |
| `Surrender_CheckVictory` | Last-team-standing check with winnerless fallback |

### Empire Wars (empirewars.scar)

| Function | Purpose |
|----------|---------|
| `EmpireWars_OnGameSetup` | Pauses challenge tracking during setup |
| `EmpireWars_PreInit` | Finds buildings, sets up starting area, spawns sheep, sets pasture rally |
| `EmpireWars_OnInit` | Finds all map resources; spawns villagers, prelates, scholars, Joan |
| `EmpireWars_Start` | Spawns Imperial Officers; queues villagers/upgrades at buildings |
| `EmpireWars_FindBuildings` | Per-civ building discovery (TC, mill, lumber camp, mining camp, gers, mosque) |
| `EmpireWars_SpawnVillagers` | Spawns and assigns 18-23 villagers per civ to food/wood/gold/stone tasks |
| `EmpireWars_FindMatchingBuildings` | Queries `_townGen` global for buildings by town/spawnSet/structureGroup IDs |
| `EmpireWars_SpawnPrelates` | HRE: spawns prelates near food and gold |
| `EmpireWars_SpawnImperialOfficers` | Chinese: spawns officers supervising mill and lumber camp |
| `EmpireWars_SpawnScholars` | Delhi: spawns 2 scholars garrisoned in mosque |
| `EmpireWars_SpawnJoan` | French HA: spawns Jeanne d'Arc with tier 2 experience |
| `EmpireWars_QueueUpgrades` | Delhi: queues Wheelbarrow, Forestry, Enhanced Production |
| `EmpireWars_GrantUpgrades` | Japanese: grants Towara (wheelbarrow) upgrade free at farmhouse |
| `EmpireWars_GrantVizierExp` | Ottoman: grants 30 Vizier Experience at start |
| `EmpireWars_MaliMineSwitch` | Mali: swaps small pit mine for large if on large gold deposit |

## KEY SYSTEMS

### Win Condition Architecture

All win conditions follow a shared module pattern:

1. **Registration**: `Core_RegisterModule(name)` — registers the module with the Core framework
2. **Lifecycle callbacks**: `_OnInit()`, `_Start()`, `_OnGameOver()`, `_OnPlayerDefeated(player, reason)`
3. **Diplomacy toggle**: `_DiplomacyEnabled(bool)` — switches between team-based (default) and free-for-all evaluation
4. **Defeat flow**: condition detected → `Core_SetPlayerDefeated(id, presentation_fn, WR_*)` → `_OnPlayerDefeated` callback → `World_KillPlayer()` → victory check
5. **Victory flow**: no enemies remain → `Core_SetPlayerVictorious(id, presentation_fn, WR_*)` for allies → `Core_OnGameOver()`
6. **Winnerless fallback**: if no human players remain, `Core_WinnerlessGameOver()` gracefully ends the match

### Win Reason Constants

| Constant | Win Condition |
|----------|---------------|
| `WR_ANNIHILATION` | Annihilation |
| `WR_CONQUEST` | Conquest (Landmark) |
| `WR_RELIGIOUS` | Religious (Holy Sites) |
| `WR_WONDER` | Wonder |
| `WR_REGICIDE` | Regicide (King) |
| `WR_ELIMINATION` | Elimination (disconnect) |
| `WR_SURRENDER` | Surrender |

### Annihilation — Detailed Logic

A player is annihilated when **all** of these are true:
- Zero squads tagged with `"annihilation_condition"` unit class (excluding siege-only splats/planned structures)
- No units currently in any production queue (`PITEM_Spawn`)
- No Landmark with production capability, **OR** has production buildings but cannot afford the cheapest unit from any of them
- No ally with a market can send tribute (when tribute is enabled)

Building types checked for cheapest unit cost: `town_center` → villager, `barracks` → spearman, `archery_range` → archer, `stable` → horseman, `siege_workshop` → springald, `monastery` → monk.

### Conquest — Detailed Logic

- Tracks entities with type `"wonder"` (Landmarks) and `"town_center_capital"` / state model `"town_center_is_capital"` (capitals)
- Excludes entities with type `"wonder_imperial_age"` (actual Wonders — those are tracked by wonder.scar)
- A Landmark is considered **active** when `Entity_IsValid(id)` and `Entity_GetStateModelBool(entity, "landmark_active")` is true
- **Team elimination**: triggered when all allies' combined Landmarks have `built > 0` and `remaining == 0`
- On elimination, `Conquest_DestroyLandmarks()` calls `Entity_Kill()` on all player Landmarks to prevent ally repair
- Damage notifications use a 30-second cooldown timer per Landmark (`conquest.landmark_damage_timer_%d`)
- Construction tracking uses a 0.25s delayed handler (`Conquest_PostConstructionComplete`) to allow deferred data model updates

### Religious — Detailed Logic

- Holy Sites are found via `World_GetAllEntitiesOfType(eg, "special_beacon")`
- Capture progress tracked per-site per-player via `Player_GetStrategicPointCaptureProgress()` (returns 0→1 for allies, 0→-1 for enemies)
- Capture state changes handled through 12 `changeType` values from `GE_StrategicPointChanged`:
  - `CT_Captured (0)` — site ownership transferred
  - `CT_Reverting (1)` — owned site being neutralized
  - `CT_UnCaptured (3)` — site fully neutralized
  - `CT_StartedCapture (5)` — capture begins/resumes
  - `CT_StartedCooldown (6)` — progress decrementing after monk exits
  - `CT_StartedRevertingCooldown (7)` — reverting cooldown after squad death
  - `CT_Halted (8)` / `CT_CapturedContested (10)` — progress paused due to enemy presence
  - `CT_CapturedContestedEnded (11)` — all contesting units leave
- Victory countdown: **10 minutes** (`time_victory = 10 * 60`), started when one alliance holds all sites
- Timer pauses when any site is contested (`CT_Reverting`, `CT_Halted`, `CT_CapturedContested`)
- Timer resumes when contesting ends (`CT_StartedRevertingCooldown`, `CT_CapturedContestedEnded`)
- Timer cancels entirely if alliance loses control of any site
- Countdown notifications at 3min, 2min, 1min with escalating music intensity
- Monks required within `conversion_radius` (10.0) to capture/neutralize

### Wonder — Detailed Logic

- Victory countdown: **15 minutes** (`time_victory = 15 * 60`), started on `GE_ConstructionComplete` for type `"wonder_imperial_age"`
- Wonder cost scales with map size: 1.2x (512/4-player), 1.4x (640/6-player), 1.6x (768+/8-player)
- Cost modifier applied via `Modifier_Create(MAT_EntityType, "resource_entity_cost_*", MUT_Multiplication)`
- FOW revealed in 12.0 radius around Wonder on construction start and completion
- Damage notification cooldown: 30 seconds per Wonder (`wonder_damage_timer_%d`)
- Countdown notifications at 12min, 9min, 6min, 3min, 2min, 1min with escalating music intensity
- Music locked to `MUSIC_TENSE` at 3min, `MUSIC_TENSE_COMBAT_RARE` at 2min, `MUSIC_RARE` at 1min
- Timer is deterministic (`timer_victory_deterministic`) — synced across all peers
- Wonder destruction ends timer, removes objectives, unreveals FOW
- Both `Wonder_Update` (1s) and `Wonder_CheckVictory` (1s) run as separate interval rules
- `Wonder_EndWonderVictoryTimer` exposed for Salisbury campaign integration
- Command-line override: `timer` parameter sets countdown in minutes

### Regicide — Detailed Logic

- King spawned per-player near Town Center using civ-specific blueprint (22 civs supported including variant civs)
- King death detected via `GE_EntityKilled` filtered by `Entity_IsOfType(context.victim, "King")`
- Killing a King grants **+50 max population** to the killer via `Modifier_Create(MAT_Player, "max_personnel_cap_player_modifier")`
- Mongol civs additionally get +50 `personnel_cap_player_modifier` (current pop, not just cap)
- On defeat, all player squads and Landmarks are killed (`SGroup_Kill`, `KillAllLandmarks`)
- Objective displays enemy King count + current population cap as sub-objective

### Elimination & Surrender — Shared Pattern

Both follow the same flow:
1. **Trigger**: Player quits/disconnects (Elimination) or presses Surrender button (Surrender)
2. **Broadcast**: Elimination uses `OnPlayerAITakeover`; Surrender uses `Network_CallEvent("Surrender_Notify")`
3. **Defeat**: `Core_SetPlayerDefeated()` → `KillAllLandmarks()` → `World_KillPlayer(id, KPR_Lost)`
4. **Victory check**: last-team-standing evaluation with winnerless fallback for AI-only games
5. **Presentation**: uses Conquest stinger sounds (`ConquestVictoryEvent`/`ConquestDefeatEvent`)
6. **Diplomacy**: both reference `_annihilation.is_diplomacy_enabled` for eliminated vs defeated display text

### Empire Wars — Game Mode Setup

Empire Wars is not a win condition but a game mode that layers on standard mode. Key aspects:
- **Imports**: `cardinal.scar`, `gathering_utility.scar`, `gamemodes/standard_mode.scar`, `missionomatic/missionomatic_utility.scar`
- **Per-civ villager counts** (18-23 villagers total): defines wood/gold/stone/sheep/farm/berry/cattle assignments for all 22+ civilizations
- **Resource finding**: uses `Gathering_FindAllResources()` to locate all map resources (wood, stone, gold, forage, sheep, deer, shore fish, deep fish, cattle)
- **Civ-specific spawns**: HRE prelates (2), Delhi scholars (2 garrisoned), Chinese Imperial Officers (2 supervising), Ottoman Vizier exp (+30), French HA Joan d'Arc (tier 2), Japanese Towara upgrade (free)
- **Town-gen integration**: `EmpireWars_FindMatchingBuildings()` queries `_townGen` global for spawned buildings by town/spawnSet/structureGroup IDs
- **Challenge tracking**: paused during setup (`Game_PauseChallengeTracking`), resumed after all spawns complete
- **Economy setup**: queues 4 villagers at TC (2 for HRE HA), queues Delhi upgrades (Wheelbarrow, Forestry, Enhanced Production)

### Timers

| Timer/Rule | File | Interval | Purpose |
|------------|------|----------|---------|
| `Conquest_CheckElimination` | conquest.scar | 1.0s | Check if any player's team Landmarks are all destroyed |
| `Religious_Update` | religious.scar | 0.125s | Poll Holy Site capture progress and update UI |
| `capture_victory_timer` | religious.scar | 10 min | Victory countdown after all sites captured |
| `wonder_victory_timer_%d` | wonder.scar | 15 min | Per-player deterministic victory countdown |
| `Wonder_Update` | wonder.scar | 1.0s | Update Wonder timer display and countdown notifications |
| `Wonder_CheckVictory` | wonder.scar | 1.0s | Check if any Wonder timer reached 0 |
| `wonder_damage_timer_%d` | wonder.scar | 30s cooldown | Damage notification cooldown per Wonder |
| `conquest.landmark_damage_timer_%d` | conquest.scar | 30s cooldown | Damage notification cooldown per Landmark |

### Presentation System

All win conditions use `_gameOver_message` (a one-shot rule) with a standardized parameter table:
- `_playerID` — affected player
- `_icon` — objective icon path
- `_endType` — localized "VICTORY", "DEFEAT", or "ELIMINATED" string
- `_sound` — stinger event name
- `_videoURI` — "stinger_victory", "stinger_defeat", or "stinger_eliminated"

Music stingers escalate during countdowns: `MUS_STING_PRIMARY_OBJ_COMPLETE_ENDGAME` for victory, `MUS_STING_PRIMARY_OBJ_FAIL` for defeat.

### Objective System Integration

All conditions create objectives via `Obj_Create()` with data templates:
- Conquest: `ConquestObjectiveTemplate` — progress bar with destroyed/total counter
- Religious: `HolySiteObjectiveDataTemplate` (primary) + `HolySiteSecondaryObjectiveDataTemplate` (per-site)
- Wonder: `WonderObjectiveTemplate` — switches from counter to timer on construction
- Regicide: `RegicideObjectiveDataTemplate` + `RegicideSecondaryObjectiveDataTemplate` (population sub-obj)
- "Or" variants (`*OrObjectiveTemplate`): used when multiple win conditions active (not the first primary)

Global `_first_primary_objective` tracks the first registered primary objective for template selection.

### Replay Statistics

Three win conditions integrate with `replaystatviewer.scar`:
- **Conquest**: `ConquestTrackerTemplate` — Landmarks built vs remaining
- **Religious**: `ReligiousTrackerTemplate` — Relics (sites) target vs current
- **Wonder**: `WonderTrackerTemplate` — timer target vs current (or -1 if not constructed)

## CROSS-REFERENCES

### Imports

| File | Imports |
|------|---------|
| religious.scar | `replay/replaystatviewer.scar` |
| wonder.scar | `replay/replaystatviewer.scar`, `cardinal.scar` |
| conquest.scar | `replay/replaystatviewer.scar` |
| regicide.scar | `replay/replaystatviewer.scar`, `cardinal.scar` |
| empirewars.scar | `cardinal.scar`, `gathering_utility.scar`, `gamemodes/standard_mode.scar`, `missionomatic/missionomatic_utility.scar` |

### Shared Globals

| Global | Used By | Purpose |
|--------|---------|---------|
| `PLAYERS` | All files | Global players table iterated for team checks |
| `player_local` | conquest, religious, wonder | Cached local player reference |
| `_first_primary_objective` | conquest, religious, wonder, regicide | Tracks first objective for template selection |
| `_annihilation.is_diplomacy_enabled` | elimination, surrender | Referenced for defeated vs eliminated display |
| `_townGen` | empirewars | Town generation data for building lookup |
| `GAMEOVER_OBJECTIVE_TIME` | All win conditions | Delay before game-over message display |

### Inter-Module Dependencies

- **Elimination/Surrender → Annihilation**: both reference `_annihilation.is_diplomacy_enabled` in loser presentation
- **Elimination/Surrender → Conquest**: both use `KillAllLandmarks()` (global utility) and Conquest stinger sounds
- **Empire Wars → Standard Mode**: imports and layers on top of `gamemodes/standard_mode.scar`
- **Wonder → Salisbury Campaign**: exposes `Wonder_EndWonderVictoryTimer()` for campaign use
- **All → Core**: all modules depend on `Core_RegisterModule`, `Core_SetPlayerDefeated`, `Core_SetPlayerVictorious`, `Core_OnGameOver`, `Core_IsPlayerEliminated`
- **Religious/Wonder**: both support command-line `timer` override for countdown duration testing

### Cross-File Function Calls

| Caller | Callee | Function |
|--------|--------|----------|
| elimination.scar | global | `KillAllLandmarks(player)` |
| surrender.scar | global | `KillAllLandmarks(player)` |
| regicide.scar | global | `KillAllLandmarks(player)` |
| empirewars.scar | gathering_utility | `Gathering_FindAllResources()`, `Gathering_AssignVillagersTo*()` |
| empirewars.scar | cardinal | `Cardinal_ConvertTypeToEntityBlueprint()`, `BP_GetSquadArchetypeBlueprintForPlayer()` |
| conquest.scar | annihilation | `Annihilation_LoserPresentation` (winnerless game over fallback) |
| wonder.scar | cardinal | `Cardinal_ConvertTypeToEntityBlueprint()` |
