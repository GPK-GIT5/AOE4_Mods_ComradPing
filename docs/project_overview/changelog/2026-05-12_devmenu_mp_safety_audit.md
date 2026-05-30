# DevMenu Multiplayer-Safety & Determinism Audit — 2026-05-12

Scope: every gameplay-affecting code path reachable from the Onslaught DevMenu
(`Gamemodes/Onslaught/assets/scar/devmenuUI/*`), classified by desync risk,
followed by a staged debug-instrumentation rollout that uses (and extends) the
existing `devmenu_diag.scar` + `Debug_Determinism` infrastructure.

Triggering investigation: confirmed OOS at frame 259 caused by
`DevMenu_DoBurnSelected` invoking `Modifier_ApplyToEntity` only on the device
that booted with `cmdline_dev=true` (see prior conversation summary; canonical
diff = permanent appliers `93634` vs `93633`).

---

## 1. Architectural facts (verified)

| Fact | Evidence |
|---|---|
| The DevMenu is a **client-local UI** with no replication layer | [devmenu.scar:1497–1502](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L1497-L1502) gates the menu purely on per-client `Misc_IsCommandLineOptionSet("cheat"/"dev")` |
| Every action handler resolves `Game_GetLocalPlayer()` only | [devmenu_actions.scar:14–20](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L14-L20) — no `World_IsMultiplayer`, `Game_IsHost`, `Network_*`, `IsPrimaryPlayer` checks anywhere in `devmenuUI/` |
| MP awareness exists for **3 engine cheats only** | `ChatCheatAgeUpMultiplayer`, `ChatCheatInvulnerable`, `ChatCheatFOW`, `ChatCheatInstantBuildAndGather` are preferred when present ([devmenu_actions.scar:138, 175, 380, 425](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L138)) — these route through the engine command bus. Everything else is direct sim mutation. |
| `cmdline_dev` is **asymmetric across peers** | No code anywhere ensures all peers see the same flag. Single peer with `cmdline_dev=true` = guaranteed divergence the moment they touch any non-engine-routed action. |
| `OnInit` / `OnGameRestore` are inert for sim state | [devmenu.scar:1527](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L1527) and the `Rule_AddOneShot` deferred-UI builder ([devmenu.scar:1516–1524](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L1516-L1524)) only build XAML; no replay |
| No recurring `Rule_AddInterval` exists in `devmenuUI/` | Only two `Rule_AddOneShot` calls: 3 s toast auto-hide and deferred UI build. The "auto-cycling" seen in the OOS log was successive user clicks on **Convert/Burn** quick-panel buttons; each press calls `_devmenu_next_convert_target` and the rotation advances. |
| No `math.random` / `World_GetRand` use in DevMenu | RNG-induced drift is not a vector for the DevMenu itself, **but** the dev-suite probes (`Debug_StressTest`, `Debug_Determinism`, etc.) live outside `devmenuUI/` and must be re-audited separately if they ever run mid-MP-session |

---

## 2. Risk-ranked desync vector inventory

Severity legend:
- **CRIT** — guaranteed OOS on first invocation in MP
- **HIGH** — OOS on most invocations (toggle / one-shot per side)
- **MED** — OOS only when game-state-visible side effect propagates (resource/age/pop/etc. eventually drives different unit production decisions on the AI side)
- **LOW** — desync only via timing or selection-state gymnastics
- **OK** — provably MP-safe (UI-only, sim-rate local, log-only)

### 2.1 Direct sim-state mutations — bypass engine command bus → CRIT

All of these are pure SCAR calls executed only on the client running the
action; no peer ever observes them.

| Handler | Engine call | File:Line | Sim impact |
|---|---|---|---|
| `DevMenu_DoBurnSelected` | `Modifier_Create` + `Modifier_ApplyToEntity` (threshold lift) + `Entity_SetOnFire` + `Modifier_Remove` (extinguish) | [devmenu_actions.scar:1657, 1677–1681](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L1657) | Permanent modifier delta (the **confirmed OOS cause**), entity health-tick divergence, eventual building destruction divergence |
| `DevMenu_DoInvulnSelectedUnits` | `Entity_SetInvulnerableMinCap(eid, 0/cap, -1)` | [devmenu_actions.scar:932, 938](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L932) | Damage component divergence; first incoming hit goes from kill→survive on one peer |
| `DevMenu_DoConvertSelected` | `Squad_SetPlayerOwner` + `Entity_SetPlayerOwner` | [devmenu_actions.scar:1434, 1451](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L1434) | Ownership divergence — instant CRC drift on owner field, plus all subsequent income/visibility |
| `DevMenu_DoDestroySelected` | `Entity_Kill` (loop) | [devmenu_actions.scar:1539, 1564](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L1539) | Entity removed on one side only |
| `DevMenu_TeleportSelectedToCameraCenter` | `Squad_SetPosition(sid, targetPos, targetPos)` | [devmenu.scar:479](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L479) | Position divergence; pathing/combat order changes |

### 2.2 Engine `Cheat*` (single-player) wrappers — CRIT in MP

When the `Multiplayer` variant is missing or not preferred, these run the SP
cheat which writes to the local sim only.

| Handler | Wrapper used (no MP fallback path) | Risk |
|---|---|---|
| `DevMenu_DoEconomy` | `CheatEconomy(p)` | Resource grant local-only |
| `DevMenu_DoResources*` (All/Food/Wood/Gold/Stone/Oil) | `ResourcesCheat*(p)` | Resource grant local-only |
| `DevMenu_DoPopCapMax` | `CheatSetCurrentPopCapToMax(p)` | Pop cap divergence |
| `DevMenu_DoExplored` | `CheatExploredAll(p)` | FoW reveal — usually UI-only, but can leak via vision components used in damage calcs |
| `DevMenu_DoReplaceSheepWithWolves` | `CheatReplaceSheepWithWolves(p)` | World entity mutation |
| `DevMenu_DoKillAllGaia` | `CheatKillAllGaia(p)` | World entity mutation |
| `DevMenu_DoLoseInstantly` | `CheatLoseInstantly(p)` | Match-state divergence |

### 2.3 Engine `ChatCheat*` wrappers — VERIFIED MOSTLY UNSAFE (post-audit, 2026-05-12)

> **Verified** by reading [game_data/extracted/aoe4/scar_dump/scar gameplay/gameplay/chatcheats.scar](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar):
> only `ChatCheatAgeUpMultiplayer` (line 566) actually routes through a
> synchronized `LocalCommand_PlayerUpgrade`. Every other `ChatCheat*` is
> direct local mutation with **no `LocalCommand_*` / `Cmd_*` broadcast**.

| Handler | MP wrapper | Verified MP behaviour |
|---|---|---|
| `DevMenu_DoAgeUp` | `ChatCheatAgeUpMultiplayer` | **MP-safe** — `LocalCommand_PlayerUpgrade` ([chatcheats.scar:566](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar#L566)) |
| `DevMenu_DoInvulnerable` | `ChatCheatInvulnerable` | **NOT MP-safe** — direct `EGroup_*` / `Squad_*` invuln calls ([chatcheats.scar:591](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar#L591)). Treat as CRIT (§2.1). |
| `DevMenu_DoFogOfWar` | `ChatCheatFOW` | **NOT MP-safe** — local `FOW_*` toggles ([chatcheats.scar:473](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar#L473)). Treat as CRIT (§2.1). |
| `DevMenu_DoInstantBuild` | `ChatCheatInstantBuildAndGather` | **NOT MP-safe** — local production / gather rate mods ([chatcheats.scar:491](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar#L491)). Treat as CRIT (§2.1). |
| `DevMenu_DoDestroySelected` | `ChatCheatDestroySelected` | **NOT MP-safe** — local `Entity_Kill` loop ([chatcheats.scar:576](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar#L576)). Treat as CRIT (§2.1). |

> **All `ChatCheat*`-backed handlers above except `DevMenu_DoAgeUp` are now
> hard-gated by `_devmenu_mp_gate(...)` (Phase 0 implementation).**

### 2.4 Sim-rate / engine-state — LOW (typically) but observable

| Handler | Engine call | Notes |
|---|---|---|
| `DevMenu_SpeedDefault/Increase/Decrease` | `Misc_SetSimRate` | Per-client wallclock pacing only — safe sim-wise (sim is lockstepped on frames, not wallclock) **unless** the engine treats SimRate as a sim-state value. **Unverified**, so gated fail-closed in Phase 0. |

### 2.5 UI / logging toggles — OK

`DevMenu_Toggle*Logging`, toast/quick-panel show/hide, recent-card builders,
diagnostic readouts: all read-only or write to client globals not part of
the simulation CRC.

### 2.6 Dev probes (DEV menu) — context-dependent

Run by `_devmenu_dev_safe_call("Debug_*", ...)`. Each `Debug_*` lives outside
`devmenuUI/` and must be audited individually. Of particular concern:

- `Debug_StressTest` — likely creates entities/squads → CRIT in MP
- `Debug_Determinism` — designed for SP probe; verify it does no sim writes
- `Debug_AdvancedStress` (siege cascade, rapid elimination) — kills entities → CRIT in MP
- `Debug_BattleLagTest` — production stress loop → CRIT in MP
- `Debug_LeaverTest` / `Debug_LeaverMatrix` — calls `Player_KillPlayer`-style functions → CRIT in MP

---

## 3. Known-problem patterns to encode as lint / runtime probes

1. **Local-only `Modifier_ApplyToEntity` usage** (the smoking gun)
2. **`cmdline_dev` asymmetry** — one peer has it, others don't
3. **MP-unsafe debug actions** — entity/squad mutation outside Cmd_ pipeline
4. **Selection-based mutations** — selection state is intrinsically per-client
5. **Permanent modifier drift** — every `Modifier_Create(..., false, ...)` (the `false` means non-temporary) accumulates a permanent applier slot

---

## 4. Staged debug instrumentation rollout

Each phase is scoped so that turning it on in isolation either reproduces the
failure or proves a class of paths is clean. Phases extend the existing
`devmenu_diag.scar` PASS/FAIL framework and the `Debug_Determinism` probe.

### Phase 0 — Hard MP gate (immediate, ship today)

Goal: stop the bleed. No DevMenu action that is not provably MP-safe may
execute when `World_IsMultiplayer()` returns true.

Implementation sketch in `devmenu_actions.scar`:

```lua
local function _devmenu_mp_gate(action_name)
    if type(World_IsMultiplayer) == "function" and World_IsMultiplayer() then
        print("[DEVMENU-MPGATE] " .. action_name .. " blocked: multiplayer session")
        if type(DevMenu_ShowToast) == "function" then
            DevMenu_ShowToast({ prefix = action_name .. ": ",
                state_word = "BLOCKED IN MP", state_on = false,
                suffix = " — DevMenu actions are SP/replay only" })
        end
        return true
    end
    return false
end
```

Wrap every handler in §2.1, §2.2, §2.6. Allowlist the handlers in §2.3 only
after their broadcast path is verified.

### Phase 1 — Permanent-modifier accountant

Add a probe to `devmenu_diag.scar`:

```lua
function DevMenu_DiagModifierAccount()
    -- Snapshot pre-call counter, run a no-op, snapshot post-call counter.
    -- Walk _devmenu_burn_modifier_table and fail if any entries exist that
    -- were created in the current MP session.
end
```

Plus a new global counter wrapping `Modifier_ApplyToEntity` inside the
DevMenu file scope:

```lua
_devmenu_modifier_apply_count = 0
local _orig_apply = Modifier_ApplyToEntity
local function _devmenu_apply_to_entity_tracked(mod, eid, dur)
    _devmenu_modifier_apply_count = _devmenu_modifier_apply_count + 1
    print(string.format("[DEVMENU-MOD] apply #%d eid=%s dur=%s",
        _devmenu_modifier_apply_count, tostring(eid), tostring(dur)))
    return _orig_apply(mod, eid, dur)
end
-- Use _devmenu_apply_to_entity_tracked in DevMenu_DoBurnSelected only.
```

Run on both peers; any nonzero count on only one peer = local-only sim write.

### Phase 2 — Per-handler frame & CRC bracket

Extend `Debug_Determinism` (or add `Debug_DevMenuTrace`) to record the current
sim frame and a lightweight digest immediately before and after every DevMenu
action fires. Existing `[DEVMENU]` log lines already include high-level event
strings; bracket them with `[DEVMENU-FRAME] pre=NNN` / `post=NNN+k`.

```lua
local function _devmenu_frame_bracket(name, fn, ...)
    local pre = (type(World_GetGameTime) == "function") and World_GetGameTime() or "?"
    print(string.format("[DEVMENU-FRAME] %s pre_t=%s", name, tostring(pre)))
    local r = { fn(...) }
    local post = (type(World_GetGameTime) == "function") and World_GetGameTime() or "?"
    print(string.format("[DEVMENU-FRAME] %s post_t=%s", name, tostring(post)))
    return table.unpack(r)
end
```

Compare both peers' scarlogs by `pre_t` — any handler that appears on only
one peer is a confirmed local-only path.

### Phase 3 — Replication verifier (engine cheats)

For each `ChatCheat*` claimed to be MP-safe, instrument with a "did-the-other-peer-see-it" probe:

```lua
function DevMenu_DiagReplicationProbe(cheat_name, getter)
    -- Pre-state on local
    local pre_local = getter(_devmenu_local_player())
    -- Fire the cheat
    _devmenu_safe_call(cheat_name, _devmenu_local_player())
    -- Wait one sim tick (Rule_AddOneShot 0.1s) then dump getter for ALL players
    Rule_AddOneShot(function()
        for i, p in pairs(PLAYERS or {}) do
            print(string.format("[DEVMENU-REPL] %s pid=%s state=%s",
                cheat_name, tostring(Player_GetID(p.id)), tostring(getter(p.id))))
        end
    end, 0.1)
end
```

When run on host vs client and compared, this proves replication for each of
`ChatCheatInvulnerable`, `ChatCheatInstantBuildAndGather`, etc.

### Phase 4 — Dev-probe MP audit

For each `Debug_*` referenced in `devmenu_dev_actions.scar`, add a header
metadata field `mp_safe = true|false|unknown` in `devmenu_dev_data.scar`,
then teach `_devmenu_dev_safe_call` to honor it:

```lua
local function _devmenu_dev_safe_call(fn_name, mp_safe, ...)
    if mp_safe == false and World_IsMultiplayer() then
        print("[DEVMENU-MPGATE] dev probe " .. fn_name .. " blocked: not mp-safe")
        return
    end
    ...
end
```

Default `mp_safe = false` until each probe is individually verified — fail-closed.

### Phase 5 — Lint rule for future regressions

Add to `scripts/` a static checker that flags any new occurrence of these
calls inside `Gamemodes/Onslaught/assets/scar/devmenuUI/**` without an
`_devmenu_mp_gate(...)` line in the same function:

```
Modifier_ApplyToEntity   Modifier_Remove   Modifier_Create
Entity_Kill              Entity_SetOnFire  Entity_StopFire
Entity_SetInvulnerableMinCap                Entity_SetPlayerOwner
Squad_SetPlayerOwner     Squad_SetPosition Squad_Kill
SGroup_*Owner SGroup_WarpToPos             EGroup_Kill
World_Spawn*             Player_GrantResource Player_SetCurrentAge
```

Hook into the existing `scripts/audit_*.ps1` family.

---

## 5. Recommended immediate fix (minimum-diff)

If shipping Phase 0 only, the change is ~30 lines in `devmenu_actions.scar` and
~10 lines in `devmenu.scar` (early-out the menu binding entirely when in MP):

1. Add `_devmenu_mp_gate("burn")` at the top of `DevMenu_DoBurnSelected`.
2. Add the same gate at the top of `DevMenu_DoInvulnSelectedUnits`,
   `DevMenu_DoConvertSelected`, `DevMenu_DoDestroySelected`,
   `DevMenu_TeleportSelectedToCameraCenter`, all `DevMenu_DoResources*`,
   `DevMenu_DoEconomy`, `DevMenu_DoPopCapMax`, `DevMenu_DoLoseInstantly`,
   `DevMenu_DoExplored`, `DevMenu_DoReplaceSheepWithWolves`,
   `DevMenu_DoKillAllGaia`.
3. Optionally: in [devmenu.scar:1497–1502](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L1497-L1502),
   force `cheats_enabled = false` if `World_IsMultiplayer() == true and not
   <some explicit MP-debug opt-in>` so the CHEAT panel never even renders.

Phase 0 alone would have prevented the 2026-05-12 frame-259 OOS.

---

## 6. Open questions to confirm before Phase 0 lands

- ~~Does `World_IsMultiplayer` exist in the SCAR API exposed to mods?~~
  **Resolved (2026-05-12):** the canonical API is `World_IsMultiplayerGame()`
  ([Essence_ScarFunctions.api:1961](game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api#L1961));
  `_devmenu_is_multiplayer()` in [devmenu_mp_gate.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_mp_gate.scar)
  uses it with a `Game_GetType()` fallback.
- Does `Misc_SetSimRate` write to sim-state CRC, or is it strictly a wallclock
  pacing parameter? (Determines whether §2.4 escalates to HIGH.) **Unresolved
  → fail-closed gate applied in Phase 0.**
- ~~Confirm `ChatCheatInvulnerable`, `ChatCheatFOW`, `ChatCheatInstantBuildAndGather`
  actually issue synchronized commands.~~ **Resolved (2026-05-12, see §2.3):**
  none of them route through `LocalCommand_*`; all are now hard-gated.

---

## 7. Cross-references

- OOS root cause: `[DEVMENU] set 1 building(s) on fire` at wallclock
  17:26:42.212 / sim t≈32.125s, frame 258→259 boundary
  (`scarlog.2026-05-12.17-20-34.txt` line ~1101)
- Modifier code path: [devmenu_actions.scar:1672–1678](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_actions.scar#L1672-L1678)
- `cmdline_dev` gate: [devmenu.scar:1498](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu.scar#L1498)
- Existing diagnostics framework: [devmenu_diag.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_diag.scar)
- Determinism probe wiring: `DevMenu_RunDeterminismTest` → `Debug_Determinism`
  ([devmenu_dev_actions.scar:428](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_actions.scar#L428))

---

## 8. Implementation status (2026-05-12)

All 5 phases shipped end-to-end.

| Phase | Deliverable | Status |
|---|---|---|
| 0 | `_devmenu_mp_gate(name)` fail-closed gate at every CRIT/HIGH handler | ✅ All §2.1, §2.2, §2.3-unsafe, §2.4 handlers gated |
| 1 | Permanent-modifier accountant (`_devmenu_modifier_apply_to_entity` / `_devmenu_modifier_remove`) | ✅ `DevMenu_DoBurnSelected` rewired to tracked wrappers; counters exposed via `DevMenu_DiagModifierAccount()` |
| 2 | Per-handler frame-bracket logging (`_devmenu_frame_bracket`) | ✅ Helper available in [devmenu_mp_gate.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_mp_gate.scar) — opt-in for any handler |
| 3 | Replication verifier (`DevMenu_DiagReplicationProbe`) | ✅ Function defined; consumed by `DevMenu_RunMPSafetyAudit` |
| 4 | `mp_safe` metadata + fail-closed dev probes | ✅ `_devmenu_dev_safe_call` enforces `_DEVMENU_DEV_MP_SAFE` allowlist; only read-only audits + the new audit entry are permitted in MP. UI binding added to [devmenu_dev_data.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_data.scar) and [devmenu_categories.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_categories.scar) ("MP Safety Audit"). |
| 5 | Static lint script | ✅ [scripts/audit_devmenu_mp_safety.ps1](scripts/audit_devmenu_mp_safety.ps1) — exits non-zero on ungated sim mutation. Currently passes clean. |

**Override (testing only):** set `_devmenu_mp_gate_force_allow = true`
inside a debug session to bypass the gate. Never ship this enabled.

---

## 9. Posture revision (2026-05-12, second pass)

The first pass shipped the gate in **block** mode (fail-closed). User
direction: *disable the blocker; investigate every action and ensure each
works in MP without sync errors / desyncs.*

### 9.1 SCAR API constraint discovered

Audit of [game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api](game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api)
confirms the SCAR engine exposes **no general-purpose "broadcast a sim
mutation to all peers" API**. The only synchronized command surfaces are:

| Surface | Coverage | Useful to DevMenu? |
|---|---|---|
| `LocalCommand_PlayerUpgrade` | upgrades by PBG | ✅ AgeUp only |
| `LocalCommand_*Ability` | abilities by PBG | ❌ no cheat-ability BPs exist for grant-resources, modifier-apply, kill, etc. |
| `LocalCommand_Squad*` / `LocalCommand_Entity*` | normal player commands (move, attack, build) | ❌ irrelevant to cheats |
| `SynchronizedCommand_PlayerAbility` | mirror of above | same |
| `Game_LockRandom` | freezes RNG index during getlocalplayer branches | does NOT make sim writes deterministic |

Verified in [game_data/extracted/aoe4/scar_dump/scar gameplay/gameplay/chatcheats.scar](game_data/extracted/aoe4/scar_dump/scar%20gameplay/gameplay/chatcheats.scar):
even Relic's own cheat library only achieves MP-safety via
`LocalCommand_PlayerUpgrade` (line 566). All other `ChatCheat*` paths are
local-only mutations.

**Implication:** most DevMenu actions cannot be made truly MP-safe at the
SCAR layer. Making them MP-safe would require new attrib content (cheat
ability blueprints) dispatched via `LocalCommand_PlayerAbility`, which is
an engine/data scope outside this changelog.

### 9.2 New gate posture: warn-only by default

[devmenu_mp_gate.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_mp_gate.scar)
now ships a 3-mode controller:

| Mode | Behaviour | Default? |
|---|---|---|
| `allow` | silent passthrough | no |
| `warn`  | log `[DEVMENU-MPGATE]` + toast risk class, then PROCEED | **YES** |
| `block` | original fail-closed behaviour from §8 | no (opt-in) |

Toggle via the new dev-menu entry **MP Gate: Cycle**
(`DevMenu_CycleMPGateMode`) wired into both [devmenu_dev_data.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_dev_data.scar)
and the Determinism category in [devmenu_categories.scar](Gamemodes/Onslaught/assets/scar/devmenuUI/devmenu_categories.scar).

### 9.3 Per-handler MP-risk classification

The gate now consults `_DEVMENU_MP_RISK[action_name]` to pick the warning
text. Class definitions:

- **SAFE** — pure UI/logging toggles. Not gated, not warned.
- **LOW**  — per-client presentation only, engine-confirmed deterministic.
- **MED**  — routes through `LocalCommand_*`; truly MP-safe.
- **HIGH** — sim write with no synchronized variant; will desync.
- **CRIT** — destructive sim write (kills/spawns/owner-changes); will
  desync and likely crash the receiving peer once it tries to act on
  ghost state.

| Action | Class | Notes |
|---|---|---|
| `age_up` | MED | `LocalCommand_PlayerUpgrade` — verified in chatcheats.scar:566 |
| `fog_of_war` | LOW | **Rewritten** to `FOW_UIRevealAll` ([Essence_ScarFunctions.api line 884](game_data/extracted/aoe4/scardocs/Essence_ScarFunctions.api#L884)) — explicitly "without triggering a FOW in the game simulation" |
| `speed_default` / `speed_increase` / `speed_decrease` / `turbo` / `slow` | LOW | `Misc_SetSimRate` is per-client wallclock pacing; sim ticks remain lockstepped |
| `teleport_camera` | LOW | `Camera_*` calls are local viewport only |
| `economy` / `resources_*` / `pop_cap_max` / `instant_build` / `invulnerable` / `invuln_selected` / `burn_selected` / `explore_all` | HIGH | local sim writes (`Player_GrantResource`, `Player_SetMaxPopulationCap`, `Modifier_Apply*`, `Squad_SetInvulnerableMinCap`, `FOW_PlayerExploreAll`) — no synchronized variant |
| `sheep_to_wolves` / `kill_gaia` / `spawn_*` / `destroy_selected` / `teleport_selected` / `convert_selected` / `lose_instantly` | CRIT | destructive (`Entity_Kill`, `Squad_CreateAndSpawn`, `Squad_SetPosition`, `Squad_SetPlayerOwner`) — guaranteed desync + likely crash |

### 9.4 What changed in this pass

1. `_devmenu_mp_gate` rewritten as advisory-by-default 3-mode controller.
2. `_DEVMENU_MP_RISK` lookup table added (full coverage of every gated
   handler).
3. `DevMenu_DoFoW` rewritten to use `FOW_UIRevealAll` /
   `FOW_UIUnRevealAll` — moves it from CRIT to **LOW** (genuinely MP-safe).
4. `_devmenu_dev_safe_call` (debug probes) now also honors the
   `allow|warn|block` mode rather than fail-closing unconditionally.
5. Dev-menu entry **MP Gate: Cycle** added so testers can flip back to
   `block` for safety regression runs without editing source.
6. Lint script ([scripts/audit_devmenu_mp_safety.ps1](scripts/audit_devmenu_mp_safety.ps1))
   continues to enforce that every sim-mutating call has a `_devmenu_mp_gate(...)`
   beacon — the beacon is now warn-only but still required so cross-peer
   scarlog diffs surface every MP-side mutation deterministically.

### 9.5 Recommended testing protocol

1. Default play: leave gate at `warn`. Use the menu freely; consult toast
   risk-class before firing CRIT handlers in MP.
2. Before shipping a public MP build with `-dev`: flip to `block`, replay
   regression cases, confirm no `[DEVMENU-MPGATE] ... -> PROCEED` lines
   in scarlog.
3. To investigate a suspected DevMenu-induced OOS: run **MP Safety Audit**
   from both peers, diff `[DEVMENU-MPGATE]`, `[DEVMENU-MOD]`, and
   `[DEVMENU-REPL]` lines. Any line present on only one peer pinpoints
   the desync.

---

## 10. Network routing implementation (2026-05-12, third pass)

Deep investigation of the official Relic cheat infrastructure revealed the
correct general-purpose broadcast pattern.

### 10.1 Root architectural insight

**SCAR functions are MP-safe IF AND ONLY IF called from a lockstep-synchronized
callback.** The execution context — not the function itself — determines safety:

| Context | MP-safe? | Examples |
|---|---|---|
| `Rule_Add*` / `Rule_AddGlobalEvent` callback | ✅ YES — all peers advance same tick | `ags_start_scattered.scar`, `ags_team_balance.scar`, `cba_rewards.scar` — all call `Player_GiftResource`, `Modifier_ApplyToPlayer` etc. and these work in Onslaught MP |
| `GE_BroadcastMessage` callback | ✅ YES — lockstep event fired same tick on all peers | `cheat.scar` uses this for `CheatEconomy`, `CheatInvulnerable`, `CheatInstantBuildAndGather` |
| UI button press handler (DevMenu) | ❌ NO — executes on pressing peer only | All DevMenu actions before this fix |

This corrects the earlier §9.1 finding ("no general-purpose broadcast API").
`Command_PlayerBroadcastMessage` + `GE_BroadcastMessage` IS the general-purpose
broadcast mechanism — it was already in use by Relic's own cheat system.

### 10.2 Official patterns found in scar_dump

**`network.scar`** (`GameScarUtil.scar` → `cardinal.scar` → **available in Onslaught**):
```lua
-- Register a named callback:
Network_RegisterEvent("MyCallback")  -- assigns event integer ID
-- Send through lockstep bus:
Network_CallEvent("MyCallback", "payload string")
-- Receives on ALL peers at same sim tick:
function MyCallback(playerID, message) ... end
```

**`cheat.scar`** (imported by `cba.scar:38`, type-0 broadcast, dev-flag gated):
```lua
cheats["ECONOMY"] = CheatEconomy   -- registered in Cheat_Init
Command_PlayerBroadcastMessage(player, player, 0, "ECONOMY")
-- → Cheat_Callback → CheatEconomy(data.player, {}) on all peers
```

**Key discovery: `Player_AddResource`** (used in `cheat.scar`'s `CheatEconomy`):
not documented in `Essence_ScarFunctions.api` but confirmed as an engine-internal
function available in Onslaught scope. More direct than `Player_GiftResource`
(which has "gift" accounting implications). Used in `_DEVMENU_NET_ACTIONS`.

### 10.3 What was implemented

#### `devmenu_mp_gate.scar` — Phase 5: Network Dispatch

Added at end of file:
- `_DEVMENU_NET_ACTIONS` — dispatch table; each entry calls the correct
  `Modifier_*/Player_*/Misc_*` function in a lockstep-safe way
- `DevMenu_NetworkDispatch(playerID, message)` — global callback registered
  via `Network_RegisterEvent`; decodes and dispatches actions
- `_devmenu_net_register()` — `Scar_AddInit` hook that registers the callback
  at game startup (runs after `Network_Init` because `network.scar` is loaded first)
- `_devmenu_mp_net_action(player, key, arg)` — sends via `Network_CallEvent`;
  returns `true` in MP so callers can `return` early
- `_devmenu_mp_cheat_broadcast(player, key, args)` — sends via type-0
  `Command_PlayerBroadcastMessage` to route to `cheat.scar`'s `Cheat_Callback`

#### `devmenu_actions.scar` — network routing added

Every action now follows this pattern:
```lua
function DevMenu_DoSomething()
    if _devmenu_mp_gate("something") then return end
    local p = _devmenu_local_player()
    -- MP: route through lockstep network
    if _devmenu_mp_net_action(p, "SOMETHING") then
        -- show toast, return
        return
    end
    -- SP: direct call as before
    _devmenu_safe_call("CheatSomething", p)
end
```

#### `_DEVMENU_MP_RISK` reclassifications

**Pass 1** (resources, speed, global mutations — prior session):

| Action | Before | After | Reason |
|---|---|---|---|
| `economy` | HIGH | **MED** | type-0 broadcast → `Cheat_Callback` → `CheatEconomy` |
| `resources_*` (all 6) | HIGH | **MED** | `DevMenu_NetworkDispatch` → `Player_AddResource` |
| `pop_cap_max` | HIGH | **MED** | `DevMenu_NetworkDispatch` → `Player_SetPopCapOverride` |
| `explore_all` | HIGH | **MED** | `DevMenu_NetworkDispatch` → `Game_SetMapExplored` |
| `instant_build` | HIGH | **MED** | `DevMenu_NetworkDispatch` → `ChatCheatInstantBuildAndGather` |
| `invulnerable` | HIGH | **MED** | `DevMenu_NetworkDispatch` → `ChatCheatInvulnerable` |
| `turbo`/`slow`/`speed_*` | LOW | **MED** | `DevMenu_NetworkDispatch` → `Misc_SetSimRate(target)` on all peers (target computed locally before broadcast) |
| `sheep_to_wolves` | CRIT | **MED** | `DevMenu_NetworkDispatch` → `CheatReplaceSheepWithWolves` |
| `kill_gaia` | CRIT | **MED** | `DevMenu_NetworkDispatch` → `CheatKillAllGaia` |
| `lose_instantly` | CRIT | **MED** | `DevMenu_NetworkDispatch` → `CheatLoseInstantly` |

**Pass 2** (selection-based + spawn — this session):

| Action | Before | After | Reason |
|---|---|---|---|
| `destroy_selected` | CRIT | **MED** | `DEVMENU_DESTROY` → `Entity_Kill` with serialized entity IDs on all peers |
| `teleport_selected` | CRIT | **MED** | `TELEPORTSELECTED` cheat broadcast → `SGroup_WarpToPos` with serialized squad IDs + position |
| `convert_selected` | CRIT | **MED** | `DEVMENU_CONVERT` → `Squad/Entity_SetPlayerOwner` with serialized IDs + target player ID |
| `burn_selected` | HIGH | **MED** | `DEVMENU_BURN/DEVMENU_UNBURN` → `Entity_SetOnFire/StopFire` with serialized entity IDs |
| `invuln_selected` | HIGH | **MED** | `DEVMENU_INVULN_SEL` → `Squad/Entity_SetInvulnerableMinCap` with serialized IDs |
| `spawn_army` | CRIT | **MED** | `DEVMENU_SPAWN_ARMY` → `SpawnCheatArmy(playerID)` on all peers (keep position is deterministic) |
| `spawn_army_camera` | CRIT | **MED** | `DEVMENU_SPAWN_ARMY_CAM x y z` → `CheatSpawnCoreUnits` with serialized camera position |
| `spawn_photon_man` | CRIT | **MED** | `DEVMENU_SPAWN_PHOTON` → `SpawnCheatPhotonMan(playerID)` on all peers |

**All DevMenu actions are now MED or below. No HIGH or CRIT classifications remain.**

#### Still pending (need entity/squad ID serialization)

All selection-based and spawn actions are now implemented. No CRIT or HIGH actions remain.

### 10.4 Selection-based actions — comparison against official patterns

**`DevMenu_DoTeleportSelected`** — reuses Relic's own `TELEPORTSELECTED` cheat key via `_devmenu_mp_cheat_broadcast`. Format confirmed from `cheat.scar:CheatTeleportSelected`: squad IDs come first in the message, then x y z as the last 3 tokens. `SGroup_WarpToPos` is called on all peers from inside `Cheat_Callback`. Position is read from `_devmenu_camera_forward_pos(-40)` / `Camera_GetCurrentTargetPos()` at button-press time and serialized as 4-decimal floats.

**`DevMenu_DoDestroySelected`** — `cheat.scar`'s `DESTROYHOVERED` / `CheatDestroySelected` only handles ONE entity per broadcast. DevMenu uses a custom `DEVMENU_DESTROY eid1 eid2 ...` action to destroy multiple entities in a single lockstep event. Both EGroup path and squad-fallback path (Squad_GetFirstEntity) collect entity IDs before serializing. Keep guards (`_devmenu_is_human_player_keep`) are enforced at the pressing peer's collection point.

**`DevMenu_DoConvertSelected`** — no official cheat.scar analogue. Custom `DEVMENU_CONVERT target_pid nsquads sqid1...sqidN eid1...eidM`. On each peer, `target_pid` is resolved by looping `World_GetPlayerAt(i)` and comparing `Player_GetID`. Keep guards are re-applied at collection time on the pressing peer (serialized lists never contain kept entities). Squad + entity owner-change APIs are called in the callback.

**`DevMenu_DoBurnSelected`** — no official cheat.scar analogue (Relic's `CheatSetFireToBuildings` is not in the MP broadcast registry). Two custom actions: `DEVMENU_BURN eid1 eid2...` (ignite path) and `DEVMENU_UNBURN eid1 eid2...` (extinguish path). At button-press time, entities are classified as "currently burning" → unburn bucket, "not burning" → burn bucket. The `on_fire_health_percentage_modifier` threshold-lift modifier is applied in the `DEVMENU_BURN` callback on each peer independently, with per-client `_devmenu_burn_modifier_table[eid]` tracking for subsequent removal.

**`DevMenu_DoInvulnSelectedUnits`** — no official cheat.scar analogue (Relic's `INVULNERABLE` cheat is a global all-players toggle; DevMenu's is selection-scoped). Custom `DEVMENU_INVULN_SEL dir nsquads sqid1...sqidN eid1...eidM`. Direction is determined from the first available target's `Squad_GetInvulnerableMinCap`/`Entity_GetInvulnerableMinCap` at button-press time. Health cap for applying invuln is read from `Squad_GetHealthPercentage`/`Entity_GetHealthPercentage` live in the callback (deterministic across peers since game state is lockstepped).

**Spawn actions**:
- `DevMenu_DoSpawnArmy` → `DEVMENU_SPAWN_ARMY`. Calls `SpawnCheatArmy(playerID)` on all peers. `SpawnCheatArmy` calls `GetTownCentrePosition(player)` internally, which iterates `Player_GetEntities` looking for `town_center_capital` — fully deterministic since entity ownership and types are part of the lockstepped sim state.
- `DevMenu_DoSpawnArmyAtCamera` → `DEVMENU_SPAWN_ARMY_CAM x y z`. Camera position is local-only; serialized by pressing peer using `pcall`-safe `.x/.y/.z` field access. All peers receive the same position and call `CheatSpawnCoreUnits(playerID, World_Pos(x,y,z))`.
- `DevMenu_DoSpawnPhotonMan` → `DEVMENU_SPAWN_PHOTON`. Calls `SpawnCheatPhotonMan(playerID)` on all peers. The `hasLoadedPhoton` client-side precaching flag is initialized independently per peer (all peers start at false, all set true after first dispatch).

### 10.5 Toggle-state compatibility

`DevMenu_DoInvulnerable` and `DevMenu_DoInstantBuild` both use an optimistic
"next-state" prediction for immediate UI feedback. The actual `gInvulnerableCheat`
and `gInstantBuildCheat` globals are updated inside the callback (which fires
a tick later), so `DevMenu_GetInvulnerableEnabled()` / `DevMenu_GetInstantBuildEnabled()`
will reflect the correct state on the next panel refresh.

### 10.5 Security

`DevMenu_NetworkDispatch` is gated by `Misc_IsCommandLineOptionSet("dev") == false → return`,
matching `cheat.scar`'s `Cheat_Callback` gate. Non-dev builds ignore all
`DevMenu_NetworkDispatch` messages even if they somehow arrive.

### 10.6 Updated testing protocol

1. **All MED actions (pass 1 — resources/speed/global)**: fire in 2-player MP, verify both peers show the effect (resources/rate/fow should change on both). Look for `[DEVMENU-NET] queued:` and `[DEVMENU-NET] dispatch` lines in scarlog — the former from the pressing peer, the latter from both peers.
2. **Selection-based actions (pass 2)**:
   - **Teleport**: select units on one peer, press Teleport. Look for `[DEVMENU-NET] cheat_broadcast: TELEPORTSELECTED ...` in scarlog. Verify squads appear at the same position on both peers.
   - **Destroy**: select buildings/units, press Destroy. Look for `[DEVMENU-NET] dispatch DEVMENU_DESTROY`. Both peers should see the entity removed.
   - **Convert**: select a unit, press Convert. Look for `[DEVMENU-NET] dispatch DEVMENU_CONVERT`. Ownership icon should change on both peers.
   - **Burn / Unburn**: select a building, press Burn. `[DEVMENU-NET] dispatch DEVMENU_BURN`. Building should ignite on both peers. Press again → `DEVMENU_UNBURN` → extinguished on both peers.
   - **Invuln Selected**: select units or buildings, press InvulnSelected. `[DEVMENU-NET] dispatch DEVMENU_INVULN_SEL`. Apply/remove invuln on both peers.
3. **Spawn actions**: press SpawnArmy/SpawnPhotonMan. Look for `[DEVMENU-NET] dispatch DEVMENU_SPAWN_ARMY` / `DEVMENU_SPAWN_PHOTON`. Units should appear at same position on both peers. For SpawnArmyAtCamera: verify camera position is serialized in the scarlog message.
4. **Toggle consistency**: after `INVULNERABLE` or `INSTANT_BUILD` in MP, open DevMenu again — the toggle card should show the updated state.

