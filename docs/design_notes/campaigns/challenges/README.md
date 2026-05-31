# Art of War Challenges — Design Notes

**Campaigns in AoE4:** Art of War Challenges are thirteen standalone tutorial/challenge missions covering economic, military, and civilization-specific training scenarios. Each mission ends with a Bronze / Silver / Gold medal benchmark.

## Missions

| Mission | Focus | Primary mechanic |
|---|---|---|
| challenge_basiccombat | Melee and ranged unit engagement | Unit-counter timing; formation basics |
| challenge_advancedcombat | Mixed-arms engagement with reinforcements | Micro-intensive flanking and retreat patterns |
| challenge_earlyeconomy | Rapid villager-to-resource pipeline | Resource-collection rate targets within time limits |
| challenge_lateeconomy | Age-III/IV economy scaling | Production building counts; resource throughput |
| challenge_earlysiege | Siege engine deployment and ram usage | Ram positioning; anti-siege defense |
| challenge_latesiege | Counter-siege and cannon defense | Outrange-and-destroy; priority target queuing |
| challenge_agincourt | Replicate historical English archer dominance | Position hold; ranged-fire-lane management |
| challenge_montgisard | Saladin cavalry engagement recreation | Cavalry speed and hit-and-run |
| challenge_towton | Snowstorm-penalized ranged combat | Weather modifier; unit positioning under penalty |
| challenge_safed | Crusader castle assault | Breach mechanics; hero support |
| challenge_malian | Malian civilization introduction | Civ-specific mechanics orientation |
| challenge_ottoman | Ottoman civilization introduction | Janissary and bombard combined-arms tutorial |
| challenge_walldefense | Tower and wall defense against assault waves | Economy-while-defending; upgrade pacing |

## Shared patterns

- **Medal benchmarking:** All challenges measure performance against a Bronze/Silver/Gold threshold using the Art of War timer and objective scoring — the same mechanism used by MissionOMatic's `missionomatic_artofwar.scar`.
- **Fail-on-timeout:** Time pressure is the primary failure mode; health and survival are secondary in most missions.
- **Minimal narrative:** No heroes, no diplomacy arcs — pure skill evaluation in a constrained scenario envelope.
- **Training flag on modules:** All Salisbury and Challenges missions tag modules with the `Training` flag in the master index, distinguishing them from narrative campaign missions.
- **Civ-gated content:** Malian and Ottoman challenges expose civilization-specific mechanics not present in standard campaign missions.