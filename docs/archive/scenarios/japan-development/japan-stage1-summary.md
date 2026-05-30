# Japan Scenario DLC Civ Support - Stage 1 Summary

Date: 2026-02-25
Scope: Stage 1 (Core resolver + generated composition maps + validation + safe AGS wrappers)

## What Changed
- Added DLC civ parent resolver with overrides and composition inheritance.
- Implemented composition map generation for DLC civs to avoid manual duplication.
- Added validation checks for parent cycles, parent existence, override structure, and composition sync.
- Rewrote AGS blueprint lookup helpers with override-first precedence and explicit failure paths.
- Updated spawn helpers to use resolver-safe map lookups.
- Refactored restrictions and siege unlock logic to use resolved civ families.
- Fixed ribauldequin restriction and unlock logic bug (always-true condition).

## DLC Civ Coverage
- mongol_ha_gol -> mongol
- byzantine_ha_mac -> byzantine
- japanese_ha_sen -> japanese
- sultanate_ha_tug -> sultanate
- lancaster -> english
- templar -> hre

## Key Files Touched
- mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_data.scar
- mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/coop_4_japanese.scar
- mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_spawns.scar
- mods/Japan/assets/scenarios/multiplayer/coop_4_japanese/scar/coop_4_japanese_objectives.scar

## Notes
- All DLC civs now resolve to a valid parent and inherit composition maps.
- Resolver checks DLC overrides before parent fallback to prevent wrong unit picks.
- Family-based restriction checks now use resolved civ keys to cover DLC variants.
- Variant-specific blueprints still use raw civ keys where required (abbasid_ha_01, french_ha_01, etc).

## Validation
- No syntax errors reported in the four modified .scar files.

# Next Phase Plan (Stage 2)

Goal: Consolidate and harden registry usage across the scenario, reduce duplicated civ checks, and improve long-term maintainability for multi-contributor updates.

1. Registry consolidation
   - Introduce helper functions for common civ-family checks (e.g., IsCivFamily(resolved_civ, "mongol")).
   - Replace remaining ad-hoc family checks with helpers to reduce drift.

2. Centralize civ metadata
   - Move civ-specific restrictions that are family-based into a single registry table.
   - Make restrictions data-driven where possible (e.g., siege unlocks, upgrade locks).

3. Add test harness (lightweight)
   - Add a small validation runner that can be called in setup to log resolver outputs per player.
   - Add a debug switch for verbose DLC resolver logging.

4. Expand DLC override support
   - If any DLC civ requires true overrides (not just parent fallback), add them in DLC_CIV_OVERRIDES and document in the registry.

5. Documentation
   - Add a short readme entry explaining the resolver flow and how to add new DLC civs safely.

6. Regression sweep
   - Verify restriction/unlock parity between Mission_SetRestrictions and Phase2_CaptureSiege_OnComplete.
   - Audit for any remaining hardcoded civ chains that should use resolved civ.

