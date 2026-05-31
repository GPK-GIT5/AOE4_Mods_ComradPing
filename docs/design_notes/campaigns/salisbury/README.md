# The Normans / Salisbury Campaign — Design Notes

**Campaigns in AoE4:** The Normans (Salisbury missions, prefixed `sal_`) is the introductory campaign that teaches foundational mechanics through a Norman knight's story arc, covering six missions across three chapters.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| sal_chp1_rebellion | Opening rebellion — first engagement | Tutorial combat; basic unit commands |
| sal_chp1_valesdun | Valesdun — village pacification | Mixed gather-and-fight economy introduction |
| sal_chp2_dinan | Dinan castle assault — William's alliance | Castle siege; breach and hold |
| sal_chp2_township | Township construction | Economy build-up; production objectives |
| sal_chp2_womanswork | Matilda's village defense | Hold-and-repair while outnumbered; prioritize survival |
| sal_chp3_brokenpromise | Broken Promise — betrayal and escape | Rearguard withdrawal; sequential retreat objectives |

## Shared patterns

- **Training flag on all missions:** All six Salisbury missions carry the `Training` flag in the master index, confirming their role as structured tutorial experiences with scaffolded complexity.
- **Gradual scope expansion:** Chapter 1 introduces pure combat; Chapter 2 adds economy and siege; Chapter 3 introduces narrative reversal (escape/withdrawal) — each chapter adds one new mechanical layer.
- **Hold-under-outnumbered:** Woman's Work places the player in a deliberate disadvantage to teach unit efficiency and building repair as survival tools rather than victory conditions.
- **Withdrawal mechanics:** Broken Promise is one of the only AoE4 campaign missions where the primary objective is retreat rather than capture or destroy — sequential rear-guard positions unlock in series.
- **Economy tutorial isolation:** Township isolates economic objectives from combat to let players focus on production building chains without enemy pressure — a deliberate scaffolding choice.