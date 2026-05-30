# DevMenu UI Sync & Feedback Fixes — 2026-05-14

## Overview

Five distinct UI-sync and user-feedback issues in the Onslaught DevMenu were
diagnosed and fixed. None caused OOS (all sim mutations remained correctly
routed through the lockstep bus from previous sessions). The issues were
exclusively in the presentation layer: toggle-card chrome not reflecting
runtime state, panels disagreeing with each other, a missing cycle indicator
in MP toasts, and a silent no-op when keep-protection filtered the entire
selection.

---

## Issue 1 — FoW Toggle Broken (FOW_UIRevealAll is presentation-only)

**Registry entry:** KI-DEVMENU-001  
**Severity:** HIGH  
**Reported as:** "Toggle FoW no longer works"

### Root Cause

Phase 4 (2026-05-13) replaced `ChatCheatFOW` with `FOW_UIRevealAll` /
`FOW_UIUnRevealAll` as an "MP-safe" rewrite. The Essence API documents
`FOW_UIRevealAll` as operating *"without triggering a FOW in the game
simulation"* — it is a rendering-only call. It does not modify `gFoWCheat`
(the boolean table read by `DevMenu_GetFoWEnabled`), so:

- The map fog never changed.
- `gFoWCheat` remained nil/false → `DevMenu_GetFoWEnabled()` always returned
  `true` (fog on) → the card permanently showed ENABLED on every refresh.

### Fix

`devmenu_actions.scar` — `DevMenu_DoFoW`:
- SP path: reverted to `ChatCheatFOW(player)` which correctly writes
  `gFoWCheat[playerID]`.
- MP path: `_devmenu_mp_net_action(player, "FOW_TOGGLE")` routes via the
  lockstep bus; `_DEVMENU_NET_ACTIONS.FOW_TOGGLE` executes `ChatCheatFOW(pid)`
  on all peers at the same sim tick — identical pattern to `INVULNERABLE` and
  `INSTANT_BUILD`.

`devmenu_mp_gate.scar` — `_DEVMENU_MP_RISK`:
- Removed old dead LOW entries for `fog_of_war`, `speed_*` (they were never
  reachable after mp_locked gating).
- Added `fog_of_war = { level = "MED", reason = "Routed via FOW_TOGGLE → ChatCheatFOW on all peers" }`.

---

## Issue 2 — Toggle Card Chrome Stale After SP Cheat Toggle

**Registry entry:** KI-DEVMENU-002  
**Severity:** MEDIUM  
**Reported as:** "Toggle options sometimes fail to refresh as expected; used toggle instant build but FoW UI triggered to switch state"

### Root Cause

All three SP toggle handlers (`DevMenu_DoFoW`, `DevMenu_DoInvulnerable`,
`DevMenu_DoInstantBuild`) used `Rule_AddOneShot(DevMenu_RefreshToggleStates, 0.1)`.

In SP, `ChatCheatFOW`, `ChatCheatInvulnerable`, and
`ChatCheatInstantBuildAndGather` update their engine globals synchronously in
the same call frame. The 100ms deferred window meant:

1. Panel shows old state for ~100ms.
2. `_devmenu_build_cheat_panel_categorized` directly *mutates* `_DEVMENU_ENTRIES`
   entries' `kind`/`hint`/`state` fields during any rebuild. If a second toggle
   action or a panel-open-triggered rebuild occurred within the 100ms window, the
   pending Rule's delayed read could land on partially-mutated entry state — making
   the wrong card appear to flip.

The "wrong toggle fires" symptom (e.g., clicking Instant Build causes FoW card
to change visually) was specifically this mutation-race effect.

### Fix

`devmenu_actions.scar` — SP paths for all three handlers:
- Changed `Rule_AddOneShot(DevMenu_RefreshToggleStates, 0.1)` →
  `DevMenu_RefreshToggleStates()` (direct synchronous call).
- MP paths retain `Rule_AddOneShot(..., 0.3)` — the net-dispatch round-trip
  requires the deferred read.

**Remaining limitation:** In MP there is an inherent ~300ms window between
pressing a toggle and the card updating (lockstep round-trip). The card shows
pre-toggle state during this window. Cannot be reduced without speculative
pre-toggling.

---

## Issue 3 — Cheat Panel / Quick Panel Toggle State Out of Sync on Open

**Registry entry:** KI-DEVMENU-003  
**Severity:** MEDIUM  
**Reported as:** "Quick panel & cheat menu toggle not synced"

### Root Cause

`DevMenu_ToggleCHEATPanel()` (in `devmenu.scar`) only set
`dc.panel_visible = true/false` on the existing DataContext. The DC was never
rebuilt on open.

If the user fired a toggle from the quick panel and then opened the cheat
modal within the deferred-refresh window, the cheat modal cards reflected the
state baked at the last `_devmenu_build_cheat_panel_categorized` call (OnPlay
or last `DevMenu_RefreshToggleStates`) — not the current runtime state.

### Fix

`devmenu.scar` — `DevMenu_ToggleCHEATPanel()` rewritten:

```lua
if dc.panel_visible then
    -- Close: flip only.
    dc.panel_visible = false
    UI_SetDataContext("DevMenuCHEATPanel", dc)
else
    -- Open: rebuild both panels from live toggle_state_fn calls.
    local _, fresh_dc = _devmenu_build_cheat_panel_categorized(_DEVMENU_ENTRIES or {})
    fresh_dc.panel_visible = true
    _devmenu.cheat_panel_data_context = fresh_dc
    UI_SetDataContext("DevMenuCHEATPanel", fresh_dc)
    -- Sync quick panel.
    local _, qdc, qcount = _devmenu_build_quick_panel(_DEVMENU_ENTRIES or {})
    qdc.panel_visible = _devmenu.quick_panel_enabled == true
    _devmenu.quick_panel_data_context = qdc
    _devmenu.quick_panel_entry_count  = qcount
    UI_SetDataContext("DevMenuCHEATQuickPanel", qdc)
end
```

---

## Issue 4 — Convert [N/M] Cycle Indicator Absent from MP Toast

**Registry entry:** KI-DEVMENU-004  
**Severity:** MEDIUM  
**Reported as:** "Convert also no longer shows 1/8 inside its confirmation message"

### Root Cause

`DevMenu_DoConvertSelected` computed `cycle_idx`, `local_idx`, `display_idx`,
and `cycle_str` inside the SP-only execution path — after the MP routing block
had already `return`-ed. The MP toast was hardcoded:

```lua
msg = string.format("%d item(s) converted ->", #sqids + #eids)
```

No `cycle_str` was appended. This was confirmed by the scarlog from session
`AoE4_05_13_22h-40m-38s`:

```
[DEVMENU-CONV] team-grouped rotation (8 players):
[DEVMENU-NET] queued: DEVMENU_CONVERT 1007 0 1000005673
```

No `[N/8]` in the queued payload or in any subsequent log output.

### Fix

`devmenu_actions.scar` — `DevMenu_DoConvertSelected`:

Moved the entire cycle computation block immediately after `target_player` is
resolved (before `if _devmenu_is_multiplayer()`). Removed the now-redundant
duplicate block in the SP path. Both paths share the same `cycle_str`:

```lua
local cycle_str = (display_idx > 0 and cycle_size > 0)
    and string.format(" [%d/%d]", display_idx, cycle_size) or ""

-- MP routing:
if _devmenu_is_multiplayer() ... then
    ...
    msg = string.format("%d item(s) converted ->%s", #sqids + #eids, cycle_str)
    ...
    return
end

-- SP path also uses cycle_str:
msg = string.format("%d item(s) converted ->%s", total_converted, cycle_str)
```

---

## Issue 5 — Keep/TC Blocker Silent No-Op When Entire Selection Is Protected

**Registry entry:** KI-DEVMENU-005  
**Severity:** MEDIUM  
**Reported as:** "Actions do not follow the allow/blocked list (e.g. convert on keep should be blocked and display message)"

### Root Cause

`_devmenu_is_human_player_keep` correctly filtered protected entities from
Convert, Destroy, and Burn. But all three handlers fell into an early `return`
with no user-visible feedback when the filter removed every item in the
selection. The behavior was indistinguishable from a missed click.

### Fix

`devmenu_actions.scar` — added specific toasts at each empty-filter point:

| Handler | Path | Toast text |
|---|---|---|
| `DevMenu_DoConvertSelected` | MP | `"N starter keep(s) protected — cannot convert"` |
| `DevMenu_DoConvertSelected` | SP | Same |
| `DevMenu_DoDestroySelected` | MP | `"N starter keep(s) protected — cannot destroy"` |
| `DevMenu_DoDestroySelected` | SP | Same |
| `DevMenu_DoBurnSelected` | MP + SP | `"No eligible buildings in selection"` |

Burn uses a generic message because it also skips non-building entities, not
only keeps.

---

## Additional: mp_locked Visual System (New Feature)

Not a bug fix — added in this session to address: "Disable simulation speed
and apply multiplayer locked to items in MISC inside cheat menu".

`devmenu_data.scar`: Added `mp_locked = true` to:
- Speed − / Speed 1x / Speed + (speed category)
- Swap Alarm SFX / Surrender / RUN DIAG NOW (misc category, all also `dev_only`)

`devmenu.scar` — `_devmenu_build_cards`: `mp_locked` detection mirrors
`dev_locked`: routes to `DevMenu_NoOp` dispatch, sets `kind = "mp_locked"`,
`hint = "MP LOCKED"`, `mplocked_vis_N = true`.

`devmenu_xaml.scar`: Added amber `mp_locked` trigger style and
`"🔒 MP LOCKED"` TextBlock (Visibility bound to `mplocked_vis_N`) to both
CHEAT panel and DEV panel XAML style blocks.

---

## Files Changed

| File | Changes |
|---|---|
| `devmenuUI/devmenu_actions.scar` | DoFoW: revert FOW_UIRevealAll → ChatCheatFOW + FOW_TOGGLE net; Invuln/InstantBuild/FoW SP: direct RefreshToggleStates; DoConvertSelected: cycle_str moved before MP routing + MP toast includes cycle_str; Convert/Destroy/Burn: keep-blocker empty-filter toasts |
| `devmenuUI/devmenu.scar` | DevMenu_ToggleCHEATPanel: rebuild-on-open for both panels; DevMenu_RefreshToggleStates: added (rebuilds both panels with live state); _devmenu_build_cards: mp_locked detection; _devmenu_suffix_card_bindings: added mplocked_vis |
| `devmenuUI/devmenu_mp_gate.scar` | _DEVMENU_NET_ACTIONS.FOW_TOGGLE added; _DEVMENU_MP_RISK fog_of_war updated to MED |
| `devmenuUI/devmenu_data.scar` | Speed −/1x/+ and Swap Alarm SFX/Surrender/RUN DIAG NOW: added mp_locked = true |
| `devmenuUI/devmenu_xaml.scar` | mp_locked trigger style + 🔒 MP LOCKED TextBlock in both style blocks |

## Audit

`scripts/audit_devmenu_mp_safety.ps1` — exit 0 after all changes.
