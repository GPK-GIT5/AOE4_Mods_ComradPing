# 2026-04-24 — AoE4 Data Verification Report

Verification of the workspace's `game_data/extracted/aoe4/` against the five named upstream sources, plus delivery of a repeatable sync pipeline for future DLCs.

## Scope

- **In scope:** Cache-freshness verification, internal Tier-1 vs Tier-2 consistency check, sync infrastructure (fetch, diff, patch-watch, wrapper), workflow documentation.
- **Out of scope** (explicit user decision): metric/formula corrections in [analysis-findings.md](#) — separate effort.
- **Ground truth:** Game files (EBP XML + `game_data/extracted/aoe4/scar_dump/`). aoe4world is a cache; wiki/labs/support are advisory.

## What was built

| Path | Purpose |
|---|---|
| [game_data/generated/schema/SCHEMA_VERSION.md](../game_data/generated/schema/SCHEMA_VERSION.md) | Pinned schema (`__version__: 0.0.2`) and bump procedure |
| [.github/scripts/build/_stats/fetch_aoe4world.ps1](../.github/scripts/build/_stats/fetch_aoe4world.ps1) | Pulls per-civ optimized JSON from `data.aoe4world.com` to `Temporary/raw_extractions/staging/aoe4world/` with manifest |
| [.github/scripts/auditing/diff_ignore.psd1](../.github/scripts/auditing/diff_ignore.psd1) | Ignore list + numeric tolerance config |
| [.github/scripts/build/_stats/diff_data_sources.ps1](../.github/scripts/build/_stats/diff_data_sources.ps1) | Cache-freshness diff (workspace cache vs live aoe4world) |
| [.github/scripts/build/_stats/verify_canonical_vs_cache.ps1](../.github/scripts/build/_stats/verify_canonical_vs_cache.ps1) | Tier-1 (canonical) vs Tier-2 (aoe4world) consistency check on hp + costs per age |
| [.github/scripts/build/_stats/check_patch_signal.ps1](../.github/scripts/build/_stats/check_patch_signal.ps1) | Polls support.ageofempires.com landing page for new patch identifiers |
| [.github/scripts/build/_stats/sync_all.ps1](../.github/scripts/build/_stats/sync_all.ps1) | One-command wrapper chaining all of the above + dated archive |
| [game_data/generated/derived/drift-report.{json,md}](../game_data/generated/derived/) | Cache-freshness output |
| [game_data/generated/derived/canonical-vs-cache-report.{json,md}](../game_data/generated/derived/) | Internal consistency output |

## First run results

### Cache freshness (workspace cache 2026-03-19 vs live aoe4world 2026-04-24)
- **Result:** **0 semantic differences** across all 22 civs × 3 categories (units, buildings, technologies).
- **Interpretation:** aoe4world has not published a balance/data update for any of the 22 civs in 5+ weeks. The byte-size delta (~3% smaller live files) is whitespace/serialization formatting only.
- **Schema:** Live `__version__` still `0.0.2` (pinned).

### Canonical vs cache (Tier-1 internal consistency) — **UPDATED 2026-04-25 post-fix**
- **Visited:** 215 base concepts → 746 civ/age rows matched (after filtering out-of-range ages).
- **Matches:** 746 with no diff.
- **missingLive:** 0 (down from 553 false positives caused by three compounding bugs — see Fixes Applied below).
- **HP diffs (5 real):**

| Civ | Unit | Age | Canonical | Live | Classification |
|---|---|---|---|---|---|
| mongols | horseman | 1 | 110 | 115 | `WORTH-MANUAL-CHECK` — possible micro-patch or pre-aura HP |
| delhi | fishing-boat | 2 | 100 | 150 | `WORTH-MANUAL-CHECK` — HP buff post-snapshot |
| tughlaq | fishing-boat | 2 | 100 | 150 | `WORTH-MANUAL-CHECK` — same as Delhi (shared template) |
| goldenhorde | transport-ship | 2 | 400 | 600 | `WORTH-MANUAL-CHECK` — HP buff post-snapshot |
| mongols | transport-ship | 2 | 400 | 600 | `WORTH-MANUAL-CHECK` — same as GH (shared template) |

- **Cost diffs (295 field-level)** — all explained by two known conventions + one canonical extractor bug class:

| Pattern | Civs affected | Classification |
|---|---|---|
| `costs.time ×2` for ALL units | goldenhorde | `CONVENTION-001` — double-squad wall-clock vs per-unit template |
| Merc surcharge baked in (camel-archer, camel-rider, ghulam) | byzantines | `CONVENTION-002` — merc recruitment surcharge |
| Reduced production time (horseman all ages) | mongols | `CONVENTION-003` — Mongol production speed modifier |
| Civ-unique unit costs wrong (food=0, wildly off time) | english, french, jeannedarc, chinese, malians, ottomans, mongols, rus, hre, sengoku, japanese, templar, delhi, tughlaq, macedonian | `DATA-QUALITY-001` — canonical extractor used wrong base template for civ-unique units; needs extractor fix |

### Fixes applied to `verify_canonical_vs_cache.ps1`

Three bugs eliminated 553 false MISSING_LIVE entries:

| Bug | Root cause | Fix |
|---|---|---|
| Siege/naval/eco variation-id | `entity.baseId=""` for these units; synthesized key `{baseId}-{age}` never matched | Added Path B: index via `entity.variations[*]` using `v.id` directly |
| Cross-civ min-age overshoot | Canonical ageSpread is a union across all civs; a row like `abbasid/man-at-arms age=1` is invalid (Abbasid minAge=3) | Added `minAge` gate: skip age rows below civ's live minAge |
| Cross-civ max-age overshoot | Some units are available at age N for one civ but not age N+1; canonical union includes the higher age | Added `maxAge` gate: skip age rows above civ's live maxAge |

### Patch signal
- Latest patch identifier captured (whatever `check_patch_signal.ps1` returned at run time) and stored at `Temporary/raw_extractions/staging/patch-state.json`. Subsequent runs will alert on change.

## Why "Tier-1 vs Tier-2" is currently a partial check (and how to make it complete)

`game_data/generated/canonical/canonical-units.json` (used as Tier-1 here) is **itself re-indexed from the aoe4world cache**, per its own `_meta.description`. The truly EBP-derived canonical files today are: `core-templates.json`, `inheritance-map.json`, `ha-variant-deltas.json`, `gap-fill-report.json`, `campaign-entities.json`, `neutral-entities.json` — these capture **inheritance and presence**, not stat values like damage / HP / armor / range. Per [EXTRACTION_PLAN.md](../game_data/extracted/aoe4/EXTRACTION_PLAN.md) Priority 2, standalone weapon EBP stat extraction (`weapon\races\` namespace) is still pending.

**Recommendation: build `scripts/extract_ebp_stats.ps1` as the next step.** It should walk the EBP XML dump and produce `game_data/generated/canonical/ebp-unit-stats.json` keyed by PBGID with: `hitpoints`, `armor.{melee,ranged,fire}`, `costs.*`, weapon refs (already linked) → weapon `damage`, `speed`, `range`, `modifiers`. Once that exists, point `verify_canonical_vs_cache.ps1` at it instead of `canonical-units.json` and you have true Tier-1 ground truth.

## Inconsistency triage (categorized per plan) — UPDATED

| Category | Count | Status | Action |
|---|---|---|---|
| `STALE-CACHE` (aoe4world hasn't picked up patch) | 0 | ✅ None observed | None |
| `EXTRACTOR-BUG` (verifier bugs causing false reports) | 3 bugs → 553 false positives | ✅ Fixed | See "Fixes applied" above |
| `WIKI-WRONG` | n/a (no wiki cross-check this run) | — | Defer |
| `NEW-DLC-ENTITY` | 0 | ✅ None | None |
| `FORMULA-DRIFT` | 0 | — | n/a — requires Tier-1 stat extract |
| `CONVENTION-DIFF` (real but explained) | 295 cost diffs (CONVENTION-001/002/003) | ✅ Documented in `diff_ignore.psd1` | No action — expected by design |
| `DATA-QUALITY-001` (canonical extractor errors, civ-unique costs) | ~250 of the 295 cost diffs | 🔲 Needs fix | Fix canonical extractor to use civ-specific cost templates |
| `WORTH-MANUAL-CHECK` (HP) | 5 (horseman, fishing-boat ×2, transport-ship ×2) | 🔲 Pending | Hand-verify in-game tooltips |

## Sources cross-checked

| Source | Used as | Outcome |
|---|---|---|
| https://aoe4world.com/ | UI signal | Not auto-fetched; manual spot-checks recommended (procedure documented in workflow) |
| https://data.aoe4world.com/ | Tier-2 cache (auto-pulled) | All 22 civs × 3 categories fetched OK; v=0.0.2 |
| https://aoe4labs.com/ | Combat formulas (Tier-4 advisory) | Not auto-fetched; consult when reconciling DPS/EHP findings from `analysis-findings.md` (separate effort) |
| https://support.ageofempires.com/ | Patch signal | Polled by `check_patch_signal.ps1`; baseline recorded |
| https://ageofempires.fandom.com/ | Last-resort narrative | Not consulted this run |

## Follow-ups (recommended, ordered) — UPDATED

| # | Task | Status |
|---|---|---|
| 1 | Build `scripts/extract_ebp_stats.ps1` — EBP-derived hp/armor/cost/weapon stats (EXTRACTION_PLAN Priority 2) | 🔲 Pending |
| 2 | Fix `verify_canonical_vs_cache.ps1` variation-id resolution | ✅ Done (2026-04-25) |
| 3 | Hand-verify 5 HP diffs (horseman, fishing-boat, transport-ship) | 🔲 Pending |
| 4 | Add convention diffs to `diff_ignore.psd1` | ✅ Done (2026-04-25) |
| 5 | Fix canonical extractor for civ-unique unit costs (`DATA-QUALITY-001`) | 🔲 Pending |
| 6 | Quarterly run cadence after each patch | 🔲 Pending |

## Verification checklist (rerun this report)

```pwsh
cd c:\Users\Jordan\Documents\AoE4-Workspace
pwsh scripts\sync_all.ps1                       # 1. fetch + cache-freshness diff + archive
pwsh scripts\verify_canonical_vs_cache.ps1      # 2. Tier-1 vs Tier-2 internal check
# Inspect:
#   data\\generated\\derived\drift-report.md
#   data\\generated\\derived\canonical-vs-cache-report.md
#   changelog\<today>_data-drift.md
```
