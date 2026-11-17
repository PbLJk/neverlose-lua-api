> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Console


<a id="console-1"></a>

## console  — global table


Gives access to console variables and console commands by their names in the engine.
Indexing this table with a name returns one of three objects.

If a console variable with this name is registered, a `console.Variable` is returned.
Otherwise, if a console command with this name is registered, a `console.Command` is returned.
Otherwise, a `console.CommandLine` is returned. You can call it, but it is not an engine object.
Names are not case sensitive.

Every lookup returns an object, so you cannot check for `nil` to find out whether a name is
registered. Check the `is_valid` field instead.

`pairs(console)` goes over the registered variables and commands only. Each value it returns
is the engine object for that name.

Lookups are not cached. A `console.CommandLine` that you keep in a variable stays a
`console.CommandLine`. If a variable or command with that name is registered later, a new
lookup returns the new engine object.


  

### `console[string]`


  

### `console.Execute`

```lua
console.Execute([...: any])
```

Runs a command line in the client console. The arguments are converted to strings and joined with spaces, so `console.Execute("buy", "ak47")` runs `buy ak47`. Calling a `console.CommandLine` does the same thing, with its name added at the start of the line.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` | The parts of the command line. |


  

### `console.ConVarType_t`

The data types that a console variable can have. The `type` field of `console.Variable` holds one of these values.


    

### `console.ConVarType_t`


| Name | Value | Description |
| --- | --- | --- |
| INVALID | -1 |  |
| BOOL | 0 |  |
| INT16 | 1 |  |
| UINT16 | 2 |  |
| INT32 | 3 |  |
| UINT32 | 4 |  |
| INT64 | 5 |  |
| UINT64 | 6 |  |
| FLOAT32 | 7 |  |
| FLOAT64 | 8 |  |
| UTLSTRING | 9 |  |
| COLOR | 10 |  |
| VECTOR2D | 11 |  |
| VECTOR3D | 12 |  |
| VECTOR4D | 13 |  |
| QANGLE | 14 |  |
| COUNT | 15 |  |


  

  

### `console.ConVarFlags_t`

The flag bits of a console variable or command, as found in the `flags` field of `console.Object`. Use `bit.band` to test them.


    

### `console.ConVarFlags_t`


| Name | Value | Description |
| --- | --- | --- |
| NONE | 0 |  |
| LINKED_CONCOMMAND | 1 |  |
| DEVELOPMENTONLY | 2 | Hidden and locked outside development builds |
| GAMEDLL | 4 | Defined by the server |
| CLIENTDLL | 8 | Defined by the client |
| HIDDEN | 16 | Hidden from listings and completion |
| PROTECTED | 32 | Value is not sent to clients |
| SPONLY | 64 | Single player only |
| ARCHIVE | 128 | Saved to the config file |
| NOTIFY | 256 | Changes are announced to players |
| USERINFO | 512 | Sent to the server as user info |
| PLACEHOLDER | 1024 |  |
| UNLOGGED | 2048 |  |
| IS_REGISTERING | 4096 |  |
| REPLICATED | 8192 | Server value is replicated to clients |
| CHEAT | 16384 | Requires sv_cheats |
| PER_USER | 32768 |  |
| DEMO | 65536 | Recorded into demos |
| DONTRECORD | 131072 | Never recorded into demos |
| CHANGE_CALLBACK_OCCURRING | 262144 |  |
| RELEASE | 524288 | Available in release builds |
| MENUBAR_ITEM | 1048576 |  |
| SCRIPTABLE | 2097152 |  |
| NOT_CONNECTED | 4194304 | Cannot be changed while connected |
| VCONSOLE_FUZZY_MATCHING | 8388608 |  |
| SERVER_CAN_EXECUTE | 16777216 | The server may run it on clients |
| CLIENT_CAN_EXECUTE | 33554432 | Clients may run it |
| SERVER_CANNOT_QUERY | 67108864 | The server cannot query the value |
| VCONSOLE_SET_FOCUS | 134217728 |  |
| CLIENTCMD_CAN_EXECUTE | 268435456 | Client commands may run it |
| EXECUTE_PER_TICK | 536870912 |  |
| DO_NOT_SNAPSHOT | 1073741824 |  |
| GC_TO_GC_SYNCHRONIZED | 2147483648 |  |
| DEVELOPMENTONLY_IMPLICIT | 4294967296 |  |


  


## console.Object — object type

The base class of console variables and console commands. All of its fields are read-only.


  

### `console.Object.flags`

The flag bits, as `console.ConVarFlags_t` values.


  

### `console.Object.help`

The registered help text, or `nil` if there is no help text.


  

### `console.Object.info`

A pointer to the registration data of the object.


  

### `console.Object.is_valid`

Whether the object refers to a valid engine object.


  

### `console.Object.name`

The registered name.


## console.Command — object type · callable


A registered console command. When you call it, the registered callback of the command runs
directly. The arguments are converted to strings and passed to the command as its arguments,
so `console.buy("ak47")` runs `buy ak47`.


  

<a id="consolecommand"></a>
### `console.Command(...)`

```lua
console.Command([...: any])
```


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` |  |


## console.CommandLine — object type · callable

A name that has no registered variable or command. When you call it, the line `name args...`
is run in the client console, so `console.drop()` does the same as `console.Execute("drop")`.
The arguments are converted to strings and joined with spaces. The engine decides whether the
line has any effect.

This class does not inherit from `console.Object`. It has no engine object, so it has no
`flags`, `info` or `help` fields.


  

<a id="consolecommandline"></a>
### `console.CommandLine(...)`

```lua
console.CommandLine([...: any])
```


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` |  |


  

### `console.CommandLine.is_valid`

Always `false`.


  

### `console.CommandLine.name`

The name that was looked up.


## console.Variable — object type


A console variable, also called a ConVar.


  

### `console.Variable.default`

The default value of the variable. Read-only.


  

### `console.Variable.max`

The maximum value of the variable. Read-only.


  

### `console.Variable.min`

The minimum value of the variable. Read-only.


  

### `console.Variable.type`

The data type of the value, as a `console.ConVarType_t` value. Read-only.


  

<a id="console-Variable-Value"></a>
### `console.Variable.value`

The current value of the variable. Its Lua type depends on the data type of the variable. You can assign a new value to this field.


  

<a id="console-Variable-Value"></a>
### `console.Variable.Value`

The Lua type of a console value depends on the registered type of the variable.
