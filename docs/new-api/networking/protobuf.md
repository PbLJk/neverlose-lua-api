> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Protocol Buffers


## protobuf.MessageWrapper — object type

A protobuf message, such as the message that a `usermsg_*` event passes. Read its fields by
name. A field that the message does not declare reads as **nil**. A repeated field reads as a
table, and a field that holds a message reads as another `protobuf.MessageWrapper`.

`pairs` goes over every field that the message declares. `tostring` returns
`protobuf.Message`, where `Name` is the name of the message type.

## protobuf — global table

Shows the game's own user messages on the local client. The messages are not sent to the
server or to other players.


  

### `protobuf.TextMsg`

```lua
protobuf.TextMsg(dest: protobuf.HudPrintDest, msg: string[, param1: string, param2: string, param3: string, param4: string])
```

Shows a `TextMsg` message on the local client, in the same way as the game shows its own status messages.


| Parameter | Type | Description |
| --- | --- | --- |
| dest | `protobuf.HudPrintDest` | The place where the message is shown. Any other value throws an error. |
| msg | `string` | The text to show, or a localization token that starts with `#`. |
| param1? | `string` | The first parameter. |
| param2? | `string` | The second parameter. |
| param3? | `string` | The third parameter. |
| param4? | `string` | The fourth parameter. |


    
`msg` is plain text or a localization token that starts with `#`. The token can contain the
placeholders `%s1`, `%s2`, `%s3` and `%s4`. They are replaced by `param1`, `param2`, `param3`
and `param4`. Parameters that are **nil** are skipped, so the parameters after them move up by
one place.


  

  

### `protobuf.SayText`

```lua
protobuf.SayText(chat: boolean[, entity: Entity], text: string)
```

Shows a `SayText` chat line on the local client, as if the given player sent it.


| Parameter | Type | Description |
| --- | --- | --- |
| chat | `boolean` | Pass `true` to show the line in the chat. Pass `false` to show it only in the console. |
| entity? | `Entity` | The player who sent the line. Pass **nil** for a message without a sender. |
| text | `string` | The line to show. |


  

### `protobuf.SayText2`

```lua
protobuf.SayText2(chat: boolean, entity: Entity, messagename: string[, param1: string, param2: string, param3: string, param4: string])
```

Shows a `SayText2` chat line on the local client. This is the localized and formatted form of a chat message.


| Parameter | Type | Description |
| --- | --- | --- |
| chat | `boolean` | Pass `true` to show the line in the chat. Pass `false` to show it only in the console. |
| entity | `Entity` | The player controller who sent the line. |
| messagename | `string` | The localization token for the format of the chat line. |
| param1? | `string` | The first parameter. It is usually the name of the player. |
| param2? | `string` | The second parameter. It is usually the text of the message. |
| param3? | `string` | The third parameter. |
| param4? | `string` | The fourth parameter. |


    
`messagename` is a localization token, for example `Cstrike_Chat_All`. The placeholders `%s1`,
`%s2`, `%s3` and `%s4` in the token are replaced by `param1`, `param2`, `param3` and `param4`.


  

  

<a id="protobuf-HudPrintDest"></a>
### `protobuf.HudPrintDest`

The place where `protobuf.TextMsg` shows a message. The values are the game's own `HUD_PRINT*` constants.


    

### `protobuf.HudPrintDest`


| Name | Value | Description |
| --- | --- | --- |
| HUD_PRINTCONSOLE | 1 | The console. |
| HUD_PRINTCONSOLE2 | 2 | The console. It looks the same as `HUD_PRINTCONSOLE`. |
| HUD_PRINTTALK | 3 | The chat. |
| HUD_PRINTTALK2 | 5 | The chat. It looks the same as `HUD_PRINTTALK`. |
| HUD_PRINTHINT | 4 | A hint with low priority, in the team colour. |
| HUD_PRINTHINTERROR | 6 | A hint with high priority, in red. |
