> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# JIT


<a id="jit-1"></a>

## jit  — global table


The `jit` library controls the LuaJIT just-in-time compiler at runtime.
You can use it through the global `jit` or get it with `require("jit")`.


  

### `jit.arch`

Target CPU architecture.


  

### `jit.os`

Target OS name.


  

### `jit.version`

LuaJIT version string


  

### `jit.version_num`

Numeric version


  

### `jit.on`

```lua
jit.on([func: function|true, recursive: boolean])
```

Enables JIT compilation for the function `func`. Pass `true` to select the function that calls `jit.on`.


| Parameter | Type | Description |
| --- | --- | --- |
| func? | `function\|true` | The function to enable, or `true` for the calling function. |
| recursive? | `boolean` | Whether to also enable sub-functions recursively. |


    
If `recursive` is `true`, the function and all functions defined inside it are selected. If
`recursive` is `false`, only the functions defined inside it are selected. If `recursive` is
omitted, only the function itself is selected.

All scripts share one JIT compiler, so a call without a function, or with `nil`, is ignored.
In a developer extension, the first ignored call also adds a warning to the Errors list of the
script. If `func` is any other value that is not a function, an error is thrown.


  

  

### `jit.off`

```lua
jit.off([func: function|true, recursive: boolean])
```

Disables JIT compilation for the function `func`. Pass `true` to select the function that calls `jit.off`.


| Parameter | Type | Description |
| --- | --- | --- |
| func? | `function\|true` | The function to disable, or `true` for the calling function. |
| recursive? | `boolean` | Whether to also disable sub-functions recursively. |


    
If `recursive` is `true`, the function and all functions defined inside it are selected. If
`recursive` is `false`, only the functions defined inside it are selected. If `recursive` is
omitted, only the function itself is selected.

All scripts share one JIT compiler, so a call without a function, or with `nil`, is ignored.
In a developer extension, the first ignored call also adds a warning to the Errors list of the
script. If `func` is any other value that is not a function, an error is thrown.


  

  

### `jit.flush`

```lua
jit.flush([func: function|true, recursive: boolean])
```

Flushes the compiled JIT code of the function `func`. Pass `true` to select the function that calls `jit.flush`. Pass a trace number to flush only that trace.


| Parameter | Type | Description |
| --- | --- | --- |
| func? | `function\|true` | The function to flush, or `true` for the calling function. |
| recursive? | `boolean` | Whether to also flush sub-functions recursively. |


    
If `recursive` is `true`, the function and all functions defined inside it are selected. If
`recursive` is `false`, only the functions defined inside it are selected. If `recursive` is
omitted, only the function itself is selected.

All scripts share one JIT compiler, so a call without a function, or with `nil`, is ignored.
In a developer extension, the first ignored call also adds a warning to the Errors list of the
script. If `func` is any other value that is not a function, an error is thrown.


  

  

### `jit.status`

```lua
jit.status(): boolean, string
```

Returns the current JIT status. The first return value is `true` if the JIT compiler is enabled. Subsequent return values are strings describing enabled CPU features and optimizations.


| Return | Type | Description |
| --- | --- | --- |
| status | `boolean` |  |
| ... | `string` |  |
