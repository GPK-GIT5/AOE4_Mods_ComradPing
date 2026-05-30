# 2026-05-14 SiegeTest MP-safety fix — Frame-1297 OOS

## Summary

OOS at frame 1297 in session `AoE4_05_13_17h-19m-54s` (host) / `AoE4_05_13_17h-20m-16s` (device 2).
Root cause: `Debug_SiegeTest()` Phase 0 setup called sim-mutating engine APIs on the dev host only.

---

## Diverging sections (frame 1297 diff)

| Section | Host | Dev 2 | Verdict |
|---|---|---|---|
| `randomstream.index` | 584 | 572 | **DIFFER** — +12 draws on host |
| `randomflow` | 12× `ALBR` IDs | empty | **DIFFER** — host consumed 12 RNG tagged ALBR |
| `playerlist.player[1002]` | 13 upgrades, resources 50k | 4 upgrades, resources 100k | **DIFFER** — 9 extra upgrades + resources spent on host |
| `statichierarchicalgrid` | `crc insert: -573352099` + 9× BV history for entity 1000005719 | `crc insert: 1308453598`, no history | **DIFFER** — entity 1000005719 moved 9× on host |
| `globalstatetreemodule` | 1158 non-det IDs | 1151 | **DIFFER** (+7 on host) |
| All other sections | — | — | SAME |

---

## Root cause

`Debug_StressGamemode_Automated` was invoked from the host DevMenu at 17:30:02 (after "expect-desync confirm" at 17:30:02). All suites through EventProbes were read-only and completed cleanly. `SiegeTest` started at 17:31:28, exactly matching frame 1297.

**`Debug_SiegeTest()` Phase 0 setup executed these sim mutations on the host-only:**

```lua
-- Around line 498 (pre-fix):
pcall(Player_SetCurrentAge, player.id, AGE_CASTLE)      -- advances P3 malian → Castle age
                                                         -- triggers 9 upgrade completions
local ok_bp, upgrade_bp = pcall(AGS_GetCivilizationUpgrade, civ, AGS_UP_SIEGE_ENGINEERS)
if ok_bp and upgrade_bp then
    pcall(Player_CompleteUpgrade, player.id, upgrade_bp) -- grants SE upgrade
end
_ST_GrantResources(player)  -- Player_SetResource × 4 → sets resources to 50k
_ST_ResetCounters(player)   -- kills existing siege, recounts
```

These ran on the host only. Device 2 received no corresponding commands. By lockstep frame 1297, player 1002 state was irrecoverably diverged.

**Player 1002 = malian = P3 (first human player found by `_ST_ResolvePlayer`).**

The `Player_SetCurrentAge` call advancing malian to Castle age is what caused the 9 extra upgrade completions (the castle age landmark/upgrade chain) and the entity 1000005719 BV changes (castle landmark placement triggering spatial grid updates). The 12 ALBR random draws appear to be from the spawning/age system.

---

## Fix

**File:** `Gamemodes/Onslaught/assets/scar/debug/cba_debug_siege_test.scar`

Added MP guard at the top of `Debug_SiegeTest()`:

```lua
if type(World_IsMultiplayerGame) == "function" and World_IsMultiplayerGame() then
    print("[SIEGE_TEST] Skipped in MP (sim-mutating: age/upgrade/resource/spawn/kill)")
    _Debug_EndMarker(_ST_SUITE, 0, 0, 0)
    return
end
```

The `_Debug_EndMarker` call is required to advance the sub-orchestrator to the next suite; a bare `return` would stall the automated run.

---

## Scope check — other automated suites

| Suite | Sim mutations? | Status |
|---|---|---|
| SmokeTests | None | Safe |
| Validation | None | Safe |
| StressTest | None | Safe |
| Coverage | None | Safe |
| EventProbes | None (pcall with nil context) | Safe |
| **SiegeTest** | **Age/upgrade/resource/spawn/kill** | **Fixed this session** |
| AdvStressAll | MaxPopPressure: fixed last session | Safe |
| AIPlayerTest | None | Safe |
| AIStressTest | None | Safe |

ComprehensiveStress has Visual phases with `Player_SetResource` and `UnitEntry_DeploySquads`, but ComprehensiveStress is NOT in the automated plan (`Debug_StressGamemode_Automated`) — only in the manual `Debug_StressGamemode`.

---

## Audit

`scripts/audit_devmenu_mp_safety.ps1` passes clean (exit 0). Note: the audit only covers `devmenuUI/**`; debug test files are outside its scope by design (they are dev-only, gated by the devmenu confirm-once pattern).
