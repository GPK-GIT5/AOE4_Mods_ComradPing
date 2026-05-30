# Data Pipeline Audit Report

Generated: 2026-03-26 21:09:22

## 1. Civ Coverage

| SCAR attribName | SCAR Prefix | Data abbr | Status |
|---|---|---|---|
| abbasid | abb_ | ab | OK |
| abbasid_ha_01 | abb_ha_01_ | ay | OK |
| byzantine | byz_ | by | OK |
| byzantine_ha_mac | byz_ha_mac_ | mac | OK |
| chinese | chi_ | ch | OK |
| chinese_ha_01 | chi_ha_01_ | zx | OK |
| english | eng_ | en | OK |
| french | fre_ | fr | OK |
| french_ha_01 | fre_ha_01_ | je | OK |
| hre | hre_ | hr | OK |
| hre_ha_01 | hre_ha_01_ | od | OK |
| japanese | jpn_ | ja | OK |
| japanese_ha_sen | jpn_ha_sen_ | sen | OK |
| lancaster | lan_ | hl | OK |
| malian | mal_ | ma | OK |
| mongol | mon_ | mo | OK |
| mongol_ha_gol | mon_ha_gol_ | gol | OK |
| ottoman | ott_ | ot | OK |
| rus | rus_ | ru | OK |
| sultanate | sul_ | de | OK |
| sultanate_ha_tug | sul_ha_tug_ | tug | OK |
| templar | tem_ | kt | OK |

All civs matched between SCAR and data sources.

## 2. Production Completeness

**Units with no producer:** 13

| baseId | Name |
|---|---|
| bedouin-skirmisher | Bedouin Skirmisher |
| bedouin-swordsman | Bedouin Swordsman |
| jeanne-darc-blast-cannon | Jeanne d'Arc - Blast Cannon |
| jeanne-darc-hunter | Jeanne d'Arc - Hunter |
| jeanne-darc-knight | Jeanne d'Arc - Knight |
| jeanne-darc-markswoman | Jeanne d'Arc - Markswoman |
| jeanne-darc-mounted-archer | Jeanne d'Arc - Mounted Archer |
| jeanne-darc-peasant | Jeanne d'Arc - Peasant |
| jeanne-darc-woman-at-arms | Jeanne d'Arc - Woman-at-Arms |
| khan | Khan |
| militia | Militia |
| wynguard-footman | Wynguard Footman |
| wynguard-ranger | Wynguard Ranger |

## 3. Upgrade Chain Continuity

**Units with age gaps:** 3

| baseId | Name | Gap |
|---|---|---|
| prelate | Prelate | Age 1 -> 3 |
| earls-guard | Earl's Guard | Age 1 -> 3 |
| healer-elephant | Healer Elephant | Age 2 -> 4 |

## 4. Alias Collisions (Display Name)

No display name collisions found.

## 5. Static Truth Conflicts (behavior-derived, not live runtime)

**Units with conflicts:** 37 / 215

| baseId | Name | Type | Detail |
|---|---|---|---|
| battering-ram | Battering Ram | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| battering-ram | Battering Ram | DPS_OUTLIER | Damage/HP ratio 0.541 (>0.4): 200 dmg / 370 HP |
| explosive-dhow | Explosive Dhow | DPS_OUTLIER | Damage/HP ratio 0.655 (>0.4): 95 dmg / 145 HP |
| fishing-boat | Fishing Boat | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| imam | Imam | TAG_MISSING | Has ranged weapon ((translation not found) (undefined)) but 'ranged' not in classes |
| springald | Springald | TAG_MISSING | Has ranged weapon (Springald) but 'ranged' not in classes |
| xebec | Xebec | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| tower-of-the-sultan | Tower of the Sultan | DPS_OUTLIER | Damage/HP ratio 0.75 (>0.4): 600 dmg / 800 HP |
| carrack | Carrack | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| demolition-ship | Demolition Ship | DPS_OUTLIER | Damage/HP ratio 0.655 (>0.4): 95 dmg / 145 HP |
| dromon | Dromon | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| grenadier | Grenadier | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| baochuan | Baochuan | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| clocktower-battering-ram | Clocktower Battering Ram | DPS_OUTLIER | Damage/HP ratio 0.541 (>0.4): 200 dmg / 370 HP |
| clocktower-springald | Clocktower Springald | TAG_MISSING | Has ranged weapon (Springald) but 'ranged' not in classes |
| explosive-junk | Explosive Junk | DPS_OUTLIER | Damage/HP ratio 0.655 (>0.4): 95 dmg / 145 HP |
| ribauldequin | Ribauldequin | TAG_MISSING | Has ranged weapon (Ribauldequin) but 'ranged' not in classes |
| wynguard-army | Wynguard Army | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| wynguard-footmen | Wynguard Footmen | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| wynguard-raiders | Wynguard Raiders | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| wynguard-rangers | Wynguard Rangers | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| royal-ribauldequin | Royal Ribauldequin | TAG_MISSING | Has ranged weapon (Ribauldequin) but 'ranged' not in classes |
| batu-khan | Batu Khan | TAG_MISSING | Has ranged weapon (Mace) but 'ranged' not in classes |
| earls-guard | Earl's Guard | TAG_MISSING | Has ranged weapon (War Hammer) but 'ranged' not in classes |
| earls-retinue | Earl's Retinue | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| garrison-command | Garrison Command | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| gunpowder-contingent | Gunpowder Contingent | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| atakebune | Atakebune | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| jeanne-darc-peasant | Jeanne d'Arc - Peasant | TAG_MISSING | Has ranged weapon (Knife) but 'ranged' not in classes |
| venetian-galley | Venetian Galley | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| hippodrome-scout | Hippodrome Scout | TAG_MISSING | Has ranged weapon ((translation not found) (undefined)) but 'ranged' not in classes |
| donso | Donso | TAG_MISSING | Has ranged weapon (Spear) but 'ranged' not in classes |
| gilded-villager | Gilded Villager | TAG_MISSING | Has ranged weapon (Knife) but 'ranged' not in classes |
| grand-galley | Grand Galley | TAG_EXTRA | Declared 'ranged' in classes but no ranged weapon found |
| mehter | Mehter | TAG_MISSING | Has ranged weapon (Bow) but 'ranged' not in classes |
| lodya-demolition-ship | Lodya Demolition Ship | DPS_OUTLIER | Damage/HP ratio 0.655 (>0.4): 95 dmg / 145 HP |
| naginata-samurai-levy | Naginata Samurai Levy | TAG_MISSING | Has ranged weapon (Naginata) but 'ranged' not in classes |
| ballista-elephant | Ballista Elephant | TAG_MISSING | Has ranged weapon (Ballista) but 'ranged' not in classes |

## 6. Summary

| Metric | Value |
|---|---|
| Canonical units (baseIds) | 215 |
| Total variations | 981 |
| Producers | 176 |
| Upgrade chains | 215 |
| SCAR civs (AGS_CIV_PREFIXES) | 22 |
| Data civs (civs-index) | 22 |
| Units without producer | 13 |
| Age-tier gaps | 3 |
| Display name collisions | 0 |
| Static truth conflicts | 37 |


