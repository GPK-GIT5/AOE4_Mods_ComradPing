# API Reference

Primary reference hub for SCAR/API lookups in this repository.

This folder is private-maintained and retained in public docs navigation because it is the canonical lookup layer for SCAR functions, signatures, constants, events, and workspace-specific indexes.

## Purpose and scope

Use this folder when you need authoritative lookup material for:

- SCAR callable functions and signatures
- Command/constants/event references
- Onslaught-oriented symbol indexes and global maps
- Navigation indexes for discovery across the reference set

This folder is reference-first and intentionally complements, rather than replaces, implementation guides in [../development_guides/](../development_guides/) and system explainers in [../game_systems/](../game_systems/).

## Structure

```
api_reference/
├── README.md
├── INDEX.md
├── api/
│   └── README.md
├── indexes/
│   ├── README.md
│   ├── onslaught-function-index.md
│   ├── onslaught-globals-index.md
│   ├── villager-engineers-map.md
│   └── excluded-sources.md
└── navigation/
	├── README.md
	├── INDEX.md
	├── master-index.md
	├── data-index.md
	└── aoe4world-data-index.md
```

## Contents and when to use them

### Root files

- [README.md](README.md) - primary navigation and usage guidance
- [INDEX.md](INDEX.md) - deep index for direct file-level lookup

### `api/` SCAR scripting overview

- [api/README.md](api/README.md) - overview of the SCAR scripting system (function surface, command constants, game enums, event system); engine catalogs removed per Xbox Game Content Usage Rules

### `indexes/` curated lookup indexes

- [indexes/onslaught-function-index.md](indexes/onslaught-function-index.md) - Onslaught function map
- [indexes/onslaught-globals-index.md](indexes/onslaught-globals-index.md) - Onslaught globals map
- [indexes/villager-engineers-map.md](indexes/villager-engineers-map.md) - villager/engineer behavior lookup
- [indexes/excluded-sources.md](indexes/excluded-sources.md) - excluded-source policy and rationale

### `navigation/` discovery and compatibility indexes

- [navigation/master-index.md](navigation/master-index.md) - broader campaign/system overview index
- [navigation/data-index.md](navigation/data-index.md) - generated dependency/data summary snapshot
- [navigation/aoe4world-data-index.md](navigation/aoe4world-data-index.md) - data cross-reference guide
- [navigation/INDEX.md](navigation/INDEX.md) - compatibility index retained for older bookmarks

## Recommended usage workflows

### Quick API lookup

1. Open [api/README.md](api/README.md) for a description of the SCAR scripting surface and its coverage areas.
2. For Onslaught-specific symbols, use [indexes/onslaught-function-index.md](indexes/onslaught-function-index.md) or [indexes/onslaught-globals-index.md](indexes/onslaught-globals-index.md).

### Deep symbol lookup (Onslaught-heavy work)

1. Start in [INDEX.md](INDEX.md).
2. Narrow with [indexes/README.md](indexes/README.md).
3. Use [indexes/onslaught-function-index.md](indexes/onslaught-function-index.md) and [indexes/onslaught-globals-index.md](indexes/onslaught-globals-index.md).

### Troubleshooting missing/ambiguous references

1. Check [indexes/excluded-sources.md](indexes/excluded-sources.md) for known source constraints.
2. Use [navigation/README.md](navigation/README.md) and [navigation/master-index.md](navigation/master-index.md) to broaden discovery.
3. Cross-check implementation context in [../gamemodes/MOD-INDEX.md](../gamemodes/MOD-INDEX.md) and [../game_systems/README.md](../game_systems/README.md).

## Related docs

- [../README.md](../README.md) - top-level docs index
- [../game_systems/README.md](../game_systems/README.md) - system-level references
- [../development_guides/README.md](../development_guides/README.md) - implementation guides
- [../gamemodes/MOD-INDEX.md](../gamemodes/MOD-INDEX.md) - mod/scenario cross-reference hub
- [../scenarios/README.md](../scenarios/README.md) - scenario runtime mirror

## Maintenance notes

- Keep [README.md](README.md) and [INDEX.md](INDEX.md) synchronized when adding or removing files.
- New index/reference documents should be linked from their subtree README and from [INDEX.md](INDEX.md).
- If compatibility links are updated, preserve [navigation/INDEX.md](navigation/INDEX.md) as a stable redirect surface for older bookmarks.
