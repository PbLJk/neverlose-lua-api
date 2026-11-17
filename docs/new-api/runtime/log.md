> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Logging

## log — global table

Writes text to the game console and to the event log on the screen.

Every function here converts its arguments to strings and joins them without a separator,
in the same way as `print`.


  

### `log.Print`

```lua
log.Print([...: any])
```

The same function as `print`. Writes a line to the game console with the `neverlose ·` prefix.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` | Values to print. |


    
When the Lua Output option of Log Events is enabled in the menu, the line is also added to
the event log on the screen.


  

  

### `log.Console`

```lua
log.Console([...: any])
```

Writes one line to the game console exactly as given, without the `neverlose ·` prefix. The line is always written to the console, whatever the Lua Output setting is. If the text is empty, nothing is written.


| Parameter | Type | Description |
| --- | --- | --- |
| ...? | `any` | Values to write. |


    
Colour codes change the colour of the text that comes after them. Use `\aRRGGBBAA` with eight
hex digits for a custom colour. The alpha digits are ignored, so the text is always fully
visible. Use `\aDEFAULT` for the default console colour and `\aACCENT` for the menu accent
colour.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/runtime/log:0:4ce450f79019"
log.Console("\a7FDBFFFFmy script\aDEFAULT loaded")
```


  

  

### `log.Event`

```lua
log.Event([icon: string, color: Color, ...: any])
```

Adds an entry to the event log on the screen. Entries are shown only while the Event Logs window is enabled in the menu. This function does not write to the game console. Use `log.Console` to write to the console. If the text is empty, no entry is added.


| Parameter | Type | Description |
| --- | --- | --- |
| icon? | `string` | The name of a Font Awesome icon, such as `"bell"`. If the name is not a known icon name, the string is drawn as it is, so you can also pass an icon character. Pass `""` to show no icon. Pass `nil` to use the default file icon. |
| color? | `Color` | The colour of the bar on the side of the entry, the icon, and the bold text. Pass `nil` to use the default blue colour, `Color(79, 125, 255)`. |
| ...? | `any` | The text of the entry. |


    
If the text is the same as the text of the last entry, the last entry stays on the screen
for longer and a counter such as `[x2]` is added to it.

Put `^` before and after the text that you want to be bold. Bold text is drawn in the colour
given by `color`. Use `\n` to start a new line.


    
```lua luaintelligence=true semantic="lua:cs2:cs2/api_reference/runtime/log:1:2ee2a095e30b"
log.Event("bell", Color(120, 200, 255), "Loaded ^", cloud.GetScript().name, "^")
```
