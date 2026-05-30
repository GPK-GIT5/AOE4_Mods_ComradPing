# Data Authority Matrix

> Which data source is authoritative for each domain.
> Generated: 2026-05-09 00:00

## Source Priority

| Data Domain | Authoritative Source | Backup / Cross-check | Notes |
|-------------|---------------------|----------------------|-------|
| Unit stats (HP, cost, damage) | Extracted game attrib (`Gameplay_data_duplicate/assets/attrib/...`) | `game_data/extracted/aoe4/data/units/all-unified.json` + runtime `BP_GetEntityBPCost` | Extraction is source of truth; JSON/runtime are validation layers |
| Building stats | Extracted game attrib (`Gameplay_data_duplicate/assets/attrib/...`) | `game_data/extracted/aoe4/data/buildings/all-unified.json` + runtime `BP_GetEntityBPCost` | Extraction is source of truth; garrison capacity remains runtime-only |
| Technology costs | Extracted game attrib (`Gameplay_data_duplicate/assets/attrib/...`) | `game_data/extracted/aoe4/data/technologies/all-unified.json` + runtime `Player_GetUpgradeBPCost` | Extraction is source of truth; JSON costs may be array format |
| New DLC civ onboarding | Extracted `Attrib.sga` (EBP/SBP/upgrade XML) | AoE4World endpoints | AoE4World is reference-only; do not seed IDs from AoE4World |
| Blueprint existence | Runtime `EBP_Exists` / `SBP_Exists` | JSON attribName presence | Runtime is ground truth |
| Civ identity | `game_data/extracted/aoe4/data/civilizations/civs-index.json` | `AGS_ENTITY_TABLE` key set | 23 civs in JSON; runtime may have more |
| Civ parent mapping | `AGS_CIV_PARENT_MAP` (SCAR) | Cross-check with DLC inventory | 6 DLC variants mapped |
| Blueprint suffix | `CBA_CIV_BP_SUFFIX` (SCAR) | Derivable from attribName patterns | SCAR table is authoritative |
| SCAR API signatures | `game_data/extracted/aoe4/scardocs/parsed_functions.json` | `docs/api_reference/api/scar-engine-api-signatures.md` | 1,983 functions |
| Game events | `docs/api_reference/api/game-events.md` | n/a | 188 GE_* events |
| Function index | `docs/api_reference/indexes/function-index.csv` | n/a | 8,989 workspace functions |
| DLC blueprint names | `game_data/extracted/aoe4/data/dlc_bp_inventory.txt` | Per-civ JSON folders | Pipe-delimited attribName-to-id map |
| Production chains | Derived from `producedBy[]` in JSON | n/a | Computed in Stage 2a |
| Unit DPS | Derived from weapons[] in JSON | n/a | Computed in Stage 2a |

## Civ Coverage (per-civ JSON file counts)

| Civ | Units | Buildings | Technologies |
|-----|-------|-----------|--------------|
| abbasid | 38 | 25 | 95 |
| ayyubids | 40 | 25 | 97 |
| byzantines | 81 | 33 | 71 |
| chinese | 46 | 33 | 68 |
| delhi | 37 | 30 | 80 |
| english | 43 | 30 | 69 |
| french | 40 | 30 | 72 |
| goldenhorde | 47 | 19 | 81 |
| hre | 38 | 30 | 71 |
| japanese | 46 | 29 | 74 |
| jeannedarc | 51 | 30 | 78 |
| lancaster | 42 | 31 | 78 |
| macedonian | 43 | 31 | 95 |
| malians | 44 | 32 | 69 |
| mongols | 53 | 21 | 99 |
| orderofthedragon | 37 | 30 | 71 |
| ottomans | 41 | 31 | 69 |
| rus | 37 | 30 | 76 |
| sengoku | 48 | 31 | 73 |
| templar | 49 | 23 | 74 |
| tughlaq | 40 | 28 | 56 |
| unified | 215 | 156 | 449 |
| zhuxi | 40 | 33 | 72 |
| jin | 0 | 0 | 0 (EBP extracted; AoE4World WIP) |

## Source Freshness

| Category | Files | Size (KB) | Last Modified |
|----------|-------|-----------|---------------|
| civilizations | 23 | 236.9 | 2026-03-19 00:23 |
| units | 1266 | 23798.9 | 2026-03-19 00:23 |
| buildings | 861 | 10914.5 | 2026-03-19 00:23 |
| technologies | 2207 | 25456.6 | 2026-03-19 00:23 |
| scardocs | 7 | 1240.5 | 2026-03-19 00:23 |
| scar_dump | 532 | 9476.8 | 2026-03-19 00:23 |
| dlc_bp_inventory | 1 | 19.5 | 2026-03-26 02:40 |
