# Onslaught Editor Metadata

The `Gamemodes/Onslaught/.aoe4/` folder from the private workspace is not present in this public repository.

## Folder covered

AoE IV Content Editor project state — created and maintained automatically by the editor for the author's local installation.

```
.aoe4/
└── CBA Custom v1f/
    ├── Layout.xml           # Editor window layout state
    └── ProjectSettings.xml  # Content Editor project configuration
```

## Integration points

Neither file is required to run the compiled mod. They are only needed when opening the project in the Content Editor, which regenerates them automatically.

## Local setup

Opening [`Gamemodes/Onslaught/CBA Custom v1f.aoe4mod`](../../../../Gamemodes/Onslaught/CBA%20Custom%20v1f.aoe4mod) in the Content Editor on any machine will regenerate `.aoe4/` locally. No manual setup needed.
