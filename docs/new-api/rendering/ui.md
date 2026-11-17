> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# User Interface


## ui — global table

Creates and reads menu elements. Scripts can add their own tabs, groups and controls to the
menu, read and change the values of these controls, and find the built-in options of the cheat
to react to them.

The paths of built-in options can change between updates. Check that the result of `ui.Lookup`
is not `nil` before you use its fields.


  

### `ui.Lookup`

```lua
ui.Lookup(root: ui.Lookup.Root[, ...: string]): ui.Variable|ui.Group|ui.Tab|nil, ui.ColorPicker?
```

Finds a menu element by its path. Returns `nil` if no element matches the path. Throws an error if it is called without arguments, or if a segment is not a string.


| Parameter | Type | Description |
| --- | --- | --- |
| root | `ui.Lookup.Root` | The first segment of the path. |
| ...? | `string` | The other segments, one for each menu level. |


| Return | Type | Description |
| --- | --- | --- |
| element | `ui.Variable\|ui.Group\|ui.Tab\|nil` |  |
| color | `ui.ColorPicker?` | The colour picker of the control, if it has one. |


Accepted values for `root`:


| Value | Type / default | Description |
| --- | --- | --- |
| "Aimbot" |  |  |
| "Common" |  |  |
| "Extensions" |  | The tabs that scripts created. |
| "Settings" |  | The settings of the menu, such as the language, the scale and the units. |
| "ESP Options" |  | The options of the ESP preview. |


    
A path has one segment for each menu level, from the root down to the element. The segments are
the category, the tab, the group, any nested groups, and then the control. Write each segment as
it is shown in the English menu. Case and colour codes are ignored, so `"Hit Chance"` and
`"hit chance"` find the same control.

To get the exact path of a control, turn on developer mode, right click the control and choose
Copy Path. The generated menu reference in `menu/*.lua` lists every built-in path, with the type
of the control and the values that it accepts.

The type of the return value depends on where the path ends.

| The path ends at                     | Returns                                                                                      |
| ------------------------------------ | -------------------------------------------------------------------------------------------- |
| a control                            | `ui.Variable`. If the control has a colour picker, the picker is returned as a second value. |
| a group                              | `ui.Group`                                                                                   |
| a tab                                | `ui.Tab`                                                                                     |
| only `"Settings"` or `"ESP Options"` | `ui.Group`                                                                                   |
| only `"Aimbot"` or `"Common"`        | `nil`                                                                                        |

Some groups have weapon presets or map presets. By default, a path finds the element in the
global preset. To find the element in a specific preset, add the name of the preset right after
the tab, for example `ui.Lookup("Aimbot", "Rage", "AWP", "Selection", "Hit Chance")`.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/rendering/ui:0:bf2b205c07db"
local hit_chance = ui.Lookup("Aimbot", "Rage", "Selection", "Hit Chance") --[[@as ui.Variable?]]
local double_tap = ui.Lookup("Common", "Visuals", "World", "Miscellaneous", "Windows", "Indicators", "Double Tap") --[[@as ui.Variable?]]
local menu_scale = ui.Lookup("Settings", "Menu Scale") --[[@as ui.Variable?]]

if hit_chance then print("hit chance: ", hit_chance.value) end
if double_tap and double_tap.value then print("double tap indicator is on") end
if menu_scale then print("menu scale: ", menu_scale.value) end
```


  

  

### `ui.AddTab`

```lua
ui.AddTab(name: string): ui.Tab
```

Returns the tab with the given name in the sidebar entry of your script. If the tab does not exist, it is created.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the tab. |


  

### `ui.GetAlpha`

```lua
ui.GetAlpha(): number
```

Returns the current opacity of the menu, from `0` to `1`.


  

### `ui.GetScale`

```lua
ui.GetScale([type: ui.ScaleType]): number
```

Returns the DPI scale factor of the given part of the interface.


| Parameter | Type | Description |
| --- | --- | --- |
| type? | `ui.ScaleType` | The part of the interface. The default is `ui.ScaleType.kMenu`. |


  

### `ui.Scaled`

```lua
ui.Scaled(value: number[, type: ui.ScaleType]): number
```

Returns `value` multiplied by the DPI scale factor of the given part of the interface.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `number` | The value to scale. |
| type? | `ui.ScaleType` | The part of the interface. The default is `ui.ScaleType.kMenu`. |


  

### `ui.GetPosition`

```lua
ui.GetPosition(): Vector2D
```

Returns the position of the top left corner of the main menu window. Returns `nil` if the menu window has not been created yet.


  

### `ui.GetSize`

```lua
ui.GetSize(): Vector2D
```

Returns the size of the main menu window. Returns `nil` if the menu window has not been created yet.


  

### `ui.GetCursorPosition`

```lua
ui.GetCursorPosition(): Vector2D
```

Returns the current position of the mouse cursor on the screen.


  

### `ui.GetStyleColor`

```lua
ui.GetStyleColor(name: ui.StyleName): Color
```

Returns one colour of the current menu theme. Returns `nil` if the name is not a known colour name.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `ui.StyleName` | The name of the theme colour. |


Accepted values for `name`:


| Value | Type / default | Description |
| --- | --- | --- |
| "Text" |  | Text |
| "Disabled Text" |  | Disabled Text |
| "Active Text" |  | Active Text |
| "Small Text" |  | Small Text |
| "Grey Text" |  | Grey Text |
| "Logo" |  | Logo |
| "Sidebar Background" |  | Sidebar Background |
| "Popup Background" |  | Popup Background |
| "Main Window Background" |  | Main Window Background |
| "Preview Background" |  | Preview Background |
| "Border" |  | Border |
| "Frame Background" |  | Frame Background |
| "Frame Active Background" |  | Frame Active Background |
| "Text Preview" |  | Text Preview |
| "Window Title" |  | Window Title |
| "Active Window Title" |  | Active Window Title |
| "Scrollbar Background" |  | Scrollbar Background |
| "Scrollbar Grab" |  | Scrollbar Grab |
| "Scrollbar Grab Active" |  | Scrollbar Grab Active |
| "Switch" |  | Switch |
| "Switch Active" |  | Switch Active |
| "Switch Background" |  | Switch Background |
| "Switch Active Background" |  | Switch Active Background |
| "Slider Background" |  | Slider Background |
| "Slider Active Background" |  | Slider Active Background |
| "Slider Grab" |  | Slider Grab |
| "Slider Grab Active" |  | Slider Grab Active |
| "Button" |  | Button |
| "Button Active" |  | Button Active |
| "Button Text" |  | Button Text |
| "Button Active Text" |  | Button Active Text |
| "Link" |  | Link |
| "Link Active" |  | Link Active |
| "Selection" |  | Selection |
| "Separator" |  | Separator |
| "Tab" |  | Tab |
| "Text Selection" |  | Text Selection |
| "Shadows" |  | Shadows |
| "Spinner" |  | Spinner |
| "Block Background" |  | Block Background |
| "Sidebar Selection" |  | Sidebar Selection |
| "Logo Back" |  | Logo Back |
| "Transparent Background" |  | Transparent Background |


  

### `ui.GetStyle`

```lua
ui.GetStyle(): table
```

Returns all colours of the current menu theme in a table. The keys are the colour names and the values are `Color` objects.


  

### `ui.SetSidebarEntry`

```lua
ui.SetSidebarEntry([name: string, icon: string])
```

Sets the name, the icon, or both, of the sidebar entry of your script. If the entry does not exist yet, it is created.


| Parameter | Type | Description |
| --- | --- | --- |
| name? | `string` | The new name. Pass `nil` to keep the current name. |
| icon? | `string` | The name of the new icon. Pass `nil` to keep the current icon. If the name is not a known icon name, the string is used as the icon as it is. |


  

### `ui.Localize`

```lua
ui.Localize(lang: string, name: string, value: string)
```

Adds a translation of a menu string for one language. When the user selects that language, the menu shows the translation. Throws an error if the language is not known.


| Parameter | Type | Description |
| --- | --- | --- |
| lang | `string` | The short name of the language, such as `"en"` for English. A custom language uses the name of its file. |
| name | `string` | The original string. |
| value | `string` | The translation that is shown when this language is selected. |


    
`name` is a string that your script uses as menu text, such as the name of a control.


  

  

### `ui.GetUnitSystem`

```lua
ui.GetUnitSystem(): ui.UnitSystem
```

Returns the measurement system that the user selected in the menu, either `"imperial"` or `"metric"`.


  

### `ui.ConvertDistance`

```lua
ui.ConvertDistance(distance: number): number, string, ui.UnitSystem
```

Converts a distance in game units to the measurement system of the user. One game unit is one inch.


| Parameter | Type | Description |
| --- | --- | --- |
| distance | `number` | The distance in game units. |


    
Returns three values. The first value is the converted distance. The second value is the unit
suffix, `"m"` for metres or `"ft"` for feet. The third value is the measurement system, either
`"imperial"` or `"metric"`.


  

  

### `ui.GetActiveBinds`

```lua
ui.GetActiveBinds([include_hidden: boolean]): ui.ActiveBind[]
```

Returns the key binds that are active now.


| Parameter | Type | Description |
| --- | --- | --- |
| include_hidden? | `boolean` | Pass `true` to also return the binds that are hidden from the list. The default is `false`. |


  

<a id="ui-Lookup-Root"></a>
### `ui.Lookup.Root`

The first segment of a path for `ui.Lookup`.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "Aimbot" |  |  |
| "Common" |  |  |
| "Extensions" |  | The tabs that scripts created. |
| "Settings" |  | The settings of the menu, such as the language, the scale and the units. |
| "ESP Options" |  | The options of the ESP preview. |


  

<a id="ui-StyleName"></a>
### `ui.StyleName`

The names of the colours in the menu theme.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "Text" |  | Text |
| "Disabled Text" |  | Disabled Text |
| "Active Text" |  | Active Text |
| "Small Text" |  | Small Text |
| "Grey Text" |  | Grey Text |
| "Logo" |  | Logo |
| "Sidebar Background" |  | Sidebar Background |
| "Popup Background" |  | Popup Background |
| "Main Window Background" |  | Main Window Background |
| "Preview Background" |  | Preview Background |
| "Border" |  | Border |
| "Frame Background" |  | Frame Background |
| "Frame Active Background" |  | Frame Active Background |
| "Text Preview" |  | Text Preview |
| "Window Title" |  | Window Title |
| "Active Window Title" |  | Active Window Title |
| "Scrollbar Background" |  | Scrollbar Background |
| "Scrollbar Grab" |  | Scrollbar Grab |
| "Scrollbar Grab Active" |  | Scrollbar Grab Active |
| "Switch" |  | Switch |
| "Switch Active" |  | Switch Active |
| "Switch Background" |  | Switch Background |
| "Switch Active Background" |  | Switch Active Background |
| "Slider Background" |  | Slider Background |
| "Slider Active Background" |  | Slider Active Background |
| "Slider Grab" |  | Slider Grab |
| "Slider Grab Active" |  | Slider Grab Active |
| "Button" |  | Button |
| "Button Active" |  | Button Active |
| "Button Text" |  | Button Text |
| "Button Active Text" |  | Button Active Text |
| "Link" |  | Link |
| "Link Active" |  | Link Active |
| "Selection" |  | Selection |
| "Separator" |  | Separator |
| "Tab" |  | Tab |
| "Text Selection" |  | Text Selection |
| "Shadows" |  | Shadows |
| "Spinner" |  | Spinner |
| "Block Background" |  | Block Background |
| "Sidebar Selection" |  | Sidebar Selection |
| "Logo Back" |  | Logo Back |
| "Transparent Background" |  | Transparent Background |


  

<a id="ui-UnitSystem"></a>
### `ui.UnitSystem`


Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "imperial" |  |  |
| "metric" |  |  |


  

### `ui.ColorKey`

Selects a colour in a set or in a category, either by its position starting at 1 or by its name.


  

<a id="ui-ScaleType"></a>
### `ui.ScaleType`

The parts of the interface that each have their own DPI scale.


    

### `ui.ScaleType`


| Name | Value | Description |
| --- | --- | --- |
| kMenu | 0 | The menu. |
| kWindows | 1 | The windows on the screen, such as the event log. |
| kEsp | 2 | The ESP. |


  

  

<a id="ui-GroupColumn"></a>
### `ui.GroupColumn`

The column that a group is placed in.


    

### `ui.GroupColumn`


| Name | Value | Description |
| --- | --- | --- |
| kAuto | -1 | The tab chooses the column. |
| kLeft | 0 | The left column. |
| kRight | 1 | The right column. |


  


## ui.Element — object type

The fields and methods that all menu element handles share. Tabs, groups and controls are all
elements.

Read a field to get its value, and assign the field to change it. Reading or assigning a field
that the element does not have throws an error. Assigning a read only field also throws an
error.

Two handles are equal with `==` when they point to the same element. For example, two calls to
`ui.Lookup` with the same path return equal handles.

You can read the fields of any element. You can assign `name`, `visible`, `disabled` and `icon`
only on elements that your script created. Assigning them on other elements throws an error.


  

### `ui.Element.disabled`

Whether the element is disabled. A disabled element is grey and the user cannot change it.


  

### `ui.Element.icon`

The name of the icon of the element.


  

### `ui.Element.id`

A number that identifies the element. It is unique in the current session and is never used again for another element in that session. Read only. The element gets a new number after a reload or a restart, so do not save it.


  

### `ui.Element.name`

The name of the element, as it is shown in the English menu.


  

### `ui.Element.visible`

Whether the element is shown.


  

### `ui.Element:Export`

```lua
ui.Element:Export(): string
```

Returns the current state of the element as a JSON string.


  

### `ui.Element:Import`

```lua
ui.Element:Import(str: string)
```

Sets the state of the element from a string that `Export` returned. Throws an error if the string is not valid JSON.


| Parameter | Type | Description |
| --- | --- | --- |
| str | `string` | A string that `Export` returned. |


## ui.Tab — object type


A tab in the sidebar of the menu. A tab holds groups.


  

### `ui.Tab:AddGroup`

```lua
ui.Tab:AddGroup(name: string[, column: ui.GroupColumn]): ui.Group
```

Returns the group with the given name in this tab. If the group does not exist, it is created.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the group. |
| column? | `ui.GroupColumn` | The column of the group. The default is `ui.GroupColumn.kAuto`. |


## ui.Group — object type


A group in a tab. A group holds controls.


  

### `ui.Group:Entity`

```lua
ui.Group:Entity(name: string[, default_color: Color|string]): ui.Variable, ui.ColorPicker
```

Adds an entity selector with a colour picker. This is a menu control, and it is not related to game entities. Use `Chip` on the returned control to add items that the user can select.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the selector. |
| default_color? | `Color\|string` | The starting colour, as a `Color` or a hex string. The default is white. |


| Return | Type | Description |
| --- | --- | --- |
| control | `ui.Variable` |  |
| color | `ui.ColorPicker` |  |


    
The main switch and each chip have their own colour, like the world entities in the ESP
settings.


  

  

### `ui.Group:AddToggle`

```lua
ui.Group:AddToggle(name: string[, default_value: boolean]): ui.Variable
```

Adds a checkbox.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| default_value? | `boolean` | The starting state. The default is `false`. |


  

### `ui.Group:AddCombo`

```lua
ui.Group:AddCombo(name: string, items: table): ui.Variable
```

Adds a dropdown where the user selects one item. The first item is selected at the start.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| items | `table` | The names of the items that the user can select. |


  

### `ui.Group:AddMultiCombo`

```lua
ui.Group:AddMultiCombo(name: string, items: table): ui.Variable
```

Adds a dropdown where the user can select several items. No item is selected at the start. Throws an error if there are more than 32 items.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| items | `table` | The names of the items that the user can select. |


  

### `ui.Group:AddList`

```lua
ui.Group:AddList(name: string, items: table): ui.Variable
```

Adds a list where the user selects one item. The first item is selected at the start.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| items | `table` | The names of the items that the user can select. |


  

### `ui.Group:AddMultiList`

```lua
ui.Group:AddMultiList(name: string, items: table): ui.Variable
```

Adds a list where the user can select several items. No item is selected at the start. Throws an error if there are more than 32 items.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| items | `table` | The names of the items that the user can select. |


  

### `ui.Group:AddTextBox`

```lua
ui.Group:AddTextBox(name: string[, default_value: string]): ui.Variable
```

Adds a text input.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| default_value? | `string` | The starting text. The default is an empty string. |


  

### `ui.Group:AddLabel`

```lua
ui.Group:AddLabel(name: string): ui.Variable
```

Adds a line of text that the user cannot change.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The text of the label. |


  

### `ui.Group:AddButton`

```lua
ui.Group:AddButton(name: string): ui.Variable
```

Adds a button. Use `AddCallback` on the returned control to run code when the button is clicked.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the button. |


  

### `ui.Group:AddHotkey`

```lua
ui.Group:AddHotkey(name: string[, default_key: integer]): ui.Variable
```

Adds a hotkey control.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| default_key? | `integer` | The starting key code. The default is `0`, which means that no key is bound. |


  

### `ui.Group:AddColorPicker`

```lua
ui.Group:AddColorPicker(name: string[, default_value: (string|Color)]): ui.ColorPicker
```

Adds a colour picker with one colour.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| default_value? | `(string\|Color)` | The starting colour, as a `Color` or a hex string such as `"#RRGGBB"` or `"#RRGGBBAA"`. The default is white. |


  

### `ui.Group:AddColorSet`

```lua
ui.Group:AddColorSet(name: string, colors: (Color|{ name: string, value: Color })[]): ui.ColorSet
```

Adds a colour set. A colour set is an ordered list of two or more colours, and each colour has a fixed role. For example, the first colour can be the start of a gradient and the second colour can be the end. Throws an error if there are fewer than two colours.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| colors | `(Color\|{ name: string, value: Color })[]` | The colours in order. Each entry is a `Color`, or a table with a `name` and a `value`. |


  

### `ui.Group:AddColorModes`

```lua
ui.Group:AddColorModes(name: string, categories: ui.ColorModes.Mode[]): ui.ColorModes
```

Adds a mode picker. A mode picker has two or more categories, and each category has its own colours. The user selects one category at a time. Throws an error if there are fewer than two categories.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| categories | `ui.ColorModes.Mode[]` | The modes that the user can select. |


    
With up to three categories, the categories are shown as tabs. With more than three categories,
they are shown in a dropdown.


  

  

### `ui.Group:AddImage`

```lua
ui.Group:AddImage(image: Image[, size: Vector2D, rounding: number, mode: render.ImageMode, color: Color]): ui.Variable
```

Adds an image to the menu.


| Parameter | Type | Description |
| --- | --- | --- |
| image | `Image` | The image to show. |
| size? | `Vector2D` | The size of the image. If both parts are `0`, the original size of the image is used. If one part is `0`, it is calculated from the other part so that the image keeps its proportions. The default is the original size. |
| rounding? | `number` | The radius of the rounded corners. The default is `0`. |
| mode? | `render.ImageMode` | How the image fills its size. The default is `render.ImageMode.kFill`. |
| color? | `Color` | The colour that the image is tinted with. The default is white. |


  

### `ui.Group:AddSlider`

```lua
ui.Group:AddSlider(name: string, min: integer, max: integer[, default: integer, scale: number, format: ui.Group.AddSlider.Format]): ui.Variable
```

Adds a slider. A slider stores an integer. `min` and `max` are rounded to the nearest integer. Throws an error if `min` or `max` is not a finite number, or if `max` is less than `min`.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the control. |
| min | `integer` | The smallest value. |
| max | `integer` | The largest value. |
| default? | `integer` | The starting value. It is rounded and kept between `min` and `max`. The default is `min`. |
| scale? | `number` | The shown value is the stored value multiplied by this number. For example, `0.1` shows one decimal place. It must be a finite number other than zero, or an error is thrown. The default is `1`. |
| format? | `ui.Group.AddSlider.Format` | How the value is shown. |


  

<a id="ui-Group-AddSlider-Format"></a>
### `ui.Group.AddSlider.Format`

Sets how the value of a slider is shown.


    
Pass a string to show it as a suffix after the number. The string is cut to five bytes, without
splitting a character. It is not a printf format.

Pass a function to build the whole text from the stored integer value. If the range of the
slider is wider than 65536 steps, the function is not used and an error message is printed.


  


## ui.Variable — object type


A control in a group. Read `v.value` to get the value, and assign `v.value = x` to change it.
The type of `value` depends on the type of the control.

| Control      | `value`                                                                                                              |
| ------------ | -------------------------------------------------------------------------------------------------------------------- |
| toggle       | `boolean`                                                                                                            |
| slider       | `integer`, the stored value before the scale is applied                                                              |
| combo        | `string`, the name of the selected item                                                                              |
| list         | `integer`, the position of the selected item, starting at 1                                                          |
| multicombo   | `string[]`, the names of the selected items                                                                          |
| multilist    | `integer[]`, the positions of the selected items, starting at 1                                                      |
| textbox      | `string`                                                                                                             |
| label        | `string`, the text of the label. Assigning it has no effect.                                                         |
| button       | `true` in the frame when the button is clicked. Assigning any value clicks the button.                               |
| color picker | `Color`. See `ui.ColorPicker`.                                                                                       |
| color set    | A view of the colours. See `ui.ColorSet`.                                                                            |
| color modes  | A view of the categories. See `ui.ColorModes`.                                                                       |
| skyboxes     | `string`, the material file name without the extension, such as `"sky_de_dust2"`. `"Default"` is the sky of the map. |

When you assign a combo, the name is compared without case, and a name that is not in the list
is ignored. To assign a multicombo or a multilist, pass a list of item names or positions, or a
table with item names as keys and `true` as values.

A skybox selector lists its names in `items`. Until the game materials are scanned, the list
holds only `"Default"`, and reading a selected skybox returns `nil`. After the scan, assigning a
name that is not in the list is ignored. Assigning a value that is not a string throws an error.

Some fields exist only for some control types. These are `values`, `raw_values`,
`effective_values`, `is_down`, `items`, `min`, `max`, `category` and `categories`. Reading them
on other control types throws an error, in the same way as unknown fields.


  

### `ui.Variable.default`

The default value, which the control is reset to. You can assign it only on controls that your script created. Assigning it also sets the value, unless the config of the user already has a saved value for this control. In that case, the saved value is kept. An active override is not changed.


  

### `ui.Variable.effective_value`

The value that features use. This is `raw_value` if an override is set, and `value` if not. Read only. It is the same as `variable:Get()`.


  

### `ui.Variable.effective_values`

Multi select controls only. The override if there is one, and the selected items if not. Read only.


  

### `ui.Variable.is_down`

Hotkeys only. Whether the hotkey is active now. Read only.


  

### `ui.Variable.items`

Combos, lists and skybox selectors only. The names of the items. Assign a table to replace the items of a combo or a list that your script created. The items of a skybox selector are read only.


  

### `ui.Variable.max`

Sliders only. The largest value. You can assign it only on sliders that your script created. The new value must be a finite number that is greater than `min`, or an error is thrown. If the range becomes wider than 65536 steps, the format function is no longer used.


  

### `ui.Variable.min`

Sliders only. The smallest value. You can assign it only on sliders that your script created. The new value must be a finite number that is less than `max`, or an error is thrown. If the range becomes wider than 65536 steps, the format function is no longer used.


  

### `ui.Variable.parent`

The group that holds this control. Read only.


  

### `ui.Variable.raw_value`

The override. Reading it returns the active override, or `nil` if there is none. Assigning it sets an override that features use instead of `value`, and the config of the user is not changed. Assign `nil` to remove the override.


  

### `ui.Variable.raw_values`

Multi select controls only. The override as a table in the same form, or `nil` if there is no override. Assigning it works like assigning `raw_value`.


  

### `ui.Variable.tooltip`

The tooltip text. You can assign it only on controls that your script created.


  

### `ui.Variable.type`

The name of the control type, such as `toggle`, `slider` or `combo`. Read only.


  

### `ui.Variable.value`

The value in the menu. Reading it ignores an active override.


  

### `ui.Variable.values`

Multi select controls only. The selected items as a table, with item names as keys and `true` as values. Assigning it works like assigning `value`.


  

### `ui.Variable:Get`

```lua
ui.Variable:Get([...: string|integer]): any
```

Returns the value that features use. This is the `raw_value` override if one is set, and `value` if not. Without arguments, it is the same as reading `effective_value`. For colour sets and colour modes, it returns a view of the colours.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `string\|integer` | Multi select controls only. The name or the position of the item to check. |


    
For multi select controls, you can pass the name of an item, or its position starting at 1. The
function then returns whether that item is selected, instead of the whole selection.


  

  

### `ui.Variable:GetValue`

```lua
ui.Variable:GetValue([...: string|integer]): any
```

Returns the value in the menu and ignores an active override. This is the method form of reading `value`. Multi select controls accept the same arguments as `Get`.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `string\|integer` | Multi select controls only. The name or the position of the item to check. |


  

### `ui.Variable:SetValue`

```lua
ui.Variable:SetValue(value: any)
```

Sets the value in the menu. This also removes an active override. This is the method form of assigning `value`.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `any` | The new value, in the form that `value` accepts for this control type. |


  

### `ui.Variable:GetRawValue`

```lua
ui.Variable:GetRawValue([...: string|integer]): any
```

Returns the active override, or **nil** if there is none. This is the method form of reading `raw_value`. Multi select controls accept the same arguments as `Get`.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `string\|integer` | Multi select controls only. The name or the position of the item to check. |


  

### `ui.Variable:SetRawValue`

```lua
ui.Variable:SetRawValue(value: any)
```

Sets an override that features use instead of the menu value. The config of the user is not changed. Pass **nil** to remove the override. This is the method form of assigning `raw_value`.


| Parameter | Type | Description |
| --- | --- | --- |
| value | `any` | The override value, or `nil` to remove the override. |


  

### `ui.Variable:Chip`

```lua
ui.Variable:Chip(name: string[, default_value: boolean]): ui.Variable, ui.ColorPicker
```

Adds a chip to an entity selector that your script created. The user can select the chip, and the chip has its own colour. Throws an error if the control is not an entity selector, or if another script created it.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The label of the chip. |
| default_value? | `boolean` | The starting selection. The default is `false`. |


| Return | Type | Description |
| --- | --- | --- |
| control | `ui.Variable` |  |
| color | `ui.ColorPicker` |  |


  

### `ui.Variable:AddGroup`

```lua
ui.Variable:AddGroup(): ui.Group
```

Returns a group that is attached to this control, so that you can add controls inside it. If the control already has such a group, that group is returned. Throws an error if the control is itself inside a group that is attached to another control.


  

### `ui.Variable:AddCallback`

```lua
ui.Variable:AddCallback(fn: fun(self: ui.Variable)[, call_now: boolean]): ui.Variable
```

Adds a function that is called with the control when its value changes. You can add several different functions. Adding the same function again has no effect.


| Parameter | Type | Description |
| --- | --- | --- |
| fn | `fun(self: ui.Variable)` | The function to add. |
| call_now? | `boolean` | Pass `true` to also call `fn` once right away. The default is `false`. |


| Return | Type | Description |
| --- | --- | --- |
|  | `ui.Variable` | The same control, so that you can chain calls. |


    
Pass `true` for `call_now` to also call the function once right away. If the function throws
an error, the error is printed and is not passed to the caller.


  

  

### `ui.Variable:RemoveCallback`

```lua
ui.Variable:RemoveCallback(fn: fun(self: ui.Variable)): ui.Variable
```

Removes a function that was added with `AddCallback`. Pass the same function value that you added.


| Parameter | Type | Description |
| --- | --- | --- |
| fn | `fun(self: ui.Variable)` | The function to remove. |


| Return | Type | Description |
| --- | --- | --- |
|  | `ui.Variable` | The same control, so that you can chain calls. |


  

### `ui.Variable:AddColorPicker`

```lua
ui.Variable:AddColorPicker([default_value: (string|Color)]): ui.ColorPicker
```

Adds a colour picker with one colour next to this control, for example next to a toggle, and returns the picker. Throws an error if your script did not create the control, or if the control does not support colour pickers.


| Parameter | Type | Description |
| --- | --- | --- |
| default_value? | `(string\|Color)` | The starting colour, as a `Color` or a hex string. The default is white. |


  

### `ui.Variable:AddColorSet`

```lua
ui.Variable:AddColorSet(colors: (Color|{ name: string, value: Color })[]): ui.ColorSet
```

Adds a colour set with two or more colours, each with a fixed role, next to this control, and returns the picker. Throws an error if there are fewer than two colours, if your script did not create the control, or if the control does not support colour pickers.


| Parameter | Type | Description |
| --- | --- | --- |
| colors | `(Color\|{ name: string, value: Color })[]` | The colours in order. |


  

### `ui.Variable:AddColorModes`

```lua
ui.Variable:AddColorModes(categories: ui.ColorModes.Mode[]): ui.ColorModes
```

Adds a mode picker with two or more categories next to this control, and returns the picker. Throws an error if there are fewer than two categories, if your script did not create the control, or if the control does not support colour pickers.


| Parameter | Type | Description |
| --- | --- | --- |
| categories | `ui.ColorModes.Mode[]` | The modes that the user can select. |


## ui.ColorPicker — object type


A picker with exactly one colour. `value`, `raw_value` and `default` are plain `Color` values.


  

### `ui.ColorPicker.default`

The default colour.


  

### `ui.ColorPicker.raw_value`

The override colour, or `nil` if there is none. Assign `nil` to remove the override.


  

### `ui.ColorPicker.value`

The colour.


## ui.ColorsNode — object type

A live view of the colours of a colour set. Index it with a `ui.ColorKey` to read a `Color` or
to assign one. An assignment changes the control right away. The view supports `#`, `pairs` and
`ipairs`. With `pairs`, the keys are the colour names, or the positions for colours that have no
name.

When you get the view through `raw_value`, reading a colour that has no override returns `nil`.
Assigning `nil` to a colour removes the override of that colour only. In other views, assigning
`nil` throws an error.

The view always shows the current state of the control, so you can keep it for as long as you
want.


  

### `ui.ColorsNode[string|integer]`


  

<a id="uicolorsnode"></a>
### `#ui.ColorsNode`


## ui.ColorSet — object type


A picker with an ordered set of two or more colours, each with a fixed role. It has no single
value. Use `value[color]` to read or assign one colour.


  

### `ui.ColorSet.default`

The default colours, one for each colour. You can assign them only on pickers that your script created. If the config of the user has a saved value, the saved value is kept.


  

### `ui.ColorSet.raw_value`

The overrides, one for each colour. You can override each colour separately. Assign `nil` to the field itself to remove all overrides.


  

### `ui.ColorSet.value`

The colours. `v.value['start'] = Color(...)` changes one colour.


## ui.ColorCategoryNode — object type

A live view of the categories of a mode picker. Index it with the position of a category,
starting at 1, or with its name, to get the colours of that category. The view supports `#`,
`pairs` and `ipairs` over the categories.


  

### `ui.ColorCategoryNode[string|integer]`


  

<a id="uicolorcategorynode"></a>
### `#ui.ColorCategoryNode`


## ui.ColorModes — object type


A picker with two or more categories, also called modes. The user switches between them, and
features check `category` to know which mode is selected. Each category has its own colours,
which you address with `value[category][color]`.


  

### `ui.ColorModes.categories`

The names of the categories. Read only.


  

### `ui.ColorModes.category`

The selected category. Reading it returns the position of the category, starting at 1. Assign a position or a category name. Throws an error if the category does not exist.


  

### `ui.ColorModes.default`

The default colours, addressed in the same way.


  

### `ui.ColorModes.raw_value`

The overrides, addressed in the same way. Assign `nil` to the field itself to remove all overrides.


  

### `ui.ColorModes.value`

The colours of all categories. `v.value['Gradient']['start'] = Color(...)` changes one colour.


  

<a id="ui-ColorModes-Mode"></a>
### `ui.ColorModes.Mode`

One mode of a picker that `AddColorModes` created. A mode is a category with its own colours.


## ui.ActiveBind — object type

One key bind in the key bind list on the screen.


  

### `ui.ActiveBind.is_active`

Whether the bind is active now.


  

### `ui.ActiveBind.mode`

How the bind is activated. `0` is toggle and `1` is hold.


  

### `ui.ActiveBind.name`

The name of the option that the bind controls, as it is shown in the list.


  

### `ui.ActiveBind.reference`

The menu control that the bind belongs to.


  

### `ui.ActiveBind.should_show`

Whether the bind should be shown in the list.


  

### `ui.ActiveBind.value`

The current value of the option that the bind controls.
