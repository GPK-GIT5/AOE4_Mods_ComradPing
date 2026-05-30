# Gameplay: Age Progression & Landmark Mechanics

## OVERVIEW

Every civilization in AoE4 advances through four ages: **Dark (I) → Feudal (II) → Castle (III) → Imperial (IV)**. Age is tracked as a set of upgrade flags and exposed to SCAR via `Player_GetCurrentAge()`. The core split is between civs that **construct landmarks** to advance and civs that use an **alternative procedure** (wing research, tent upgrades, or commandery selection). Most HA variant civs mirror their base civ's procedure using a different BP suffix.

> **Sources of truth:** `game_data/generated/derived/bp-suffix-catalog.json` (all landmark BPs per civ) · `game_data/extracted/aoe4/scar_dump/scar gameplay/gameplay/` (age-up UI scripts) · `game_data/extracted/blueprints/` (BP IDs)

---

## FUNCTION INDEX

| Function | File | Purpose |
|----------|------|---------|
| `Player_GetCurrentAge` | cardinal.scar | Returns 1–4 based on which age upgrades the player holds |
| `Player_SetCurrentAge` | cardinal.scar | Grants/removes age upgrades to teleport a player to a target age |
| `Player_SetMaximumAge` | cardinal.scar | Locks landmark construction menus to cap age progression |
| `Player_GetMaximumAge` | cardinal.scar | Returns the cap set by `Player_SetMaximumAge` |
| `Player_HasUpgrade` | SCAR API | Checks whether a specific upgrade BP is held |
| `Player_CompleteUpgrade` | SCAR API | Directly grants an upgrade BP to a player |
| `BP_IsUpgradeOfType` | SCAR API | Checks upgrade class — used to detect `"age_up_upgrade"` for Golden Horde |

**Age constants** (cardinal.scar):

| Constant | Value | Meaning |
|----------|-------|---------|
| `AGE_DARK` | 1 | Dark Age |
| `AGE_FEUDAL` | 2 | Feudal Age |
| `AGE_CASTLE` | 3 | Castle Age |
| `AGE_IMPERIAL` | 4 | Imperial Age |

**Age upgrade BPs** used by `Player_HasUpgrade` / `Player_CompleteUpgrade`:

| Upgrade | Age it signals |
|---------|---------------|
| `feudal_age` | Feudal (II) |
| `castle_age` | Castle (III) |
| `imperial_age` | Imperial (IV) |

*Apply upgrades in reverse order* (Imperial → Castle → Feudal) to avoid audio-cue overlap. See `classic_start.scar` for the canonical pattern.

---

## KEY SYSTEMS

### Procedure Taxonomy

| Category | Civs |
|----------|------|
| **Standard landmark** | English, French, HRE, Rus, Delhi Sultanate, Chinese, Malians, Ottomans, Byzantines, Japanese |
| **Wing research** | Abbasid Dynasty, Ayyubids |
| **Core-building upgrade** | Golden Horde (`BP_IsUpgradeOfType("age_up_upgrade")`) |
| **Nomadic landmark** (packable wonders) | Mongols |
| **Commandery selection** | Knights Templar / Order of the Temple |
| **Standard + parallel progression** | Jeanne d'Arc (hero XP), Order of the Dragon (gilded units), House of Lancaster (manor economy), Macedonian Dynasty (silver economy), Sengoku Daimyo (clan alignment), Tughluq Dynasty (governor/fort layer), Zhu Xi's Legacy (dynasty system) |

---

## CIVILIZATION REFERENCE

### Standard Landmark Civs

Each civ offers **two mutually exclusive choices per age transition** (I→II, II→III, III→IV). Constructing either advances the age. Blueprint format: `building_landmark_age{N}_{name}_{suffix}`.

#### English (`eng`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_westminster_hall_eng` | `building_landmark_age1_westminster_abbey_eng` |
| II → III | `building_landmark_age2_westminster_palace_eng` | `building_landmark_age2_white_tower_eng` |
| III → IV | `building_landmark_age3_whitehall_palace_eng` | `building_landmark_age3_windsor_castle_eng` |

#### French (`fre`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_casernes_centrales_fre` | `building_landmark_age1_chamber_of_commerce_fre` |
| II → III | `building_landmark_age2_guild_hall_fre` | `building_landmark_age2_la_chateau_rouge_fre` |
| III → IV | `building_landmark_age3_ecole_de_poudre_a_canon_fre` | `building_landmark_age3_le_grande_university_fre` |

#### Holy Roman Empire (`hre`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_imperial_palace_of_paderborn_hre` | `building_landmark_age1_palantine_chapel_hre` |
| II → III | `building_landmark_age2_bamberg_cathedral_hre` | `building_landmark_age2_nuremberg_castle_hre` |
| III → IV | `building_landmark_age3_eltz_castle_hre` | `building_landmark_age3_hohenzollern_castle_hre` |

#### Rus (`rus`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_golden_gate_vladimir_control_rus` | `building_landmark_age1_novgorod_kremlin_control_rus` |
| II → III | `building_landmark_age2_muscovy_trade_company_control_rus` | `building_landmark_age2_trinity_lavra_control_rus` |
| III → IV | `building_landmark_age3_kremlin_armoury_rus` | `building_landmark_age3_spassakaya_tower_control_rus` |

#### Delhi Sultanate (`sul`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_qutub_minar_control_sul` | `building_landmark_age1_quwwat_ul_islam_control_sul` |
| II → III | `building_landmark_age2_khiji_mosque_control_sul` | `building_landmark_age2_siri_fort_control_sul` |
| III → IV | `building_landmark_age3_bijay_mandal_palace_control_sul` | `building_landmark_age3_madrasa_e_firoz_sul` |

#### Chinese (`chi`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_academy_control_chi` | `building_landmark_age1_gatehouse_control_chi` |
| II → III | `building_landmark_age2_clocktower_control_chi` | `building_landmark_age2_palace_control_chi` |
| III → IV | `building_landmark_age3_great_wall_control_chi` | `building_landmark_age3_spirit_way_control_chi` |

**Special — Dynasty System:** Additional layer tracked in `current_dynasty_ui.scar`. Building both landmarks of the same age triggers a dynasty transition (Tang → Song → Yuan → Ming). Dynasties are stored as upgrade state (`player_dynasty0_chi` … `player_dynasty3_chi`) and unlock unique unit BPs. Landmark Victory destruction check applies to both landmark options.

#### Malians (`mal`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_landmarka_mal` (Saharan Trade Network) | `building_landmark_age1_landmarkb_mal` (Mansa Quarry) |
| II → III | `building_landmark_age2_landmarkc_control_mal` (Grand Fulani Corral) | `building_landmark_age2_landmarkd_control_mal` (Farimba Garrison) |
| III → IV | `building_landmark_age3_landmarke_mal` (Griot Bara) | `building_landmark_age3_landmarkf_mal` (Fort of the Huntress) |

*Note: Malian BPs use generic `landmarka–landmarkf` internal names; real names from `game_data/extracted/aoe4/data/buildings/malians/*.json`.*

#### Ottomans (`ott`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_cifte_minareli_medrese_ott` | `building_landmark_age1_han_caravanserai_ott` |
| II → III | `building_landmark_age2_tophane_armory_ott` | `building_landmark_age2_topkapi_palace_ott` |
| III → IV | `building_landmark_age3_istanbul_observatory_ott` | `building_landmark_age3_kilitbahir_castle_ott` |

*Special: Military Schools continuously produce units for free; age-up compounding this engine is a dominant design intent.*

#### Byzantines (`byz`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_hippodrome_byz` | `building_landmark_age1_winery_byz` |
| II → III | `building_landmark_age2_cistern_byz` | `building_landmark_age2_galata_tower_byz` |
| III → IV | `building_landmark_age3_eastern_merc_house_byz` | `building_landmark_age3_western_merc_house_byz` |

#### Japanese (`jpn`)
| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_shinobi_jpn` | `building_landmark_age1_storehouse_jpn` |
| II → III | `building_landmark_age2_buddhist_jpn` | `building_landmark_age2_shinto_jpn` |
| III → IV | `building_landmark_age3_ozutsu_jpn` | `building_landmark_age3_treasure_jpn` |

---

### Wing-Research Civs

#### Abbasid Dynasty (`abb`)
No landmarks. Age up by researching wing packages on the **House of Wisdom** (`building_house_of_wisdom_control_abb`). Each age requires selecting one of four wing types:

| Wing | Upgrade BPs (example — Feudal tier) |
|------|-------------------------------------|
| Culture | `UPGRADE_ADD_CULTURE_WING_FEUDAL` |
| Economy | `UPGRADE_ADD_ECONOMY_WING_FEUDAL` |
| Military | `UPGRADE_ADD_MILITARY_WING_FEUDAL` |
| Trade | `UPGRADE_ADD_TRADE_WING_FEUDAL` |

Suffixes: `_FEUDAL`, `_CASTLE`, `_IMPERIAL`. Full IDs in `game_data/extracted/blueprints/abbasid-blueprints.md`. Up to four wings can be completed in total; each adds scaling benefits. `cardinal.scar` has special handling for Abbasid wing upgrades (ages via research, not landmark construction).

#### Ayyubids (`abbasid_ha_01`)
Same House of Wisdom wing system using `building_house_of_wisdom_control_abb_ha_01`. Wing upgrade BPs follow the `_abb_ha_01` suffix pattern. Design emphasis: each wing package delivers an immediate strategic bundle (units, economy, tech) as a tempo decision vs. long-term scaling.

---

### Nomadic / Packable Landmark Civ

#### Mongols (`mon`)
Age-up landmarks use the **`building_wonder`** class (not `building_landmark`). All structures are packable and redeployable. Two choices per transition:

| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_wonder_age1_deer_stones_moving_mon` | `building_wonder_age1_kurultai_moving_mon` |
| II → III | `building_wonder_age2_karakorum_moving_mon` | `building_wonder_age2_khara_khoto_moving_mon` |
| III → IV | `building_wonder_age3_khanbaliq_moving_mon` | `building_wonder_age3_stupa_moving_mon` |

> **SCAR note:** Mongol age-up wonders match `BP_IsEntityOfType("wonder")`, **not** `"landmark"`. `Player_SetMaximumAge` still locks their construction menus. No keep, mining camp, lumber camp, mill, stone walls, or palisades.

---

### Core-Building Upgrade Civ

#### Golden Horde (`mongol_ha_gol`)
Age-up is performed via upgrades researched on the **Golden Tent** (`building_landmark_golden_tent_mon_ha_gol`) — a single centralized building. The age-up event is detected in `event_cues.scar` via:

```lua
player.raceName == "mongol_ha_gol" and BP_IsUpgradeOfType(context.upgrade, "age_up_upgrade")
```

There are no per-age landmark construction choices. `landmark_building = false` in functional taxonomy.

---

### Commandery-Selection Civ

#### Knights Templar / Order of the Temple (`templar`)
No traditional landmarks or wing research. Age progression is via **Templar Headquarters** research with **Commandery selection**. Each age bracket offers three commanderies that grant special units as rewards:

| Age | Commanderies |
|-----|-------------|
| Feudal (II) | Knight Hospitaller, Kingdom of France, Principality of Antioch |
| Castle (III) | Angevin Empire, Republic of Genoa, Kingdom of Castile |
| Imperial (IV) | Kingdom of Poland, Teutonic Knights, Republic of Venice |

Unit roster and costs managed in `templar_age_up_ui.scar`. Venice commandery grants two additional unit types (Venetian Galley, Venetian Trader). `landmark_building = false`.

---

### HA Variant Civs

All HA variants follow their base civ's age **procedure** using a distinct BP suffix. Exceptions are noted.

| Civ | Suffix | Base Procedure | Notes |
|-----|--------|---------------|-------|
| Jeanne d'Arc (`french_ha_01`) | `_fre_ha_01` | Standard landmarks | Same 6 landmark BP names as French + suffix. Parallel hero-XP system. |
| Order of the Dragon (`hre_ha_01`) | `_hre_ha_01` | Standard landmarks | Same 6 landmark BPs as HRE + suffix. Parallel gilded-unit system. |
| Zhu Xi's Legacy (`chinese_ha_01`) | `_chi_ha_01` | Standard landmarks + dynasty | Distinct landmark BPs; same dynasty-layer mechanics as base Chinese. |
| Macedonian Dynasty (`byzantine_ha_mac`) | `_byz_ha_mac` | Standard landmarks | Same 6 landmark BPs as Byzantines + suffix. Parallel silver-economy system. |
| Sengoku Daimyo (`japanese_ha_sen`) | `_jpn_ha_sen` | Standard landmarks | Distinct DLC landmark BPs (Ryokan, Koka Township, Sake Brewery, etc.). Parallel clan-alignment. |
| Tughluq Dynasty (`sultanate_ha_tug`) | `_sul_ha_tug` | Standard landmarks | Same 6 landmark BPs as Delhi + suffix (DLC display names differ). Parallel governor/fort layer. |
| Ayyubids (`abbasid_ha_01`) | `_abb_ha_01` | Wing research | Same House of Wisdom system + suffix. See Wing-Research section. |
| Golden Horde (`mongol_ha_gol`) | `_mon_ha_gol` | Core-building upgrade | Golden Tent, not landmarks. See Core-Building section. |

**Zhu Xi's distinct landmark BPs:**

| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_meditation_gardens_control_chi_ha_01` | `building_landmark_age1_prefecture_chi_ha_01` |
| II → III | `building_landmark_age2_shaolin_temple_control_chi_ha_01` | `building_landmark_age2_white_deer_grotto_control_chi_ha_01` |
| III → IV | `building_landmark_age3_library_chi_ha_01` | `building_landmark_age3_temple_of_the_sun_control_chi_ha_01` |

**Sengoku distinct landmark BPs:**

| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_ryokan_jpn_ha_sen` | `building_landmark_age1_shinobi_jpn_ha_sen` |
| II → III | `building_landmark_age2_brewery_jpn_ha_sen` | `building_landmark_age2_buddhist_jpn_ha_sen` |
| III → IV | `building_landmark_age3_crow_jpn_ha_sen` | `building_landmark_age3_statue_jpn_ha_sen` |

---

### DLC Civ: House of Lancaster (`lan`)
Standard landmark procedure with distinct BPs (not English-derived):

| Transition | Option A | Option B |
|-----------|----------|----------|
| I → II | `building_landmark_age1_lancastercastle_lan` (Lancaster Castle) | `building_landmark_age1_abbey_lan` (Abbey of Kings) |
| II → III | `building_landmark_age2_white_tower_lan` (The White Tower) | `building_landmark_age2_kingscollege_lan` (King's College) |
| III → IV | `building_landmark_age3_wynguard_lan` (Wynguard Palace) | `building_landmark_age3_berkshire_lan` (Berkshire Palace) |

---

## SCRIPTING REFERENCE

### Applying or Checking Age in SCAR

```lua
-- Read
local age = Player_GetCurrentAge(player.id)  -- 1 (Dark) to 4 (Imperial)

-- Write (force a player to Castle Age)
Player_SetCurrentAge(player.id, AGE_CASTLE)

-- Cap (prevent advancing past Feudal)
Player_SetMaximumAge(player.id, AGE_FEUDAL)

-- Low-level upgrade check
if Player_HasUpgrade(player.id, BP_GetUpgradeBlueprint("castle_age")) then ...

-- Detecting Abbasid age-up (wing research event)
-- Age is granted as a side effect of wing research; listen via OnPlayerUpgrade or similar

-- Detecting Golden Horde age-up (tent upgrade event)
if player.raceName == "mongol_ha_gol" and BP_IsUpgradeOfType(context.upgrade, "age_up_upgrade") then ...
```

### `Player_SetMaximumAge` Behavior
- Removes construction menus for all landmarks beyond the capped age.
- Abbasid: also hides higher-tier wing research options.
- Mongols: hides higher-tier packable wonder options.
- Does **not** retroactively strip an upgrade already granted.

### Scenario Age Locks (from `coop_4_taiga`)
Use `Player_SetUpgradeAvailability` + `ITEM_LOCKED` to block specific wing options without locking the whole age system:

```lua
Player_SetUpgradeAvailability(player.id,
    BP_GetUpgradeBlueprint("UPGRADE_ADD_CULTURE_WING_FEUDAL"), ITEM_LOCKED)
```

---

## CROSS-REFERENCES

| Topic | Doc |
|-------|-----|
| Starting age initialization | `docs/game_systems/gameplay/startconditions.md` — Classic Start age chain |
| Landmark victory tracking | `Gamemodes/Onslaught/assets/scar/observerui/uidatacontext/updateui_landmarkvictory.scar` |
| Chinese dynasty state model | `game_data/extracted/aoe4/scar_dump/scar gameplay/gameplay/chi/current_dynasty_ui.scar` |
| Templar commandery UI data | `game_data/extracted/aoe4/scar_dump/scar gameplay/gameplay/templar/templar_age_up_ui.scar` |
| Abbasid wing upgrade BPs | `game_data/extracted/blueprints/abbasid-blueprints.md` |
| All landmark BPs per civ | `game_data/generated/derived/bp-suffix-catalog.json` |
| DLC landmark display names | `game_data/extracted/aoe4/data/dlc_bp_inventory.txt` |
| Malian landmark real names | `game_data/extracted/aoe4/data/buildings/malians/*.json` |
| AGS starting-age upgrades | `Gamemodes/Dependencies/Advanced Game Settings/assets/scar/gameplay/ags_starting_age.scar` |
| UI age model (`scarModel.Age`) | `docs/game_systems/ui/UI_SetPlayerDataContext_FieldDiscovery.md` |
