# 2026-04-26 — Infinite-Resource Civ Danger Audit (Phases 1–8)

## Summary
Executed the full Civ Danger Audit plan (Phases 1–8). Built [scripts/analyze_civ_danger.ps1](scripts/analyze_civ_danger.ps1) which joins canonical evaluated states with derived DPS to produce per-civ danger rankings and train-time adjustment proposals. All 10 regression gates pass; baseline hash unchanged.

## Outputs
- [game_data/generated/derived/civ-danger-report.json](game_data/generated/derived/civ-danger-report.json) — full per-unit ranked dataset with per-civ percentile bands and proposal queue.
- [game_data/generated/derived/civ-danger-report.md](game_data/generated/derived/civ-danger-report.md) — human-readable report (global top 30, per-civ summary, 34 train-time proposals, missing-DPS coverage gaps).
- [game_data/generated/canonical/unit-truth-evaluated-exhaustive.json](game_data/generated/canonical/unit-truth-evaluated-exhaustive.json) — refreshed (643 states, 24 civs, 13 fields, hash `0efada0b912ecf34…`).

## Headline Numbers
- **Civs ranked:** 20 competitive (4 campaign-only excluded: `crusader_cmp`, `templar`, `ayyubid_cmp`, `lancaster`).
- **Land non-siege combat units ranked:** 175.
- **Train-time adjustment proposals:** 34 (capped at +20% per pass, min ±1s).
- **Missing-DPS coverage gaps:** 43 entities (mostly HA/DLC variants and renamed Mongol units, dominated by `crusader_cmp` 16 and `mongol_ha_gol` 7).

## Top Danger Outliers (production_pressure = HP × DPS / train_time)
1. mongol — `unit_knight_4_mon` (3861) — DPS=328 likely includes multi-hardpoint sum; flagged but capped at +20%.
2. mongol — `unit_knight_3_mon` (2804).
3. mongol_ha_gol — `unit_bodyguard_4_mon_ha_gol` (2184).
4. mongol — `unit_knight_2_mon` (1960).
5. hre_ha_01 — `unit_manatarms_4_hre_ha_01` (987).

## Regression Status
- 10/10 gates pass.
- Determinism: 3-run hash match (`0efada0b912ecf34…`).
- Baseline unchanged → no baseline rotation needed.

## Caveats
- `damage.melee/ranged`, `armor.melee/ranged`, `healingRate` are `UNDECLARED_FIELD` in the canonical evaluator (EBPS dump doesn't carry them). DPS sourced from [game_data/generated/derived/dps-by-unit.json](game_data/generated/derived/dps-by-unit.json) (2026-03-26 snapshot).
- Armor omitted from survivability proxy.
- `pop=1` assumed (no authoritative pop_size in canonical schema).
- Most-buffed branch (highest HP across tech_state) selected per (entity, civ, age) as the "tech-complete" infinite-resource snapshot.
- Proposals touched by hand-authored `civ_defs` / `tech_defs` are tagged `confidence: design_assumption_influenced`.

## Next Steps (deferred)
- Refresh `dps-by-unit.json` from current weapon/races XML once Phase 6 state_tree re-export lands (will eliminate Mongol HA missing-DPS rows).
- Re-investigate Mongol knight DPS=328 (suspected weapon-row sum including charge bonus) before applying any train-time bump from this pass.
- Two-pass publication option: high-confidence `authoritative_ebps` proposals first, `design_assumption_influenced` second.
