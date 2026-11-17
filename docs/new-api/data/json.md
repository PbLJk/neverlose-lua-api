> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# JSON


<a id="json-1"></a>

## json  — object type


Encodes Lua values as JSON and decodes JSON into Lua values.


  

### `json.new`

```lua
json.new(): json
```

`json.new` can be used to instantiate an independent copy of the Lua CJSON module. The new module has a separate persistent encoding buffer, and default settings.


  

### `json.decode`

```lua
json.decode(json_text: string): any
```

`json.decode` will deserialise any UTF-8 JSON string into a Lua value or table.


| Parameter | Type | Description |
| --- | --- | --- |
| json_text | `string` |  |


| Return | Type | Description |
| --- | --- | --- |
| value | `any` |  |


    
UTF-16 and UTF-32 JSON strings are not supported.

`json.decode` requires that any NULL (ASCII 0) and double quote (ASCII 34)
characters are escaped within strings. All escape codes will be decoded and
other bytes will be passed transparently. UTF-8 characters are not validated
during decoding and should be checked elsewhere if required.

JSON `null` will be converted to NULL `lightuserdata` value.

By default, numbers incompatible with the JSON specification (infinity,
NaN, hexadecimal) can be decoded. This default can be changed with
`json.decode_invalid_numbers`.


**Warning:** 
Care must be taken after decoding JSON objects with numeric keys. Each
numeric key will be stored as a Lua `string`. Any subsequent code assuming
type `number` may break.


  

  

### `json.decode_invalid_numbers`

```lua
json.decode_invalid_numbers([setting: boolean]): boolean
```

Lua CJSON may generate an error when trying to decode numbers not supported by the JSON specification. *Invalid numbers* are defined as:


| Parameter | Type | Description |
| --- | --- | --- |
| setting? | `boolean` |  |


| Return | Type | Description |
| --- | --- | --- |
| setting | `boolean` |  |


    
* infinity
* not-a-number (NaN)
* hexadecimal

Available settings:

* `true`: Accept and decode *invalid numbers*. This is the default setting.
* `false`: Throw an error when *invalid numbers* are encountered.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.decode_max_depth`

```lua
json.decode_max_depth([depth: integer]): integer
```

Lua CJSON will generate an error when parsing deeply nested JSON once the maximum array/object depth has been exceeded. This check prevents unnecessarily complicated JSON from slowing down the application, or crashing the application due to a lack of process stack space.


| Parameter | Type | Description |
| --- | --- | --- |
| depth? | `integer` | must be a positive integer. |


| Return | Type | Description |
| --- | --- | --- |
| depth | `integer` |  |


    
An error may be generated before the depth limit is hit if Lua is unable to
allocate more objects on the Lua stack.

By default, Lua CJSON will reject JSON with arrays and/or objects nested
more than 1000 levels deep.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.encode`

```lua
json.encode(value: unknown): string
```

`json.encode` will serialise a Lua value into a string containing the JSON representation.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `unknown` |  |


| Return | Type | Description |
| --- | --- | --- |
| json_text | `string` |  |


    
`json.encode` supports the following types:

* `boolean`
* `lightuserdata` (NULL value only)
* `nil`
* `number`
* `string`
* `table`

The remaining Lua types will generate an error:

* `function`
* `lightuserdata` (non-NULL values)
* `thread`
* `userdata`

By default, numbers are encoded with 14 significant digits. Refer to
`json.encode_number_precision` for details.

Lua CJSON will escape the following characters within each UTF-8 string:

* Control characters (ASCII 0 - 31)
* Double quote (ASCII 34)
* Forward slash (ASCII 47)
* Backslash (ASCII 92)
* Delete (ASCII 127)

All other bytes are passed transparently.


**Warning:** 
Lua CJSON will successfully encode/decode binary strings, but this is
technically not supported by JSON and may not be compatible with other
JSON libraries. To ensure the output is valid JSON, applications should
ensure all Lua strings passed to `json.encode` are UTF-8.


Lua CJSON uses a heuristic to determine whether to encode a Lua table as a
JSON array or an object. A Lua table with only positive integer keys of type
`number` will be encoded as a JSON array. All other tables will be encoded
as a JSON object.

Lua CJSON does not use metamethods when serialising tables.

* `rawget` is used to iterate over Lua arrays
* `next` is used to iterate over Lua objects

Lua arrays with missing entries (*sparse arrays*) may optionally be encoded
in several different ways. Refer to `json.encode_sparse_array` for details.

JSON object keys are always strings. Hence `json.encode` only supports
table keys which are type `number` or `string`. All other types will
generate an error.

By default, encoding the following Lua values will generate errors:

* Numbers incompatible with the JSON specification (infinity, NaN)
* Tables nested more than 1000 levels deep
* Excessively sparse Lua arrays

These defaults can be changed with:

* `json.encode_invalid_numbers`
* `json.encode_max_depth`
* `json.encode_sparse_array`


  

  

### `json.encode_invalid_numbers`

```lua
json.encode_invalid_numbers([setting: true|false|"null"]): true|false|"null"
```

Lua CJSON may generate an error when encoding floating point numbers not supported by the JSON specification (*invalid numbers*):


| Parameter | Type | Description |
| --- | --- | --- |
| setting? | `true\|false\|"null"` |  |


| Return | Type | Description |
| --- | --- | --- |
| setting | `true\|false\|"null"` |  |


    
* infinity
* not-a-number (NaN)

Available settings:

* `true`: Allow *invalid numbers* to be encoded. This will generate
  non-standard JSON, but this output is supported by some libraries.

* `"null"`: Encode *invalid numbers* as a JSON `null` value. This allows
  infinity and NaN to be encoded into valid JSON.

* `false`: Throw an error when attempting to encode *invalid numbers*. This
  is the default setting.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.encode_keep_buffer`

```lua
json.encode_keep_buffer([keep: boolean]): boolean
```

Lua CJSON can reuse the JSON encoding buffer to improve performance.


| Parameter | Type | Description |
| --- | --- | --- |
| keep? | `boolean` |  |


| Return | Type | Description |
| --- | --- | --- |
| keep | `boolean` |  |


    
Available settings:

* `true`: The buffer will grow to the largest size required and is not freed
  until the Lua CJSON module is garbage collected. This is the default
  setting.

* `false`: Free the encode buffer after each call to `json.encode`.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.encode_max_depth`

```lua
json.encode_max_depth([depth: integer]): integer
```

Once the maximum table depth has been exceeded Lua CJSON will generate an error. This prevents deeply nested or recursive data structure from crashing the application.


| Parameter | Type | Description |
| --- | --- | --- |
| depth? | `integer` | must be a positive integer. |


| Return | Type | Description |
| --- | --- | --- |
| depth | `integer` |  |


    
By default, Lua CJSON will generate an error when trying to encode data
structures with more than 1000 nested tables.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.encode_number_precision`

```lua
json.encode_number_precision([precision: integer]): integer
```

Sets the number of significant digits used when encoding numbers. Lower values reduce precision.


| Parameter | Type | Description |
| --- | --- | --- |
| precision? | `integer` |  |


| Return | Type | Description |
| --- | --- | --- |
| precision | `integer` |  |


    
By default, Lua CJSON will output 14 significant digits when converting a
number to text.

The current setting is always returned, and is only updated when an argument
is provided.


  

  

### `json.encode_sparse_array`

```lua
json.encode_sparse_array([convert: boolean, ratio: integer, safe: integer]): boolean, integer, integer
```

Lua CJSON classifies a Lua table into one of three kinds when encoding a JSON array. This is determined by the number of values missing from the Lua array as follows:


| Parameter | Type | Description |
| --- | --- | --- |
| convert? | `boolean` |  |
| ratio? | `integer` | must be a non-negative integer. |
| safe? | `integer` | must be a positive integer. |


| Return | Type | Description |
| --- | --- | --- |
| convert | `boolean` |  |
| ratio | `integer` |  |
| safe | `integer` |  |


    
* **Normal**: All values are available.
* **Sparse**: At least one value is missing.
* **Excessively sparse**: The number of values missing exceeds the
  configured ratio.

Lua CJSON encodes sparse Lua arrays as JSON arrays using JSON `null` for the
missing entries.

An array is excessively sparse when all the following conditions are met:

* `ratio > 0`
* `maximum_index > safe`
* `maximum_index > item_count * ratio`

Lua CJSON will never consider an array to be *excessively sparse* when
`ratio == 0`. The `safe` limit ensures that small Lua arrays are always
encoded as sparse arrays.

By default, attempting to encode an *excessively sparse* array will generate
an error. If `convert` is set to `true`, *excessively sparse* arrays will be
converted to a JSON object.

The current settings are always returned. A particular setting is only
changed when the argument is provided (non-`nil`).
