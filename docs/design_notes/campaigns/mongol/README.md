# Mongol Empire Campaign — Design Notes

**Campaigns in AoE4:** The Mongol Empire campaign covers Genghis Khan and his successors' westward expansion across nine missions, emphasizing mobile cavalry warfare, strategic encirclement, and siege of fortified cities.

## Missions

| Mission | Setting | Primary mechanic |
|---|---|---|
| mon_chp1_kalka_river | Kalka River ambush — initial Mongol raid into Kievan Rus | Cavalry flanking; lure-and-destroy |
| mon_chp1_juyong | Juyong Gate — breach of the Great Wall | Siege escalation; tower destruction chain |
| mon_chp1_zhongdu | Zhongdu siege — fall of the Jin capital | Progressive breach of concentric walls |
| mon_chp2_kiev | Kiev sack | Multi-district capture sequence |
| mon_chp2_liegnitz | Liegnitz — engagement with Polish/German coalition | Feigned retreat; cavalry encirclement |
| mon_chp2_mohi | Mohi — river crossing ambush | Flank approach; bridge seizure |
| mon_chp3_lumen_shan | Lumen Shan — mountain fortification assault | Altitude-advantage siege; supply line mechanics |
| mon_chp3_xiangyang_1267 | Xiangyang 1267 — opening of the siege | Blockade establishment; supply interdiction |
| mon_chp3_xiangyang_1273 | Xiangyang 1273 — final assault after six years | Full siege resolution; trebuchet bombardment |

## Shared patterns

- **Cavalry-first design:** Mongol missions disproportionately reward speed, flanking, and hit-and-run over static defense — missions are designed around mobile unit compositions.
- **Feigned retreat mechanic:** Liegnitz explicitly scribes an enemy that retreats to draw the player army into an encirclement — a rare offensive-AI ambush pattern.
- **Multi-stage siege arc:** The two Xiangyang missions form a connected arc across a six-year in-game timeline, with the first establishing a siege state that the second resolves.
- **Progressive breach:** Juyong and Zhongdu both use successive wall/district layers, each requiring destruction to unlock the next combat zone.
- **Supply/blockade mechanic:** Lumen Shan and Xiangyang 1267 introduce supply-line objectives where the player must interdict enemy resupply rather than destroy a single target.