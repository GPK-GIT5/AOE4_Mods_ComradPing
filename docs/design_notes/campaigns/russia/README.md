# Rise of Moscow Campaign — Design Notes

**Campaigns in AoE4:** Rise of Moscow (internally prefixed `gdm_`) traces the emergence of the Russian state from the Mongol tribute period through the unification of the northern principalities across eight missions.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| gdm_chp1_moscow | Early Moscow — survive Mongol tribute demands | Tribute delivery against a timer; defend against reprisal |
| gdm_chp2_kulikovo | Kulikovo Field — first major Russian victory over the Mongols | Flanking ambush; forest concealment mechanic |
| gdm_chp2_tribute | Extended tribute arc | Recurring resource-delivery objectives with escalating demand |
| gdm_chp3_moscow | Moscow consolidation — city growth phase | Production build-up under diplomatic pressure |
| gdm_chp3_novgorod | Novgorod campaign — northern trade republic annexation | City capture with sympathetic faction management |
| gdm_chp3_ugra | Great Stand on the Ugra River — confrontation without battle | Defensive hold mechanic; objective resolves without combat |
| gdm_chp4_kazan | Kazan Khanate campaign | Combined arms siege; artillery-forward assault |
| gdm_chp4_smolensk | Smolensk annexation — western expansion | Multi-district capture; political conversion |

## Shared patterns

- **Tribute/resource delivery arc:** Two missions use resource delivery as the primary mechanic — a timer-gated collection objective with fail-on-miss. This is the most explicit economic pressure loop in any AoE4 campaign.
- **Diplomatic restraint objective:** Ugra is unusual in that the primary win condition is *not* destroying the enemy; the player must hold the river line long enough for the Mongols to withdraw, rewarding patience over aggression.
- **Forest concealment:** Kulikovo's ambush relies on units positioned in forest terrain being invisible to the approaching enemy — a map-geometry-driven encounter design rather than scripted invisibility.
- **Faction sympathy:** Novgorod introduces a neutral faction that can be swayed by player actions, providing a mini-diplomacy layer atop the military objectives.
- **Production build-up under pressure:** Moscow Ch.3 extends the economic arc from Ch.1 into a city-building phase where construction objectives run alongside external threat monitoring.