# AoE4 Extraction & Regression Pipeline — Full System Audit
**Date:** 2026-04-26  
**Scope:** Schema integrity • classification correctness • hidden dependencies • inheritance chains • binary-only resources • deterministic regression stability • baseline hash consistency  
**Verdict:** **PASS — pipeline is internally consistent, no false blockers found, prior Phase 5 closure is correct.**

---

## 1. Schema Integrity — PASS

**File:** [game_data/generated/canonical/modifier-types-schema.json](game_data/generated/canonical/modifier-types-schema.json)

- 13 OVERRIDE fields, all with explicit source paths in EBPS (`health_ext.hitpoints`, `cost_ext.time_cost.cost.{food,wood,gold,stone}`, `cost_ext.time_cost.time_seconds`, `moving_ext.default_speed`, `cost_ext.unit_types`, `armor_ext.armor.{melee_attack_armor,ranged_attack_armor}`, `combat_ext.hardpoints[*].weapons[*].damage.{melee,ranged}`, `health_ext.hp_regen_rate`).
- All 13 fields are referenced by at least one entry in `tech_defs.json` or `civ_defs.json`.
- No orphaned/unused schema fields.
- Schema explicitly excludes `tier_ext` (entity-switch upgrades) — correctly handled at Phase 0 EBPS extraction layer instead.

## 2. Classification Correctness — PASS (with corrected numbers)

**Verified counts** (run [scripts/audits/_audit_classify2.ps1](scripts/audits/_audit_classify2.ps1)):

| Container | Entries | Modifiers (design / aoe4world / gamefile) | state_tree_refs |
|---|---|---|---|
| `tech_defs.json` | **115** | **95 / 13 / 10** | 82 entries have refs |
| `civ_defs.json` | **24** | **11 / 0 / 0** | n/a |

**Design-assumption breakdown (tech):** 63 entries with state_tree_refs + 32 entries without.

**Discrepancy with prior session note (76/19):** the older "76 indirect_state_tree + 19 no_safe_mapping" figures referenced an earlier snapshot; current canonical files give 63/32 at the entry level. Updated numbers are now authoritative. No data loss — the underlying decision (cannot safely map to schema fields without state_tree) is unchanged.

## 3. Hidden Dependency Audit — PASS (one finding, NOT a blocker reversal)

### 3.1 `statemodel_schema` — confirmed schema-only
- 459 `.rgd` files in `Gameplay_data_duplicate/assets/attrib/instances/statemodel_schema/`.
- These are binary schema definitions, **not** state_tree node value tables.
- No `.xml` decoded form exists in either source directory.
- Documented in [game_data/extracted/aoe4/EXTRACTION_PLAN.md](game_data/extracted/aoe4/EXTRACTION_PLAN.md) and stored in repo memory.

### 3.2 `state_tree` — confirmed absent (binary-only & not yet decoded)
- **NOT present** in `C:\Users\Jordan\Documents\Gameplay_data_duplicate\assets\attrib\instances\` (XML source).
- **NOT present** in `C:\Users\Jordan\Documents\AOE4_Attributes\attrib\` (RGD parallel source — only `statetree_event/` exists, which is a different attribute set).
- Genuine blocker for resolving design_assumption → authoritative type/scope mapping.

### 3.3 `upgradebag_float_property` discovery — values present, mapping still requires state_tree
**New finding this audit.** Upgrade XMLs contain blocks like:
```xml
<list name="float_properties">
    <template_reference name="float" value="upgradebag_float_property">
        <float name="value" value="0.15" />
        <enum name="id" value="survival_techniques_food" />
    </template_reference>
</list>
```
Cross-reference scan ([scripts/audits/_audit_upgradebag_floats.ps1](scripts/audits/_audit_upgradebag_floats.ps1)) of all 1,513 upgrade XMLs:
- 300 files contain `upgradebag_float_property` blocks.
- 555 total `(id → value)` pairs.
- 78 unique IDs.

**Cross-reference result:** the IDs (e.g., `survival_techniques_food`, `armor_fire`, `ranged_damage`, `enclosures_gold_rate_eng`, `heal_rate`) are **state_tree node identifiers**, NOT schema field names and NOT `tech_defs.modifiers[*].field` values. Without state_tree definitions, each ID cannot be resolved into the required `(field, type, scope)` triple (e.g., `armor_fire` could be `armor.melee` ADDITIVE or `armor.ranged` MULTIPLICATIVE; `heal_rate` could be `healingRate` OVERRIDE or ADDITIVE).

**Conclusion:** Phase 5's "values absent" framing was slightly imprecise — the **values exist** in upgrade XML, but their **semantic mapping is absent**. The blocker stands. State_tree is the genuine prerequisite for Phase 6. No false blocker; Phase 5 closure is correct.

### 3.4 Tier-upgrade misclassification (low-priority finding)
Entries like `upgrade_unit_horseman_3_mon` carry `cost.gold OVERRIDE` design_assumption modifiers, but their upgrade XML has empty `<list name="float_properties">` because the upgrade is an **entity-switch** to `unit_horseman_3_mon` whose stats are authoritative in EBPS (`time_seconds=18 overrideParent="True"` confirmed). These entries are arguably mismodeled — the schema explicitly excludes `tier_ext` — but this is a **modeling refinement**, not a regression bug. Recommended for Phase 6.5 cleanup; does not block any current gate.

## 4. Inheritance Chain (`parent_pbg`) Audit — PASS

- 100% upgrade-XML coverage for tech_defs entries (verified earlier this session: 0 missing of 115).
- Sampled parent chains (`upgrade_armor_clad_eng`, `upgrade_econ_villager_hunting_gear_1`, etc.): parent upgrades contain only research-cost floats at top level, no modifier values that escape the same state_tree-mapping requirement.
- 22 of 32 design-no-refs entries have no extractable floats; 13 of those reference parent upgrades that follow the same pattern.
- No orphan modifiers detected — every modifier traces to either a present state_tree_ref, an aoe4world entry, a gamefile reference, or a documented design_assumption.

## 5. Binary-Only Resources — PASS (documented limits)

- **RGD files:** present in `AOE4_Attributes/attrib/` (e.g., 1,513 upgrade.rgd, 3,553 ebps.rgd). No RGD→XML converter exists in this workspace. Treated as opaque; XML decoded forms in `Gameplay_data_duplicate` are the authoritative readable source.
- **EBPS XMLs:** complete coverage — `unit_horseman_3_mon.xml` and other tier targets readable.
- **weapon/races:** 1,364 XML files across 27 civs — confirmed PRESENT (prior session's "missing" claim was reversed).
- **statemodel_schema:** RGD-only, schema definitions, not state_tree value tables.
- No code path treats binary RGDs as authoritative for Phases 1–5; they are a fallback documentation aid only.

## 6. Deterministic Stability — PASS

Full regression suite re-run this audit (`scripts/stats/run_regression_suite.ps1`):

```
Gate results: 10/10 passed
  ✓ schema_compliance      ✓ EXHAUSTIVE×Permissive
  ✓ EXHAUSTIVE×Strict      ✓ STATIC×Permissive
  ✓ OPTIMISTIC×Permissive  ✓ permissive_strict_hash_match
  ✓ nonbranching_count_match  ✓ benchmark
  ✓ determinism            ✓ baseline_hash
OVERALL: PASS
```

- 643 states (629 conditional + 14 unreachable). 26 dedup-removed branches. 0 truncation removals.
- 3-run determinism: identical SHA256 across all runs.
- **Baseline SHA256:** `0efada0b912ecf34…` — matches stored baseline.
- Avg runtime 14.0s (min 12.0s, max 15.0s) — well within budget.

## 7. Inconsistencies / False Blockers — NONE

| Suspected issue | Verdict |
|---|---|
| `upgradebag_float_property` is a hidden authoritative source | **Not a false blocker.** Values exist; mapping still requires state_tree. |
| `statemodel_schema` could substitute for state_tree | **Not a false blocker.** Confirmed RGD schema-only, no value tables. |
| `weapon/races` was missing | **Was a false blocker in old docs.** Already corrected this session. |
| Prior 76/19 vs current 63/32 entry split | **Documentation drift only.** No data loss; canonical files are current. |
| Tier-upgrade `cost.gold` design modifiers | **Modeling smell, not a bug.** Captured for Phase 6.5; does not affect any gate. |

## 8. Confirmed Genuine Blockers for Phase 6

1. **`state_tree` re-export** — required to resolve 95 tech + 11 civ design_assumption modifiers into authoritative `(field, type, scope, value)` tuples. Either:
   - Locate decoded `state_tree/` XML directory, OR
   - Build/locate an RGD→XML converter for `attrib/state_tree/*.rgd`.
2. (Optional) **Tier-upgrade re-classification** — split entity-switch upgrades from field-mutation modifiers in `tech_defs.json` schema.

No other blockers detected. The pipeline is stable, deterministic, and ready for Phase 6 the moment state_tree is available.

---

## Audit Artifacts
- [scripts/audits/_audit_classify2.ps1](scripts/audits/_audit_classify2.ps1) — entry/modifier counts
- [scripts/audits/_audit_upgradebag_floats.ps1](scripts/audits/_audit_upgradebag_floats.ps1) — upgradebag id/value scan + cross-reference
- [scripts/audits/_audit_xml_coverage.ps1](scripts/audits/_audit_xml_coverage.ps1) — 100% upgrade-XML coverage
- [scripts/audits/_audit_floats.ps1](scripts/audits/_audit_floats.ps1) — design-no-refs float scan
- [scripts/audits/_audit_parent_chain.ps1](scripts/audits/_audit_parent_chain.ps1) — parent_pbg traversal sampling
- [game_data/generated/derived/regression-report.json](game_data/generated/derived/regression-report.json) — full regression output
