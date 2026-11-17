> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Table


<a id="table-1"></a>

## table  — global table


Standard Lua table library, providing utilities for manipulating array-style and general tables.


  

### `table.concat`

```lua
table.concat(list: table[, sep: string, i: integer, j: integer]): string
```

Returns the elements of `list` joined into a string, with `sep` inserted between each element. Only elements from index `i` to `j` are included. All elements must be strings or numbers.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `table` | Array-like table whose elements to join. |
| sep? | `string` | Separator string placed between elements. Defaults to `""`. |
| i? | `integer` | Start index. Defaults to `1`. |
| j? | `integer` | End index. Defaults to `#list`. |


  

### `table.foreach`

```lua
table.foreach(list: any, callback: fun(key: string, value: any): T|nil): T|nil
```

Iterates over all key-value pairs in `list` (including non-integer keys) and calls `callback` for each. If `callback` returns a non-nil value, the iteration stops and that value is returned. Deprecated — prefer `pairs` for new code.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `any` | Table to iterate over. |
| callback | `fun(key: string, value: any): T\|nil` | Called for each key-value pair. |


  

### `table.foreachi`

```lua
table.foreachi(list: any, callback: fun(key: string, value: any): T|nil): T|nil
```

Iterates over the integer keys of `list` in order and calls `callback` for each. If `callback` returns a non-nil value, the iteration stops and that value is returned. Deprecated — prefer `ipairs` for new code.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `any` | Table to iterate over. |
| callback | `fun(key: string, value: any): T\|nil` | Called for each index-value pair. |


  

### `table.getn`

```lua
table.getn(list: T[]): integer
```

Returns the "getn" size of a table, which is the largest integer key `n` such that `t[n]` is not nil. Deprecated — use the `#` length operator for new code.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `T[]` | Table to measure. |


  

### `table.insert`

```lua
table.insert(list: table, pos: integer, value: any)
```

Inserts `value` into `list`. If `pos` is given, inserts before the element at `pos`, shifting up elements `pos..#list`. If only `value` is given, appends it to the end (`list[#list + 1] = value`).


| Parameter | Type | Description |
| --- | --- | --- |
| list | `table` | Array-like table to insert into. |
| pos | `integer` | Position to insert before. |
| value | `any` | Value to insert. |


  

### `table.maxn`

```lua
table.maxn(table: table): integer
```

Returns the largest positive numerical key in `table`, or zero if no such key exists. Unlike `#`, this scans all keys and works correctly with sparse tables.


| Parameter | Type | Description |
| --- | --- | --- |
| table | `table` | Table to scan. |


  

### `table.move`

```lua
table.move(a1: table, f: integer, e: integer, t: integer[, a2: table]): table
```

Moves elements from table `a1` into table `a2` (or `a1` itself if `a2` is omitted). Copies elements `a1[f]` through `a1[e]` into `a2` starting at index `t`.


| Parameter | Type | Description |
| --- | --- | --- |
| a1 | `table` | Source table. |
| f | `integer` | First source index. |
| e | `integer` | Last source index (inclusive). |
| t | `integer` | Destination start index in `a2`. |
| a2? | `table` | Destination table. Defaults to `a1`. |


| Return | Type | Description |
| --- | --- | --- |
| a2 | `table` |  |


  

### `table.pack`

```lua
table.pack([...: unknown]): table
```

Packs all arguments into a new table and stores the argument count in the field `n`. Equivalent to `{ n = select('#', ...), ... }`.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `unknown` |  |


  

### `table.remove`

```lua
table.remove(list: table[, pos: integer]): any
```

Removes and returns the element at position `pos` from `list`, shifting down all subsequent elements. If `pos` is omitted, removes and returns the last element.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `table` | Array-like table to remove from. |
| pos? | `integer` | Position to remove. Defaults to `#list`. |


  

### `table.sort`

```lua
table.sort(list: T[][, comp: fun(a: T, b: T): boolean])
```

Sorts the elements of `list` in place. `comp` is an optional comparator function; if omitted, the standard `<` operator is used. The sort algorithm is not guaranteed to be stable.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `T[]` | Array-like table to sort. |
| comp? | `fun(a: T, b: T): boolean` | Returns `true` when `a` should come before `b`. |


  

### `table.unpack`

```lua
table.unpack(list: table[, i: integer, j: integer]): T1, T2, T3, T4, T5, T6, T7, T8, T9, T10
```

Returns the elements of `list` as multiple return values, from index `i` to `j`. Equivalent to `return list[i], list[i+1], ..., list[j]`.


| Parameter | Type | Description |
| --- | --- | --- |
| list | `table` |  |
| i? | `integer` | First index to unpack. Defaults to `1`. |
| j? | `integer` | Last index to unpack. Defaults to `#list`. |
