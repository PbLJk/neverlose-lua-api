> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Table Allocation

## Functions — global functions


  

### `table.new`

```lua
table.new(narray: integer, nhash: integer): table
```

An extra library function `table.new()` can be made available via `require("table.new")`. Returns an empty table with the requested array and hash capacity reserved.


| Parameter | Type | Description |
| --- | --- | --- |
| narray | `integer` | Pre-allocated array slots |
| nhash | `integer` | Pre-allocated hash slots |
