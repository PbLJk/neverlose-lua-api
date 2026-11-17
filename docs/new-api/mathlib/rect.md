> Math implementation ported in 3.7.5.41; requires existing Allow Insecure. Native legacy APIs may require their old vector/color types.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Rectangle


## Rect\_t — cdata


A rectangle of whole numbers, stored as a position and a size. The position `x`, `y` is the
top left cell. The last column and the last row are part of the rectangle, so `MaximumX` is
`x + width - 1` and `MaximumY` is `y + height - 1`.

Only engine structures use this type. The render functions use floats.

The `==` operator compares all four fields and returns `false` when the other value is not
a `Rect_t`.

```cpp lines=false
typedef struct Rect_t {
    int x, y;
    int width, height;
} Rect_t;
```


  

### `Rect_t.height`


  

### `Rect_t.width`


  

### `Rect_t.x`

The left column.


  

### `Rect_t.y`

The top row.


<a id="rect_t-1"></a>

## Rect_t  — ctype · callable


Call `Rect_t()` to create a rectangle with every field set to 0. Call
`Rect_t(x, y, width, height)` to set the fields. A field that is not given is set to 0. Call
`Rect_t(other)` to make a copy of another rectangle. Any other first argument throws an
error.


  

<a id="rect_t"></a>
### `Rect_t()`

```lua
Rect_t(): Rect_t
```

A rectangle with every field set to 0.


  

### `Rect_t(x, y, width, height)`

```lua
Rect_t(x: integer[, y: integer, width: integer, height: integer]): Rect_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| x | `integer` |  |
| y? | `integer` |  |
| width? | `integer` |  |
| height? | `integer` |  |


  

### `Rect_t(self)`

```lua
Rect_t(self: Rect_t): Rect_t
```


| Parameter | Type | Description |
| --- | --- | --- |
| self | `Rect_t` |  |


  

### `Rect_t.Clear`

```lua
Rect_t.Clear(rect: Rect_t)
```

Sets every field of the rectangle to 0.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to change. |


  

### `Rect_t.Copy`

```lua
Rect_t.Copy(src: Rect_t, dst: Rect_t)
```

Copies one rectangle into another rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| src | `Rect_t` | The rectangle to copy from. |
| dst | `Rect_t` | The rectangle to copy into. |


  

### `Rect_t.Unpack`

```lua
Rect_t.Unpack(rect: Rect_t): integer, integer, integer, integer
```

Returns the X, Y, width and height of the rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to unpack. |


| Return | Type | Description |
| --- | --- | --- |
| x | `integer` |  |
| y | `integer` |  |
| width | `integer` |  |
| height | `integer` |  |


  

### `Rect_t.Size`

```lua
Rect_t.Size(rect: Rect_t): integer
```

Returns the area of the rectangle, which is `width * height`.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to read. |


  

### `Rect_t.IsEmpty`

```lua
Rect_t.IsEmpty(rect: Rect_t): boolean
```

Returns `true` if the width or the height is 0 or negative.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to check. |


  

### `Rect_t.MaximumX`

```lua
Rect_t.MaximumX(rect: Rect_t): integer
```

Returns the last column of the rectangle, which is `x + width - 1`.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to read. |


  

### `Rect_t.MaximumY`

```lua
Rect_t.MaximumY(rect: Rect_t): integer
```

Returns the last row of the rectangle, which is `y + height - 1`.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to read. |


  

### `Rect_t.Intersects`

```lua
Rect_t.Intersects(rect: Rect_t, other: Rect_t): boolean
```

Returns `true` if the two rectangles share at least one cell. Rectangles that only touch at an edge do not share a cell.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The first rectangle. |
| other | `Rect_t` | The second rectangle. |


  

### `Rect_t.Contains`

```lua
Rect_t.Contains(rect: Rect_t, other: Rect_t): boolean
```

Returns `true` if the other rectangle is completely inside this rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The outer rectangle. |
| other | `Rect_t` | The inner rectangle. |


  

### `Rect_t.ContainsPoint`

```lua
Rect_t.ContainsPoint(rect: Rect_t, px: integer, py: integer): boolean
```

Returns `true` if the cell at the given column and row is inside the rectangle.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to read. |
| px | `integer` | The column of the cell. |
| py | `integer` | The row of the cell. |


  

### `Rect_t.SetFromMaxMins`

```lua
Rect_t.SetFromMaxMins(rect: Rect_t, min_x: integer, min_y: integer, max_x: integer, max_y: integer)
```

Sets the rectangle from its first and last cells. Both cells are part of the rectangle, so the width is `max_x - min_x + 1` and the height is `max_y - min_y + 1`.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to change. |
| min_x | `integer` |  |
| min_y | `integer` |  |
| max_x | `integer` |  |
| max_y | `integer` |  |


  

### `Rect_t.IntersectWith`

```lua
Rect_t.IntersectWith(rect: Rect_t, other: Rect_t)
```

Shrinks the rectangle to the cells that it shares with another rectangle. If the rectangles do not share a cell, the result has a width or a height of 0 or less.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to change. |
| other | `Rect_t` | The rectangle to intersect with. |


  

### `Rect_t.Union`

```lua
Rect_t.Union(rect: Rect_t, other: Rect_t)
```

Grows the rectangle to the smallest rectangle that contains both rectangles.


| Parameter | Type | Description |
| --- | --- | --- |
| rect | `Rect_t` | The rectangle to change. |
| other | `Rect_t` | The rectangle to include. |
