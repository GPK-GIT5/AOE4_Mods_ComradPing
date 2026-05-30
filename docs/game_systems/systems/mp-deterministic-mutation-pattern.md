# Multiplayer Deterministic Mutation Pattern (UI → Network → Handler)

**Status:** Authoritative architecture reference for any SCAR system that mutates simulation state in response to a UI action, timer, or per-peer condition.

**Audience:** Onslaught (and future) gamemode contributors. Applies to BoonUI selections, reward unlocks, debug prompts, surrender, tribute, age-up choices, and any future "player decides → game changes" feature.

**One-line rule:** *Local UI captures intent; the simulation is mutated only inside a function dispatched by `Network_CallEvent`.*

---

## 1. Why This Pattern Exists

AoE4's multiplayer simulation is **lockstep deterministic**: every peer must execute identical script code against identical state every simulation frame. Two failure modes produce a hard sync error:

1. **Local-only mutation** — one peer mutates a player/world value the others do not.
2. **Local-conditional branching that mutates** — `if Game_GetLocalPlayer() == p then Player_CompleteUpgrade(...) end` runs on exactly one peer's CPU.

Both are easy to introduce accidentally, especially via UI callbacks (which are *always* local-only) and per-player loops that read `Game_GetLocalPlayer()` / `localPlayer.civ` to decide what to do.

---

## 2. The Authoritative Boundary

```
┌────────────────────┐      Network_CallEvent       ┌──────────────────────────┐
│  LOCAL ONLY        │ ──────────────────────────►  │  RUNS ON EVERY PEER      │
│  (intent capture)  │  Command_PlayerBroadcastMsg  │  (sim mutation)          │
│                    │       enqueues on            │                          │
│  • UI clicks       │       engine command queue   │  • Player_CompleteUpgrade│
│  • Timeout fires   │                              │  • Player_SetCurrentAge  │
│  • Default pick    │       GE_BroadcastMessage    │  • Modify_*, World_*     │
│                    │       fires on every peer    │  • Cmd_*, Squad_*        │
│  Calls:            │       → Network_Callback     │                          │
│   Network_CallEvent│       → _G[handler](sender,  │  Reads:                  │
│                    │              data)           │   sendingPlayer, data    │
│  Never calls:      │                              │  Never reads:            │
│   Player_*Mutate   │                              │   Game_GetLocalPlayer()  │
│   Modify_*         │                              │   for gameplay decisions │
└────────────────────┘                              └──────────────────────────┘
```

The boundary is `Network_CallEvent`. Anything *before* it is local presentation; anything *inside* the registered handler is synchronized simulation.

---

## 3. Verified Execution Flow

Cited evidence (do not paraphrase, do not infer):

| Stage | Code | Evidence |
|---|---|---|
| 1. UI button bound to a global by name | `cmd_1 = UI_CreateCommand("BoonSelection_OnClick1")` | [boon_selection.scar#L77](../../Gamemodes/Onslaught/assets/scar/boonui/boon_selection.scar#L77) |
| 2. Click → resolver → callback | `pcall(cb, idx)` | [boon_selection.scar#L260](../../Gamemodes/Onslaught/assets/scar/boonui/boon_selection.scar#L260) |
| 3. Callback should call **only** `Network_CallEvent` | `Network_CallEvent(eventName, "p,c")` | Pattern (see §4) |
| 4. Engine broadcast | `Command_PlayerBroadcastMessage(local,local,evtId,msg)` | [scar_dump/network.scar#L29](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/network.scar#L29) |
| 5. Per-peer dispatch | `Rule_AddGlobalEvent(Network_Callback, GE_BroadcastMessage)` then `_G[func](data.player, data.message)` | [scar_dump/network.scar#L11](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/network.scar#L11), [#L34-L40](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/network.scar#L34) |
| 6. Sim mutation runs on every peer | `Game_ChartACourseGrantPlayerUpgradeChoice(sendingPlayer, selected_index)` (comment: *"Called from network function above, executed locally on all machines"*) | [scar_dump/.../chart_a_course.scar#L433-L449](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/gamemodes/chart_a_course.scar#L433) |

The official `chart_a_course.scar` is the strongest reference implementation in the script dump and should be treated as the canonical template.

---

## 4. Canonical Template

Copy this shape verbatim for any new "UI → mutation" system.

```lua
-- =============================================================================
-- 1. REGISTER ONCE (e.g., from Mod_OnInit / Mod_PreInit / module OnPlay)
-- =============================================================================
function MyMod_OnInit()
    Network_RegisterEvent("MyMod_ApplyChoiceNtw")
end

-- =============================================================================
-- 2. UI / TIMER / AUTOPICK ENTRY POINTS — local-only, NO mutation
-- =============================================================================

-- Called from UI button click closure / BoonSelection on_select
function MyMod_RequestApplyChoice(player_index, choice_index)
    -- Pack everything the handler will need into a string payload.
    local data = string.format("%d,%d", player_index, choice_index)
    Network_CallEvent("MyMod_ApplyChoiceNtw", data)
end

-- Called when a per-peer fallback path needs to make the same choice
-- (timeout, AI, non-local autopick). MUST also go through Network_CallEvent.
function MyMod_RequestAutoPickFor(target_player, choice_index)
    -- IMPORTANT: only one peer should originate the request to avoid duplicate
    -- broadcasts. Pick a deterministic owner: the local peer if the target is
    -- local, otherwise the host or a designated "owner" peer.
    if not target_player.isLocal then return end
    MyMod_RequestApplyChoice(target_player.index, choice_index)
end

-- =============================================================================
-- 3. SYNCHRONIZED HANDLER — runs on EVERY peer, mutates the sim
-- =============================================================================

-- Must be a top-level global (Network_Callback uses _G[name]).
function MyMod_ApplyChoiceNtw(sendingPlayer, data)
    local parts = string.split(data) -- comma-separated
    local player_index = tonumber(parts[1])
    local choice_index = tonumber(parts[2])

    -- Resolve the TARGET player by index (deterministic).
    -- Do NOT use Game_GetLocalPlayer() to identify the target.
    local target = World_GetPlayerAt(player_index)
    if target == nil then return end

    -- === Sim mutation (runs on every peer with identical inputs) ===
    local upg_bp = BP_GetUpgradeBlueprint(MyMod_LookupUpgradeName(choice_index))
    Player_CompleteUpgrade(target, upg_bp)
    -- Any other Modify_/World_/Cmd_ calls go here.

    -- === UI-only side effects (gated to the local viewer) ===
    if sendingPlayer == Game_GetLocalPlayer() then
        UI_CreateEventCue(LOC("$xxxx;Choice applied"), Loc_Empty(), ...)
        -- Cleanup the panel, play a sound, etc.
    end
end
```

### Five non-negotiables

1. **Register before first call.** `network_events[eventName]` must be populated before the broadcast or the engine sees an invalid event id.
2. **The handler is a top-level global.** `Network_Callback` resolves it via `_G[func]`. Local functions and closures cannot be handlers.
3. **The payload is a string.** Encode all needed values (player index, choice index, sub-options) into a delimited string and parse on the other side. Do not capture closures.
4. **Identify the target by index, not by `Game_GetLocalPlayer()`.** The local player differs per peer; the target must be the same on every peer.
5. **`Game_GetLocalPlayer()` inside the handler is allowed only for UI-only side effects** (event cues, sounds, panel removal). Never for gameplay branching.

---

## 5. Anti-Patterns (forbidden in any future code)

### A) UI callback mutates the sim directly

```lua
-- ❌ DO NOT DO THIS
BoonSelection_Show({
    choices = choices,
    on_select = function(idx)
        Player_CompleteUpgrade(player.id, upg_bp)   -- runs ONLY on local peer
        Player_SetCurrentAge(player.id, target_age) -- runs ONLY on local peer
    end,
})
```

### B) Local/non-local branching that decides whether to mutate

```lua
-- ❌ DO NOT DO THIS
if not player.isLocal then
    return MyMod_AutoPick(player) -- non-local mutates immediately
end
BoonSelection_Show(...)           -- local waits for click
-- Result: peers diverge whenever the local player picks anything other than
-- the autopick default.
```

### C) Per-player loop that reads `localPlayer.*` for the decision

```lua
-- ❌ DO NOT DO THIS
for _, p in ipairs(PLAYERS) do
    local civ = Player_GetRaceName(localPlayer.id) -- always local's civ!
    if civ == "malian" then ... end
end
```

### D) Closure passed to `Rule_AddOneShot` / handler

```lua
-- ❌ DO NOT DO THIS
Rule_AddOneShot(function() Player_CompleteUpgrade(...) end, 5)
-- Handlers and rules require named globals for determinism.
```

---

## 6. Onslaught Migration Plan

The following sites currently violate §5 and must be migrated. Listed in order of impact.

### 6.1 BoonUI special-civ age-up — `cba_auto_age.scar` (HIGH, reproducible sync error)

**Affected functions / lines:**

- [`CBA_AutoAge_ForceSpecialAgeChoicePrompt`](../../Gamemodes/Onslaught/assets/scar/gameplay/cba_auto_age.scar#L962) — local/non-local split at L983; closure `_OnSpecialChoice` mutates at L1025/L1040
- [`CBA_AutoAge_TryAutoSelectSpecialUpgrade`](../../Gamemodes/Onslaught/assets/scar/gameplay/cba_auto_age.scar#L877) — direct mutation at L938/L950 on each peer

**Migration steps:**

1. Add a registered event during `Mod_OnInit`:
   ```lua
   Network_RegisterEvent("CBA_AutoAge_ApplySpecialChoiceNtw")
   ```
2. Create `CBA_AutoAge_RequestApplySpecialChoice(target_player_index, target_age, choice_index)` that does *only* `Network_CallEvent("CBA_AutoAge_ApplySpecialChoiceNtw", string.format("%d,%d,%d", target_player_index, target_age, choice_index))`.
3. Replace the body of `_OnSpecialChoice(idx)` (the BoonSelection callback) with a single call to that requester. Remove `Player_CompleteUpgrade`, `Player_SetCurrentAge`, `CBA_Options_RevalidateAll`, `ReconcileSpecialProgress`, `SyncSpecialUpgradeAvailability` from inside the closure.
4. Replace the body of `CBA_AutoAge_TryAutoSelectSpecialUpgrade` with: compute the autopick *index* deterministically, then call the requester (gated so only one peer originates — see §4 step 5 in the template).
5. Implement `CBA_AutoAge_ApplySpecialChoiceNtw(sendingPlayer, data)` as a top-level global containing **all** existing mutation logic from both paths. Resolve target by `World_GetPlayerAt(target_player_index)`. Recompute `upg_name` from `(civ, tier, choice_index)` inside the handler — do not pass blueprint handles across the network.
6. Move every `print("[AUTOAGE] ...")` log line that names a mutation result into the handler so logs match across peers.
7. Keep BoonSelection panel show / hide / timeout *strictly local*. The panel is presentation only; no panel API call may run inside the handler.
8. Verification: with two human peers, force every special-civ tier with `CBA_Auto_Age_AgeUp(PLAYERS[1])` + `BoonDebug_ForceSelect(2)` and `(3)`. No sync error and identical `Player_HasUpgrade` results on both peers.

### 6.2 `AGS_Toggle_EconBuildings` — `ags_auto_resources.scar` (HIGH)

**Site:** `for _, player in ipairs(PLAYERS)` reads `Player_GetRaceName(localPlayer.id)` to gate Malian ranch removal — see [ags_auto_resources.scar#L74](../../Gamemodes/Onslaught/assets/scar/AGS/options/ags_auto_resources.scar#L74) (verify line on read).

**Migration:** the loop already iterates per player; replace `localPlayer.id` / `localPlayer.civ` with `player.id` / `player.raceName`. No network event needed — the function already runs on every peer; only the read was wrong.

### 6.3 Reward unlock callbacks — `cba_rewards_onslaught.scar`

**Audit task (not an immediate bug):** confirm that no `on_unlock` / reward callback mutates inside an `if player.isLocal` branch. If any do, migrate them through the same pattern (`CBA_Rewards_ApplyRewardNtw`).

### 6.4 Debug UI prompts — `cba_debug_ui_prompts.scar`

These are debug-only and may stay local. Add a header comment stating they are unsafe in MP and should not be used to drive gameplay.

### 6.5 PlayerUI / observer UI

Verified read-only / presentation-only (see prior audit). No migration required. Add a top-of-file comment in `playerui.scar` and `playerui_updateui.scar` reaffirming "no Player_*/World_*/Modify_* mutation in this module".

---

## 7. Reference Implementations to Copy From

In priority order:

1. **Official:** [`chart_a_course.scar`](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/gamemodes/chart_a_course.scar) — register at L239, broadcast at L425/L430, handler at L433. UI cue gated by `sendingPlayer == Game_GetLocalPlayer()` at L443. AI parallel at L411.
2. **Official:** [`diplomacy.scar`](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/diplomacy.scar) — `Diplomacy_ChangeRelationNtw` (L124, L206), `Diplomacy_SendTributeNtw` (L125, L280).
3. **Official:** [`combat_mode.scar`](../../game_data/extracted/aoe4/scar_dump/scar%20gameplay/gamemodes/combat_mode.scar) — `CombatMode_Surrender` (L444, L1162).
4. **Onslaught (correct):** [`ags_surrender.scar`](../../Gamemodes/Onslaught/assets/scar/AGS/conditions/ags_surrender.scar) — register L33, broadcast L50, handler L83.

If any new gamemode mutation cannot be expressed as `(target_index, choice_index)` plus a small string payload, simplify the design until it can.

---

## 8. Determinism Verification Checklist (per system migration)

- [ ] `Network_RegisterEvent("<Name>")` is called exactly once, before first broadcast.
- [ ] Handler is declared as a top-level global function (no `local function`, no closure).
- [ ] Handler resolves target player via `World_GetPlayerAt(index)` or equivalent — never `Game_GetLocalPlayer()` for gameplay decisions.
- [ ] Every mutation API (`Player_*`, `Modify_*`, `World_*`, `Cmd_*`, `Squad_*`, `Entity_*`) called by the system lives inside the handler.
- [ ] No `if player.isLocal` / `if Game_GetLocalPlayer() == ...` branch contains a mutation.
- [ ] No closure is passed to `Rule_AddOneShot` / `Rule_AddInterval` / `Rule_AddGlobalEvent` for any mutation path.
- [ ] Payload is a string only; no Lua references, no blueprint handles.
- [ ] Repro test: two human peers, every code path exercised, no sync error, identical post-state.

---

## 9. Open Items / Inferred Behavior

These remain inferred (see the strict verification companion analysis) and should be re-checked if engine source becomes available:

- Exact ordering / latency / drop semantics of `Command_PlayerBroadcastMessage`.
- Whether `GE_BroadcastMessage` fires exactly once per peer per broadcast under packet loss / replay.
- Behavior when a non-host human peer originates a broadcast (assumed symmetric; not directly demonstrated in dump).

The pattern in §4 is robust under all reasonable interpretations of these unknowns because every peer enters the handler with the same `(sendingPlayer, data)` and never reads `Game_GetLocalPlayer()` for a mutation decision.
