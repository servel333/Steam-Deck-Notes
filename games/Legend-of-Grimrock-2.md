
- [grimrock.net Scripting Reference](http://www.grimrock.net/modding/scripting-reference/) ([Local copy](./Legend-of-Grimrock-2/Scripting-Reference.md))

# Console commands quick reference

## Heal party

```lua
party.party:heal()
party:heal()
```

## How Get Champion works

```lua
-- @param (number) $ChampionIndex  The index of the champion in the part. 1 to 4 (top left, top right, bottom left, bottom right, respectively).
-- @param (number) $amount
-- party.party:getChampion( $ChampionIndex )
party.party:getChampion(1)  // Top Left champion
party.party:getChampion(2)  // Top Right champion
party.party:getChampion(3)  // Bottom Left champion
party.party:getChampion(4)  // Bottom Right champion

-- Example with
party.party:getChampion(1):addSkillPoints(1)
```

## Add skill points to one of your champions.

Note, as long as you have unspent skill points, your champion portraits will show "level up". If you add more skill points than you can spend, this message will be visible forever.

```lua
-- @param (number) $ChampionIndex  The index of the champion in the part. 1 to 4.
-- @param (number) $amount
-- party.party:getChampion( $ChampionIndex ):consumeFood( $amount )
party.party:getChampion(1):addSkillPoints(1)  // Add one skill point to the top left champion.
party.party:getChampion(1):addSkillPoints(-1) // May remove a skill point
```

```lua
party.party:getChampion(1):addSkillPoints(200)
party.party:getChampion(2):addSkillPoints(200)
party.party:getChampion(3):addSkillPoints(200)
party.party:getChampion(4):addSkillPoints(200)
```

## set count of held item

```lua
getMouseItem():setStackSize(10)
```

## Fill hunger

```lua
-- @param (number) $amount
-- party.party:getChampion( $ChampionIndex ):consumeFood( $amount )

party.party:getChampion(1):consumeFood(100)
```

## Gain Experience

```lua
-- party.party:getChampion( $ChampionIndex ):gainExp( $xp )

party.party:getChampion(1):gainExp(1000)
```

## Modify a champion stat

```lua
party.party:getChampion(1):modifyBaseStat("strength",  1)
party.party:getChampion(1):modifyBaseStat("dexterity", 1)
party.party:getChampion(1):modifyBaseStat("vitality",  1)
party.party:getChampion(1):modifyBaseStat("willpower", 1)
```

## Create an item on the floor in front of you

Make sure the space in front of you is empty.

```lua
spawn "wooden_box"
```

## Get the name of an item held in the mouse

You can then use this name to `spawn` an item.

```lua
print( getMouseItem().go.name )
```

# Item List

- [grimrock.net "Item listing for Console"](http://www.grimrock.net/forum/viewtopic.php?t=1991)

```lua
spawn("wooden_box")
spawn "wooden_box"
```

| Category         | Name                        |
| ---------------- | --------------------------- |
| container        | `sack`                      |
| container        | `wooden_box`                |
| crafting         | `mortar`                    |
| decoration       | `floor_corpse`              |
| dungeon elements | `alcove`                    |
| dungeon elements | `altar`                     |
| dungeon elements | `barrel_crate_block`        |
| dungeon elements | `blocker`                   |
| dungeon elements | `catacomb_empty`            |
| dungeon elements | `catacomb_skeleton_down`    |
| dungeon elements | `catacomb_skeleton_up`      |
| dungeon elements | `cave_in_ceiling`           |
| dungeon elements | `cave_in`                   |
| dungeon elements | `ceiling_shaft`             |
| dungeon elements | `counter`                   |
| dungeon elements | `daemon_head_eye_slots`     |
| dungeon elements | `daemon_head`               |
| dungeon elements | `dragon_statue`             |
| dungeon elements | `dungeon_ceiling_root_1`    |
| dungeon elements | `dungeon_ceiling_root_2`    |
| dungeon elements | `dungeon_ceiling_root_3`    |
| dungeon elements | `dungeon_ivy_1`             |
| dungeon elements | `dungeon_ivy_2`             |
| dungeon elements | `dungeon_spider_web_1`      |
| dungeon elements | `dungeon_spider_web_2`      |
| dungeon elements | `dungeon_spider_web_3`      |
| dungeon elements | `dungeon_spider_web_4`      |
| dungeon elements | `dungeon_wall_dirt_1`       |
| dungeon elements | `dungeon_wall_dirt_2`       |
| dungeon elements | `eye_socket_left`           |
| dungeon elements | `eye_socket_right`          |
| dungeon elements | `floor_corpse`              |
| dungeon elements | `floor_dirt`                |
| dungeon elements | `floor_drainage`            |
| dungeon elements | `fountain`                  |
| dungeon elements | `fx`                        |
| dungeon elements | `gladiator_statue_axe`      |
| dungeon elements | `gladiator_statue_flail`    |
| dungeon elements | `gladiator_statue_spear`    |
| dungeon elements | `gladiator_statue_sword`    |
| dungeon elements | `gobelin`                   |
| dungeon elements | `goromorg_fourway`          |
| dungeon elements | `goromorg_statue`           |
| dungeon elements | `healing_crystal`           |
| dungeon elements | `iron_gate`                 |
| dungeon elements | `lever`                     |
| dungeon elements | `lock_gear`                 |
| dungeon elements | `lock_golden`               |
| dungeon elements | `lock_ornate`               |
| dungeon elements | `lock_prison`               |
| dungeon elements | `lock_round`                |
| dungeon elements | `lock`                      |
| dungeon elements | `map_marker`                |
| dungeon elements | `metal_door`                |
| dungeon elements | `metal_junk_block`          |
| dungeon elements | `mouth_socket`              |
| dungeon elements | `pillar`                    |
| dungeon elements | `pit`                       |
| dungeon elements | `portcullis`                |
| dungeon elements | `pressure_plate_hidden`     |
| dungeon elements | `pressure_plate`            |
| dungeon elements | `prison_bench`              |
| dungeon elements | `prison_ceiling_lamp`       |
| dungeon elements | `prison_door`               |
| dungeon elements | `prison_wall_1`             |
| dungeon elements | `prison_wall_2`             |
| dungeon elements | `prison_wall_3`             |
| dungeon elements | `prison_wall_4`             |
| dungeon elements | `prison_wall_5`             |
| dungeon elements | `prison_wall_6`             |
| dungeon elements | `receptor_hidden`           |
| dungeon elements | `receptor`                  |
| dungeon elements | `secret_button_large`       |
| dungeon elements | `secret_button_small`       |
| dungeon elements | `secret_button_tiny`        |
| dungeon elements | `secret`                    |
| dungeon elements | `sliding_wall`              |
| dungeon elements | `spawner`                   |
| dungeon elements | `spider_eggs`               |
| dungeon elements | `stairs_down`               |
| dungeon elements | `stairs_up`                 |
| dungeon elements | `stone_seal`                |
| dungeon elements | `teleporter`                |
| dungeon elements | `temple_ceiling_lamp`       |
| dungeon elements | `temple_door`               |
| dungeon elements | `temple_glass_wall_1`       |
| dungeon elements | `temple_glass_wall_2`       |
| dungeon elements | `temple_glass_wall_3`       |
| dungeon elements | `temple_mosaic_wall_1`      |
| dungeon elements | `temple_mosaic_wall_2`      |
| dungeon elements | `timer`                     |
| dungeon elements | `torch_holder`              |
| dungeon elements | `wall_button`               |
| dungeon elements | `wall_drainage`             |
| dungeon elements | `wall_grating`              |
| dungeon elements | `wall_moss`                 |
| dungeon elements | `wall_painted`              |
| dungeon elements | `wall_text_long`            |
| dungeon elements | `wall_text`                 |
| dungeon elements | `wooden_gate_locked`        |
| dungeon elements | `wooden_gate`               |
| food             | `baked_maggot`              |
| food             | `boiled_beetle`             |
| food             | `grim_cap`                  |
| food             | `herder_cap`                |
| food             | `ice_lizard_steak`          |
| food             | `mole_jerky`                |
| food             | `pitroot_bread`             |
| food             | `rat_shank`                 |
| food             | `snail_slice`               |
| hand - casting   | `golden_orb`                |
| hand - casting   | `lightning_rod`             |
| hand - casting   | `magic_orb`                 |
| hand - casting   | `shaman_staff`              |
| hand - casting   | `whitewood_wand`            |
| hand - close     | `assassin_dagger`           |
| hand - close     | `battle_axe`                |
| hand - close     | `crossbow`                  |
| hand - close     | `cudgel`                    |
| hand - close     | `dagger`                    |
| hand - close     | `dismantler`                |
| hand - close     | `fire_blade`                |
| hand - close     | `fist_dagger`               |
| hand - close     | `flail`                     |
| hand - close     | `icefall_hammer`            |
| hand - close     | `knife`                     |
| hand - close     | `knoffer`                   |
| hand - close     | `long_sword`                |
| hand - close     | `machete`                   |
| hand - close     | `nex_sword`                 |
| hand - close     | `power_weapon`              |
| hand - close     | `short_bow`                 |
| hand - close     | `shuriken`                  |
| hand - close     | `throwing_knife`            |
| hand - close     | `venom_edge`                |
| hand - close     | `warhammer`                 |
| hand - ranged    | `arrow`                     |
| hand - ranged    | `cold_arrow`                |
| hand - ranged    | `cold_quarrel`              |
| hand - ranged    | `fire_arrow`                |
| hand - ranged    | `fire_quarrel`              |
| hand - ranged    | `poison_arrow`              |
| hand - ranged    | `poison_quarrel`            |
| hand - ranged    | `quarrel`                   |
| hand - ranged    | `shock_arrow`               |
| hand - ranged    | `shock_quarrel`             |
| hand - ranged    | `sling`                     |
| hand - shield    | `heavy_shield`              |
| hand - thrown    | `fire_bomb`                 |
| hand - thrown    | `frost_bomb`                |
| hand - thrown    | `poison_bomb`               |
| hand - thrown    | `rock`                      |
| hand - thrown    | `shock_bomb`                |
| healing          | `healing_crystal`           |
| herb             | `blooddrop_blossom`         |
| herb             | `cave_nettle`               |
| herb             | `milkreed`                  |
| herb             | `tar_bead`                  |
| keys             | `brass_key`                 |
| keys             | `gold_key`                  |
| keys             | `iron_key`                  |
| keys             | `ornate_key`                |
| keys             | `prison_key`                |
| keys             | `round_key`                 |
| misc             | `blue_gem`                  |
| misc             | `flask`                     |
| misc             | `golden_figure`             |
| misc             | `green_gem`                 |
| misc             | `skull`                     |
| monster          | `crab`                      |
| monster          | `crowern`                   |
| monster          | `cube`                      |
| monster          | `goromorg`                  |
| monster          | `green_slime`               |
| monster          | `herder_big`                |
| monster          | `herder_small`              |
| monster          | `herder_swarm`              |
| monster          | `herder`                    |
| monster          | `ice_lizard`                |
| monster          | `ogre`                      |
| monster          | `scavenger_swarm`           |
| monster          | `scavenger`                 |
| monster          | `shrakk_torr`               |
| monster          | `skeleton_archer_patrol`    |
| monster          | `skeleton_archer`           |
| monster          | `skeleton_patrol`           |
| monster          | `skeleton_warrior`          |
| monster          | `skeleton`                  |
| monster          | `snail`                     |
| monster          | `spider_boss`               |
| monster          | `spider`                    |
| monster          | `tentacles`                 |
| monster          | `uggardian`                 |
| monster          | `warden`                    |
| monster          | `wyvern`                    |
| potion           | `potion_cure_disease`       |
| potion           | `potion_energy`             |
| potion           | `potion_healing`            |
| scroll           | `scroll_darkness`           |
| scroll           | `scroll_enchant_fire_arrow` |
| scroll           | `scroll_fire_shield`        |
| scroll           | `scroll_fireball`           |
| scroll           | `scroll_fireburst`          |
| scroll           | `scroll_frostbolt`          |
| scroll           | `scroll_invisibility`       |
| scroll           | `scroll_poison_bolt`        |
| scroll           | `scroll_poison_shield`      |
| scroll           | `scroll_shock`              |
| set - chitin     | `chitin_boots`              |
| set - chitin     | `chitin_mail`               |
| set - leather    | `leather_boots`             |
| set - leather    | `leather_cap`               |
| set - leather    | `leather_gloves`            |
| set - leather    | `leather_greaves`           |
| set - leather    | `leather_pants`             |
| set - lurker     | `lurker_boots`              |
| set - lurker     | `lurker_pants`              |
| set - plate      | `plate_boots`               |
| set - plate      | `plate_cuirass`             |
| set - plate      | `plate_gauntlets`           |
| set - plate      | `plate_greaves`             |
| set - ring       | `ring_boots`                |
| set - ring       | `ring_gauntlets`            |
| set - ring       | `ring_greaves`              |
| set - ring       | `ring_mail`                 |
| set - valor      | `boots_valor`               |
| set - valor      | `cuirass_valor`             |
| set - valor      | `gauntlets_valor`           |
| set - valor      | `greaves_valor`             |
| set - valor      | `helmet_valor`              |
| set - valor      | `shield_valor`              |
| tomes            | `tome_fire`                 |
| tomes            | `tome_wisdom`               |
| unsorted         | `ancient_apparatus`         |
| unsorted         | `ancient_axe`               |
| unsorted         | `arrow`                     |
| unsorted         | `assassin_dagger`           |
| unsorted         | `baked_maggot`              |
| unsorted         | `battle_axe`                |
| unsorted         | `blooddrop_blossom`         |
| unsorted         | `blue_gem`                  |
| unsorted         | `blueberry_pie`             |
| unsorted         | `boiled_beetle`             |
| unsorted         | `bone_amulet`               |
| unsorted         | `boots_valor`               |
| unsorted         | `brace_fortitude`           |
| unsorted         | `bracelet_tirin`            |
| unsorted         | `brass_key`                 |
| unsorted         | `cave_nettle`               |
| unsorted         | `chitin_boots`              |
| unsorted         | `chitin_greaves`            |
| unsorted         | `chitin_mail`               |
| unsorted         | `chitin_mask`               |
| unsorted         | `circlet_war`               |
| unsorted         | `cold_arrow`                |
| unsorted         | `cold_quarrel`              |
| unsorted         | `compass`                   |
| unsorted         | `conjurers_hat`             |
| unsorted         | `crossbow`                  |
| unsorted         | `cudgel`                    |
| unsorted         | `cuirass_valor`             |
| unsorted         | `cutlass`                   |
| unsorted         | `dagger`                    |
| unsorted         | `dismantler`                |
| unsorted         | `diviner_cloak`             |
| unsorted         | `doublet`                   |
| unsorted         | `fire_arrow`                |
| unsorted         | `fire_blade_empty`          |
| unsorted         | `fire_blade`                |
| unsorted         | `fire_bomb`                 |
| unsorted         | `fire_quarrel`              |
| unsorted         | `fire_torc`                 |
| unsorted         | `fist_dagger`               |
| unsorted         | `flail`                     |
| unsorted         | `flarefeather_cap`          |
| unsorted         | `flask`                     |
| unsorted         | `frost_bomb`                |
| unsorted         | `frostbite_necklace`        |
| unsorted         | `full_helmet`               |
| unsorted         | `gauntlets_valor`           |
| unsorted         | `gear_key`                  |
| unsorted         | `gear_necklace`             |
| unsorted         | `gold_key`                  |
| unsorted         | `golden_chalice`            |
| unsorted         | `golden_crown`              |
| unsorted         | `golden_dragon`             |
| unsorted         | `golden_figure`             |
| unsorted         | `golden_goromorg`           |
| unsorted         | `golden_orb`                |
| unsorted         | `great_axe`                 |
| unsorted         | `greaves_valor`             |
| unsorted         | `green_gem`                 |
| unsorted         | `grim_cap`                  |
| unsorted         | `hand_axe`                  |
| unsorted         | `hardstone_bracelet`        |
| unsorted         | `heavy_shield`              |
| unsorted         | `helmet_valor`              |
| unsorted         | `herder_cap`                |
| unsorted         | `hide_vest`                 |
| unsorted         | `huntsman_cloak`            |
| unsorted         | `ice_lizard_steak`          |
| unsorted         | `icefall_hammer`            |
| unsorted         | `iron_basinet`              |
| unsorted         | `iron_key`                  |
| unsorted         | `knife`                     |
| unsorted         | `knoffer`                   |
| unsorted         | `leather_boots`             |
| unsorted         | `leather_brigandine`        |
| unsorted         | `leather_cap`               |
| unsorted         | `leather_gloves`            |
| unsorted         | `leather_greaves`           |
| unsorted         | `leather_pants`             |
| unsorted         | `legionary_helmet`          |
| unsorted         | `legionary_shield`          |
| unsorted         | `legionary_spear`           |
| unsorted         | `lightning_blade_empty`     |
| unsorted         | `lightning_blade`           |
| unsorted         | `lightning_rod_empty`       |
| unsorted         | `lightning_rod`             |
| unsorted         | `loincloth`                 |
| unsorted         | `long_sword`                |
| unsorted         | `longbow`                   |
| unsorted         | `lurker_boots`              |
| unsorted         | `lurker_hood`               |
| unsorted         | `lurker_pants`              |
| unsorted         | `lurker_vest`               |
| unsorted         | `machete`                   |
| unsorted         | `machine_junk1`             |
| unsorted         | `machine_junk2`             |
| unsorted         | `machine_junk3`             |
| unsorted         | `machine_junk4`             |
| unsorted         | `machine_junk5`             |
| unsorted         | `machine_junk6`             |
| unsorted         | `machine_part_east`         |
| unsorted         | `machine_part_north`        |
| unsorted         | `machine_part_south`        |
| unsorted         | `machine_part_west`         |
| unsorted         | `magic_orb`                 |
| unsorted         | `milkreed`                  |
| unsorted         | `mole_jerky`                |
| unsorted         | `mortar`                    |
| unsorted         | `nex_sword`                 |
| unsorted         | `nomad_boots`               |
| unsorted         | `nomad_mittens`             |
| unsorted         | `note`                      |
| unsorted         | `ogre_hammer`               |
| unsorted         | `ornate_key`                |
| unsorted         | `peasant_breeches`          |
| unsorted         | `peasant_cap`               |
| unsorted         | `peasant_tunic`             |
| unsorted         | `pit_gauntlets`             |
| unsorted         | `pitroot_bread`             |
| unsorted         | `plate_boots`               |
| unsorted         | `plate_cuirass`             |
| unsorted         | `plate_gauntlets`           |
| unsorted         | `plate_greaves`             |
| unsorted         | `pointy_shoes`              |
| unsorted         | `poison_arrow`              |
| unsorted         | `poison_bomb`               |
| unsorted         | `poison_quarrel`            |
| unsorted         | `potion_cure_disease`       |
| unsorted         | `potion_cure_poison`        |
| unsorted         | `potion_energy`             |
| unsorted         | `potion_healing`            |
| unsorted         | `potion_poison`             |
| unsorted         | `potion_rage`               |
| unsorted         | `potion_speed`              |
| unsorted         | `power_weapon`              |
| unsorted         | `prison_key`                |
| unsorted         | `quarrel`                   |
| unsorted         | `rat_shank`                 |
| unsorted         | `red_gem`                   |
| unsorted         | `remains_of_toorum`         |
| unsorted         | `ring_boots`                |
| unsorted         | `ring_gauntlets`            |
| unsorted         | `ring_greaves`              |
| unsorted         | `ring_mail`                 |
| unsorted         | `rock`                      |
| unsorted         | `rotten_pitroot_bread`      |
| unsorted         | `round_key`                 |
| unsorted         | `round_shield`              |
| unsorted         | `sack`                      |
| unsorted         | `sandals`                   |
| unsorted         | `scaled_cloak`              |
| unsorted         | `scroll_darkness`           |
| unsorted         | `scroll_enchant_fire_arrow` |
| unsorted         | `scroll_fire_shield`        |
| unsorted         | `scroll_fireball`           |
| unsorted         | `scroll_fireburst`          |
| unsorted         | `scroll_frost_shield`       |
| unsorted         | `scroll_frostbolt`          |
| unsorted         | `scroll_ice_shards`         |
| unsorted         | `scroll_invisibility`       |
| unsorted         | `scroll_light`              |
| unsorted         | `scroll_lightning_bolt`     |
| unsorted         | `scroll_poison_bolt`        |
| unsorted         | `scroll_poison_cloud`       |
| unsorted         | `scroll_poison_shield`      |
| unsorted         | `scroll_shock_shield`       |
| unsorted         | `scroll_shock`              |
| unsorted         | `scroll`                    |
| unsorted         | `serpent_bracer`            |
| unsorted         | `shaman_staff`              |
| unsorted         | `shield_elements`           |
| unsorted         | `shield_valor`              |
| unsorted         | `shock_arrow`               |
| unsorted         | `shock_bomb`                |
| unsorted         | `shock_quarrel`             |
| unsorted         | `short_bow`                 |
| unsorted         | `shuriken`                  |
| unsorted         | `silk_hose`                 |
| unsorted         | `slime_bell`                |
| unsorted         | `tar_bead`                  |
| unsorted         | `tattered_cloak`            |
| unsorted         | `throwing_axe`              |
| unsorted         | `throwing_knife`            |
| unsorted         | `tome_fire`                 |
| unsorted         | `tome_health`               |
| unsorted         | `tome_wisdom`               |
| unsorted         | `torch_everburning`         |
| unsorted         | `torch`                     |
| unsorted         | `venom_edge_empty`          |
| unsorted         | `venom_edge`                |
| unsorted         | `warhammer`                 |
| unsorted         | `water_flask`               |
| unsorted         | `whitewood_wand`            |
| unsorted         | `wooden_box`                |
| unsorted         | `zhandul_orb`               |
| utility          | `compass`                   |
| utility          | `torch`                     |
| warn             | `hide_vest`                 |
| warn             | `loincloth`                 |
| warn             | `peasant_cap`               |
| warn             | `peasant_tunic`             |
| warn - back      | `diviner_cloak`             |
| warn - back      | `huntsman_cloak`            |
| warn - back      | `scaled_cloak`              |
| warn - back      | `tattered_cloak`            |
| warn - bracers   | `brace_fortitude`           |
| warn - bracers   | `bracelet_tirin`            |
| warn - bracers   | `hardstone_bracelet`        |
| warn - bracers   | `peasant_breeches`          |
| warn - bracers   | `serpent_bracer`            |
| warn - feet      | `nomad_boots`               |
| warn - feet      | `pointy_shoes`              |
| warn - feet      | `sandals`                   |
| warn - hand      | `legionary_helmet`          |
| warn - hands     | `nomad_mittens`             |
| warn - head      | `conjurers_hat`             |
| warn - head      | `full_helmet`               |
| warn - legs      | `silk_hose`                 |
| warn - neck      | `fire_torc`                 |
| warn - neck      | `frostbite_necklace`        |
| warn - neck      | `spirit_mirror_pendant`     |
