# AGS Integration — Vendored Subset

Covers `Gamemodes/Onslaught/assets/scar/AGS/` — a subset of Woprock's Advanced Game Settings mod vendored inside Onslaught.

This folder **is present** in the public repository at [`Gamemodes/Onslaught/assets/scar/AGS/`](../../../../../Gamemodes/Onslaught/assets/scar/AGS/) because it is part of the published Onslaught source (included per the "copy all `.scar` files as-is" directive).

## Structure (vendored subset only)

```
AGS/
├── ags_global_settings.scar   # AGS global settings table
├── CBA/                       # CBA-specific AGS hooks
├── helpers/                   # Shared AGS utility functions
└── specials/                  # AGS specials integration
```

This is a **subset** of AGS, not the full mod. The full mod has many additional trees that Onslaught does not directly consume.

## Integration points

| Onslaught file | Imports |
|---|---|
| `cba.scar` | AGS global settings and CBA hooks |
| `cba_ai/` modules | AGS helper utilities |
| Reward/special systems | AGS specials integration |

## Upstream source

**Author**: Woprock — Advanced Game Settings for Age of Empires IV.  
Full mod: see [docs/gamemodes/dependencies/advanced-game-settings/README.md](../../dependencies/advanced-game-settings/README.md) for where to obtain it and how to set up a local build.

## Attribution

Vendored from Woprock's Advanced Game Settings. See [CREDITS.md](../../../../../CREDITS.md) for full attribution.
