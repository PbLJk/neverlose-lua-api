> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Memory


<a id="memory-1"></a>

## memory  — global table


Finds game interfaces and searches the memory of loaded modules for byte patterns.


**Warning:** 
These functions are for advanced users. They return raw native addresses. If you use a wrong
pattern or a wrong address, the game will crash. The script must list `ffi` in the requirements
of its `extension.json`. Without it, these functions are **nil**.


  

### `memory.CreateInterface`

```lua
memory.CreateInterface(module: string, interface: string): userdata?
```

Returns a game interface that a loaded module exports. Returns **nil** if the module is not loaded or does not export an interface with this name.


| Parameter | Type | Description |
| --- | --- | --- |
| module | `string` | The name of a loaded module, for example `engine2.dll`. |
| interface | `string` | The name of the interface, for example `Source2EngineToClient001`. |


    
Interface names can change after game updates.


  

  

### `memory.FindPattern`

```lua
memory.FindPattern(module: string, pattern: string[, find_all: boolean]): userdata
```

Searches a loaded module for a byte pattern and returns the addresses where it is found. By default, only the first match is returned. If the module is not loaded, nothing is returned.


| Parameter | Type | Description |
| --- | --- | --- |
| module | `string` | The name of a loaded module. |
| pattern | `string` | A byte pattern in IDA style, for example `48 8B ? ?`. Use `?` for a byte that can have any value. |
| find_all? | `boolean` | Pass `true` to search the whole module and return every match. This is much slower. The default is `false`, which stops at the first match. |


| Return | Type | Description |
| --- | --- | --- |
| ... | `userdata` | Each match is a separate return value, in order from the lowest address to the highest. If the pattern is not found, nothing is returned. Use `local results = {memory.FindPattern(module, pattern, true)}` to put all matches in a table. |


  

### `memory.BindVirtual`

```lua
memory.BindVirtual(module: string, interface: string, index: integer[, ...: ffi.ct**]): function
```

Creates a Lua function that calls a virtual function of an interface.


| Parameter | Type | Description |
| --- | --- | --- |
| module | `string` | The name of a loaded module, for example `client.dll`. |
| interface | `string` | The name of the interface, for example `Source2EngineToClient001`. |
| index | `integer` | The slot index of the function in the virtual table. |
| ...? | `ffi.ct**` | The C type of the function, given as the arguments that `ffi.typeof` takes. This is a declaration string, which can be followed by values for its `$` parameters. |


    
The function finds `interface` in `module`, reads the function pointer at slot `index` of the
virtual table of the interface, and casts it to the given C type. The interface instance is
stored in the returned function, so you do not pass the `this` pointer when you call it.

Throws an error if the interface is not found or the C type is not valid. The slot index and
the C type must match the interface in the loaded module.

This function exists only in scripts that have access to `ffi`.


  

  

### `memory.VirtualThunk`

```lua
memory.VirtualThunk(index: integer[, ...: ffi.ct**]): function
```

Creates a Lua function that calls a virtual function on any instance that you pass to it.


| Parameter | Type | Description |
| --- | --- | --- |
| index | `integer` | The slot index of the function in the virtual table. |
| ...? | `ffi.ct**` | The C type of the function, given as the arguments that `ffi.typeof` takes. This is a declaration string, which can be followed by values for its `$` parameters. |


    
The returned function takes the instance pointer as its first argument. When you call it, it
reads slot `index` of the virtual table of that instance. You can use it with every object
that has the same virtual table layout. `memory.BindVirtual` instead stores one instance in
the returned function.

Throws an error if the C type is not valid. The returned function throws an error if the
instance is nil or a null pointer. The slot index and the C type must match every instance
that you pass.

This function exists only in scripts that have access to `ffi`.


  

  

### `memory.BindPattern`

```lua
memory.BindPattern(module: string, interface: string, signature: string[, ...: ffi.ct**]): function
```

Creates a Lua function that calls a function found by an IDA style byte pattern.


| Parameter | Type | Description |
| --- | --- | --- |
| module | `string` | The name of a loaded module, for example `client.dll`. |
| interface | `string` | The name of the interface, for example `Source2EngineToClient001`. |
| signature | `string` | An IDA style byte pattern with `?` wildcards, for example `48 8B ? ?`. |
| ...? | `ffi.ct**` | The C type of the function, given as the arguments that `ffi.typeof` takes. This is a declaration string, which can be followed by values for its `$` parameters. |


    
The function finds `interface` in `module` to get the instance. Then it searches `module` for
`signature` to find the address of the function and casts that address to the given C type.
The interface instance is stored in the returned function and is passed as the first argument
when you call it.

Throws an error if the interface is not found, the pattern is not found, or the C type is not
valid. The pattern and the C type must match the function in the loaded module.

This function exists only in scripts that have access to `ffi`.
