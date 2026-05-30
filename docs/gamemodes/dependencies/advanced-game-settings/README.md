# Dependency: Advanced Game Settings (AGS)

The `Gamemodes/Dependencies/Advanced Game Settings/` folder in the source workspace contains a full local copy of Woprock's **Advanced Game Settings** mod. That copy is not published in this repository because the mod is an independent third-party project with its own release channel.

## Upstream

- **Author**: Woprock
- **Mod**: Advanced Game Settings for Age of Empires IV
- **Where to get it**: Subscribe through the Age of Empires IV in-game mod browser, or download from the official Age of Empires IV mod portal.

## Why Onslaught depends on it

Onslaught builds on top of AGS for its game-setting framework, win-condition wiring, balance helpers, and several gameplay subsystems. The published Onslaught SCAR source under [Gamemodes/Onslaught/assets/scar](../../../../Gamemodes/Onslaught/assets/scar/) imports AGS modules and includes a vendored subset of AGS code under `assets/scar/AGS/` for ease of local development.

## Local setup for Onslaught development

1. Subscribe to or download Woprock's Advanced Game Settings mod.
2. Place it under `Gamemodes/Dependencies/Advanced Game Settings/` in your local workspace, mirroring the structure shown below.
3. Open `Gamemodes/Onslaught/CBA Custom v1f.aoe4mod` in the AoE IV Content Editor and build.

## Original subtree shape (for orientation only)

```
Advanced Game Settings/
├── Advanced Game Settings.aoe4mod
├── assets/
│   ├── locdb/
│   └── scar/
│       ├── ags_cardinal.scar
│       ├── ags_global_settings.scar
│       ├── ai/  balance/  conditions/  coreconditions/
│       ├── diplomacy/  gamemodes/  gameplay/  helpers/
│       ├── replay/  specials/  startconditions/  winconditions/
└── docs/
```

## License

Advanced Game Settings is © Woprock and distributed under the terms set by its author. This project does not relicense or redistribute it.
