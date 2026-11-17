> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Table Clearing

## Functions — global functions


  

### `table.clear`

```lua
table.clear(tab: table)
```

An extra library function `table.clear()` can be made available via `require("table.clear")`. This clears all keys and values from a table, but preserves the allocated array/hash sizes. Existing references still point to the cleared table, allowing its storage to be reused.


| Parameter | Type | Description |
| --- | --- | --- |
| tab | `table` | Table to clear |
