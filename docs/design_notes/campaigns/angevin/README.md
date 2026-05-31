# Angevin Empire Campaign — Design Notes

**Campaigns in AoE4:** The Normans / Angevin Empire traces the Norman conquest of England and the subsequent Angevin dynasty through eleven missions, emphasizing faction diplomacy, castle sieges, and combined-arms maneuver warfare.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| ang_chp0_intro | Tutorial introduction | Basic command and control orientation |
| ang_chp1_hastings | Hastings 1066 — Norman invasion landing | Formation combat; flanking with cavalry |
| ang_chp1_york | York pacification | Town capture with garrison clearance |
| ang_chp2_bayeux | Norman consolidation in Normandy | Building-construction objective chain |
| ang_chp2_bremule | Cavalry engagement on open ground | Mounted flanking and counter-charge |
| ang_chp2_tinchebray | Fraternal civil war siege | Defender siege mechanics; breach objectives |
| ang_chp3_lincoln | First Lincoln — relief of a besieged garrison | Approach under fire; relieving a hold-objective |
| ang_chp3_wallingford | Prolonged siege and stalemate | Attrition; time-pressure reinforcement window |
| ang_chp4_dover | Coastal fortification defense | Repel waves from multiple approach vectors |
| ang_chp4_lincoln | Second Lincoln — rebel suppression | Multi-front engagement; priority targeting |
| ang_chp4_rochester | Rochester Castle siege | Progressive breach and objective unlock chain |

## Shared patterns

- **Multi-chapter arc:** Missions are grouped into 4 chapters; each chapter escalates tactical complexity (intro → cavalry maneuver → siege → combined arms).
- **Progressive objective unlock:** Many Angevin missions gate later objectives behind completion of earlier ones, creating a linear chain rather than parallel branches.
- **Garrison clearance:** Town and castle interiors require unit-by-unit clearance with fallback garrisoning by defenders — a pattern distinct from open-field campaigns.
- **Relief + hold duality:** Several missions pair an attacker role (relieve a position) with an immediate defender role (hold it once reached), creating a mid-mission pivot.
- **Named character persistence:** Hero units carry across mission phases, creating implicit protect objectives even when no explicit fail condition is stated.