> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Input


## input.ButtonHandle — object type

The state of one physical button on the keyboard, mouse or gamepad. All fields are read-only.

`pressed` and `released` are true only during the input poll in which the change happened.


  

### `input.ButtonHandle.binding`

The console command that is bound to this button.


  

### `input.ButtonHandle.down`

True while the button is held down.


  

### `input.ButtonHandle.pressed`

True if the button went down in the current input poll.


  

### `input.ButtonHandle.pressed_tick`

The input poll tick of the last press. This is a tick of the input system, so it does not match game ticks or simulation ticks.


  

### `input.ButtonHandle.released`

True if the button went up in the current input poll.


  

### `input.ButtonHandle.released_tick`

The input poll tick of the last release. This is a tick of the input system, so it does not match game ticks or simulation ticks.


## input.buttons — object type

The physical buttons, indexed by their engine names in lowercase, for example `input.buttons.mouse1`.
Names must be written in lowercase. An unknown name returns nil. All entries are read-only.

Read the `pressed` and `released` states inside the `input_poll` event, because they are only true
during the poll in which the change happened.


  

### `input.buttons[string]`


## input.analog — object type

The physical axes, indexed by their engine names in lowercase. Names must be written in lowercase.
An unknown name returns nil. All entries are read-only.

The mouse wheel value is a running total. To get the movement since your last reading, subtract
the last reading from the current one. A negative result means the wheel moved down, and a
positive result means it moved up. Several wheel steps can add up between two callbacks.


  

### `input.analog[string]`


  

### `input.analog.mouse_wheel`

The running total of the mouse wheel position. Subtract the last reading to get the movement. Read-only.


<a id="input-1"></a>

## input  — global table


  

<a id="inputanalog"></a>
### `input.analog`

The live values of the physical axes, indexed by their engine names in lowercase. Read-only.


  

<a id="inputbuttons"></a>
### `input.buttons`

The live state of the physical buttons, indexed by their engine names in lowercase. Read-only.


  

### `input.poll_tick`

The current input poll tick. Compare it with `pressed_tick` and `released_tick` of a button. Read-only.


## input.InputPollContext — object type

The argument of the `input_poll` event. It holds the live input state of the current poll,
before the game turns it into a user command.

To steer the local player, use `SetViewAngles` and the writable button fields. These change
the input in the same way as the mouse and keyboard. Use them instead of writing to the user
command directly.

Enabled legitbot features run after the callback and can override what it sets. When the
aimbot has a target, it replaces the view angles. Movement features override the same buttons.

Use this object only inside the callback. Using it outside the callback throws an error.
Reading or writing an unknown field also throws an error.

To change the view angles, read them with `GetViewAngles`, edit the returned copy, and pass it
to `SetViewAngles`.

The timing, position and shot fields are read-only. The shot fields are nil while the data
that the game last presented is out of date. The writable button fields are listed below.


  

### `input.InputPollContext.aim_punch`

The aim punch at the presented player time. It uses the same angle space as `shoot_angles`. The value is nil while the presented data is out of date. Read-only.


  

### `input.InputPollContext.eye_position`

The eye position of the rendered player, which is the origin plus the view offset. Aim and field of view calculations use this position. A shot does not start from this position. Read-only.


  

### `input.InputPollContext.frame_start`

True if this is the first poll of the frame. Read-only.


  

### `input.InputPollContext.in_attack`

Primary fire.


  

### `input.InputPollContext.in_attack2`

Secondary fire or scope.


  

### `input.InputPollContext.in_back`

Move backward.


  

### `input.InputPollContext.in_duck`

Duck.


  

### `input.InputPollContext.in_forward`

Move forward.


  

### `input.InputPollContext.in_joyautosprint`

Automatic sprint with a gamepad.


  

### `input.InputPollContext.in_jump`

Jump.


  

### `input.InputPollContext.in_look_at_weapon`

Inspect the weapon.


  

### `input.InputPollContext.in_moveleft`

Move left.


  

### `input.InputPollContext.in_moveright`

Move right.


  

### `input.InputPollContext.in_reload`

Reload.


  

### `input.InputPollContext.in_score`

Show the scoreboard.


  

### `input.InputPollContext.in_speed`

Walk.


  

### `input.InputPollContext.in_turnleft`

Turn left with the keyboard or a gamepad.


  

### `input.InputPollContext.in_turnright`

Turn right with the keyboard or a gamepad.


  

### `input.InputPollContext.in_use`

Use or interact.


  

### `input.InputPollContext.in_useorreload`

The shared button for use and reload.


  

### `input.InputPollContext.in_zoom`

Zoom or toggle the scope.


  

### `input.InputPollContext.input_fraction`

The fraction of the current tick at which this poll happened. Read-only.


  

### `input.InputPollContext.input_time`

The time at which this poll happened, in seconds. Read-only.


  

### `input.InputPollContext.loopback`

True if the game is connected to a local server. Read-only.


  

### `input.InputPollContext.player_fraction`

The corrected fraction of the player tick of this poll. Read-only.


  

### `input.InputPollContext.player_tick`

The corrected player tick of this poll. Read-only.


  

### `input.InputPollContext.pred_fraction`

The prediction time fraction of this poll. It is always `0` during the poll. Use `player_tick` and `player_fraction` for the corrected time. Read-only.


  

### `input.InputPollContext.shoot_angles`

The view angles that a shot fired from this poll uses, without aim punch. Add `aim_punch` to get the real direction of the bullet. The value is nil while the presented data is out of date. Read-only.


  

### `input.InputPollContext.shoot_position`

The position in world space from which a shot fired in this poll starts. It is different from `eye_position`. The value is nil while the presented data is out of date. Read-only.


  

### `input.InputPollContext.shoot_velocity`

The speed and direction in which `shoot_position` moves, in units per second. It is the change of `shoot_position` over the one tick before the presented player time. It includes the movement of the view offset when the player ducks or lands, so it is different from `m_vecAbsVelocity` of the pawn. The value is nil while the presented data is out of date. Read-only.


  

### `input.InputPollContext.tick_start`

True if this is the first poll of the tick. Read-only.


  

### `input.InputPollContext.tick_start_time`

The time at which the current tick started, in seconds. Read-only.


  

### `input.InputPollContext.time_delta`

The time since the last poll, in seconds. Read-only.


  

### `input.InputPollContext:GetViewAngles`

```lua
input.InputPollContext:GetViewAngles(): QAngle
```

Returns a copy of the view angles for this poll. The angles include the mouse input of the user and the angles set by `SetViewAngles` so far. Changing the copy does not change the poll. Pass the copy to `SetViewAngles` to apply it.


    
Call this function only inside the `input_poll` event.


  

  

### `input.InputPollContext:SetViewAngles`

```lua
input.InputPollContext:SetViewAngles(angles: QAngle)
```

Turns the view to the given angles in this poll, in the same way as mouse movement. The difference is converted with the mouse sensitivity, and there is no limit on how far the view turns in one poll. Enabled legitbot features run afterwards and can still change the angles.


| Parameter | Type | Description |
| --- | --- | --- |
| angles | `QAngle` | The target angles. They are copied into the input of this poll. |


    
Call this function only inside the `input_poll` event. The angles must be finite numbers and
the roll must be zero, otherwise the function throws an error. While the game does not control
the mouse, for example while the menu is open, the call is ignored.
