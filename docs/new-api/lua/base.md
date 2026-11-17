> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Environment


## \_G — object type

A global variable (not a function) that holds the global environment (that is, `_G._G = _G`).
Lua itself does not use this variable; changing its value does not affect any environment, nor vice-versa.

## Functions — global functions


  

### `assert`

```lua
assert([v: T, message: any, ...: any]): T, any
```

Issues an error when the value of its argument `v` is false (i.e., **nil** or **false**); otherwise, returns all its arguments. `message` is an error message; when absent, it defaults to "assertion failed!"


| Parameter | Type | Description |
| --- | --- | --- |
| v? | `T` | Value to test. |
| message? | `any` | Error message used when `v` is false or nil. |
| ...? | `any` | Extra values returned after `v` when the assertion succeeds. |


| Return | Type | Description |
| --- | --- | --- |
|  | `T` |  |
| ... | `any` |  |


  

### `collectgarbage`

```lua
collectgarbage([opt: string, arg: integer]): (boolean|number)??
```

This function is a generic interface to the garbage collector. It performs different functions according to its first argument, opt: - **"collect":** performs a full garbage-collection cycle. This is the default option. - **"stop":** This option is ignored, and the collector keeps running. All scripts share one garbage collector, so a script cannot stop it. - **"restart":** restarts the garbage collector. - **"count":** returns the total memory in use by Lua (in Kbytes). - **"step":** performs a garbage-collection step. The step "size" is controlled by arg (larger values mean more steps) in a non-specified way. If you want to control the step size you must experimentally tune the value of arg. Returns true if the step finished a collection cycle. - **"setpause":** This option does not change the pause of the collector. It returns the current pause value. - **"setstepmul":** This option does not change the step multiplier of the collector. It returns the current step multiplier.


| Parameter | Type | Description |
| --- | --- | --- |
| opt? | `string` |  |
| arg? | `integer` |  |


    
The first time a script uses `"stop"`, `"setpause"` or `"setstepmul"`, a warning is added to the
Errors list of the script and written to the game console.


  

  

### `error`

```lua
error(message: any[, level: integer])
```

Terminates the last protected function called and returns `message` as the error message. Function `error` never returns.


| Parameter | Type | Description |
| --- | --- | --- |
| message | `any` | Error object to raise. |
| level? | `integer` | Stack level used to report the error location. |


    
Usually, `error` adds some information about the error position at the beginning of the message.
The `level` argument specifies how to get the error position.
With level 1 (the default), the error position is where the `error` function was called.
Level 2 points the error to where the function that called `error` was called; and so on.
Passing a level 0 avoids the addition of error position information to the message.


  

  

### `getmetatable`

```lua
getmetatable(object: any): table
```

If `object` does not have a metatable, returns **nil**. Otherwise, if the object's metatable has a `"__metatable"` field, returns the associated value. Otherwise, returns the metatable of the given object.


| Parameter | Type | Description |
| --- | --- | --- |
| object | `any` | Value whose metatable is queried. |


| Return | Type | Description |
| --- | --- | --- |
| metatable | `table` |  |


  

### `ipairs`

```lua
ipairs(t: T): fun(table: V[], i?: integer): integer, V, T, integer
```

Returns three values: an iterator function, the table `t`, and 0, so that the construction


| Parameter | Type | Description |
| --- | --- | --- |
| t | `T` | Table to iterate. |


| Return | Type | Description |
| --- | --- | --- |
|  | `fun(table: V[], i?: integer): integer, V` |  |
|  | `T` |  |
| i | `integer` |  |


    
for i,v in ipairs(t) do --\[\[body]] end

will iterate over the pairs (`1,t[1]`), (`2,t[2]`), ···, up to the first integer key absent from the table.


  

  

### `next`

```lua
next(table: table<K, V>[, index: K]): K?, V?
```

Allows a program to traverse all fields of a table. Its first argument is a table and its second argument is an index in this table. `next` returns the next index of the table and its associated value. When called with **nil** as its second argument, `next` returns an initial index and its associated value. When called with the last index, or with **nil** in an empty table, `next` returns **nil**. If the second argument is absent, then it is interpreted as **nil**. In particular, you can use `next(t)` to check whether a table is empty.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `table<K, V>` | Table being traversed. |
| index? | `K` | Previous key, or `nil` to start traversal. |


    
The order in which the indices are enumerated is not specified, *even for numeric indices*.
(To traverse a table in numeric order, use a numerical **for** or the `ipairs` function.)

The behavior of `next` is *undefined* if, during the traversal, you assign any value to a non-existent field in the table.
You may however modify existing fields. In particular, you may clear existing fields.


  

  

### `pairs`

```lua
pairs(t: T): fun(table: table<K, V>, index?: K): K, V, T
```

Returns three values: the `next` function, the table `t`, and **nil**, so that the construction


| Parameter | Type | Description |
| --- | --- | --- |
| t | `T` | Table to iterate. |


    
for k,v in pairs(t) do --\[\[body]] end

will iterate over all key–value pairs of table `t`.

See function `next` for the caveats of modifying the table during its traversal.


  

  

### `pcall`

```lua
pcall(f: fun(...): unknown[, arg1: any, ...: any]): boolean, any, any
```

Calls function `f` with the given arguments in _protected mode_. This means that any error inside `f` is not propagated; instead, `pcall` catches the error and returns a status code. Its first result is the status code (a boolean), which is true if the call succeeds without errors. In such case, `pcall` also returns all results from the call, after this first result. In case of any error, `pcall` returns **false** plus the error message.


| Parameter | Type | Description |
| --- | --- | --- |
| f | `fun(...): unknown` | Function to call. |
| arg1? | `any` | First argument passed to `f`. |
| ...? | `any` | Additional arguments passed to `f`. |


| Return | Type | Description |
| --- | --- | --- |
| success | `boolean` |  |
| result | `any` |  |
| ... | `any` |  |


  

### `print`

```lua
print([...: any])
```

The same function as `log.Print`. Converts its arguments to strings, joins them without a separator, and writes them as one line to the game console with the `neverlose ·` prefix. When the Lua Output option of Log Events is enabled in the menu, the line is also added to the event log on the screen. `print` is not intended for formatted output, but only as a quick way to show a value, typically for debugging. For formatted output, use `string.format`.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` | Values to print. |


  

### `rawequal`

```lua
rawequal(v1: any, v2: any): boolean
```

Checks whether `v1` is equal to `v2`, without invoking any metamethod. Returns a boolean.


| Parameter | Type | Description |
| --- | --- | --- |
| v1 | `any` | First value to compare. |
| v2 | `any` | Second value to compare. |


  

### `rawget`

```lua
rawget(table: table, index: any): any
```

Gets the real value of `table[index]`, without invoking any metamethod. `table` must be a table; `index` may be any value.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `table` | Table to read from. |
| index | `any` | Key to read. |


  

### `rawlen`

```lua
rawlen(v: table|string|userdata|ffi.cdata*): integer
```

Returns the length of the object `v`, which must be a table or a string, without invoking the `__len` metamethod. Returns an integer.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `table\|string\|userdata\|ffi.cdata*` | Object to measure. |


| Return | Type | Description |
| --- | --- | --- |
| len | `integer` |  |


  

### `rawset`

```lua
rawset(table: table, index: any, value: any): table
```

Sets the real value of `table[index]` to `value`, without invoking any metamethod. `table` must be a table, `index` any value different from **nil**, and `value` any Lua value.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `table` | Table to modify. |
| index | `any` | Key to assign. |
| value | `any` | Value to store. |


    
This function returns `table`.


  

  

### `require`

```lua
require(modname: string): unknown
```

Returns the module with the name `modname`. The name can be one of the following.


| Parameter | Type | Description |
| --- | --- | --- |
| modname | `string` | Module name to load. |


    
The name of a module from the `requirements` section of `extension.json`, such as `ffi`,
`neverlose/name` or `local/name`. These modules are loaded before the script runs, and
`require` returns the loaded module. If the module is not listed in the requirements,
`require` throws an error.

The name of a standard library, which is `math`, `bit`, `string`, `jit`, `table`, `coroutine`,
`json` or `msgpack`. `require` returns the copy of the library that the script uses.

The path of a Lua file of the script, without the `.lua` extension. The file runs the first
time it is required. Later calls return the same result without running the file again.

`table.new` or `table.clear`.

If no module has this name, or if the module throws an error while it loads, `require` throws
an error.


  

  

### `select`

```lua
select(index: integer|"#"[, ...: any]): any
```

If `index` is a number, returns all arguments after argument number `index`. Otherwise, `index` must be the string `"#"`, and `select` returns the total number of extra arguments it received.


| Parameter | Type | Description |
| --- | --- | --- |
| index | `integer\|"#"` | Argument index to select, or "#" to count arguments. |
| ...? | `any` | Values to select from. |


  

### `setmetatable`

```lua
setmetatable(table: table[, metatable: metatable|table]): table
```

Sets the metatable for the given table. (You cannot change the metatable of other types from Lua, only from C.) If `metatable` is **nil**, removes the metatable of the given table. If the original metatable has a `"__metatable"` field, raises an error.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `table` | Table to update. |
| metatable? | `metatable\|table` | New metatable, or nil to remove it. |


    
This function returns `table`.


  

  

### `tonumber`

```lua
tonumber(e: any): number?
```

Tries to convert its argument to a number. If the argument is already a number or a string convertible to a number, then `tonumber` returns this number; otherwise, it returns **nil**.


| Parameter | Type | Description |
| --- | --- | --- |
| e | `any` | Value to convert. |


    
An optional argument specifies the base to interpret the numeral.
The base may be any integer between 2 and 36, inclusive.
In bases above 10, the letter '`A`' (in either upper or lower case) represents 10, '`B`' represents 11, and so forth, with '`Z`' representing 35.
In base 10 (the default), the number can have a decimal part, as well as an optional exponent part.
In other bases, only unsigned integers are accepted.


  

  

### `tostring`

```lua
tostring(v: any): string
```

Receives an argument of any type and converts it to a string in a reasonable format. For complete control of how numbers are converted, use `string.format`.


| Parameter | Type | Description |
| --- | --- | --- |
| v | `any` | Value to convert. |


    
If the metatable of `e` has a `"__tostring"` field, then `tostring` calls the corresponding value with `e` as argument, and uses the result of the call as its result.


  

  

### `xpcall`

```lua
xpcall(f: fun(...): unknown, msgh: function[, arg1: any, ...: any]): boolean, any, any
```

This function is similar to `pcall`, except that you can set a new error handler.


| Parameter | Type | Description |
| --- | --- | --- |
| f | `fun(...): unknown` | Function to call. |
| msgh | `function` | Error handler called with the error object. |
| arg1? | `any` | First argument passed to `f`. |
| ...? | `any` | Additional arguments passed to `f`. |


| Return | Type | Description |
| --- | --- | --- |
| success | `boolean` |  |
| result | `any` |  |
| ... | `any` |  |


    
`xpcall` calls function `f` in protected mode, using `err` as the error handler.
Any error inside `f` is not propagated; instead, `xpcall` catches the error, calls the `err` function with the original error object, and returns a status code.
Its first result is the status code (a boolean), which is true if the call succeeds without errors.
In this case, `xpcall` also returns all results from the call, after this first result.
In case of any error, `xpcall` returns **false** plus the result from `err`.


  

  

### `unpack`

```lua
unpack(list: table[, i: integer, j: integer]): T1, T2, T3, T4, T5, T6, T7, T8, T9, T10
```

Returns the elements from the given table. This function is equivalent to


| Parameter | Type | Description |
| --- | --- | --- |
| list | `table` |  |
| i? | `integer` | First index to unpack. |
| j? | `integer` | Last index to unpack. |


    
return list\[i], list\[i+1], ···, list\[j]

except that the above code can be written only for a fixed number of elements.
By default, `i` is 1 and `j` is the length of the list, as defined by the length operator.


  

  

### `type`

```lua
type(v: any): "boolean"|"cdata"|"function"|"nil"|"number"|"string"|"table"|"thread"|"userdata"
```

Returns the type of its only argument, coded as a string. The possible results of this function are "`nil`" (a string, not the value **nil**), "`number`", "`string`", "`boolean`", "`table`", "`function`", "`thread`", "`userdata`", and "`cdata`".


| Parameter | Type | Description |
| --- | --- | --- |
| v | `any` | Value to inspect. |


    
There are nine basic types in LuaJIT: *nil*, *boolean*, *number*, *string*, *function*, *userdata*, *thread*, *table*, and *cdata*.


  

  

### `inext`

```lua
inext(table: V[][, index: integer]): integer, V
```

The iterator function that `ipairs` returns. It walks the array part of a table, in the same way as `next` walks all keys.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `V[]` | The table to iterate over. |
| index? | `integer` | The previous index. Pass `0` to start at index `1`. If no number is given, the function throws an error. |


    
Given a table and an index `i`, it returns `i + 1` and the value at index `i + 1`. When that
value is **nil**, it returns nothing and the loop ends. `for i, v in inext, t, 0 do end` works
in the same way as `for i, v in ipairs(t) do end`.


  

  

### `defer`

```lua
defer(callback: function[, ...: any])
```

Registers a cleanup function for the current script. The arguments are passed to the function exactly as given, including **nil** values at the end.


| Parameter | Type | Description |
| --- | --- | --- |
| callback | `function` | The cleanup function. It must be a function. Tables with a `__call` metamethod and other values are not accepted. |
| ...? | `any` | The arguments to pass to the cleanup function. |


    
The cleanup functions run when the script is unloaded, reloaded, or fails to start. They run
after the `shutdown` callbacks and before the resources of the script are released. The last
function registered runs first. If one function throws an error, the error is logged and the
other functions still run.

If a module fails to load, the cleanup functions that it registered run at once. Functions
that are registered while the script is already cleaning up are ignored.


  

  

### `traceback`

```lua
traceback([message: string]): string
```

Builds a stack traceback for the place where it is called, with `message` in front of it. Use it as the message handler of `xpcall`. The handler runs inside the failing call, so it can still see the stack of that call.


| Parameter | Type | Description |
| --- | --- | --- |
| message? | `string` | The text to put in front of the traceback. |


| Return | Type | Description |
| --- | --- | --- |
|  | `string` | The message and the traceback. Each frame is on its own line and starts with a tab. |


    
Each frame names its file in the form `My Script/main.lua:12`. A file that comes from a
dependency is named after the dependency, for example `local/bar/util.lua:5`.

Deep stacks are shortened. The first 12 frames and the last 10 frames are kept, and a line
such as `... 30 more frames` replaces the frames between them.

If `message` already has a traceback in it, it is returned unchanged. If `message` is not a
string, for example a table or **nil**, it is returned unchanged. If you call `traceback` with
no arguments, the result is only the traceback.

Only developer scripts have this function. Market scripts do not have it.


  

  

### `perf`

```lua
perf(): ScriptPerformance?
```

Returns how much time and memory the code of this script used in the last measuring window. These are the numbers that the scripts list shows. A window is about one second long.


| Return | Type | Description |
| --- | --- | --- |
|  | `ScriptPerformance?` | The values of the last window, or `nil` if no window has ended yet. |


    
The values are totals for the whole window. They are not values per second. Divide a total
by `window_ms` to get a rate. The values change only when a new window ends. Use `window` to
tell one window from the next.

`freed_kb` is the memory that was released while the code of this script ran. Most of it is
released by the garbage collector, and it can include garbage of other scripts. When
`freed_kb` is high, part of `self_ms` is time that the garbage collector used.

Returns `nil` until the first window has ended. Only developer scripts have this function,
in the same way as `traceback`.


  

  

### `printf`

```lua
printf(text: string[, ...: any])
```

Formats a message with `string.format` and passes the result to `print`.


| Parameter | Type | Description |
| --- | --- | --- |
| text | `string` | The format string. It follows the rules of `string.format`. |
| ...? | `any` | The values to put into the format string. |


  

### `toticks`

```lua
toticks(time: number): integer
```

Converts a time in seconds to a number of ticks. There are 64 ticks in one second.


| Parameter | Type | Description |
| --- | --- | --- |
| time | `number` | The time in seconds. |


    
The result is rounded in the same way as the engine's `TIME_TO_TICKS` macro. Half a tick is
added to the value, and then the fractional part is removed, rounding toward zero.


  

  

### `totime`

```lua
totime(ticks: number): number
```

Converts a number of ticks to a time in seconds. There are 64 ticks in one second.


| Parameter | Type | Description |
| --- | --- | --- |
| ticks | `number` | The number of ticks. |


## nil — object type

*Nil* is the type of the value **nil**, whose main property is to be different from any other value; it usually represents the absence of a useful value.

## boolean — object type

*Boolean* is the type of the values **false** and **true**.
Both **nil** and **false** make a condition false; any other value makes it true.

## number — object type

*Number* represents real (double-precision floating-point) numbers.

## integer — object type


*Integer* isn't an actual Lua type, but it can either mean an integer Lua `number` or LuaJIT `cdata` 64-bit integer, i.e. `cdata<int64_t>`/`cdata<uint64_t>`.

## Types — types


  

<a id="int64_t"></a>
### `int64_t`

A signed 64-bit integer. Values that exceed the range of a Lua `number` are represented as a boxed `cdata<int64_t>` rather than a plain `number`, so full 64-bit precision is preserved. Can be declared using the `LL` suffix, which stands for `long long`.


  

<a id="uint64_t"></a>
### `uint64_t`

An unsigned 64-bit integer. Values that exceed the range of a Lua `number` are represented as a boxed `cdata<uint64_t>` rather than a plain `number`, so full 64-bit precision is preserved. Can be declared using the `ULL` suffix, which stands for `unsigned long long`.


## string — object type

*String* represents arrays of characters.
Lua is 8-bit clean: strings can contain any 8-bit character, including embedded zeros ('`\0`')

## userdata — object type

The type *userdata* is provided to allow arbitrary C data to be stored in Lua variables.
This type corresponds to a block of raw memory and has no pre-defined operations in Lua, except assignment and identity test.
However, by using *metatables*, the programmer can define operations for userdata values.
Userdata values cannot be created or modified in Lua, only through the C API.
This guarantees the integrity of data owned by the host program.

Use `ffi.cast` to convert a userdata value to a pointer type. Do this to work with an
address returned by a pattern search or an interface lookup.

## function — object type

A callable Lua function or C function exposed to Lua.

## metatable — object type

Metatable fields that customize operations on Lua values.

`__gc` runs for userdata and cdata only, never for tables.


  

### `metatable.__add`

Handles addition.


  

### `metatable.__call`

Handles calls on non-function values.


  

### `metatable.__concat`

Handles concatenation.


  

### `metatable.__div`

Handles division.


  

### `metatable.__eq`

Handles equality comparison.


  

### `metatable.__gc`

Finalizer called when userdata is collected.


  

### `metatable.__index`

Handles reads for missing keys.


  

### `metatable.__le`

Handles less-than-or-equal comparison.


  

### `metatable.__len`

Handles the length operator.


  

### `metatable.__lt`

Handles less-than comparison.


  

### `metatable.__metatable`

Value returned by `getmetatable` and used to protect the metatable.


  

### `metatable.__mod`

Handles modulo.


  

### `metatable.__mode`

Weak table mode for values, keys, or both.


  

### `metatable.__mul`

Handles multiplication.


  

### `metatable.__newindex`

Handles writes to missing keys.


  

### `metatable.__pow`

Handles exponentiation.


  

### `metatable.__sub`

Handles subtraction.


  

### `metatable.__tostring`

Called by `tostring` to produce a string representation.


  

### `metatable.__unm`

Handles unary minus.


## ScriptPerformance — object type

The table that `perf` returns.


  

### `ScriptPerformance.alloc_kb`

The memory that the code of this script allocated during the window, in KB. Memory that was freed is not subtracted.


  

### `ScriptPerformance.calls`

The number of callbacks that ran during the window.


  

### `ScriptPerformance.freed_kb`

The memory that was freed while the code of this script ran, in KB. Most of it is freed by the garbage collector.


  

### `ScriptPerformance.load_ms`

The time that `main.lua` took the last time it ran, in milliseconds. It is not part of the window.


  

### `ScriptPerformance.long_calls`

The number of calls whose own code took 50 ms or more. The player sees each of these calls as a frozen frame.


  

### `ScriptPerformance.max_ms`

The time of the longest single call, in milliseconds. Only the code of this script is counted.


  

### `ScriptPerformance.self_ms`

The time spent in the code of this script during the window, in milliseconds.


  

### `ScriptPerformance.share`

`self_ms` divided by the real length of the window. The value is from 0 to 1.


  

### `ScriptPerformance.total_ms`

The same as `self_ms`, plus the time spent in code of other scripts that this script called, in milliseconds.


  

### `ScriptPerformance.window`

A number that changes each time a new window ends.


  

### `ScriptPerformance.window_ms`

The real length of the window, in milliseconds.


  

### `ScriptPerformance.worst_event`

The event that the longest call ran for, such as `"render"`. It is `nil` if there were no calls.
