# PlayerUI Elimination Transition Binding Safety

Purpose: document binding choices for elimination transition rollout in Onslaught PlayerUI.

---

## Confirmed baseline — validated in previous session

The following were fully tested and confirmed stable before the current transition work began:

- **Slot-reuse reset hardening**: identity mismatch guard atomically clears all index-scoped state.
- **`_elimPresentationRevealed` sticky latch**: prevents re-hide/re-reveal of already-visible eliminated rows during `_leaver_transfer_state` windows.
- **Dirty-gated DataContext push**: `eliminationTickNeeded` vs `anyChanged` split — tick self-pauses when converged.
- **Dead-path cleanup**: `PlayerUI_Animate_UpdateEliminationAnimations()` removed.
- **Set-if-changed helper**: `_PlayerUI_SetIfChanged(t, k, v)` — all transition field writes are idempotent.

User validation quote: *"Test confirms no visible issues; the only remaining gap is the elimination transition, which currently snaps instantly into the grey state instead of easing in with a visible transition."*

---

## Implemented (awaiting in-game validation)

v3 — fade-based row transition, implemented 2026-03-27:

1. `Opacity="{Binding [rowOpacity]}"` on both name and stats row Grids.
2. `EnableEliminationDim = true` — enables 1.0 → 0.4 animated fade.
3. Scale binding reverted (unsatisfactory visual); `eliminationScaleFactor` still computed, not XAML-bound.
4. All retrigger hardening preserved.

Status: **code-complete, not yet in-game tested**.

---

## Proposed next (not yet implemented)

See session plan for Phase A/B/C detail.

---

## Binding safety summary

Source policy: .github/instructions/coding/xaml-ui.instructions.md

- ACTIVE (used in this rollout):
  - `Opacity="{Binding [rowOpacity]}"` on row container Grids — WARN-HIGH, explicitly accepted.
  - Existing safe triggers: Visibility + BoolToVis, Text, Foreground, Fill.

- REVERTED:
  - `ScaleTransform ScaleX/ScaleY` bound to `eliminationScaleFactor` — removed from XAML.

- FORBIDDEN:
  - `Width="{Binding ...}"` and `Height="{Binding ...}"` are FATAL in XamlPresenter.

## Implementation notes

- Animation ownership:
  - Tick writer owns transient transition fields (`rowOpacity`, `eliminationScaleFactor`, elapsed/active).
  - Completion handoff commits steady visual state.
  - Update loop writes steady fallback only when no active elimination animation.

- Push policy:
  - Tick remains dirty-gated and pauses when converged.
  - Active elimination rows drive `anyChanged` from transition field deltas, enabling visible opacity fade.

## Rollback sequence

If regression appears:

1. Remove `Opacity="{Binding [rowOpacity]}"` from both Grid elements in playerui_hud.scar.
2. Set `EnableEliminationDim = false` in playerui_settings.scar.
3. Keep SCAR animation math untouched.
4. Re-test retrigger matrix (transfer windows, slot reuse, simultaneous events).

## Validation checklist

1. Elimination with unchanged rank shows visible opacity fade (1.0 → 0.4).
2. Surrender/disconnect use same fade path.
3. Existing eliminated rows do not retrigger during unrelated transfers.
4. Slot reuse still animates first elimination correctly.
5. HUD hide/show during active fade does not crash or leave stale opacity.
5. No crash or persistent tick activity after convergence.
