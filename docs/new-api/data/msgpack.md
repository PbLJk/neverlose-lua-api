> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# MessagePack

## msgpack — object type


  

### `msgpack.pack`

```lua
msgpack.pack([...: any]): string
```

Packs one or more Lua values into one string of MessagePack data.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` |  |


| Return | Type | Description |
| --- | --- | --- |
| msgpack_stream | `string` |  |


    
`nil` is packed as MessagePack `nil`, and a boolean is packed as `true` or `false`. A number
without a fractional part is packed as an integer. Any other number is packed as a 32 bit
float when that keeps its exact value, and as a 64 bit double otherwise. A string is packed as
raw bytes.

A table is packed as an array when its keys are exactly the integers from 1 to N. An empty
table is packed as an empty array. Any other table is packed as a map. Tables that are nested
more than 16 levels deep are packed as `nil`.

Values of any other type, such as functions and userdata, are packed as `nil`.

You must pass at least one value. If you call `pack` with no values, it throws an error. When
you pass more than one value, the string holds one MessagePack object for each value, one
after the other.


  

  

### `msgpack.unpack`

```lua
msgpack.unpack(msgpack_stream: string): any
```

Unpacks every object in a string of MessagePack data and returns them as separate values. For example, a string made by `msgpack.pack(a, b, c)` returns `a`, `b` and `c`.


| Parameter | Type | Description |
| --- | --- | --- |
| msgpack_stream | `string` |  |


| Return | Type | Description |
| --- | --- | --- |
| ... | `any` |  |


    
Throws an error if the data is cut short, has a bad format, or is nested more than 16 levels
deep.


  

  

### `msgpack.unpack_one`

```lua
msgpack.unpack_one(msgpack_stream: string[, offset: integer]): integer, any
```

Unpacks one object from a string of MessagePack data, starting at `offset`.


| Parameter | Type | Description |
| --- | --- | --- |
| msgpack_stream | `string` |  |
| offset? | `integer` |  |


| Return | Type | Description |
| --- | --- | --- |
| resume_offset | `integer` |  |
| object | `any` |  |


    
`offset` is a byte position in `msgpack_stream`. The first byte is at offset `0`, which is
also the default.

The function returns `resume_offset` first and the object second. Pass `resume_offset` to the
next `unpack_one` call to read the next object. When the end of the data is reached,
`resume_offset` is `-1`.

Throws an error if `offset` is negative or larger than the length of the data, or if the data
is invalid.


  

  

### `msgpack.unpack_limit`

```lua
msgpack.unpack_limit(msgpack_stream: string, limit: integer[, offset: integer]): integer, any
```

Unpacks up to `limit` objects from a string of MessagePack data, starting at `offset`.


| Parameter | Type | Description |
| --- | --- | --- |
| msgpack_stream | `string` |  |
| limit | `integer` |  |
| offset? | `integer` |  |


| Return | Type | Description |
| --- | --- | --- |
| resume_offset | `integer` |  |
| ... | `any` |  |


    
`offset` is a byte position in `msgpack_stream`. The first byte is at offset `0`, which is
also the default. If the data ends first, fewer than `limit` objects are returned.

The function returns `resume_offset` first and the objects after it. Pass `resume_offset` to
`unpack_limit` or `unpack_one` to continue reading. When the end of the data is reached,
`resume_offset` is `-1`.

If `limit` and `offset` are both `0`, the function works like `msgpack.unpack`. It returns
every object and does not return `resume_offset`.

Throws an error if `offset` or `limit` is negative, if `offset` is larger than the length of
the data, or if the data is invalid.
