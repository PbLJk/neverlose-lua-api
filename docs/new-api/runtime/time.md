> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Time


<a id="time-1"></a>

## time  — global table


Gets the current time and runs functions after a delay. Scripts do not have the `os` library,
so use these functions to get the time.


  

### `time.GetEpochMilliseconds`

```lua
time.GetEpochMilliseconds(): int64_t
```

Returns the number of milliseconds since 1 January 1970, UTC.


  

### `time.GetUnixTime`

```lua
time.GetUnixTime(): int64_t
```

Returns the number of seconds since 1 January 1970, UTC.


  

### `time.GetLocalTime`

```lua
time.GetLocalTime(): integer, integer, integer, integer
```

Returns the current local time of day as four numbers. These are the hour from 0 to 23, the minute, the second, and the millisecond from 0 to 999.


| Return | Type | Description |
| --- | --- | --- |
| hour | `integer` |  |
| minute | `integer` |  |
| second | `integer` |  |
| millisecond | `integer` |  |


  

### `time.Format`

```lua
time.Format(format: string[, t: int64_t]): string?
```

Formats a time as local time with a C `strftime` format string, for example `"%H:%M:%S"`.


| Parameter | Type | Description |
| --- | --- | --- |
| format | `string` | The `strftime` format string. |
| t? | `int64_t` | A Unix timestamp in seconds. If it is not given, the current time is used. |


    
Returns **nil** if the format uses a code that the Windows runtime does not know, such as `%P`,
`%l` or `%-d`. Also returns **nil** if the time cannot be converted to local time, for example
a negative timestamp.


  

  

### `time.Schedule`

```lua
time.Schedule(delay: number, callback: function[, ...: any])
```

Runs a function once after a delay.


| Parameter | Type | Description |
| --- | --- | --- |
| delay | `number` | The delay in seconds. |
| callback | `function` | The function to run after the delay. |
| ...? | `any` | The arguments to pass to the function. |


    
The delay is rounded down to whole milliseconds. A negative delay is treated as `0`. If
`delay` is NaN, the function throws an error. A script can have at most 16384 scheduled calls
that have not run yet. Past that, this function throws an error.

Scheduled calls that have not run yet are dropped when the script shuts down.
