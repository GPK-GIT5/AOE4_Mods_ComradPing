# BoonUI Integration — Vendored Subset

Covers `Gamemodes/Onslaught/assets/scar/boonui/` — three SCAR files derived from the BoonUI community selection-panel pattern, vendored inside Onslaught.

This folder **is present** in the public repository at [`Gamemodes/Onslaught/assets/scar/boonui/`](../../../../../Gamemodes/Onslaught/assets/scar/boonui/) because it is part of the published Onslaught source.

## Structure

```
boonui/
├── boon_selection.scar        # Public API: BoonSelection_Show(), _Hide(), _IsActive()
├── boon_selection_data.scar   # Data model and state management
└── boon_selection_xaml.scar   # XamlPresenter template and bindings
```

**Entry point**: `boon_selection.scar` — the only file directly imported by Onslaught systems.

## Integration points

| Onslaught system | Integration |
|---|---|
| Reward selection events | Calls `BoonSelection_Show(options)` with reward choices |
| Cleanup hooks | Calls `BoonSelection_Hide()` on round transition or disconnect |

## Upstream guide

See the authored integration guide: [docs/development_guides/third_party/boonui-community/boonui-guide.md](../../../../development_guides/third_party/boonui-community/boonui-guide.md)

## Attribution

Community-derived BoonUI pattern. See [CREDITS.md](../../../../../CREDITS.md) for full attribution.
