> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Cheat Events


  

### `aim_ack`

```lua
events.aim_ack:Set(callback: fun(shot: ragebot.Shot))
```


| Parameter | Type | Description |
| --- | --- | --- |
| shot | `ragebot.Shot` | A shot record, passed to `events.aim_fire` and `events.aim_ack`. |


  

### `aim_fire`

```lua
events.aim_fire:Set(callback: fun(shot: ragebot.Shot))
```


| Parameter | Type | Description |
| --- | --- | --- |
| shot | `ragebot.Shot` | A shot record, passed to `events.aim_fire` and `events.aim_ack`. |


  

### `config_state`

```lua
events.config_state:Set(callback: fun(state: events.ConfigState))
```


| Parameter | Type | Description |
| --- | --- | --- |
| state | `string` | The step of a config load or a config save that `config_state` passes. |


Accepted values for `state`:


| Value | Type / default | Description |
| --- | --- | --- |
| "pre_load" |  | A config was requested. Every option will be replaced next. |
| "post_load" |  | The config is applied, and `cloud.GetConfig()` returns it. This also fires for a config that was rejected, because every option was reset first. |
| "pre_save" |  | The options will be written into the config next. Changes that you make here are saved. |
| "post_save" |  | The options were written. This fires before the server confirms the save. |


  

### `console_input`

```lua
events.console_input:Set(callback: fun(text: string): false?)
```

Fires for a line that is entered in the game console or in VConsole. Return `false` to block the line.


| Parameter | Type | Description |
| --- | --- | --- |
| text | `string` | _String_ represents arrays of characters. |


  

### `createmove`

```lua
events.createmove:Set(callback: fun(cmd: UserCmd, player: simulation.Player))
```

Fires last for each command, after `post_movement`. Read or change the input here before the command is finalized.


| Parameter | Type | Description |
| --- | --- | --- |
| cmd | `UserCmd` | The input command that the client sends to the server every tick. |
| player | `simulation.Player` | A snapshot of a player for prediction. |


  

### `display_mode_changed`

```lua
events.display_mode_changed:Set(callback: fun(mode: engine.DisplayMode))
```

Fires when the game applies a new display mode. A new resolution, window mode, vsync setting or MSAA setting changes the display mode. `mode` and `engine.GetDisplayMode()` already hold the new mode. `engine.GetScreenSize()` returns the new size from the next frame.


| Parameter | Type | Description |
| --- | --- | --- |
| mode | `engine.DisplayMode` | A display mode copied from the engine. |


  

### `entity_created`

```lua
events.entity_created:Set(callback: fun(ent: client.C_BaseEntity))
```

Fires when the first networked data of a new entity has been applied. It fires just before `entity_networked` for the same entity.


| Parameter | Type | Description |
| --- | --- | --- |
| ent | `client.C_BaseEntity` |  |


  

### `entity_created_early`

```lua
events.entity_created_early:Set(callback: fun(ent: client.C_BaseEntity))
```

Fires early while an entity is created. At this time, not all networked fields of the entity are available.


| Parameter | Type | Description |
| --- | --- | --- |
| ent | `client.C_BaseEntity` |  |


  

### `entity_deleted`

```lua
events.entity_deleted:Set(callback: fun(ent: client.C_BaseEntity))
```

Fires when an entity is deleted. Read the entity only during the callback.


| Parameter | Type | Description |
| --- | --- | --- |
| ent | `client.C_BaseEntity` |  |


  

### `entity_networked`

```lua
events.entity_networked:Set(callback: fun(ent: client.C_BaseEntity))
```

Fires when networked data of an entity has been applied.


| Parameter | Type | Description |
| --- | --- | --- |
| ent | `client.C_BaseEntity` |  |


  

### `execute_client_cmd`

```lua
events.execute_client_cmd:Set(callback: fun(text: string): false|string)
```

Fires when the game or its UI runs a command line, for example `say "hello"` from the chat box. `text` is the whole line. It can contain several commands separated by `;`.


| Parameter | Type | Description |
| --- | --- | --- |
| text | `string` | _String_ represents arrays of characters. |


    
Return `false` to block the line. Return a string to run that string instead. If one listener
returns `false`, the line is blocked even if other listeners return a string. If several
listeners return a string, the string of the last listener is used.

Lines that are typed in the console, key binds and commands that scripts run do not fire this
event.


  

  

### `input_poll`

```lua
events.input_poll:Set(callback: fun(input: input.InputPollContext))
```

Read or change the current input poll inside this callback. Do not keep the context after the callback returns.


| Parameter | Type | Description |
| --- | --- | --- |
| input | `input.InputPollContext` | The argument of the `input_poll` event. |


  

### `level_init`

```lua
events.level_init:Set(callback: fun())
```

Fires when the client is fully connected to a level. It also fires when the client reconnects to the same map.


  

### `mouse_input`

```lua
events.mouse_input:Set(callback: fun(mouse: events.MouseInput): boolean?)
```

Fires for every mouse update. Return `false` to block the input, so that the game and the menu do not receive it. Any other return value lets the input through.


  

### `override_view`

```lua
events.override_view:Set(callback: fun(view: view.ViewContext))
```

Read or change the camera inside this callback. Do not keep the context after the callback returns.


| Parameter | Type | Description |
| --- | --- | --- |
| view | `view.ViewContext` | The camera of the current frame. |


  

### `override_viewmodel`

```lua
events.override_viewmodel:Set(callback: fun(viewmodel: view.ViewmodelContext))
```

Read or change the root of the first person viewmodel in each frame. Do not keep the context after the callback returns.


| Parameter | Type | Description |
| --- | --- | --- |
| viewmodel | `view.ViewmodelContext` | The root of the first person viewmodel. |


  

### `post_data_update`

```lua
events.post_data_update:Set(callback: fun())
```

Fires after the networked data of all entities in an update has been applied. It fires after every `entity_networked` event of that update.


  

### `post_movement`

```lua
events.post_movement:Set(callback: fun(cmd: UserCmd, player: simulation.Player))
```

Fires for each command, after `pre_movement` and before `createmove`.


| Parameter | Type | Description |
| --- | --- | --- |
| cmd | `UserCmd` | The input command that the client sends to the server every tick. |
| player | `simulation.Player` | A snapshot of a player for prediction. |


  

### `post_update_viewmodel`

```lua
events.post_update_viewmodel:Set(callback: fun(arms: client.C_CS2HudModelArms, weapon: client.C_CS2HudModelWeapon))
```

Fires after the first person HUD arms are placed and their animation is evaluated for this frame. Attachments that you read here match the current pose. Use `SetAbsAngles` and `SetAbsOrigin` to move both roots.


| Parameter | Type | Description |
| --- | --- | --- |
| arms | `client.C_CS2HudModelArms` |  |
| weapon | `client.C_CS2HudModelWeapon` |  |


  

### `pre_movement`

```lua
events.pre_movement:Set(callback: fun(cmd: UserCmd, player: simulation.Player))
```

Fires for each command, before `post_movement`. Changes that you make here can still be overwritten before the command is sent. Clone the simulation that you receive before you advance it.


| Parameter | Type | Description |
| --- | --- | --- |
| cmd | `UserCmd` | The input command that the client sends to the server every tick. |
| player | `simulation.Player` | A snapshot of a player for prediction. |


  

### `ready_for_match`

```lua
events.ready_for_match:Set(callback: fun())
```

Fires when the ready prompt of the lobby appears for a match that was found.


  

### `render`

```lua
events.render:Set(callback: fun())
```


  

### `shutdown`

```lua
events.shutdown:Set(callback: fun(reason: events.ShutdownReason))
```


| Parameter | Type | Description |
| --- | --- | --- |
| reason | `string` | The reason why `shutdown` fired. |


Accepted values for `reason`:


| Value | Type / default | Description |
| --- | --- | --- |
| "unload" |  | The script stops. It was turned off or removed, its code failed, or the cheat is closing. A change of settings that restarts the script also gives `"unload"`. |
| "reload" |  | The files of the script changed, or the files of a local library that it requires changed. The new code of the script runs next. |
| "refresh" |  | Another script in the same runtime was turned on, turned off, or reloaded. This script runs again next. |


  

### `usermsg_call_vote_failed`

```lua
events.usermsg_call_vote_failed:Set(callback: fun(msg: CCSUsrMsg_CallVoteFailed))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_CallVoteFailed` |  |


  

### `usermsg_report_hit`

```lua
events.usermsg_report_hit:Set(callback: fun(msg: CCSUsrMsg_ReportHit))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_ReportHit` |  |


  

### `usermsg_say_text`

```lua
events.usermsg_say_text:Set(callback: fun(msg: CUserMessageSayText2))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CUserMessageSayText2` |  |


  

### `usermsg_vote_failed`

```lua
events.usermsg_vote_failed:Set(callback: fun(msg: CCSUsrMsg_VoteFailed))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_VoteFailed` |  |


  

### `usermsg_vote_pass`

```lua
events.usermsg_vote_pass:Set(callback: fun(msg: CCSUsrMsg_VotePass))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_VotePass` |  |


  

### `usermsg_vote_setup`

```lua
events.usermsg_vote_setup:Set(callback: fun(msg: CCSUsrMsg_VoteSetup))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_VoteSetup` |  |


  

### `usermsg_vote_start`

```lua
events.usermsg_vote_start:Set(callback: fun(msg: CCSUsrMsg_VoteStart))
```


| Parameter | Type | Description |
| --- | --- | --- |
| msg | `CCSUsrMsg_VoteStart` |  |
