# Hundred Years' War Campaign — Design Notes

**Campaigns in AoE4:** The Hundred Years' War follows the French reclamation of territory from English occupation across eight missions, emphasizing siege warfare, Joan of Arc's campaigns, and the final expulsion of English forces from France.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| hun_chp1_combat30 | Early tactical engagement | Time-pressure melee objective within 30 seconds |
| hun_chp1_paris | Paris defense | Hold-and-repair against attacker waves |
| hun_chp2_cocherel | Cocherel cavalry ambush | Flanking ambush triggered by enemy approach vector |
| hun_chp2_pontvallain | Pontvallain night pursuit | Rapid-advance pursuit with attrition |
| hun_chp3_orleans | Siege of Orléans relief | Lift siege by destroying enemy artillery; Joan hero survival |
| hun_chp3_patay | Patay cavalry charge | Fast-moving cavalry engagement; lane exploitation |
| hun_chp4_formigny | Formigny cannon engagement | Destroy enemy cannon emplacements under fire |
| hun_chp4_rouen | Rouen final assault | Progressive breach + building-destruction chain |

## Shared patterns

- **Compressed early mission (combat30):** The first mission is a time-compressed scenario that functions as a skill gate rather than a full mission — a technique for immediate engagement before longer narrative missions.
- **Hero-centric narrative:** Joan of Arc appears across Chapter 3 missions as both a named hero unit and a fail condition; her loss ends the mission.
- **Siege relief duality:** Orleans and Patay both start the player in a relief role (reach and break an ongoing siege) then transition to a consolidation phase, reversing the attacker/defender relationship mid-mission.
- **Artillery as primary objective:** Formigny places enemy cannon as the explicit destruction target rather than buildings or armies, prioritizing siege counter-play.
- **Wave defense at Paris:** `hun_chp1_paris` follows a pure wave-defense model with building-repair as the secondary mechanic — the most structurally similar official campaign mission to co-op survival modes.