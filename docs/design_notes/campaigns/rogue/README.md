# Rogue Mode — Design Notes

**Campaigns in AoE4:** Rogue Mode is AoE4's standalone roguelike survival game mode. Players defend a centrally-placed Wonder against escalating enemy waves while exploring maps for Points of Interest, resources, and allied units. Four maps share common infrastructure; two additional scripts serve as debug harnesses.

## Maps

| Map | Theme | Distinguishing mechanic |
|---|---|---|
| Coastline | Byzantine coastal / naval | Naval pirate raids alongside land waves; naval POI rewards; warship and galleass unlocks |
| Forest | Forest / HRE bandit | Bandit camp conversion; no naval units; wolf spawning; HRE-themed side bases |
| Japanese Daimyo | Japanese feudal / shinobi | Day/night cycle; abandoned-village shinobi trap; civ-specific unit composition |
| Mongol Steppe | Cavalry-heavy steppe | Horse archer economy for raiders; patrol-army guard network; cavalry-weighted wave composition |

## Shared infrastructure

All four maps use the same core Rogue framework:

- **Lane-based wave delivery:** Each map defines 2–4 named lanes with 3 sublanes each; waves are assigned to lanes by the scheduler based on priority, timing, and locks.
- **Combinatorial wave composition:** Wave templates are auto-generated from unit type combinatorics, then weighted by age, lane, and resource value. No hand-authored wave list.
- **Polynomial difficulty scaling:** A 7–8 tier difficulty system (Bronze through Conqueror) drives resource budgets, unit counts, and timing via a polynomial equation rather than discrete tables.
- **Medal progression:** Bronze / Silver / Gold / Conqueror medals are awarded at time and kill thresholds; Conqueror mode adds environmental stressors (halved resources, roaming enemies, super rams, long-range trebuchet threats).
- **POI reward system:** 30+ Point of Interest types across two tiers deliver civ-specific rewards (champion units, resource packs, allied armies, upgrades). POIs spawn at Nook markers chosen by the objective system.
- **Endless Mode:** After the Gold medal threshold, rounds repeat infinitely with accelerating intervals.

## UGC template

A separate UGC template map (`ugc_map.scar`) demonstrates a simplified MissionOMatic recipe-based mission — two-player setup, roving armies, sequential capture/destroy objectives — without Rogue mode mechanics. Intended as a starting point for user-generated content.


