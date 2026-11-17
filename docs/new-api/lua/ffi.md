> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# FFI


<a id="ffi-1"></a>

## ffi  — global table


The `ffi` library lets you call external C functions and use C data structures from pure Lua code.
To use this library, add `ffi` to the `requirements` section of `extension.json`.


  

### `ffi.C`

Default C namespace. Resolves symbols from the default set of loaded libraries.


  

### `ffi.arch`

Target architecture string (e.g. `"x64"`).


  

### `ffi.os`

Target OS name string (e.g. `"Windows"`).


  

### `ffi.cdef`

```lua
ffi.cdef(def: string[, params: any, ...: unknown])
```

Adds multiple C declarations for types, external variables, or external functions. `def` is a string holding one or more C declarations, separated by semicolons. Additional arguments substitute `$` placeholders in parameterized declarations, in order.


| Parameter | Type | Description |
| --- | --- | --- |
| def | `string` | C declarations to parse and add to the FFI. |
| params? | `any` | Optional parameters for parameterized type definitions. |
| ...? | `unknown` |  |


  

### `ffi.load`

```lua
ffi.load(name: string[, global: boolean]): ffi.C.namespace*
```

Loads the dynamic library at the given path or name and returns a new C library namespace. On POSIX systems, `global=true` makes symbols globally visible. The flag is ignored on Windows.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | Library path or name to load. |
| global? | `boolean` | Whether to also load symbols into the global C namespace. |


| Return | Type | Description |
| --- | --- | --- |
| clib | `ffi.C.namespace*` |  |


  

### `ffi.new`

```lua
ffi.new(ct: ffi.ct**[, nelem: integer, init: any, ...: unknown]): ffi.cdata*
```

Creates a new C data object with the given C type and optional initial value. For VLAs, `nelem` specifies the number of elements.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type specifier (declaration string, ctype, or cdata). |
| nelem? | `integer` | Number of elements for variable-length arrays. |
| init? | `any` | Initial value or initializer list. |
| ...? | `unknown` |  |


| Return | Type | Description |
| --- | --- | --- |
| cdata | `ffi.cdata*` |  |


  

### `ffi.typeof`

```lua
ffi.typeof(ct: ffi.ct**[, params: any, ...: unknown]): ffi.ctype**
```

Creates a C type object for the given C type specifier. Caching the result of `ffi.typeof` and using it repeatedly is more efficient than passing strings directly.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type specifier. |
| params? | `any` | Optional parameters for parameterized types. |
| ...? | `unknown` |  |


| Return | Type | Description |
| --- | --- | --- |
| ctype | `ffi.ctype**` |  |


  

### `ffi.cast`

```lua
ffi.cast(ct: ffi.ct**, init: any): ffi.cdata*
```

Casts a C data object to a different C type. This is a low-level, unsafe operation — no bounds or type checking is performed.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | Target C type to cast to. |
| init | `any` | C data object or value to cast. |


| Return | Type | Description |
| --- | --- | --- |
| cdata | `ffi.cdata*` |  |


  

### `ffi.metatype`

```lua
ffi.metatype(ct: ffi.ct**, metatable: table): ffi.ctype**
```

Attaches a metatable to a C type, enabling Lua-style OOP on C structures. Only one metatable can be attached per type. This cannot be changed afterwards.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type to attach the metatable to. |
| metatable | `table` | Metatable to attach. |


| Return | Type | Description |
| --- | --- | --- |
| ctype | `ffi.ctype**` |  |


  

### `ffi.gc`

```lua
ffi.gc(cdata: ffi.cdata*[, finalizer: function]): ffi.cdata*
```

Attaches a finalizer to a C data pointer, called when it is garbage collected. Pass `nil` as the finalizer to remove a previously set finalizer.


| Parameter | Type | Description |
| --- | --- | --- |
| cdata | `ffi.cdata*` | C data object to attach the finalizer to. |
| finalizer? | `function` | Function called with `cdata` when it is collected. Pass `nil` to remove. |


| Return | Type | Description |
| --- | --- | --- |
| cdata | `ffi.cdata*` |  |


  

### `ffi.sizeof`

```lua
ffi.sizeof(ct: ffi.ct**[, nelem: integer]): integer|nil
```

Returns the size in bytes of the given C type or C data object. Returns `nil` for types of unknown or variable size (e.g. incomplete types).


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type or C data to measure. |
| nelem? | `integer` | Number of elements for VLA size calculation. |


| Return | Type | Description |
| --- | --- | --- |
| size | `integer\|nil` |  |


  

### `ffi.alignof`

```lua
ffi.alignof(ct: ffi.ct**): integer
```

Returns the minimum required alignment in bytes for the given C type.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type to query alignment for. |


| Return | Type | Description |
| --- | --- | --- |
| align | `integer` | Alignment requirement in bytes. |


  

### `ffi.offsetof`

```lua
ffi.offsetof(ct: ffi.ct**, field: string): integer, integer?, integer?
```

Returns the byte offset of a field within a C struct or union. For bit fields, also returns the bit position and bit size.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C struct or union type to query. |
| field | `string` | Name of the field. |


| Return | Type | Description |
| --- | --- | --- |
| ofs | `integer` |  |
| bpos | `integer?` |  |
| bsize | `integer?` |  |


  

### `ffi.istype`

```lua
ffi.istype(ct: ffi.ct**, obj: any): boolean
```

Checks whether `obj` is a C data object compatible with the C type `ct`.


| Parameter | Type | Description |
| --- | --- | --- |
| ct | `ffi.ct**` | C type to test against. |
| obj | `any` | Value to test. |


| Return | Type | Description |
| --- | --- | --- |
| status | `boolean` |  |


  

### `ffi.errno`

```lua
ffi.errno([newerr: integer]): integer
```

Gets or sets the OS error number (errno). If `newerr` is given, sets errno to that value and returns the previous value. C runtime `errno` is distinct from Win32 `GetLastError`.


| Parameter | Type | Description |
| --- | --- | --- |
| newerr? | `integer` | New errno value to set. |


| Return | Type | Description |
| --- | --- | --- |
| err | `integer` |  |


  

### `ffi.string`

```lua
ffi.string(ptr: any[, len: integer]): string
```

Converts a C data pointer to a Lua string. If `len` is given, copies exactly that many bytes; otherwise copies until the first null byte.


| Parameter | Type | Description |
| --- | --- | --- |
| ptr | `any` | Pointer to the data to convert. |
| len? | `integer` | Number of bytes to copy. Defaults to `strlen(ptr)`. |


| Return | Type | Description |
| --- | --- | --- |
| str | `string` |  |


  

### `ffi.copy`

```lua
ffi.copy(dst: any, src: any, len: integer)
```

Copies `len` bytes from `src` to `dst`. If given a string as `src` and no `len`, copies the full string including the null terminator.


| Parameter | Type | Description |
| --- | --- | --- |
| dst | `any` | Destination pointer. |
| src | `any` | Source pointer or string. |
| len | `integer` | Number of bytes to copy. |


  

### `ffi.fill`

```lua
ffi.fill(dst: any, len: integer[, c: any])
```

Fills `len` bytes starting at `dst` with the byte value `c` (default 0).


| Parameter | Type | Description |
| --- | --- | --- |
| dst | `any` | Destination pointer. |
| len | `integer` | Number of bytes to fill. |
| c? | `any` | Byte value to fill with. Defaults to `0`. |


  

### `ffi.abi`

```lua
ffi.abi(param: string): boolean
```

Checks for ABI parameters of the target platform. Common params: `"32bit"`, `"64bit"`, `"le"`, `"be"`, `"fpu"`, `"softfp"`, `"hardfp"`, `"eabi"`, `"win"`.


| Parameter | Type | Description |
| --- | --- | --- |
| param | `string` | ABI parameter string to test. |


| Return | Type | Description |
| --- | --- | --- |
| status | `boolean` |  |


  

<a id="ffi-ct"></a>
### `ffi.ct*`


## ffi.ctype\* — object type · callable


Represents a C type object created by `ffi.typeof`. Callable to construct new `ffi.cdata*` instances.


  

### `ffi.ctype*(init, ...)`

```lua
ffi.ctype*([init: any, ...: any]): ffi.cdata*
```


| Parameter | Type | Description |
| --- | --- | --- |
| init? | `any` |  |
| ...? | `any` |  |


  

### `ffi.ctype*(nelem, init, ...)`

```lua
ffi.ctype*([nelem: integer, init: any, ...: any]): ffi.cdata*
```


| Parameter | Type | Description |
| --- | --- | --- |
| nelem? | `integer` |  |
| init? | `any` |  |
| ...? | `any` |  |


## ffi.cb\* — object type


Represents a C callback object. Use `:free()` to release it and `:set()` to replace the Lua function.


  

### `ffi.cb*:free`

```lua
ffi.cb*:free()
```

Releases the resources associated with a C callback object. The callback must not be called after this — doing so is undefined behavior.


  

### `ffi.cb*:set`

```lua
ffi.cb*:set(func: function)
```

Replaces the Lua function of an existing C callback object with a new one. This avoids the overhead of allocating a new callback.


| Parameter | Type | Description |
| --- | --- | --- |
| func | `function` | New Lua function to use for the callback. |
