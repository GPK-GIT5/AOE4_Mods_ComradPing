# Reward Animation — Visual Plan & Enhancement Reference

## Current Phase Flow

```
idle → (requirement change detected, enqueue milestones)
     → AdvanceQueue
         → completion_center  (0.35s, motion only, scale convergence)
         → completion_highlight (1.0s, glow peak+decay, deemphasis)
         → completion_fadeout   (0.4s, lead fades+slides left, shrinks)
         → reshuffle            (0.4s, 4th-icon entrance, new lead slides in)
         → advance
             → AdvanceQueue → (next milestone or idle)
```

**Total active duration per milestone**: ~2.15s (center 0.35 + highlight 1.0 + fadeout 0.4 + reshuffle 0.4)

---

## Target Animation Flow

### 1. Completion Center (0.35s)
- Unlocked reward icon moves to center position (slot 1)
- Scale eases up from 1.0 → 1.20 (highlight emphasis)
- Queued icons stagger right (+20px per slot) and scale down to 0.80
- Convergence gate: advance when scale reaches target ±0.01 or timeout at 0.6s

### 2. Completion Highlight (1.0s)
- Completed icon holds at center with gold border (#FFD700)
- Gold glow overlay: holds at 35% opacity for first 30%, then linear decay to 0
- Queued icons de-emphasize: opacity dims from 1.0 → 0.30 in first 30% of phase
- Bar shows 100% with gold fill color

### 3. Completion Fadeout (0.4s)
- Completed icon fades out: opacity 1.0 → 0.0
- Completed icon slides left by 20px and shrinks: scale 1.20 → 0.60
- Queued icons hold at de-emphasis positions, begin converging offset back toward 0

### 4. Reshuffle (0.4s) — Card Shuffle
- Completed icon is removed from the strip
- **New lead** (queue[1]): slides left into position from +20px offset, border crossfades grey → gold
- **Existing queue** (queue[2]): restores opacity 0.30 → 1.0, scale 0.80 → 1.0
- **4th reward entrance** (queue[3]): fades in from 0 opacity, slides from +20px offset, scale eases 0.80 → 1.0
- Bar decays from gold (100%) → green (0%), title crossfades dim → bright
- All color channels (fill, border, label, separator) lerp gold → idle values

### 5. Advance
- Pops next milestone from queue and re-enters completion_center (or idle if queue empty)
- On idle: syncs smoothing state, resets strip offset, starts idle bar from 0

---

## Timing Constants

| Constant | Value | Purpose |
|---|---|---|
| `CENTER_DURATION` | 0.35s | Scale convergence target |
| `CENTER_TIMEOUT` | 0.6s | Max center wait (fallback) |
| `HIGHLIGHT_DURATION` | 1.0s | Glow hold + decay |
| `FADEOUT_DURATION` | 0.4s | Lead icon fade + slide + shrink |
| `RESHUFFLE_DURATION` | 0.4s | Card shuffle + 4th-icon entrance |
| `ICON_OFFSET_SLIDE` | 20px | Stagger distance per slot |
| `SCALE_HIGHLIGHT` | 1.20 | Completed icon emphasis |
| `SCALE_DEEMPH` | 0.80 | Queued icon during highlight |
| `FADEOUT_SCALE_END` | 0.60 | Completed icon shrink target |
| `DEEMPHASIS_OPACITY` | 0.30 | Queued icon dim level |
| `GLOW_PEAK_OPACITY` | 0.35 | Gold overlay peak |
| `GLOW_HOLD_RATIO` | 0.30 | Fraction of highlight at peak |

---

## Polish Recommendations

### Easing Curves
- **Completion center scale**: currently linear interpolation. Recommend ease-out quadratic for snappier initial response: `progress = 1 - (1 - t)^2`
- **Fadeout slide**: currently linear. Recommend ease-in for acceleration as icon departs: `progress = t^2`
- **4th-icon entrance**: currently linear. Recommend ease-out for deceleration as icon arrives: `progress = 1 - (1 - t)^2`
- **Reshuffle lead slide**: ease-out to feel like icon "lands" in position

### Anticipation Timing
- Add a brief 50-100ms pause between fadeout end and reshuffle start where the strip holds empty at the vacated position. This creates an "anticipation beat" — the viewer registers the completed icon is gone before the shuffle begins.
- Implementation: insert an `anticipation` phase between `completion_fadeout` and `reshuffle` with empty delta, or add a start delay to reshuffle progress calculation.

### Sound Cues (AoE4 Engine: Sound_Play2DOnScreen)
- **Reward completion**: subtle gold "ding" or chime when entering `completion_highlight`
- **4th-icon entrance**: soft "whoosh" or slide sound during reshuffle
- **Queue drain → idle**: completion fanfare (if multiple milestones played in burst)
- Implementation considerations: Sound_Play2DOnScreen is available; sound assets would need to be identified from existing AoE4 mod sound banks or custom audio.

### Particle / Visual Effects
- **Glow overlay enhancement**: the current glow is a single Rectangle Fill with #AARRGGBB alpha. For richer effect, consider a second Rectangle with larger dimensions (34×34) behind the icon that pulses — simulating a bloom/halo. This stays within the Margin-safe binding approach.
- **Border pulse**: during completion_highlight, the gold border could briefly thicken (StrokeThickness lerp 2→3→2) over the glow hold period. Note: StrokeThickness DataContext binding needs testing for D3D safety.
- **Threshold text flash**: the threshold number below the completed icon could briefly change to gold color during highlight, then reset in reshuffle.

---

## Shuffle Logic — Current Analysis & Improvement Proposals

### Current Architecture
Each phase tick completely rebuilds the `comp_icons` array with computed positions. The smoothing system (`_PlayerUI_SmoothRewardIcons` / `_PlayerUI_TickRewardIconSmoothing`) only operates during idle — during playback, icon arrays are set directly.

**Strengths:**
- Deterministic: each tick computes values from `progress` alone (no accumulated state drift)
- Simple to reason about: phase progress → icon properties, pure function style
- Guard-safe: _SafeQueueEntry prevents nil icons at any index

**Weaknesses:**
- No inter-frame interpolation during phases (each tick snaps to computed position)
- No shared state between phases (reshuffle can't smoothly continue from fadeout positions)
- 4th-icon entrance previously had no animation (now added via reshuffle qi=3 special handling)

### Proposed Improvements (Future)

#### A. Phase-Aware Smoothing Integration
Route phase-generated icon arrays through `_PlayerUI_SmoothRewardIcons` before setting `ctx.rewardIcons`. This would enable:
- Automatic fade-in interpolation on slot content changes between phases
- Border color lerping via existing smoothing infrastructure
- Offset and scale lerping via slot state targets

**Cost**: moderate refactor. Each phase would set `targetOffsetX` / `targetScale` on slot state instead of computing final values. The smoothing tick would interpolate.
**Risk**: coupling phases to smoothing state could introduce drift if smoothing tick rate doesn't match phase expectations.

#### B. Eased Progress Functions
Replace linear `progress = elapsed / duration` with parametric easing:
```lua
local function _easeOut(t) return 1 - (1 - t) * (1 - t) end
local function _easeIn(t) return t * t end
local function _easeInOut(t)
    if t < 0.5 then return 2 * t * t end
    return 1 - (-2 * t + 2)^2 / 2
end
```
Per-phase easing profiles:
- `completion_center`: ease-out (fast start, gentle landing)
- `completion_highlight`: linear (steady hold, glow decay is already shaped)
- `completion_fadeout`: ease-in (slow departure, accelerating fade)
- `reshuffle`: ease-out (snappy shuffle, gentle settle)

#### C. Stagger Delay for Multi-Icon Motion
During reshuffle, stagger the start time of each icon's motion by a small delta (50-80ms per slot). The new lead starts moving first, queue[2] follows, 4th-icon enters last. Creates a "wave" shuffle feel.

**Implementation**: offset each icon's effective progress by `qi * staggerDelay / duration`.

---

## Debugger Command Reference

| Command | Alias | Description |
|---|---|---|
| `Debug_PlayerUI_RewardPlayback_Snapshot()` | `debug.playerUI.rewardSnapshot()` | One-shot state dump (phase, queue, icons, offsets, guards) |
| `Debug_PlayerUI_RewardPlayback_Inject(threshold, count)` | `debug.playerUI.rewardInject(50, 3)` | Inject synthetic milestones |
| `Debug_PlayerUI_RewardPlayback_InjectReal(score_delta)` | `debug.playerUI.rewardInjectReal(75)` | Add +score_delta real milestones from civ tree |
| `Debug_PlayerUI_RewardPlayback_CaptureFull(threshold, count, timeout)` | `debug.playerUI.rewardCaptureFull()` | Auto-capture idle + mid-animation + phase timing summary |
| `Debug_PlayerUI_RewardPlayback_SkipPhase()` | `debug.playerUI.rewardSkip()` | Skip current phase to next |
| `Debug_PlayerUI_RewardPlayback_Reset()` | `debug.playerUI.rewardReset()` | Force-reset to idle |

### Example Test Sequence
```
-- 1. Reset state
debug.playerUI.rewardReset()

-- 2. Full automated capture with phase timing
debug.playerUI.rewardCaptureFull(50, 3, 10)

-- 3. Real reward injection (+200 score from current kills)
debug.playerUI.rewardInjectReal(200)

-- 4. Snapshot mid-animation
debug.playerUI.rewardSnapshot()

-- 5. Skip to next phase for rapid iteration
debug.playerUI.rewardSkip()
```
