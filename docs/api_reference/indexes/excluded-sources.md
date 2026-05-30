# Excluded Index Sources

The following index files are generated from Age of Empires IV game data or from Relic's SCAR documentation and are not redistributed in the public repository:

| File | Source | Reason |
|---|---|---|
| `campaign-index.md` | Relic campaign SCAR dump | Derived from Relic IP |
| `cardinal-ucs-strings.csv` | `cardinal.ucs` (game localization) | Game IP |
| `construction-menu-map.{csv,lua,md}` | AoE4World JSON + AGS construction menu | Derived third-party data |
| `function-index.{csv,md}` | Relic SCAR dump | Derived from Relic IP |
| `gameplay-index.md` | Relic gameplay SCAR dump | Derived from Relic IP |
| `globals-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `groups-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `imports-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `objectives-index.csv` | Relic SCAR dump | Derived from Relic IP |
| `scar-engine-functions.csv` | Relic `Essence_ScarFunctions.api` | Engine API surface |
| `scar-engine-constants.csv` | Relic `Essence_Constants.api` | Engine API surface |
| `ebp_alias_map.json` | Empty pipeline stub | No content yet |

## What remains

Only project-owned indexes (`onslaught-*.{csv,md}`, `villager-engineers-map.{csv,md}`) are published here. They are derived from this repository's own Onslaught SCAR source and are safe to redistribute.

## Local regeneration

The generator scripts that produce the excluded indexes live in the private/internal tree and rely on a local extraction of the official AoE IV game data. They are not part of the public repository. To regenerate them locally, you must:

1. Install the official Age of Empires IV Content Editor.
2. Use the editor's export tools to extract `cardinal.ucs`, the SCAR documentation, and any blueprint XML you need.
3. Run the private extraction pipeline against that local data.

No portion of that pipeline or its output is included in the public repository.
