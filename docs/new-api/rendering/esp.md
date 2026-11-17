> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# ESP


<a id="esp-1"></a>

## esp  — global table


Adds custom elements to the built-in ESP. Your script can draw extra information next to the
ESP of each entity, and the user can turn each element on or off in the menu.


  

### `esp.AddItem`

```lua
esp.AddItem(category: esp.Category, name: string): esp.Element
```

Adds a simple ESP element to the given category. The element appears in the ESP options, and the user can turn it on or off. The element does not draw anything by itself. Your script does the drawing.


| Parameter | Type | Description |
| --- | --- | --- |
| category | `esp.Category` | The ESP category to add the element to. |
| name | `string` | The name of the element in the menu. |


  

### `esp.AddText`

```lua
esp.AddText(category: esp.Category, name: string, preview: string, callback: esp.AddText.Callback[, position: esp.Position]): esp.Element
```

Adds a custom text element. `callback` is called for each entity and returns the text to draw.


| Parameter | Type | Description |
| --- | --- | --- |
| category | `esp.Category` | The ESP category to add the element to. |
| name | `string` | The name of the element in the menu. |
| preview | `string` | The sample text that is shown in the preview in the menu. |
| callback | `esp.AddText.Callback` | Called for each entity. Returns the text to draw. |
| position? | `esp.Position` | The default position. Defaults to `esp.Position.kBottom`. |


  

### `esp.AddBar`

```lua
esp.AddBar(category: esp.Category, name: string, callback: esp.AddBar.Callback[, position: esp.Position]): esp.Element
```

Adds a custom bar element, similar to the built-in health bar. `callback` is called for each entity and returns the values of the bar.


| Parameter | Type | Description |
| --- | --- | --- |
| category | `esp.Category` | The ESP category to add the element to. |
| name | `string` | The name of the element in the menu. |
| callback | `esp.AddBar.Callback` | Called for each entity. Returns the values of the bar. |
| position? | `esp.Position` | The default position. Defaults to `esp.Position.kBottom`. |


  

<a id="esp-AddText-Callback"></a>
### `esp.AddText.Callback`

The callback of a custom text element. It is called for each entity and returns the text to draw for that entity.


| Parameter | Type | Description |
| --- | --- | --- |
| entity | `client.C_BaseEntity` |  |


| Return | Type | Description |
| --- | --- | --- |
|  | `string` |  |


    
Return an empty string to hide the text for that entity. The callback receives **nil** when
there is no entity. Return an empty string in that case.

If the callback throws an error or returns a value that is not a string, nothing is drawn and
the error is shown as a script error.


  

  

<a id="esp-AddBar-Callback"></a>
### `esp.AddBar.Callback`

The callback of a custom bar element. It is called for each entity. The values are converted to integers.


| Parameter | Type | Description |
| --- | --- | --- |
| entity | `client.C_BaseEntity` |  |


| Return | Type | Description |
| --- | --- | --- |
|  | `integer` |  |
|  | `integer?` |  |


    
Return the current value, and optionally the maximum value. If you return a maximum, the bar is
filled to the current value as a percentage of the maximum, from 0 to 100, and the bar shows the
current value. If you do not return a maximum, the current value is used directly as the fill.

Return a negative current value to hide the bar. A maximum of 0 or less also hides the bar. The
callback receives **nil** when there is no entity. Return -1 in that case.

If the callback throws an error or returns a value that is not a number, nothing is drawn and
the error is shown as a script error.


  

  

<a id="esp-Category"></a>
### `esp.Category`

The ESP categories that a custom element can be added to. The first two are the player ESP lists. The others are the world ESP lists. Each world list draws its own kind of entity.


    

### `esp.Category`


| Name | Value | Description |
| --- | --- | --- |
| kEnemy | 0 | The player ESP for enemies. |
| kTeammates | 1 | The player ESP for teammates. |
| kBomb | 2 | The world ESP for the planted and the dropped C4. |
| kWeapon | 3 | The world ESP for dropped weapons. |
| kHostages | 4 | The world ESP for hostages. |
| kGrenades | 5 | The world ESP for grenades in flight and grenades that are deployed. |


  

  

<a id="esp-Position"></a>
### `esp.Position`

The side of the ESP box where a custom text or bar element is placed at first. This value is only the default. If the user saved a position for the element, the saved position is used.


    

### `esp.Position`


| Name | Value | Description |
| --- | --- | --- |
| kLeft | 0 | On the left of the box. |
| kTop | 1 | Above the box. |
| kRight | 2 | On the right of the box. |
| kBottom | 3 | Below the box. |


    
The world ESP categories always place their elements at the bottom. They accept any value, but
they always use `kBottom`.


  


## esp.Element — object type

A handle to a custom ESP element that was created by `esp.AddItem`, `esp.AddText` or
`esp.AddBar`. Reading or writing a field that does not exist throws an error.


  

### `esp.Element.name`

The name of the element in the menu. Read-only.


  

### `esp.Element.value`

Whether the user has turned the element on. You can also set this field.


  

### `esp.Element:AddGroup`

```lua
esp.Element:AddGroup(): ui.Group
```

Returns the options group of the colour picker of the element. You can add more controls to this group.
