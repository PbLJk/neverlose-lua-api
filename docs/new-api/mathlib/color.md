> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Color


<a id="color-1"></a>

## Color  — cdata


A colour with red, green, blue and alpha channels. Each channel is a byte from 0 to 255.

`Color(r, g, b)` creates a colour that is fully visible, because an alpha that is not given
is set to 255. A red, green or blue channel that is not given is set to 0.

The `==` operator compares all four channels and returns `false` when the other value is
not a `Color`.


  

### `Color.a`

The alpha channel, from 0 to 255. 0 is fully transparent and 255 is fully visible.


  

### `Color.b`

The blue channel, from 0 to 255.


  

### `Color.g`

The green channel, from 0 to 255.


  

### `Color.r`

The red channel, from 0 to 255.


<a id="color-2"></a>

## Color  — ctype · callable


Call `Color(r, g, b, a)` to create a colour. Call `Color(other)` to make a copy of another
colour.


  

### `Color(r, g, b, a)`

```lua
Color([r: integer, g: integer, b: integer, a: integer]): Color
```

The alpha is 255 if it is not given.


| Parameter | Type | Description |
| --- | --- | --- |
| r? | `integer` |  |
| g? | `integer` |  |
| b? | `integer` |  |
| a? | `integer` |  |


  

### `Color(self)`

```lua
Color(self: Color): Color
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Color` |  |


  

### `Color.Unpack`

```lua
Color.Unpack(col: Color): integer, integer, integer, integer
```

Returns the red, green, blue and alpha channels of the colour.


| Parameter | Type | Description |
| --- | --- | --- |
| col | `Color` | The colour to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| r | `integer` |  |
| g | `integer` |  |
| b | `integer` |  |
| a | `integer` |  |


  

### `Color.Lerp`

```lua
Color.Lerp(a: Color, b: Color, t: number): Color
```

Returns a new colour between two colours. This is linear interpolation. Each channel of the result is rounded to the nearest whole number and clamped to the range from 0 to 255.


| Parameter | Type | Description |
| --- | --- | --- |
| a | `Color` | The start colour. |
| b | `Color` | The end colour. |
| t | `number` | The interpolation factor. 0 returns `a` and 1 returns `b`. |


  

### `Color.Hex`

```lua
Color.Hex(col: Color): string
```

Returns the colour as a hex string in the format `RRGGBBAA`, with upper case letters. For example, `Color(255, 128, 0)` returns `"FF8000FF"`.


| Parameter | Type | Description |
| --- | --- | --- |
| col | `Color` | The colour to format. |
