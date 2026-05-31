# Abbasid Dynasty Campaign — Design Notes

**Campaigns in AoE4:** Abbasid Dynasty follows the Abbasid Caliphate's military campaigns across the Crusades era, concluding with the Mongol invasions. Nine missions span naval warfare, tug-of-war control mechanics, resource denial, and siege escalation.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| Bonus | Crusader territory — destroy rival landmarks and subdue Holy Orders | Dual win conditions; capture-and-merge Templar/Teutonic/Hospitaller keeps |
| abb_m1_tyre | Coastal city defense against Frankish siege escalation | Enemy resource accumulation threshold → assault countdown; "The Beast" siege ram boss |
| abb_m2_egypt | Alexandria control-point struggle | Tug-of-war balance score; lose at zero, win at max — reinforcement wave timer |
| abb_m3_redsea | Naval tutorial + gold accumulation with allies | Staged naval objectives (fishing → trade → combat); accumulated resource threshold win |
| abb_m4_hattin | Ambush and flanking engagement | Terrain-gated ambush squads; escort survival |
| abb_m5_mansurah | Urban canal warfare | Position-hold with timed reinforcements; leader hero survival |
| abb_m6_aynjalut | Open-field Mongol confrontation | Enemy wave cycling; patrol army mechanics |
| abb_m7_acre | Siege of a fortified port | Building-destruction primary; dock optional objective |
| abb_m8_cyprus | Island naval assault | Combined arms — transport landing + land siege |

## Shared patterns

- **Dual win condition:** Bonus mission requires both landmark destruction and keep subdual; each arm completes independently and both must finish to trigger victory.
- **Resource-threshold assault:** `abb_m1_tyre` models an enemy that accumulates resources toward a garrison/construction threshold, then triggers a timed assault phase.
- **Tug-of-war balance:** `abb_m2_egypt` tracks a signed balance score; constant pressure from both sides makes momentum management the core challenge.
- **Leader survival:** Multiple missions track hero-unit liveness as an implicit or explicit fail condition.
- **Mercenary unlock through optional objective:** Completing the trade route optional in the Bonus mission unlocks a reinforcement panel — pattern for expanding player capability mid-mission.