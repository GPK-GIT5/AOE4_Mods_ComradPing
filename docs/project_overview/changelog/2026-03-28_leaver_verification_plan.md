# Leaver Military Pipeline — Full Runtime Verification Plan
**Date:** 2026-03-28  
**Objective:** Confirm that military units always convert or explicitly destroy, with zero hidden transfer behavior and consistent statistics across all scenarios.

---

## Executive Summary

The military conversion pipeline has been refactored to enforce a strict rule:
> **Every military squad either converts through a deterministic resolution path OR is explicitly destroyed.**
> **No Squad_SetPlayerOwner re-owns are permitted in the military branch.**

This plan validates:
1. All hero units follow locked policies (khan/jeanne/abbey_king → archetype; wynguard → destroy)
2. Elephant mappings correct (both → knight, ratio 0.3, tier 4)
3. All five conversion routes work independently (direct, tier-bump, civ-unique archetype, receiver-class, generic archetype)
4. No hidden transfer-only military squads
5. Stats bucket exclusivity (conversion routes + destroy routes are mutually exclusive per squad)
6. Backward-compatible aggregates match route breakdown
7. Cross-civ combinations are stable and balanced

---

## Infrastructure Overview

### Code Changes (cba.scar)
- **Lines 1216–1280:** `_LEAVER_CIV_UNIQUE_FALLBACK` table (36 entries; heroes now archetype-eligible)
- **Lines 1310–1330:** `_LEAVER_CANONICAL_ROLE` table (24 archetype role mappings; **NEW**)
- **Lines 1467–1516:** `_ResolveGenericArchetypeFallback()` (Tier 5 resolver; **NEW**)
- **Lines 1518–1568:** `_ResolveMilitaryRoute()` (centralized 5-tier resolver; **NEW**)
- **Lines 1613–1656:** Updated `_ResolveMilitarySquadBP` (now returns route name as 2nd value)
- **Lines 2555–2620:** Military branch rewrite (uses route helper, ZERO `Squad_SetPlayerOwner` in mil paths except same-BP approved exception)
- **Lines 2280–2295:** Stats initialization (12 mutually exclusive buckets)
- **Lines 2676–2740:** Stats persistence + LEAVER_END format (new breakdown format)

### Debug Infrastructure
- `cba_debug_leaver.scar` — Existing: 6-stage full validation, stress tests, coverage audits
- `cba_verify_military_pipeline.scar` — **NEW:** Automated route validation, hero audit, elephant check, stats consistency

### Test Automation (PowerShell)
- `leaver_verification_fullpass.ps1` — Log analyzer and test orchestrator

---

## Locked Policy Reference

### Hero Behavior (NEW POLICY)
| Unit | Policy | Target | Ratio | Tier | Rationale |
|------|--------|--------|-------|------|-----------|
| `unit_khan_` | archetype | horseman | 1.0 | 2 | Interchangeable with knights |
| `unit_jeanne_` | archetype | knight | 1.0 | 3 | Heavy unit equivalent |
| `unit_abbey_king_` | archetype | manatarms | 1.0 | 3 | Infantry equivalent |
| `unit_wynguard_` | destroy | — | — | — | Event/army unit; unreplaceable |

### Elephant Mapping (CHANGED POLICY)
| Unit | Policy | Target | Ratio | Tier | Note |
|------|--------|--------|-------|------|------|
| `unit_war_elephant_` | archetype | **knight** | **0.3** | 4 | Reduced from 0.5 to limit power spike |
| `unit_tower_elephant_` | archetype | **knight** | **0.3** | 4 | Unified with war_elephant; was springald |

### Approved Exceptions
1. **Same-BP military:** Transfer-only if src_civ = dst_civ AND src_bp = dst_bp (counted as `mil_same_bp`)
2. **Transfer-only non-military:** gaia_* and herdable families only (counted as `mil_transfer_only`)

---

## Test Execution Plan

### Phase 1: Pre-Game Setup (5 minutes)
1. Load Onslaught mod with latest cba.scar
2. Start a skirmish game with 4 human/AI players (variety of civs)
3. Enable debug flags in console:
   ```
   _LEAVER_DEBUG_VERBOSE = true
   _LEAVER_DEBUG_BYPASS_GATES = true  -- (optional: skip age-gating for stress tests)
   ```

### Phase 2: Automated Route Validation (2 minutes)
Run in console (run all 6 commands in order):

```
LeaverVerify_AutoRunAll()
```

**Expected Output:**
```
[LEAVER_VERIFY] Hero behavior: 4 pass, 0 fail
[LEAVER_VERIFY] Elephant mapping: 2 pass, 0 fail
[LEAVER_VERIFY] Military routes: 6 pass, 0 fail (or higher if testing more routes)
[LEAVER_VERIFY] Transfer-only classifier: ✓ PASS
[LEAVER_VERIFY] Stats consistency: ✓ ALL CHECKS PASSED
```

**If any FAIL:** Stop, investigate the specific failure, and report findings.

### Phase 3: Manual Military Resolve Testing (3 minutes)
Run detailed military resolution tests:

```
Debug_LeaverConversion_MilResolve(1, 2)
Debug_LeaverConversion_MilResolve(2, 3)
Debug_LeaverConversion_MilResolve(1, 4)
```

**Expected Output:**
```
[LEAVER_MIL_RESOLVE] Direct suffix swap: X routes
[LEAVER_MIL_RESOLVE] Tier-bump fallback: Y routes
[LEAVER_MIL_RESOLVE] Civ-unique archetype: Z routes
[LEAVER_MIL_RESOLVE] Receiver-class remap: A routes
[LEAVER_MIL_RESOLVE] Generic archetype: B routes
[LEAVER_MIL_RESOLVE] No resolve (destroy): C routes
```

**Validation:** 
- All route types should have non-zero counts
- No routes should ever re-own (0 transfers)

### Phase 4: Full Pipeline Stress Test (5 minutes)
Disconnect 2–4 players sequentially to trigger the leaver pipeline:

```
Debug_LeaverConversion_Stress(3)
```

**Expected Behavior:**
- Player 1 eliminated → transfers to best ally
- Player 2 eliminated → transfers to best ally
- Player 3 eliminated → transfers to best ally
- After each: scarlog shows [LEAVER_END] with new format

**Expected Output Format:**
```
[LEAVER_END] <src_civ>→<dst_civ> | <elapsed>s | ent=X sq=Y | bldg[...] eco[...] mil[conv=A dest=B same=C xfer=D | direct=E bump=F unique=G class=H generic=I | d:pol=J age=K fail=L nomap=M ratio=N] bypass=false
```

**Validation Criteria:**
1. `mil[conv=X dest=Y]` — All squads accounted for (conv + dest > 0)
2. `mil[...]` route breakdown non-zero (at least some routes used)
3. NO `mil_transfer_only` except for gaia/herdables
4. NO hidden transfers (all military either in a route or destroyed)

### Phase 5: Coverage Audit (10 minutes)
Run all-civ coverage check:

```
Debug_LeaverCoverage_AllCivPairs()
```

**Expected Output:**
```
[COVERAGE] All civ-pairs: <total> tested
[COVERAGE] avg_quality: X.X/3.0
[COVERAGE] gaps: <number> (should be low; ideally 0-5)
```

**Validation Criteria:**
- Quality should be ≥ 2.0 (most builds convert exactly or with minor fallbacks)
- Gaps should be minimal (≤5 out of 400+ civ-pairs)

### Phase 6: Performance Check (2 minutes)
Review pipeline timing from last run:

```
Debug_LeaverPerformance()
```

**Expected Output:**
```
[LEAVER_DETAIL] Phase3=X.XXs Phase4+5=Y.YYs Phase7=Z.ZZs
```

**Validation:** All phases complete in < 0.5s each (no obvious hangs or infinite loops)

---

## Log Analysis & Result Interpretation

### Scarlog (Expected Locations)
- **During tests:** `%USERPROFILE%\Documents\My Games\Age of Empires IV\LogFiles\<YYYY-MM-DD>\scarlog*.txt`

### Key Log Patterns to Verify

#### 1. Hero Behavior
```
[LEAVER_VERIFY] unit_khan_ [chinese]: unit_khan_→unit_horseman_(t2) | ✓ PASS
[LEAVER_VERIFY] unit_jeanne_ [french]: unit_jeanne_→unit_knight_(t3) | ✓ PASS
[LEAVER_VERIFY] unit_abbey_king_ [english]: unit_abbey_king_→unit_manatarms_(t3) | ✓ PASS
[LEAVER_VERIFY] unit_wynguard_ [english]: destroy_policy | ✓ PASS
```

#### 2. Elephant Mapping
```
[LEAVER_VERIFY] unit_war_elephant_: found | ratio=0.3 (expect 0.3) ✓ | target=unit_knight_ (expect unit_knight_) ✓ | tier=4 (expect 4) ✓
[LEAVER_VERIFY] unit_tower_elephant_: found | ratio=0.3 (expect 0.3) ✓ | target=unit_knight_ (expect unit_knight_) ✓ | tier=4 (expect 4) ✓
```

#### 3. Military Routes Active (during LEAVER_END)
```
[LEAVER_XFER] unit_archer_2_fre → unit_archer_2_eng | direct | mil_direct
[LEAVER_XFER] unit_archer_1_fre → unit_archer_2_eng | tier_bump | mil_tier_bump
[LEAVER_XFER] unit_khan_3_chi → unit_horseman_3_mal | civ_unique_archetype | mil_civ_unique_archetype
[LEAVER_XFER] unit_manatarms_3_jpn [destroyed] | destroy_policy | mil_destroy_policy
```

#### 4. No Hidden Transfers (should NOT appear anywhere)
```
[LEAVER_XFER] <military_unit> [transfer-only] — if this appears, failure!
[LEAVER_XFER] <military_unit> | mil_no_fallback_unit — old counter, shouldn't appear
```

#### 5. Stats Aggregates (from LEAVER_END or LEAVER_DETAIL)
```
mil[conv=50 dest=30 same=5 xfer=0 | direct=15 bump=10 unique=15 class=5 generic=5 | d:pol=10 age=5 fail=8 nomap=5 ratio=2]
```
→ All buckets sum correctly: 50 = 15+10+15+5+5 ✓, 30 = 10+5+8+5+2 ✓

---

## Issue Resolution Tree

### Issue: `✗ FAIL` in Hero Behavior Test
**Action:**
1. Check `_LEAVER_CIV_UNIQUE_FALLBACK` table around lines 1216–1240
2. Verify khan/jeanne/abbey_king have `policy = "archetype"` (not `"destroy"`)
3. Verify wynguard has `policy = "destroy"`
4. Run `LeaverVerify_HeroBehavior()` again

### Issue: Elephant Ratios ≠ 0.3
**Action:**
1. Read lines 1256–1257 in cba.scar directly
2. If they show `0.5`, rerun the edit from the implementation commit
3. If they show `0.3` but test still fails, check if generic archetype layer is overriding them

### Issue: Military Routes All Show "destroy"
**Action:**
1. Check if age-gating is blocking all routes: run with `_LEAVER_DEBUG_BYPASS_GATES = true`
2. Check receiver civ has any military units at all (some edge civs may have gaps)
3. Verify `_ResolveMilitarySquadBP`, `_ResolveReceiverClassFallback`, and `_ResolveGenericArchetypeFallback` are present in cba.scar

### Issue: Stats Don't Sum (convert + destroy ≠ squad_total)
**Action:**
1. Check `mil_transfer_only` count — it's NOT included in mil_converted but SHOULD be
2. Verify no [WARN] logs about unreachable code
3. Run `LeaverVerify_StatsConsistency()` for detailed bucket breakdown

### Issue: Stress Test Hangs
**Action:**
1. Check for infinite loops in `_Leaver_ContinueTransfer` while-loop (lines 2445+)
2. Check if `rule_pause` state is stuck: run `Debug_LeaverPipelineStatus()`
3. Enable `_LEAVER_DEBUG_VERBOSE` to see per-frame progress

---

## Sanity Checks (Spot Validation)

Before finalizing, run these spot checks manually:

### ✓ Check 1: Khan Routes to Horseman
```
_ResolveMilitaryRoute("unit_khan_3_chi", "chinese", "malian")
-- Expected: { route = "civ_unique_archetype", to_sbp = unit_horseman_3_mal, ratio = 1.0, ... }
```

### ✓ Check 2: Elephant Route
```
_ResolveMilitaryRoute("unit_war_elephant_4_sul", "sultanate", "abbasid")
-- Expected: { route = "civ_unique_archetype", to_sbp = unit_knight_4_abb, ratio = 0.3, ... }
```

### ✓ Check 3: No Transfer-Only Military
```
-- These should all be false (not classified as transfer-only):
_Leaver_IsNeutralOrTransferOnlySquad(nil, "unit_archer_2_fre")  -- false
_Leaver_IsNeutralOrTransferOnlySquad(nil, "unit_monk_3_fre")    -- false (eco, not transfer-only in military!)
_Leaver_IsNeutralOrTransferOnlySquad(nil, "gaia_wolf")          -- true (this is fine, gaia)
```

### ✓ Check 4: Stats Recorded
After any disconnect:
```
if _leaver_last_transfer_stats then
  print("mil_direct=" .. (_leaver_last_transfer_stats.mil_direct or 0))
  print("mil_destroy_policy=" .. (_leaver_last_transfer_stats.mil_destroy_policy or 0))
  -- etc.
end
```

---

## Final Validation Checklist

Before marking verification complete:

- [ ] All 6 `LeaverVerify_*()` functions return PASS/✓ 
- [ ] Heroes behave according to locked policy (khan/jeanne/abbey_king→archetype, wynguard→destroy)
- [ ] Elephants map to knight with 0.3 ratio
- [ ] Military resolve tests show all 5 routes active (direct, tier-bump, unique, class, generic)
- [ ] No transfer-only military outside of gaia/herdables
- [ ] Stats buckets are mutually exclusive and sum correctly
- [ ] Stress test (3–4 disconnects) completes without hangs
- [ ] Coverage audit shows <10 gaps out of 400+ civ-pairs
- [ ] LEAVER_END format matches new structure (route breakdown included)
- [ ] Performance is stable (all phases < 0.5s)
- [ ] No unexpected destroy spikes (all destroys have explicit reason: policy/age/create-fail/no-map/ratio)

---

## Success Criteria

**PASS:** 
- ✓ Military never transfers except: same-BP approved exception, gaia/herdable transfer-only
- ✓ All heroes route or destroy per policy
- ✓ All elephants map to knight at 0.3 ratio
- ✓ Stats are consistent and traceable
- ✓ Cross-civ combinations stable and balanced

**FAIL:**
- ✗ Any hidden military `Squad_SetPlayerOwner` transfer (except approved exceptions)
- ✗ Hero policies violated
- ✗ Stats buckets don't sum or are inconsistent
- ✗ Stress test hangs or crashes
- ✗ Destroy spike without clear reason

---

## Appendix: Debug Commands Quick Reference

| Command | Purpose | Time |
|---------|---------|------|
| `LeaverVerify_AutoRunAll()` | Full verification suite | 2m |
| `Debug_LeaverConversion_MilResolve(1,2)` | Military resolve for P1→P2 | 1m |
| `Debug_LeaverConversion_Stress(3)` | Disconnect 3 players sequentially | 5m |
| `Debug_LeaverCoverage_AllCivPairs()` | All-civ coverage audit | 10m |
| `Debug_LeaverConversion_Full(1)` | Single full 6-stage pipeline | 3m |
| `Debug_LeaverPerformance()` | Per-phase timing from last run | <1m |
| `Debug_LeaverPipelineStatus()` | Current pipeline state | <1m |

---

**Report:** `leaver_verification_report_<DATE>.txt`  
**Status:** Ready for live testing  
**Next Step:** Execute Phase 1 setup and run test suite
