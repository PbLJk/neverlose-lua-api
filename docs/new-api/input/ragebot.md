> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Ragebot


<a id="ragebot-1"></a>

## ragebot  — global table


Provides the ragebot shot information, the state of the anti-aim mouse override, and the state
of the quick peek assist.


  

### `ragebot.IsMouseOverrideActive`

```lua
ragebot.IsMouseOverrideActive(): boolean
```

Returns true if the anti-aim mouse override has a yaw selected.


    
Holding the hotkey while the mouse is inside the deadzone does not select a yaw. A selected yaw
can stay active after the hotkey is released.


  

  

### `ragebot.GetQuickPeekState`

```lua
ragebot.GetQuickPeekState(): ragebot.QuickPeekState?
```

Returns the state of the quick peek assist for the last processed command.


    
In the `pre_movement` event, this is the state of the previous command, because quick peek runs
after the event returns. In the `post_movement` and `createmove` events, this is the state of
the current command.

Returns nil if the quick peek assist is not active or the local player is dead.


  

  

<a id="ragebot-QuickPeekPhase"></a>
### `ragebot.QuickPeekPhase`

The phase of the quick peek assist, returned in `ragebot.GetQuickPeekState`.


    

### `ragebot.QuickPeekPhase`


| Name | Value | Description |
| --- | --- | --- |
| kArmed | 0 | The retreat point is set and the player is not returning to it. If a maximum distance is set in the menu, the point can follow the player. |
| kReturning | 1 | The player is walking back to the retreat point. |
| kHolding | 2 | The player is back at the retreat point and stays there until the weapon can fire again. |


  


## ragebot.QuickPeekState — object type

The state of the quick peek assist, returned by `ragebot.GetQuickPeekState`.


  

### `ragebot.QuickPeekState.interpolated_position`

The retreat point, smoothed between commands. The built-in circle is drawn at this point. Use it when you draw.


  

### `ragebot.QuickPeekState.phase`

The current phase of the quick peek assist.


  

### `ragebot.QuickPeekState.position`

The retreat point in world space. It is updated once per command.


## ragebot.Shot — object type

A shot record, passed to `events.aim_fire` and `events.aim_ack`. All fields are read-only.
Reading an unknown field throws an error.


  

### `ragebot.Shot.aim_point`

The chosen point on the target, in world space.


  

### `ragebot.Shot.command_number`

The command number of the shot.


  

### `ragebot.Shot.damage`

The damage registered on the target. It is `-1` if the shot missed and `0` if a damage rejection was detected.


  

### `ragebot.Shot.estimated_damage`

The predicted damage at the chosen aim point.


  

### `ragebot.Shot.force_shot`

True if the shot was fired with force shot active at perfect accuracy.


  

### `ragebot.Shot.health_left`

The health of the target after the matching hurt event, or `-1` if it is not known.


  

### `ragebot.Shot.hitchance`

The estimated hit chance, from 0 to 1. Multiply it by 100 to get a percentage.


  

### `ragebot.Shot.hitgroup`

The hitgroup that the server reported, or `-1` if the shot missed.


  

### `ragebot.Shot.manual_shot`

True if the user forced the shot with a manual attack.


  

### `ragebot.Shot.minimum_damage`

The minimum damage required for this target and shot.


  

<a id="ragebot-Shot-Result"></a>
### `ragebot.Shot.result`

The result of the shot, or the reason for the miss.


  

### `ragebot.Shot.server_shoot_position`

The most likely shoot position that the server used for the shot. It can be inaccurate.


  

### `ragebot.Shot.shoot_position`

The predicted position in world space from which the shot was aimed.


  

### `ragebot.Shot.simulation_time`

The simulation tick and fraction of the lag compensation record of the target.


  

### `ragebot.Shot.target`

The entity index of the player controller of the target.


  

### `ragebot.Shot.tickcount`

The tick count of the local player when the shot was fired.


  

### `ragebot.Shot.wanted_hitgroup`

The hitgroup of the chosen hitbox of the target.


  

### `ragebot.Shot.weapon`

A handle to the weapon. It is not a weapon entity and it is not an entity index.


  

<a id="ragebot-Shot-Result"></a>
### `ragebot.Shot.Result`

The result of a shot, returned in `ragebot.Shot.result`. A shot that deals damage can still be counted as a miss if the damage is less than the minimum damage of the ragebot.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "hit" |  | The shot dealt the required damage. |
| "death" |  | The local player died before the shot was processed. |
| "player death" |  | Another player killed the target before the shot was processed. |
| "timeout" |  | The server did not confirm the command of the shot in time. |
| "damage rejection" |  | A hit was detected, but the server did not register any damage. |
| "unregistered shot" |  | The server did not report a matching shot in time. |
| "prediction error" |  | The shot missed because of an engine prediction error. This usually happens in situations that cannot be predicted, for example when the player is slowed down by damage. |
| "shootpos misprediction" |  | The shoot position was calculated incorrectly. |
| "hitchance misprediction" |  | The hit chance was estimated incorrectly. |
| "spread" |  | The shot missed because of spread. |
| "lagcomp misprediction" |  | The position of the enemy was predicted incorrectly, so the lag compensation state on the server was different from the prediction. |
| "lagcomp failure" |  | A prediction error caused wrong timing, so lag compensation failed. |
| "occlusion" |  | The penetration simulation was wrong. |
| "extrapolation" |  | The position of the enemy was extrapolated incorrectly. |
| "unknown" |  | Everything was correct and the shot should have hit, but it did not. |
