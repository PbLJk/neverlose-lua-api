> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# String


<a id="string-1"></a>

## string  — global table


Standard Lua string library. All functions are also available as methods on string values
via the `string` metatable (e.g. `("hello"):upper()`).


  

### `string.byte`

```lua
string.byte(s: string|number[, i: integer, j: integer]): integer
```

Returns the numeric byte values of the characters in `s` from position `i` to `j`. `i` defaults to `1`; `j` defaults to `i`. Negative indices count from the end of the string.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |
| i? | `integer` | Start position. Defaults to `1`. |
| j? | `integer` | End position. Defaults to `i`. |


| Return | Type | Description |
| --- | --- | --- |
| ... | `integer` |  |


  

### `string.char`

```lua
string.char(byte: integer[, ...: integer]): string
```

Returns a string formed by the concatenation of characters with the given byte values.


| Parameter | Type | Description |
| --- | --- | --- |
| byte | `integer` | First byte value. |
| ...? | `integer` | Additional byte values. |


  

### `string.find`

```lua
string.find(s: string|number, pattern: string|number[, init: integer, plain: boolean]): integer|nil, integer|nil, any|nil
```

Searches for the first match of `pattern` in `s`, starting at position `init`. If `plain` is true, the pattern is treated as a plain substring (no magic characters). Returns the start and end positions of the match, plus any captures.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | String to search in. |
| pattern | `string\|number` | Pattern to search for. |
| init? | `integer` | Starting position. Defaults to `1`. Negative values count from the end. |
| plain? | `boolean` | If `true`, disables pattern matching and does a plain substring search. |


| Return | Type | Description |
| --- | --- | --- |
| start | `integer\|nil` |  |
| end | `integer\|nil` |  |
| ... | `any\|nil` |  |


  

### `string.format`

```lua
string.format(s: string|number[, ...: any]): string
```

Returns a formatted string, following the same rules as the C `printf` family. Supported conversion specifiers: `%d`, `%i`, `%u`, `%o`, `%x`, `%X`, `%f`, `%e`, `%E`, `%g`, `%G`, `%c`, `%s`, `%q`, `%%`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Format string. |
| ...? | `any` | Values to format. |


  

### `string.gmatch`

```lua
string.gmatch(s: string|number, pattern: string|number): fun(): string, unknown
```

Returns an iterator function that, each time it is called, returns the next set of captures from `pattern` over `s`. If the pattern has no captures, the whole match is returned each iteration.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | String to iterate over. |
| pattern | `string\|number` | Pattern to match repeatedly. |


  

### `string.gsub`

```lua
string.gsub(s: string|number, pattern: string|number, repl: string|number|table|function[, n: integer]): string, integer
```

Returns a copy of `s` with all matches of `pattern` replaced by `repl`. `repl` can be a string (with `%0`–`%9` capture references), a table (keyed by the first capture), or a function (called with the captures, returning the replacement). `n` limits the number of substitutions.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |
| pattern | `string\|number` | Pattern to match. |
| repl | `string\|number\|table\|function` | Replacement value. |
| n? | `integer` | Maximum number of substitutions. Defaults to unlimited. |


| Return | Type | Description |
| --- | --- | --- |
|  | `string` |  |
| count | `integer` |  |


  

### `string.len`

```lua
string.len(s: string|number): integer
```

Returns the length of string `s` in bytes. Equivalent to `#s`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | String to measure. |


  

### `string.lower`

```lua
string.lower(s: string|number): string
```

Returns a lowercase copy of `s`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |


  

### `string.match`

```lua
string.match(s: string|number, pattern: string|number[, init: integer]): any
```

Searches for the first match of `pattern` in `s`, starting at position `init`. Returns the captures if the pattern has them, or the whole match otherwise.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | String to search in. |
| pattern | `string\|number` | Pattern to match. |
| init? | `integer` | Starting position. Defaults to `1`. Negative values count from the end. |


| Return | Type | Description |
| --- | --- | --- |
| ... | `any` |  |


  

### `string.rep`

```lua
string.rep(s: string|number, n: integer[, sep: string|number]): string
```

Returns a string that is the concatenation of `n` copies of `s`, separated by `sep`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | String to repeat. |
| n | `integer` | Number of repetitions. |
| sep? | `string\|number` | Separator between copies. Defaults to `""`. |


  

### `string.reverse`

```lua
string.reverse(s: string|number): string
```

Returns a string that is the reverse of `s`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |


  

### `string.sub`

```lua
string.sub(s: string|number, i: integer[, j: integer]): string
```

Returns the substring of `s` from position `i` to `j` (inclusive). Negative indices count from the end of the string (`-1` is the last character).


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |
| i | `integer` | Start position. |
| j? | `integer` | End position. Defaults to `-1` (end of string). |


  

### `string.upper`

```lua
string.upper(s: string|number): string
```

Returns an uppercase copy of `s`.


| Parameter | Type | Description |
| --- | --- | --- |
| s | `string\|number` | Source string. |
