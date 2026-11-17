> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Game Events


  

### `achievement_earned`

```lua
events.achievement_earned:Set(callback: fun(e: events.achievement_earned))
```


  

### `achievement_earned_local`

```lua
events.achievement_earned_local:Set(callback: fun(e: events.achievement_earned_local))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `achievement_event`

```lua
events.achievement_event:Set(callback: fun(e: events.achievement_event))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `achievement_info_loaded`

```lua
events.achievement_info_loaded:Set(callback: fun(e: events.achievement_info_loaded))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `achievement_write_failed`

```lua
events.achievement_write_failed:Set(callback: fun(e: events.achievement_write_failed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `add_bullet_hit_marker`

```lua
events.add_bullet_hit_marker:Set(callback: fun(e: events.add_bullet_hit_marker))
```


  

### `add_player_sonar_icon`

```lua
events.add_player_sonar_icon:Set(callback: fun(e: events.add_player_sonar_icon))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ammo_pickup`

```lua
events.ammo_pickup:Set(callback: fun(e: events.ammo_pickup))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ammo_refill`

```lua
events.ammo_refill:Set(callback: fun(e: events.ammo_refill))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `announce_phase_end`

```lua
events.announce_phase_end:Set(callback: fun(e: events.announce_phase_end))
```


  

### `begin_new_match`

```lua
events.begin_new_match:Set(callback: fun(e: events.begin_new_match))
```


  

### `bomb_abortdefuse`

```lua
events.bomb_abortdefuse:Set(callback: fun(e: events.bomb_abortdefuse))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bomb_abortplant`

```lua
events.bomb_abortplant:Set(callback: fun(e: events.bomb_abortplant))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bomb_beep`

```lua
events.bomb_beep:Set(callback: fun(e: events.bomb_beep))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bomb_begindefuse`

```lua
events.bomb_begindefuse:Set(callback: fun(e: events.bomb_begindefuse))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bomb_beginplant`

```lua
events.bomb_beginplant:Set(callback: fun(e: events.bomb_beginplant))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bomb_defused`

```lua
events.bomb_defused:Set(callback: fun(e: events.bomb_defused))
```


  

### `bomb_dropped`

```lua
events.bomb_dropped:Set(callback: fun(e: events.bomb_dropped))
```


  

### `bomb_exploded`

```lua
events.bomb_exploded:Set(callback: fun(e: events.bomb_exploded))
```


  

### `bomb_pickup`

```lua
events.bomb_pickup:Set(callback: fun(e: events.bomb_pickup))
```


  

### `bomb_planted`

```lua
events.bomb_planted:Set(callback: fun(e: events.bomb_planted))
```


  

### `bonus_updated`

```lua
events.bonus_updated:Set(callback: fun(e: events.bonus_updated))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bot_takeover`

```lua
events.bot_takeover:Set(callback: fun(e: events.bot_takeover))
```


  

### `break_breakable`

```lua
events.break_breakable:Set(callback: fun(e: events.break_breakable))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `break_prop`

```lua
events.break_prop:Set(callback: fun(e: events.break_prop))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `broken_breakable`

```lua
events.broken_breakable:Set(callback: fun(e: events.broken_breakable))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bullet_damage`

```lua
events.bullet_damage:Set(callback: fun(e: events.bullet_damage))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `bullet_impact`

```lua
events.bullet_impact:Set(callback: fun(e: events.bullet_impact))
```


  

### `buymenu_close`

```lua
events.buymenu_close:Set(callback: fun(e: events.buymenu_close))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `buymenu_open`

```lua
events.buymenu_open:Set(callback: fun(e: events.buymenu_open))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `buytime_ended`

```lua
events.buytime_ended:Set(callback: fun(e: events.buytime_ended))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `cart_updated`

```lua
events.cart_updated:Set(callback: fun(e: events.cart_updated))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `choppers_incoming_warning`

```lua
events.choppers_incoming_warning:Set(callback: fun(e: events.choppers_incoming_warning))
```


  

### `client_disconnect`

```lua
events.client_disconnect:Set(callback: fun(e: events.client_disconnect))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `client_loadout_changed`

```lua
events.client_loadout_changed:Set(callback: fun(e: events.client_loadout_changed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `clientside_lesson_closed`

```lua
events.clientside_lesson_closed:Set(callback: fun(e: events.clientside_lesson_closed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `clientside_reload_custom_econ`

```lua
events.clientside_reload_custom_econ:Set(callback: fun(e: events.clientside_reload_custom_econ))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `cs_game_disconnected`

```lua
events.cs_game_disconnected:Set(callback: fun(e: events.cs_game_disconnected))
```


  

### `cs_intermission`

```lua
events.cs_intermission:Set(callback: fun(e: events.cs_intermission))
```


  

### `cs_match_end_restart`

```lua
events.cs_match_end_restart:Set(callback: fun(e: events.cs_match_end_restart))
```


  

### `cs_pre_restart`

```lua
events.cs_pre_restart:Set(callback: fun(e: events.cs_pre_restart))
```


  

### `cs_prev_next_spectator`

```lua
events.cs_prev_next_spectator:Set(callback: fun(e: events.cs_prev_next_spectator))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `cs_round_final_beep`

```lua
events.cs_round_final_beep:Set(callback: fun(e: events.cs_round_final_beep))
```


  

### `cs_round_start_beep`

```lua
events.cs_round_start_beep:Set(callback: fun(e: events.cs_round_start_beep))
```


  

### `cs_win_panel_match`

```lua
events.cs_win_panel_match:Set(callback: fun(e: events.cs_win_panel_match))
```


  

### `cs_win_panel_round`

```lua
events.cs_win_panel_round:Set(callback: fun(e: events.cs_win_panel_round))
```


  

### `decoy_detonate`

```lua
events.decoy_detonate:Set(callback: fun(e: events.decoy_detonate))
```


  

### `decoy_firing`

```lua
events.decoy_firing:Set(callback: fun(e: events.decoy_firing))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `decoy_started`

```lua
events.decoy_started:Set(callback: fun(e: events.decoy_started))
```


  

### `defuser_dropped`

```lua
events.defuser_dropped:Set(callback: fun(e: events.defuser_dropped))
```


  

### `defuser_pickup`

```lua
events.defuser_pickup:Set(callback: fun(e: events.defuser_pickup))
```


  

### `demo_skip`

```lua
events.demo_skip:Set(callback: fun(e: events.demo_skip))
```


  

### `demo_start`

```lua
events.demo_start:Set(callback: fun(e: events.demo_start))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `demo_stop`

```lua
events.demo_stop:Set(callback: fun(e: events.demo_stop))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `difficulty_changed`

```lua
events.difficulty_changed:Set(callback: fun(e: events.difficulty_changed))
```


  

### `dm_bonus_weapon_start`

```lua
events.dm_bonus_weapon_start:Set(callback: fun(e: events.dm_bonus_weapon_start))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `door_break`

```lua
events.door_break:Set(callback: fun(e: events.door_break))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `door_close`

```lua
events.door_close:Set(callback: fun(e: events.door_close))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `door_closed`

```lua
events.door_closed:Set(callback: fun(e: events.door_closed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `door_moving`

```lua
events.door_moving:Set(callback: fun(e: events.door_moving))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `door_open`

```lua
events.door_open:Set(callback: fun(e: events.door_open))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `drone_above_roof`

```lua
events.drone_above_roof:Set(callback: fun(e: events.drone_above_roof))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `drone_cargo_detached`

```lua
events.drone_cargo_detached:Set(callback: fun(e: events.drone_cargo_detached))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `drone_dispatched`

```lua
events.drone_dispatched:Set(callback: fun(e: events.drone_dispatched))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `dronegun_attack`

```lua
events.dronegun_attack:Set(callback: fun(e: events.dronegun_attack))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `drop_rate_modified`

```lua
events.drop_rate_modified:Set(callback: fun(e: events.drop_rate_modified))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `dynamic_shadow_light_changed`

```lua
events.dynamic_shadow_light_changed:Set(callback: fun(e: events.dynamic_shadow_light_changed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `dz_item_interaction`

```lua
events.dz_item_interaction:Set(callback: fun(e: events.dz_item_interaction))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `enable_restart_voting`

```lua
events.enable_restart_voting:Set(callback: fun(e: events.enable_restart_voting))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `endmatch_cmm_start_reveal_items`

```lua
events.endmatch_cmm_start_reveal_items:Set(callback: fun(e: events.endmatch_cmm_start_reveal_items))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `endmatch_mapvote_selecting_map`

```lua
events.endmatch_mapvote_selecting_map:Set(callback: fun(e: events.endmatch_mapvote_selecting_map))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `enter_bombzone`

```lua
events.enter_bombzone:Set(callback: fun(e: events.enter_bombzone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `enter_buyzone`

```lua
events.enter_buyzone:Set(callback: fun(e: events.enter_buyzone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `enter_rescue_zone`

```lua
events.enter_rescue_zone:Set(callback: fun(e: events.enter_rescue_zone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `entity_killed`

```lua
events.entity_killed:Set(callback: fun(e: events.entity_killed))
```


  

### `entity_visible`

```lua
events.entity_visible:Set(callback: fun(e: events.entity_visible))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `event_ticket_modified`

```lua
events.event_ticket_modified:Set(callback: fun(e: events.event_ticket_modified))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `exit_bombzone`

```lua
events.exit_bombzone:Set(callback: fun(e: events.exit_bombzone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `exit_buyzone`

```lua
events.exit_buyzone:Set(callback: fun(e: events.exit_buyzone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `exit_rescue_zone`

```lua
events.exit_rescue_zone:Set(callback: fun(e: events.exit_rescue_zone))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `finale_start`

```lua
events.finale_start:Set(callback: fun(e: events.finale_start))
```


  

### `firstbombs_incoming_warning`

```lua
events.firstbombs_incoming_warning:Set(callback: fun(e: events.firstbombs_incoming_warning))
```


  

### `flare_ignite_npc`

```lua
events.flare_ignite_npc:Set(callback: fun(e: events.flare_ignite_npc))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `flashbang_detonate`

```lua
events.flashbang_detonate:Set(callback: fun(e: events.flashbang_detonate))
```


  

### `game_end`

```lua
events.game_end:Set(callback: fun(e: events.game_end))
```

a game ended


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `game_init`

```lua
events.game_init:Set(callback: fun(e: events.game_init))
```

sent when a new game is started


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `game_message`

```lua
events.game_message:Set(callback: fun(e: events.game_message))
```

a message send by game logic to everyone


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `game_newmap`

```lua
events.game_newmap:Set(callback: fun(e: events.game_newmap))
```

send when new map is completely loaded


  

### `game_phase_changed`

```lua
events.game_phase_changed:Set(callback: fun(e: events.game_phase_changed))
```


  

### `game_start`

```lua
events.game_start:Set(callback: fun(e: events.game_start))
```

a new game starts


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `gameinstructor_draw`

```lua
events.gameinstructor_draw:Set(callback: fun(e: events.gameinstructor_draw))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `gameinstructor_nodraw`

```lua
events.gameinstructor_nodraw:Set(callback: fun(e: events.gameinstructor_nodraw))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `gameui_hidden`

```lua
events.gameui_hidden:Set(callback: fun(e: events.gameui_hidden))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `gc_connected`

```lua
events.gc_connected:Set(callback: fun(e: events.gc_connected))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `gg_killed_enemy`

```lua
events.gg_killed_enemy:Set(callback: fun(e: events.gg_killed_enemy))
```


  

### `grenade_bounce`

```lua
events.grenade_bounce:Set(callback: fun(e: events.grenade_bounce))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `grenade_thrown`

```lua
events.grenade_thrown:Set(callback: fun(e: events.grenade_thrown))
```


  

### `guardian_wave_restart`

```lua
events.guardian_wave_restart:Set(callback: fun(e: events.guardian_wave_restart))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hegrenade_detonate`

```lua
events.hegrenade_detonate:Set(callback: fun(e: events.hegrenade_detonate))
```


  

### `helicopter_grenade_punt_miss`

```lua
events.helicopter_grenade_punt_miss:Set(callback: fun(e: events.helicopter_grenade_punt_miss))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hide_deathpanel`

```lua
events.hide_deathpanel:Set(callback: fun(e: events.hide_deathpanel))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hltv_cameraman`

```lua
events.hltv_cameraman:Set(callback: fun(e: events.hltv_cameraman))
```

a spectator/player is a cameraman


  

### `hltv_changed_mode`

```lua
events.hltv_changed_mode:Set(callback: fun(e: events.hltv_changed_mode))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hltv_chase`

```lua
events.hltv_chase:Set(callback: fun(e: events.hltv_chase))
```

shot of a single entity


  

### `hltv_chat`

```lua
events.hltv_chat:Set(callback: fun(e: events.hltv_chat))
```

a HLTV chat msg sent by spectators


  

### `hltv_fixed`

```lua
events.hltv_fixed:Set(callback: fun(e: events.hltv_fixed))
```

show from fixed view


  

### `hltv_message`

```lua
events.hltv_message:Set(callback: fun(e: events.hltv_message))
```

a HLTV message send by moderators


  

### `hltv_rank_camera`

```lua
events.hltv_rank_camera:Set(callback: fun(e: events.hltv_rank_camera))
```

a camera ranking


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hltv_rank_entity`

```lua
events.hltv_rank_entity:Set(callback: fun(e: events.hltv_rank_entity))
```

an entity ranking


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hltv_replay`

```lua
events.hltv_replay:Set(callback: fun(e: events.hltv_replay))
```


  

### `hltv_replay_status`

```lua
events.hltv_replay_status:Set(callback: fun(e: events.hltv_replay_status))
```


  

### `hltv_status`

```lua
events.hltv_status:Set(callback: fun(e: events.hltv_status))
```

general HLTV status


  

### `hltv_title`

```lua
events.hltv_title:Set(callback: fun(e: events.hltv_title))
```


  

### `hltv_versioninfo`

```lua
events.hltv_versioninfo:Set(callback: fun(e: events.hltv_versioninfo))
```


  

### `hostage_call_for_help`

```lua
events.hostage_call_for_help:Set(callback: fun(e: events.hostage_call_for_help))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hostage_follows`

```lua
events.hostage_follows:Set(callback: fun(e: events.hostage_follows))
```


  

### `hostage_hurt`

```lua
events.hostage_hurt:Set(callback: fun(e: events.hostage_hurt))
```


  

### `hostage_killed`

```lua
events.hostage_killed:Set(callback: fun(e: events.hostage_killed))
```


  

### `hostage_rescued`

```lua
events.hostage_rescued:Set(callback: fun(e: events.hostage_rescued))
```


  

### `hostage_rescued_all`

```lua
events.hostage_rescued_all:Set(callback: fun(e: events.hostage_rescued_all))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hostage_stops_following`

```lua
events.hostage_stops_following:Set(callback: fun(e: events.hostage_stops_following))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `hostname_changed`

```lua
events.hostname_changed:Set(callback: fun(e: events.hostname_changed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `inferno_expire`

```lua
events.inferno_expire:Set(callback: fun(e: events.inferno_expire))
```


  

### `inferno_extinguish`

```lua
events.inferno_extinguish:Set(callback: fun(e: events.inferno_extinguish))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `inferno_startburn`

```lua
events.inferno_startburn:Set(callback: fun(e: events.inferno_startburn))
```


  

### `inspect_weapon`

```lua
events.inspect_weapon:Set(callback: fun(e: events.inspect_weapon))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `instructor_close_lesson`

```lua
events.instructor_close_lesson:Set(callback: fun(e: events.instructor_close_lesson))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `instructor_server_hint_create`

```lua
events.instructor_server_hint_create:Set(callback: fun(e: events.instructor_server_hint_create))
```

create a hint using data supplied entirely by the server/map. Intended for hints to smooth playtests before content is ready to make the hint unneccessary. NOT INTENDED AS A SHIPPABLE CRUTCH


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `instructor_server_hint_stop`

```lua
events.instructor_server_hint_stop:Set(callback: fun(e: events.instructor_server_hint_stop))
```

destroys a server/map created hint


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `instructor_start_lesson`

```lua
events.instructor_start_lesson:Set(callback: fun(e: events.instructor_start_lesson))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `inventory_updated`

```lua
events.inventory_updated:Set(callback: fun(e: events.inventory_updated))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `item_equip`

```lua
events.item_equip:Set(callback: fun(e: events.item_equip))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `item_pickup`

```lua
events.item_pickup:Set(callback: fun(e: events.item_pickup))
```


  

### `item_pickup_failed`

```lua
events.item_pickup_failed:Set(callback: fun(e: events.item_pickup_failed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `item_pickup_slerp`

```lua
events.item_pickup_slerp:Set(callback: fun(e: events.item_pickup_slerp))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `item_purchase`

```lua
events.item_purchase:Set(callback: fun(e: events.item_purchase))
```


  

### `item_remove`

```lua
events.item_remove:Set(callback: fun(e: events.item_remove))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `item_schema_initialized`

```lua
events.item_schema_initialized:Set(callback: fun(e: events.item_schema_initialized))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `jointeam_failed`

```lua
events.jointeam_failed:Set(callback: fun(e: events.jointeam_failed))
```


  

### `local_player_controller_team`

```lua
events.local_player_controller_team:Set(callback: fun(e: events.local_player_controller_team))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `local_player_pawn_changed`

```lua
events.local_player_pawn_changed:Set(callback: fun(e: events.local_player_pawn_changed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `local_player_team`

```lua
events.local_player_team:Set(callback: fun(e: events.local_player_team))
```


  

### `loot_crate_opened`

```lua
events.loot_crate_opened:Set(callback: fun(e: events.loot_crate_opened))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `loot_crate_visible`

```lua
events.loot_crate_visible:Set(callback: fun(e: events.loot_crate_visible))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `map_shutdown`

```lua
events.map_shutdown:Set(callback: fun(e: events.map_shutdown))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `map_transition`

```lua
events.map_transition:Set(callback: fun(e: events.map_transition))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `match_end_conditions`

```lua
events.match_end_conditions:Set(callback: fun(e: events.match_end_conditions))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `material_default_complete`

```lua
events.material_default_complete:Set(callback: fun(e: events.material_default_complete))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `mb_input_lock_cancel`

```lua
events.mb_input_lock_cancel:Set(callback: fun(e: events.mb_input_lock_cancel))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `mb_input_lock_success`

```lua
events.mb_input_lock_success:Set(callback: fun(e: events.mb_input_lock_success))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `molotov_detonate`

```lua
events.molotov_detonate:Set(callback: fun(e: events.molotov_detonate))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `nav_blocked`

```lua
events.nav_blocked:Set(callback: fun(e: events.nav_blocked))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `nav_generate`

```lua
events.nav_generate:Set(callback: fun(e: events.nav_generate))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `nextlevel_changed`

```lua
events.nextlevel_changed:Set(callback: fun(e: events.nextlevel_changed))
```

a game event, name may be 32 characters long


  

### `open_crate_instr`

```lua
events.open_crate_instr:Set(callback: fun(e: events.open_crate_instr))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `other_death`

```lua
events.other_death:Set(callback: fun(e: events.other_death))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `parachute_deploy`

```lua
events.parachute_deploy:Set(callback: fun(e: events.parachute_deploy))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `parachute_pickup`

```lua
events.parachute_pickup:Set(callback: fun(e: events.parachute_pickup))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `physgun_pickup`

```lua
events.physgun_pickup:Set(callback: fun(e: events.physgun_pickup))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_activate`

```lua
events.player_activate:Set(callback: fun(e: events.player_activate))
```


  

### `player_avenged_teammate`

```lua
events.player_avenged_teammate:Set(callback: fun(e: events.player_avenged_teammate))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_blind`

```lua
events.player_blind:Set(callback: fun(e: events.player_blind))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_changename`

```lua
events.player_changename:Set(callback: fun(e: events.player_changename))
```


  

### `player_chat`

```lua
events.player_chat:Set(callback: fun(e: events.player_chat))
```

a public player chat


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_connect`

```lua
events.player_connect:Set(callback: fun(e: events.player_connect))
```

a new client connected


  

### `player_connect_full`

```lua
events.player_connect_full:Set(callback: fun(e: events.player_connect_full))
```

player has sent final message in the connection sequence


  

### `player_death`

```lua
events.player_death:Set(callback: fun(e: events.player_death))
```

a game event, name may be 32 characters long this extents the original player_death by a new fields


  

### `player_decal`

```lua
events.player_decal:Set(callback: fun(e: events.player_decal))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_disconnect`

```lua
events.player_disconnect:Set(callback: fun(e: events.player_disconnect))
```

a client was disconnected


  

### `player_falldamage`

```lua
events.player_falldamage:Set(callback: fun(e: events.player_falldamage))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_footstep`

```lua
events.player_footstep:Set(callback: fun(e: events.player_footstep))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_full_update`

```lua
events.player_full_update:Set(callback: fun(e: events.player_full_update))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_given_c4`

```lua
events.player_given_c4:Set(callback: fun(e: events.player_given_c4))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_hintmessage`

```lua
events.player_hintmessage:Set(callback: fun(e: events.player_hintmessage))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_hurt`

```lua
events.player_hurt:Set(callback: fun(e: events.player_hurt))
```


  

### `player_info`

```lua
events.player_info:Set(callback: fun(e: events.player_info))
```

a player changed his name


  

### `player_jump`

```lua
events.player_jump:Set(callback: fun(e: events.player_jump))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_ping`

```lua
events.player_ping:Set(callback: fun(e: events.player_ping))
```


  

### `player_ping_stop`

```lua
events.player_ping_stop:Set(callback: fun(e: events.player_ping_stop))
```


  

### `player_radio`

```lua
events.player_radio:Set(callback: fun(e: events.player_radio))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_reset_vote`

```lua
events.player_reset_vote:Set(callback: fun(e: events.player_reset_vote))
```


  

### `player_score`

```lua
events.player_score:Set(callback: fun(e: events.player_score))
```

players scores changed


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_shoot`

```lua
events.player_shoot:Set(callback: fun(e: events.player_shoot))
```

player shoot his weapon


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_sound`

```lua
events.player_sound:Set(callback: fun(e: events.player_sound))
```


  

### `player_spawn`

```lua
events.player_spawn:Set(callback: fun(e: events.player_spawn))
```

player spawned in game


  

### `player_spawned`

```lua
events.player_spawned:Set(callback: fun(e: events.player_spawned))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `player_stats_updated`

```lua
events.player_stats_updated:Set(callback: fun(e: events.player_stats_updated))
```


  

### `player_team`

```lua
events.player_team:Set(callback: fun(e: events.player_team))
```

player change his team


  

### `ragdoll_dissolved`

```lua
events.ragdoll_dissolved:Set(callback: fun(e: events.ragdoll_dissolved))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `read_game_titledata`

```lua
events.read_game_titledata:Set(callback: fun(e: events.read_game_titledata))
```

read user titledata from profile


  

### `repost_xbox_achievements`

```lua
events.repost_xbox_achievements:Set(callback: fun(e: events.repost_xbox_achievements))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `reset_game_titledata`

```lua
events.reset_game_titledata:Set(callback: fun(e: events.reset_game_titledata))
```

reset user titledata; do not automatically write profile


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_announce_final`

```lua
events.round_announce_final:Set(callback: fun(e: events.round_announce_final))
```


  

### `round_announce_last_round_half`

```lua
events.round_announce_last_round_half:Set(callback: fun(e: events.round_announce_last_round_half))
```


  

### `round_announce_match_point`

```lua
events.round_announce_match_point:Set(callback: fun(e: events.round_announce_match_point))
```


  

### `round_announce_match_start`

```lua
events.round_announce_match_start:Set(callback: fun(e: events.round_announce_match_start))
```


  

### `round_announce_warmup`

```lua
events.round_announce_warmup:Set(callback: fun(e: events.round_announce_warmup))
```


  

### `round_end`

```lua
events.round_end:Set(callback: fun(e: events.round_end))
```


  

### `round_end_upload_stats`

```lua
events.round_end_upload_stats:Set(callback: fun(e: events.round_end_upload_stats))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_freeze_end`

```lua
events.round_freeze_end:Set(callback: fun(e: events.round_freeze_end))
```


  

### `round_mvp`

```lua
events.round_mvp:Set(callback: fun(e: events.round_mvp))
```


  

### `round_officially_ended`

```lua
events.round_officially_ended:Set(callback: fun(e: events.round_officially_ended))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_poststart`

```lua
events.round_poststart:Set(callback: fun(e: events.round_poststart))
```

sent after all other round restart actions


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_prestart`

```lua
events.round_prestart:Set(callback: fun(e: events.round_prestart))
```

sent before all other round restart actions


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_start`

```lua
events.round_start:Set(callback: fun(e: events.round_start))
```


  

### `round_start_post_nav`

```lua
events.round_start_post_nav:Set(callback: fun(e: events.round_start_post_nav))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_start_pre_entity`

```lua
events.round_start_pre_entity:Set(callback: fun(e: events.round_start_pre_entity))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `round_time_warning`

```lua
events.round_time_warning:Set(callback: fun(e: events.round_time_warning))
```


  

### `seasoncoin_levelup`

```lua
events.seasoncoin_levelup:Set(callback: fun(e: events.seasoncoin_levelup))
```


  

### `server_cvar`

```lua
events.server_cvar:Set(callback: fun(e: events.server_cvar))
```

a server console var has changed


  

### `server_message`

```lua
events.server_message:Set(callback: fun(e: events.server_message))
```

a generic server message


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `server_pre_shutdown`

```lua
events.server_pre_shutdown:Set(callback: fun(e: events.server_pre_shutdown))
```

server is about to be shut down


  

### `server_shutdown`

```lua
events.server_shutdown:Set(callback: fun(e: events.server_shutdown))
```

server shut down


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `server_spawn`

```lua
events.server_spawn:Set(callback: fun(e: events.server_spawn))
```

send once a server starts


  

### `set_instructor_group_enabled`

```lua
events.set_instructor_group_enabled:Set(callback: fun(e: events.set_instructor_group_enabled))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `sfuievent`

```lua
events.sfuievent:Set(callback: fun(e: events.sfuievent))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `show_deathpanel`

```lua
events.show_deathpanel:Set(callback: fun(e: events.show_deathpanel))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `show_survival_respawn_status`

```lua
events.show_survival_respawn_status:Set(callback: fun(e: events.show_survival_respawn_status))
```


  

### `silencer_detach`

```lua
events.silencer_detach:Set(callback: fun(e: events.silencer_detach))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `silencer_off`

```lua
events.silencer_off:Set(callback: fun(e: events.silencer_off))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `silencer_on`

```lua
events.silencer_on:Set(callback: fun(e: events.silencer_on))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `smoke_beacon_paradrop`

```lua
events.smoke_beacon_paradrop:Set(callback: fun(e: events.smoke_beacon_paradrop))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `smokegrenade_detonate`

```lua
events.smokegrenade_detonate:Set(callback: fun(e: events.smokegrenade_detonate))
```


  

### `smokegrenade_expired`

```lua
events.smokegrenade_expired:Set(callback: fun(e: events.smokegrenade_expired))
```


  

### `spec_mode_updated`

```lua
events.spec_mode_updated:Set(callback: fun(e: events.spec_mode_updated))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `spec_target_updated`

```lua
events.spec_target_updated:Set(callback: fun(e: events.spec_target_updated))
```


  

### `start_halftime`

```lua
events.start_halftime:Set(callback: fun(e: events.start_halftime))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `start_vote`

```lua
events.start_vote:Set(callback: fun(e: events.start_vote))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `store_pricesheet_updated`

```lua
events.store_pricesheet_updated:Set(callback: fun(e: events.store_pricesheet_updated))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `survival_announce_phase`

```lua
events.survival_announce_phase:Set(callback: fun(e: events.survival_announce_phase))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `survival_no_respawns_final`

```lua
events.survival_no_respawns_final:Set(callback: fun(e: events.survival_no_respawns_final))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `survival_no_respawns_warning`

```lua
events.survival_no_respawns_warning:Set(callback: fun(e: events.survival_no_respawns_warning))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `survival_paradrop_break`

```lua
events.survival_paradrop_break:Set(callback: fun(e: events.survival_paradrop_break))
```


  

### `survival_paradrop_spawn`

```lua
events.survival_paradrop_spawn:Set(callback: fun(e: events.survival_paradrop_spawn))
```


  

### `survival_teammate_respawn`

```lua
events.survival_teammate_respawn:Set(callback: fun(e: events.survival_teammate_respawn))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `switch_team`

```lua
events.switch_team:Set(callback: fun(e: events.switch_team))
```


  

### `tagrenade_detonate`

```lua
events.tagrenade_detonate:Set(callback: fun(e: events.tagrenade_detonate))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `team_info`

```lua
events.team_info:Set(callback: fun(e: events.team_info))
```

info about team


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `team_intro_end`

```lua
events.team_intro_end:Set(callback: fun(e: events.team_intro_end))
```


  

### `team_intro_start`

```lua
events.team_intro_start:Set(callback: fun(e: events.team_intro_start))
```


  

### `team_score`

```lua
events.team_score:Set(callback: fun(e: events.team_score))
```

team score changed


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `teamchange_pending`

```lua
events.teamchange_pending:Set(callback: fun(e: events.teamchange_pending))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `teamplay_broadcast_audio`

```lua
events.teamplay_broadcast_audio:Set(callback: fun(e: events.teamplay_broadcast_audio))
```

emits a sound to everyone on a team


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `teamplay_round_start`

```lua
events.teamplay_round_start:Set(callback: fun(e: events.teamplay_round_start))
```

round restart


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `tournament_reward`

```lua
events.tournament_reward:Set(callback: fun(e: events.tournament_reward))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `trial_time_expired`

```lua
events.trial_time_expired:Set(callback: fun(e: events.trial_time_expired))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ugc_file_download_finished`

```lua
events.ugc_file_download_finished:Set(callback: fun(e: events.ugc_file_download_finished))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ugc_file_download_start`

```lua
events.ugc_file_download_start:Set(callback: fun(e: events.ugc_file_download_start))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ugc_map_download_error`

```lua
events.ugc_map_download_error:Set(callback: fun(e: events.ugc_map_download_error))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ugc_map_info_received`

```lua
events.ugc_map_info_received:Set(callback: fun(e: events.ugc_map_info_received))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `ugc_map_unsubscribed`

```lua
events.ugc_map_unsubscribed:Set(callback: fun(e: events.ugc_map_unsubscribed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `update_matchmaking_stats`

```lua
events.update_matchmaking_stats:Set(callback: fun(e: events.update_matchmaking_stats))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `user_data_downloaded`

```lua
events.user_data_downloaded:Set(callback: fun(e: events.user_data_downloaded))
```

fired when achievements/stats are downloaded from Steam or XBox Live


  

### `vip_escaped`

```lua
events.vip_escaped:Set(callback: fun(e: events.vip_escaped))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vip_killed`

```lua
events.vip_killed:Set(callback: fun(e: events.vip_killed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_cast`

```lua
events.vote_cast:Set(callback: fun(e: events.vote_cast))
```


  

### `vote_cast_no`

```lua
events.vote_cast_no:Set(callback: fun(e: events.vote_cast_no))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_cast_yes`

```lua
events.vote_cast_yes:Set(callback: fun(e: events.vote_cast_yes))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_changed`

```lua
events.vote_changed:Set(callback: fun(e: events.vote_changed))
```


  

### `vote_ended`

```lua
events.vote_ended:Set(callback: fun(e: events.vote_ended))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_failed`

```lua
events.vote_failed:Set(callback: fun(e: events.vote_failed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_options`

```lua
events.vote_options:Set(callback: fun(e: events.vote_options))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_passed`

```lua
events.vote_passed:Set(callback: fun(e: events.vote_passed))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `vote_started`

```lua
events.vote_started:Set(callback: fun(e: events.vote_started))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `warmup_end`

```lua
events.warmup_end:Set(callback: fun(e: events.warmup_end))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `weapon_fire`

```lua
events.weapon_fire:Set(callback: fun(e: events.weapon_fire))
```


  

### `weapon_fire_on_empty`

```lua
events.weapon_fire_on_empty:Set(callback: fun(e: events.weapon_fire_on_empty))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `weapon_reload`

```lua
events.weapon_reload:Set(callback: fun(e: events.weapon_reload))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `weapon_zoom`

```lua
events.weapon_zoom:Set(callback: fun(e: events.weapon_zoom))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `weapon_zoom_rifle`

```lua
events.weapon_zoom_rifle:Set(callback: fun(e: events.weapon_zoom_rifle))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.


  

  

### `weaponhud_selection`

```lua
events.weaponhud_selection:Set(callback: fun(e: events.weaponhud_selection))
```


  

### `write_game_titledata`

```lua
events.write_game_titledata:Set(callback: fun(e: events.write_game_titledata))
```

write user titledata in profile


  

### `write_profile_data`

```lua
events.write_profile_data:Set(callback: fun(e: events.write_profile_data))
```


    


**Warning:** 
Nothing in the game listens for this event, so the server does not send it and this callback never runs.
