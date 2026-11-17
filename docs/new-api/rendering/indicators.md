> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Indicators


<a id="indicators-1"></a>

## indicators  — global table


Adds indicators of your script to the indicator stack on the screen. The cheat shows its own
status lines in the same stack. Script indicators use the style of the stack, and they fade,
resize and stack in the same way as the built-in indicators.

Script indicators have no menu option. The script decides when they are shown. When the script
is unloaded, all indicators that it created are removed.

The built-in indicators are not available here, but their menu switches are normal options,
for example `ui.Lookup("Common", "Visuals", "World", "Miscellaneous", "Windows", "Indicators", "Double Tap")`.


  

### `indicators.position`

The position of the top of the indicator stack on the screen. Read only.


  

### `indicators.Create`

```lua
indicators.Create(id: string): indicators.Item
```

Creates an indicator for the calling script and returns its handle. If the script already has an indicator with this id, that indicator is returned. Throws an error if the id is empty, or if the script already has 64 indicators.


| Parameter | Type | Description |
| --- | --- | --- |
| id | `string` | The identifier of the indicator. It is also used as the name that is shown. |


    
A new indicator is hidden and empty. Add elements with `AddText`, `AddLines`, `AddSpinner` and
`AddIcon`. The elements are drawn from left to right in the order that they were added. Then set
`visible` to `true` in any event to show the indicator.


  


## indicators.Item — object type

A handle to one indicator that a script created. Read and assign its fields directly. Reading
an unknown field returns `nil`. Assigning an unknown field or a read only field throws an
error.

Two handles are equal with `==` when they point to the same indicator. An indicator exists until
the script is unloaded, so keep the handle if you need it later.


  

### `indicators.Item.anim`

The progress of the fade animation, from `0` to `1`. You can use it to match your own drawing to the indicator. Read only.


  

### `indicators.Item.color`

The colour of the accent line. Assign `nil` to use the default colour of the style.


  

### `indicators.Item.id`

The identifier. Read only.


  

### `indicators.Item.size`

The current size of the indicator window, with the animation applied. Read only.


  

### `indicators.Item.visible`

Whether the indicator is shown. It fades in and out with the animation of the stack.


  

### `indicators.Item:AddText`

```lua
indicators.Item:AddText([text: string]): indicators.Text
```

Adds a text element and returns its handle.


| Parameter | Type | Description |
| --- | --- | --- |
| text? | `string` | The starting text. The default is an empty string. |


  

### `indicators.Item:AddLines`

```lua
indicators.Item:AddLines(count: integer): indicators.Lines
```

Adds a block of text lines on top of each other and returns its handle. The block takes the space of one element. The number of lines cannot be changed later, so hide a line instead of removing it. Throws an error if `count` is not between 1 and 8.


| Parameter | Type | Description |
| --- | --- | --- |
| count | `integer` | The number of lines, from `1` to `8`. |


  

### `indicators.Item:AddSpinner`

```lua
indicators.Item:AddSpinner([alt_style: boolean]): indicators.Spinner
```

Adds a round progress spinner and returns its handle.


| Parameter | Type | Description |
| --- | --- | --- |
| alt_style? | `boolean` | Pass `true` to use the symmetric sweep style instead of the arc. The default is `false`. |


  

### `indicators.Item:AddIcon`

```lua
indicators.Item:AddIcon(source: integer|string|Image[, scale: number, rotation: number, invert: boolean]): indicators.Icon
```

Adds an icon element and returns its handle. The source can be a weapon id as an integer, a Panorama image path as a string, such as `"panorama/images/icons/ui/bullet.vsvg_c"`, or an `Image` object that was loaded with the `render` API.


| Parameter | Type | Description |
| --- | --- | --- |
| source | `integer\|string\|Image` | The source of the icon. |
| scale? | `number` | The height, relative to the base icon size of the indicator. The default is `1`. |
| rotation? | `number` | The rotation in degrees. The default is `0`. |
| invert? | `boolean` | Pass `true` to flip the icon vertically. The default is `false`. |


    
A weapon id or a Panorama path works only if the game resources for it are available.


  


## indicators.Text — object type

A text element of an indicator.


  

### `indicators.Text.color`

The colour of the text. Assign `nil` to use the default colour of the style.


  

### `indicators.Text.text`

The text that is shown. Assigning it also makes the element visible.


  

### `indicators.Text.visible`

Whether the element is drawn.


## indicators.Lines — object type

A block of text lines on top of each other. Use `lines[1]` to `lines[count]` to get each line as
an `indicators.Text` handle. An index outside this range throws an error.


  

### `indicators.Lines[integer]`

The handle of a line. The first line has the index 1.


  

### `indicators.Lines.count`

The number of lines. Read only.


  

### `indicators.Lines.visible`

Whether the whole block is drawn.


## indicators.Spinner — object type

A round progress spinner element.


  

### `indicators.Spinner.color`

The colour of the spinner. Assign `nil` to use the default colour of the style.


  

### `indicators.Spinner.percent`

The progress, from `0` to `1`. A value outside this range is changed to the nearest end of the range.


  

### `indicators.Spinner.visible`

Whether the element is drawn.


## indicators.Icon — object type

An icon element.


  

### `indicators.Icon.color`

The tint colour. Assign `nil` to use the default colour of the style.


  

### `indicators.Icon.invert`

Whether the icon is flipped vertically.


  

### `indicators.Icon.rotation`

The rotation in degrees.


  

### `indicators.Icon.scale`

The height, relative to the base icon size of the indicator.


  

### `indicators.Icon.source`

The source of the icon. It is a weapon id, a Panorama path or an `Image` object.


  

### `indicators.Icon.visible`

Whether the element is drawn.
