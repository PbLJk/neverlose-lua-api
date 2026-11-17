> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Bit Operations

## bit — global table

LuaJIT's `bit` library provides bitwise operations. Numeric operands are normalized to
32 bits, and numeric results use the signed 32-bit range.


  

### `bit.tobit`

```lua
bit.tobit(x: integer): integer
```

Normalizes a number to the signed 32-bit range used by bit operations.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to normalize to a 32-bit integer. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.tohex`

```lua
bit.tohex(x: integer[, n: integer]): string
```

Converts its first argument to a hex string. The number of hex digits is given by the absolute value of the optional second argument. Negative values produce uppercase hex digits. If omitted, the default is 8 digits.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to convert. |
| n? | `integer` | Number of hex digits (negative for uppercase). Defaults to 8. |


| Return | Type | Description |
| --- | --- | --- |
| y | `string` |  |


  

### `bit.bnot`

```lua
bit.bnot(x: integer): integer
```

Returns the bitwise **NOT** of its argument.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to invert. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.bor`

```lua
bit.bor(x: integer[, ...: integer]): integer
```

Returns the bitwise **OR** of all of its arguments.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | First operand. |
| ...? | `integer` | Additional operands. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.band`

```lua
bit.band(x: integer[, ...: integer]): integer
```

Returns the bitwise **AND** of all of its arguments.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | First operand. |
| ...? | `integer` | Additional operands. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.bxor`

```lua
bit.bxor(x: integer[, ...: integer]): integer
```

Returns the bitwise **XOR** of all of its arguments.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | First operand. |
| ...? | `integer` | Additional operands. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.lshift`

```lua
bit.lshift(x: integer, n: integer): integer
```

Returns the bitwise **logical left-shift** of its first argument by the number of bits given by the second argument. Bits shifted out on either end are lost. Vacant bits are filled with zeros.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to shift. |
| n | `integer` | Number of bit positions to shift left. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.rshift`

```lua
bit.rshift(x: integer, n: integer): integer
```

Returns the bitwise **logical right-shift** of its first argument by the number of bits given by the second argument. Bits shifted out on either end are lost. Vacant bits are filled with zeros.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to shift. |
| n | `integer` | Number of bit positions to shift right. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.arshift`

```lua
bit.arshift(x: integer, n: integer): integer
```

Returns the bitwise **arithmetic right-shift** of its first argument by the number of bits given by the second argument. Vacant bits are filled with the sign bit (bit 31) of the original value, preserving the sign.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to shift. |
| n | `integer` | Number of bit positions to shift right arithmetically. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.rol`

```lua
bit.rol(x: integer, n: integer): integer
```

Returns the bitwise **left rotation** of its first argument by the number of bits given by the second argument. Bits rotated out on the left are inserted on the right.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to rotate. |
| n | `integer` | Number of bit positions to rotate left. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.ror`

```lua
bit.ror(x: integer, n: integer): integer
```

Returns the bitwise **right rotation** of its first argument by the number of bits given by the second argument. Bits rotated out on the right are inserted on the left.


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value to rotate. |
| n | `integer` | Number of bit positions to rotate right. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |


  

### `bit.bswap`

```lua
bit.bswap(x: integer): integer
```

Returns the **byte-swapped** value of its argument. This reverses the byte order of the 32-bit integer (e.g. for converting between little-endian and big-endian).


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` | Value whose bytes are to be swapped. |


| Return | Type | Description |
| --- | --- | --- |
| y | `integer` |  |
