# PlayerUI Architecture — Quick Reference

**Scope:** Onslaught gamemode custom observer/player HUD  
**Date:** March 26, 2026  
**Path:** `Gamemodes/Onslaught/assets/scar/playerui/`

---

## File Map

```
playerui/
├── playerui.scar                  ← Entry point: OnInit, player list, UI_CreateScreen
├── playerui_settings.scar         ← Feature flags (PlayerUI_Settings table)
├── playerui_constants.scar        ← Resource icon path mappings
├── playerui_datacontext.scar      ← Root PlayerUiDataContext table (team summaries, rewards, limits)
├── playerui_initialization.scar   ← Lifecycle framework (Initialize/Reset/Stop)
├── playerui_rulesystem.scar       ← 1.0s data-gathering rule interval
├── playerui_animate.scar          ← 0.1s animation engine (number lerp, FLIP, decay, pulse)
├── playerui_ranking.scar          ← Rank sorting with hysteresis + FLIP animation
├── playerui_updateui.scar         ← Per-cycle data sync (35+ functions), team aggregation, HUD toggle
├── uidatacontext/
│   └── initialize_datacontext.scar ← Per-player slot defaults, team-split arrays
├── xaml/
│   ├── playerui_hud.scar          ← Main HUD XAML template (cards, center panel, unit strip)
│   └── playerui_togglebutton.scar ← Toggle button XAML (bottom-right HUD button)
└── tracking/
    ├── tracking_populationcomposition.scar  ← Worker/military/siege breakdown
    ├── tracking_gameobjectrepository.scar   ← Age tracking, landmark detection
    ├── tracking_ownedsquads.scar            ← Squad inventory by blueprint
    ├── tracking_queuedstuff.scar            ← Production queue snapshots
    ├── tracking_reliclocations.scar         ← Carried vs. deposited relic counts
    └── tracking_agingupprogress.scar        ← Age-up state, ETA, progress %
```

**Debug files** (separate directory):
```
debug/
├── cba_debug_playerui.scar       ← 4-phase diagnostic (init/data/UI/ranking)
└── cba_debug_playerui_anim.scar  ← 6-phase anim diagnostic, monitor, stress test, feature presets
```

---

## Execution Flow

```
PlayerUI_OnInit()
  ├─ Build _PlayerUI_AllPlayers (sorted: local, allies, enemies)
  ├─ PlayerUiRuleSystem:Initialize()        → 1.0s rule: _PlayerUI_RingRule
  │     └─ PlayerUI_UpdateDataContext()      → sync all player data
  │     └─ PlayerUI_ApplyDataContext()       → push to XAML
  ├─ PlayerUiInitialization:Initialize()    → lifecycle for all modules
  │     └─ PlayerUIDataContextMappings:Initialize() → per-player slots (max 8)
  ├─ PlayerUI_Animate_Init()                → 0.1s tick (self-pausing)
  │     └─ _PlayerUI_Animate_Tick()         → lerp, FLIP, decay, pulse
  │     └─ PlayerUI_Animate_ApplyDisplayValues() → write back to DataContext
  ├─ PlayerUI_Ranking_Init()                → initial rank state
  └─ UI_CreateScreen("PlayerUIHud", playerui_hud.scar)
```

**Two timing layers:**
| Interval | Driver | Purpose |
|----------|--------|---------|
| **1.0s** | `_PlayerUI_RingRule` | Read game state → populate DataContext |
| **0.1s** | `_PlayerUI_Animate_Tick` | Smooth transitions → write display values → push to XAML |

The 0.1s tick self-pauses when idle and unpauses when `SetTarget`/`TriggerDecay`/`TriggerScorePulse` is called.

---

## Data Flow

```
Game State (SCAR API)
    │
    ▼  [1.0s cycle]
PlayerUI_UpdateDataContext()          ← reads scores, pop, relics, rewards
    │  writes raw values into per-player slots
    │  calls PlayerUI_Animate_SetTarget("kill_1", rawScore)
    │  calls PlayerUI_Ranking_Update()
    │
    ▼  [0.1s tick]
_PlayerUI_Animate_Tick()
    │  lerps display values toward targets
    │  decays pulses, positions, highlights
    │
    ▼
PlayerUI_Animate_ApplyDisplayValues()
    │  writes animated values back into DataContext
    │  calls PlayerUI_UpdateTeamSummaries()
    │  calls PlayerUI_ApplyDataContext()
    │
    ▼
UI_SetDataContext("PlayerUIHud", PlayerUiDataContext)  → XAML bindings update
```

---

## Key Data Structures

### Root DataContext (`PlayerUiDataContext`)

| Key | Type | Source |
|-----|------|--------|
| `players` | array[8] | All player slots (indexed) |
| `teamLeft` | array | Local + allies |
| `teamRight` | array | Enemies |
| `localPlayer` | table | Ref to local player slot |
| `TeamSummaryLeft` / `Right` | table | Aggregated team totals |
| `AllPlayersSummary` | table | Combined totals (min 1 for div-zero safety) |
| `limits` | table | Siege/prod/workshop/outpost limits (local) |
| `rewards` | table | Reward progression (local) |
| `elapsedTimeDisplay` | string | Game clock |

### Per-Player Slot Fields

| Field | Type | Written By |
|-------|------|------------|
| `killScore` | number | animate (display value) |
| `killScoreColor` | string | animate → `_PlayerUI_GetScoreColor()` |
| `scoreGlowTier` | number | animate → `_PlayerUI_GetScoreGlowTier()` |
| `killScorePulseScale` | number | animate (pulse engine) |
| `killScorePulseFontSize` | number | animate (18 + scale * 16) |
| `killScorePulseActive` | boolean | animate (pulse > epsilon) |
| `isScoreUpdating` | boolean | animate → `IsTransitioning()` |
| `rankPosition` | number | ranking |
| `rankChangeType` | string | ranking ("none"/"minor"/"major") |
| `isContested` | boolean | ranking |
| `isTopPlayer` | boolean | ranking |
| `rankPredictionUp/Down` | boolean | ranking |
| `rankTranslateY` | number | ranking (FLIP animation) |
| `rankOffsetMargin` | string | ranking → "0,Y,0,0" |
| `rankScale` | number | ranking |
| `rankHighlightOpacity` | number | ranking (decay) |
| `rowOpacity` | number | ranking (1.0 or 0.4 if eliminated) |
| `rewardProgressText` | string | updateui |
| `rewardBarWidth` | number | updateui (0–100) |
| `rewardEarnedFlash` | boolean | updateui (decay-triggered) |

---

## Animation API

| Function | Use |
|----------|-----|
| `SetTarget(key, value)` | Queue smooth transition to value |
| `GetDisplay(key) → number` | Read current animated display value |
| `IsTransitioning(key) → bool` | True while animating |
| `TriggerScorePulse(index, score)` | Fire visual pulse on player card |
| `TriggerDecay(key, start, rate)` | Start timed decay (e.g., reward flash) |
| `GetDecay(key) → number` | Read current decay value |
| `SetPosition(key, value)` | Set FLIP invert offset |
| `SetPositionTarget(key, target)` | Set FLIP play target |

**Pulse constants:**
```
_PLAYERUI_PULSE_SCALE_PEAK  = 0.12   -- max font boost factor
_PLAYERUI_PULSE_DECAY       = 0.30   -- per-tick decay
_PLAYERUI_PULSE_EPSILON     = 0.01   -- snap-to-zero threshold
```

---

## Common Edit Patterns

### Change score display font/color/animation
- **XAML binding**: `xaml/playerui_hud.scar` → look for `KillScoreText` (player card) or `TeamSummaryLeft/Right` (center)
- **Color gradient**: `playerui_updateui.scar` → `_PlayerUI_GetScoreColor()` + color constants at top
- **Pulse behavior**: `playerui_animate.scar` → `ApplyDisplayValues()` pulse section + constants

### Add a new per-player field
1. **Default**: `initialize_datacontext.scar` → `PlayerUIDataContextMappings:Initialize()` loop
2. **Fallback**: `playerui_updateui.scar` → player init block (~line 146) + else-block (~line 258)
3. **Population**: `playerui_animate.scar` → `ApplyDisplayValues()` per-player loop
4. **XAML**: `xaml/playerui_hud.scar` → bind via `{Binding [fieldName]}`
5. **Debug**: `cba_debug_playerui_anim.scar` → `required_fields` table + snapshot format string

### Add a team summary field
1. **Default**: `playerui_datacontext.scar` → `TeamSummaryLeft`/`Right` tables
2. **Aggregation**: `playerui_updateui.scar` → `PlayerUI_UpdateTeamSummaries()`
3. **XAML**: `xaml/playerui_hud.scar` → `{Binding [TeamSummaryLeft][FieldName]}`

### Change rank behavior
- **Thresholds/cooldowns**: `playerui_ranking.scar` → constants at top
- **FLIP animation**: `playerui_ranking.scar` → `Ranking_Update()` phase 9
- **Prediction arrows**: `playerui_ranking.scar` → `_Ranking_WriteFieldsToSlots()`
- **Feature toggle**: `playerui_settings.scar` → `EnableRankTranslateAnimation`, `EnableRankScaleAnimation`

### Toggle a feature on/off
- All flags in `playerui_settings.scar` → `PlayerUI_Settings` table
- Runtime toggle via debug console: `PlayerUI_Settings.EnableX = false`

### Modify HUD layout
- **Player card row**: `xaml/playerui_hud.scar` → `DataTemplate x:Key="PlayerUiTeamResources"`
- **Center panel**: `xaml/playerui_hud.scar` → `DataTemplate x:Key="PlayerUiCenterPanel"`
- **Toggle button**: `xaml/playerui_togglebutton.scar`

---

## XAML Safety Rules

1. **Never bind** `Opacity`, `Width`, or `Height` dynamically — known crash vector
2. Use `DataTrigger` with **static Setter values** only (no converters on Opacity/Width)
3. `FontSize` binding to a number field is safe (used for pulse animation)
4. All `UI_SetDataContext` calls wrapped in `pcall` crash guard (when `EnableToggleCrashGuard = true`)
5. Pre-warm HUD visibility at init to avoid first-frame binding errors

---

## Debug Console Commands

### Quick diagnostics
```lua
Debug_PlayerUI()                         -- full 4-phase diagnostic
Debug_PlayerUI_Anim()                    -- full 6-phase animation diagnostic
Debug_PlayerUI_Anim_Snapshot()           -- one-shot field dump
Debug_PlayerUI_Anim_FeatureStatus()      -- print all 13 feature flags
Debug_PlayerUI_Anim_ValidateDataContext() -- binding coverage check
```

### Feature isolation
```lua
Debug_PlayerUI_Anim_PresetSafe()         -- all animations OFF (stable baseline)
Debug_PlayerUI_Anim_PresetAll()          -- all animations ON
Debug_PlayerUI_Anim_Features(move, scale, pulse, dim)  -- selective toggle
```

### Stress testing
```lua
Debug_PlayerUI_Anim_Stress(10)           -- 10 rapid rank swaps
Debug_PlayerUI_Anim_Pulse(1)             -- force pulse on player 1
Debug_PlayerUI_Anim_Monitor()            -- continuous invariant monitor (0.5s)
Debug_PlayerUI_Anim_MonitorStop()
```

---

## Session Summary (March 26, 2026)

Changes made during this session:

1. **Score color gradient** — replaced reward-ratio tiers with score-based gradient (white→yellow→orange→red at 0/5000/7500/10000)
2. **Rank prediction arrows** — added up/down arrows computed from adjacent score comparison; renamed `isScoreIncreasing` → `rankPredictionUp/Down`
3. **Background effects removed** — stripped `KillScorePulseFlash` rectangle, `RankChangeStatsHighlight`, and DropShadow glow DataTriggers from player cards
4. **Score pulse** — whole-score `FontSize` pulse on player cards via `killScorePulseFontSize` binding; triggered on displayed score increment
5. **Center section alignment fix** — center panel scores set to `TextAlignment="Center"`, removed `TranslateTransform X="1"` pixel offset from icon
6. **Dead field cleanup** — removed `killScoreDigitPulseFontSize`, `killScorePrefix`, `killScoreLastDigit` from all files (init, updateui, animate, debug)
