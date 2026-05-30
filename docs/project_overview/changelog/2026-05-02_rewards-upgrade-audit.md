# Onslaught Reward Upgrade Audit

- Date: 2026-05-02
- Rewards file: Gamemodes/Onslaught/assets/scar/rewards/cba_rewards_onslaught.scar
- AGS map file: Gamemodes/Onslaught/assets/scar/AGS/CBA/helpers/ags_blueprints.scar
- Canonical inventory: game_data/generated/canonical/upgrade-inventory.json
- Civ tables audited: 22
- AGS_UP constants used: 14
- upgradeBP entries used: 54
- Duplicate threshold collisions: 0
- Failures: 0

## AGS_UP Mapping Check

| Constant | Key | Mapped Civ Tables | Status | Notes |
|---|---|---:|---|---|
| AGS_UP_A_MELEE_I | melee1_attack | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_A_MELEE_II | melee2_attack | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_A_MELEE_III | melee3_attack | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_A_RANGED_I | ranged1_attack | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_A_RANGED_II | ranged2_attack | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_BARDING | barding | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_D_MELEE_I | melee1_defense | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_D_RANGED_II | ranged2_defense | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_D_RANGED_III | ranged3_defense | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_GRAPERED_LANCE | grapered_lance | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_MANATARMS_ELITE | maa_elite_tactics | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_MILITARY_ACADEMY | military_academy | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_SIEGE_ADJUSTABLE_CROSSBAR | adjustable_crossbar | 22 | PASS | Mapped for all configured reward civs |
| AGS_UP_SPEARMAN_ELITE | spear_elite_tactics | 22 | PASS | Mapped for all configured reward civs |

## upgradeBP Existence Check

| upgradeBP | Civ Count | Status | Notes |
|---|---:|---|---|
| upgrade_age3_war_elephant_elite_sul | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_archer_poison_arrow_mal | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_armor_clad_eng | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_building_fire_armor_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_camel_archer_comp_bow_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_camel_armor_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_camel_speed_boost_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_barding_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_bloodline_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_cantled_saddle_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_chivalry_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_grapered_lance_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_grapered_lance_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_hp_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_cavalry_melee_damage_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_gothic_plate_armour_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_gunpowder_damage_chi | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_improved_siege_engineers_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_improved_swords_sul | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_infantry_marching_drills_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_landmark_fire_siege_armor_sul | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_landmark_force_march_sul | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_landmark_keep_defense_sul | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_landsknecht_charge_drills_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_longbow_make_camp_eng | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_man_at_arms_maces_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_man_at_arms_two_handed_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_manatarms_aoe_chi | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_manatarms_battle_hardened_chi | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_manatarms_elite_army_tactics_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_melee_damage_i_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_mil_camel_archers_improved_weapon_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_mil_camel_support_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_mil_mameluke_shields_abb | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_crossbow_cranequin_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_crossbow_drills_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_crossbow_stirrups_fre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_janissary_guns_ott | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_longbow_arrow_volley_eng | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_ranged_palings_eng | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_reinforced_defenses_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_reload_drills_chi | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_riveted_chain_armour_hre | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_siege_crew_training_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_siege_fined_tuned_guns_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_siege_improvements_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_sofa_armor_mal | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_sofa_farima_leadership_mal | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_spearman_elite_spear_tactics_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_springald_range_rus | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_stealth_healing_mal | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_tech_military_academy_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_tech_university_biology_improved_mon | 1 | PASS | Found in canonical upgrade-inventory attribName |
| upgrade_trebuchet_aoe_eng | 1 | PASS | Found in canonical upgrade-inventory attribName |

## Duplicate Threshold Check

- PASS: No duplicate civ+threshold reward keys detected.