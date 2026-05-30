# Onslaught Options Schema

Auto-generated on 2026-04-02 05:31 from `ags_global_settings.scar`.
Complete schema of `AGS_GLOBAL_SETTINGS` with types, defaults, enums, and descriptions.

- **95** option keys
- **50** enum constants across 12 groups

## Enum Constants

### Team Victory

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_TEAM_VICTORY_FFA` | 0 |  |
| `AGS_GS_TEAM_VICTORY_STANDARD` | 1 |  |
| `AGS_GS_TEAM_VICTORY_DYNAMIC` | 2 |  |

### Settlement

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_SETTLEMENT_SCATTERED` | 0 |  |
| `AGS_GS_SETTLEMENT_NOMADIC` | 1 |  |
| `AGS_GS_SETTLEMENT_SETTLED` | 2 |  |
| `AGS_GS_SETTLEMENT_FORTIFIED` | 3 |  |
| `AGS_GS_SETTLEMENT_PILGRIMS` | 4 |  |

### Team Balance

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_TEAM_BALANCE_NONE` | 0 |  |
| `AGS_GS_TEAM_BALANCE_POPULATION` | 1 |  |
| `AGS_GS_TEAM_BALANCE_RESOURCES` | 2 |  |
| `AGS_GS_TEAM_BALANCE_FULL` | 3 |  |

### Wonder

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_WONDER_SCALE_COST_DISABLED` | -1 |  |

### Team Vision

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_TEAM_VISION_NONE` | 0 |  |
| `AGS_GS_TEAM_VISION_REQUIRES_MARKET` | 1 |  |
| `AGS_GS_TEAM_VISION_ALWAYS` | 2 |  |

### Map Vision

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_MAP_VISION_CONCEALED` | 0 |  |
| `AGS_GS_MAP_VISION_EXPLORED` | 1 |  |
| `AGS_GS_MAP_VISION_REVEALED` | 2 |  |

### Age

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_AGE_NONE` | 0 |  |
| `AGS_GS_AGE_DARK` | 1 |  |
| `AGS_GS_AGE_FEUDAL` | 2 |  |
| `AGS_GS_AGE_CASTLE` | 3 |  |
| `AGS_GS_AGE_IMPERIAL` | 4 |  |
| `AGS_GS_AGE_LATE_IMPERIAL` | 5 |  |

### Resources

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_RESOURCES_NONE` | 0 |  |
| `AGS_GS_RESOURCES_LOW` | 1 |  |
| `AGS_GS_RESOURCES_NORMAL` | 2 |  |
| `AGS_GS_RESOURCES_MEDIUM` | 3 |  |
| `AGS_GS_RESOURCES_HIGH` | 4 |  |
| `AGS_GS_RESOURCES_VERY_HIGH` | 5 |  |
| `AGS_GS_RESOURCES_MAXIMUM` | 6 |  |

### Town Centers

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_TC_RESTRICTIONS_NONE` | 0 |  |
| `AGS_GS_TC_RESTRICTIONS_NORMAL` | 1 |  |
| `AGS_GS_TC_RESTRICTIONS_LANDMARKS` | 2 |  |

### Handicap

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_HANDICAP_TYPE_DISABLED` | 0 |  |
| `AGS_GS_HANDICAP_TYPE_ECONOMIC` | 1 |  |
| `AGS_GS_HANDICAP_TYPE_MILITARY` | 2 |  |
| `AGS_GS_HANDICAP_TYPE_BOTH` | 3 |  |

### Colors

| Constant | Value | Note |
|----------|-------|------|
| `AGS_GS_COLOR_BLUE` | 1 | Azure Blue |
| `AGS_GS_COLOR_RED` | 2 | Red Orange |
| `AGS_GS_COLOR_YELLOW` | 3 | Citrine Yellow |
| `AGS_GS_COLOR_GREEN` | 4 | Vibrant Green |
| `AGS_GS_COLOR_TURQUOISE` | 5 | Bright Turquoise |
| `AGS_GS_COLOR_PURPLE` | 6 | Purple Mimosa |
| `AGS_GS_COLOR_ORANGE` | 7 | Blaze Orange |
| `AGS_GS_COLOR_PINK` | 8 | Hot Pink |
| `AGS_GS_COLOR_GREY` | 9 | Monsoon/Natural Grey |

### CBA Fixed Limits

| Constant | Value | Note |
|----------|-------|------|
| `AGS_CBA_FIXED_MAX_PRODUCTION_BUILDINGS` | 15 |  |
| `AGS_CBA_FIXED_MAX_SIEGE_WORKSHOP` | 2 |  |

## Settings Schema

### CBA Mode Settings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `AutoAge` | int | `600` |  |  |
| `NoSiege` | bool | `false` |  |  |
| `NoWall` | bool | `false` |  |  |
| `NoArsenal` | bool | `false` |  |  |
| `DockHouse` | bool | `false` |  |  |
| `EliminatedLoseKeep` | bool | `true` |  |  |
| `Option_Reward_Age` | bool | `false` |  |  |
| `CBA_Rewards` | string | `"onslaught"` |  |  |
| `gatherRates` | float | `1.00` |  |  |
| `MaximumProductionBuildings` | unknown | `AGS_CBA_FIXED_MAX_PRODUCTION_BUILDINGS` |  |  |
| `MaximumSiegeWorkshop` | unknown | `AGS_CBA_FIXED_MAX_SIEGE_WORKSHOP` |  |  |
| `SpecialPopulationUI` | bool | `false` |  |  |

### ConquestSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Capital` | bool | `true` |  |  |
| `Landmarks` | bool | `true` |  |  |
| `TownCenters` | bool | `false` |  |  |
| `Keeps` | bool | `false` |  |  |
| `Wonder` | bool | `false` |  |  |
| `IsTeamShared` | bool | `false` |  |  |

### Core Match Conditions

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Settlement` | enum | `AGS_GS_SETTLEMENT_SETTLED` | Settlement | Initial start of each player. |
| `Treaty` | bool | `false` |  | Initial peace time disabled. |
| `TeamVictory` | enum | `AGS_GS_TEAM_VICTORY_STANDARD` | Team Victory | Who is considered potential winner. |
| `TeamSolidarity` | bool | `false` |  | Team is eliminated together. |
| `MaintainTeamBalance` | enum | `AGS_GS_TEAM_BALANCE_NONE` | Team Balance |  |

### EliminationSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `EnableAITakeover` | bool | `false` |  | Disconnected players are eliminated; assets converted via Mod_EliminatePlayerUnits. |

### Game Rules

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Diplomacy` | bool | `true` |  | undefined, disables whole diplomacy module. |
| `Tributes` | bool | `true` |  |  |
| `Relations` | bool | `false` |  |  |
| `TeamVision` | enum | `AGS_GS_TEAM_VISION_ALWAYS` | Team Vision |  |
| `MapVision` | enum | `AGS_GS_MAP_VISION_CONCEALED` | Map Vision |  |

### Legacy/Arcade Toggles

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `StartingKings` | int | `0` |  |  |
| `Ding` | bool | `false` |  |  |
| `SimulationSpeed` | float | `1.00` |  |  |
| `EmpoweredKings` | bool | `false` |  |  |
| `WonderConstruction` | bool | `false` |  |  |
| `Treasures` | bool | `false` |  |  |

### Match Setup

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `ScoreVisibility` | bool | `false` |  |  |
| `MinimumPopulation` | int | `100` |  |  |
| `MinimumPopulationReset` | bool | `false` |  | undefined, removes mongol bonus |
| `MaximumPopulation` | int | `200` |  |  |
| `MaximumMedicPopulation` | int | `15` |  |  |
| `StartingVillagers` | int | `6` |  |  |
| `StartingKeeps` | int | `1` |  |  |
| `EarlyMarket` | bool | `false` |  |  |
| `NoDock` | bool | `false` |  |  |
| `TreeBombardment` | bool | `false` |  |  |
| `GameRates` | float | `1.00` |  |  |
| `UnitRates` | float | `1.00` |  |  |
| `DoubleWorkers` | bool | `false` |  |  |
| `TownCenterRestrictions` | enum | `AGS_GS_TC_RESTRICTIONS_NONE` | Town Centers |  |

### PlayerColors

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `IsEnforcing` | bool | `false` |  |  |

### PlayerHandicaps

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `HandicapType` | enum | `AGS_GS_HANDICAP_TYPE_DISABLED` | Handicap |  |
| `FirstSlot` | float | `0.0` |  |  |
| `SecondSlot` | float | `0.0` |  |  |
| `ThirdSlot` | float | `0.0` |  |  |
| `FourthSlot` | float | `0.0` |  |  |
| `FifthSlot` | float | `0.0` |  |  |
| `SixthSlot` | float | `0.0` |  |  |
| `SeventhSlot` | float | `0.0` |  |  |
| `EighthSlot` | float | `0.0` |  |  |
| `MatchUI` | bool | `true` |  | undefined |

### Progression

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `StartingAge` | enum | `AGS_GS_AGE_DARK` | Age |  |
| `EndingAge` | enum | `AGS_GS_AGE_LATE_IMPERIAL` | Age |  |
| `TechnologyAge` | enum | `AGS_GS_AGE_NONE` | Age |  |
| `StartingResources` | enum | `AGS_GS_RESOURCES_NORMAL` | Resources |  |
| `RevealFowOnElimination` | bool | `true` |  |  |

### ReligiousSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Timer` | int | `10` |  |  |
| `ResumableTimer` | bool | `false` |  |  |

### RevealSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Radius` | int | `70` |  | undefined |
| `Duration` | float | `0.25` |  | undefined |
| `IsTestMode` | bool | `false` |  | undefined |
| `IsAdjustingAI` | bool | `true` |  | undefined |
| `EnableUtilities` | bool | `true` |  | undefined |
| `AllowLoserSpectation` | bool | `true` |  | undefined |
| `UsingPrefabStart` | bool | `true` |  | undefined, is related to .rdo file starting conditions |

### ScoreSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Timer` | int | `60` |  |  |
| `ShowPlacement` | bool | `false` |  |  |

### Start Extras

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `ScatteredScout` | bool | `false` |  | defined only for nomad |
| `StartingMonks` | int | `1` |  | undefined |
| `StartingScouts` | int | `1` |  | undefined |
| `StartingSheeps` | int | `1` |  | undefined |
| `StartingTownCenters` | int | `1` |  | undefined |
| `RevealSpawn` | bool | `true` |  | undefined |

### TreatySettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Timer` | int | `0` |  | Duration of treaty period. |
| `ChangeRelations` | bool | `true` |  | undefined, used for testing treaty without diplomacy module. |

### Win Conditions

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Annihilation` | bool | `true` |  | Player loses everything. |
| `Elimination` | bool | `true` |  | Player quits. |
| `Surrender` | bool | `true` |  | Player surrenders. |
| `Conquest` | bool | `true` |  | Player objective conquest. |
| `Regicide` | bool | `false` |  | Player kind defeat. |
| `Religious` | bool | `true` |  | Player control sites. |
| `Wonder` | bool | `true` |  | Player defend wonder. |
| `Score` | bool | `false` |  | Player achieve highest score. |

### WonderSettings

| Key | Type | Default | Enum Group | Description |
|-----|------|---------|------------|-------------|
| `Timer` | int | `15` |  |  |
| `LastStand` | bool | `false` |  |  |
| `ScaleCost` | enum | `AGS_GS_WONDER_SCALE_COST_DISABLED` | Wonder |  |

## CBA / Onslaught-Specific Options

These options are unique to Onslaught mode (not present in standard AGS):

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| `AutoAge` | int | `600` |  |
| `NoSiege` | bool | `false` |  |
| `NoWall` | bool | `false` |  |
| `NoArsenal` | bool | `false` |  |
| `DockHouse` | bool | `false` |  |
| `EliminatedLoseKeep` | bool | `true` |  |
| `Option_Reward_Age` | bool | `false` |  |
| `CBA_Rewards` | string | `"onslaught"` |  |
| `gatherRates` | float | `1.00` |  |
| `MaximumProductionBuildings` | unknown | `AGS_CBA_FIXED_MAX_PRODUCTION_BUILDINGS` |  |
| `MaximumSiegeWorkshop` | unknown | `AGS_CBA_FIXED_MAX_SIEGE_WORKSHOP` |  |
| `SpecialPopulationUI` | bool | `false` |  |

