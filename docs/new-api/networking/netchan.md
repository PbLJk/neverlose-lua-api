> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Network Channel

## netchan — global table

Statistics for the current network connection to the game server. All fields are read-only.

Each field is read from the engine's net channel at the moment you access it. When the game is
not connected to a server, every field is **nil**.


  

### `netchan.address`

The address of the server.


  

### `netchan.avg_data`

The average amount of data in bytes per second, for each direction.


  

### `netchan.avg_latency`

The average network ping, in seconds.


  

### `netchan.avg_packets`

The average number of packets per second, for each direction.


  

### `netchan.data_rate`

The data rate set for the connection, in bytes per second.


  

### `netchan.dropped`

The fraction of packets that were dropped, for each direction.


  

### `netchan.engine_latency`

The outgoing ping that the engine measures, in seconds.


  

### `netchan.is_localhost`

Whether the server runs on the local computer.


  

### `netchan.is_loopback`

Whether the connection is a loopback connection.


  

### `netchan.is_playback`

Whether a demo is playing. This is `false` for a live connection.


  

### `netchan.is_timing_out`

Whether the connection is timing out at the moment.


  

### `netchan.late`

The fraction of packets that arrived too late, for each direction.


  

### `netchan.name`

The name of the connection.


  

### `netchan.peak_jitter`

The highest delivery jitter in milliseconds, for each direction.


  

### `netchan.sequence_nr`

The current packet sequence number, for each direction.


  

### `netchan.time`

The current time of the net channel, in seconds.


  

### `netchan.time_connected`

The number of seconds since the connection was made.


  

### `netchan.time_since_last_received`

The number of seconds since the last packet was received.


  

### `netchan.time_until_timeout`

The number of seconds that are left before the connection times out.


  

### `netchan.timeout`

The connection timeout in seconds.


  

### `netchan.total_data`

The total number of bytes sent or received, for each direction.


  

### `netchan.total_packets`

The total number of packets sent or received, for each direction.


  

### `netchan.RemoteFrametime`

```lua
netchan.RemoteFrametime(): number?, number?, number?
```

Returns the frame timing of the server, in seconds. The three values are the frame time, the standard deviation of the frame time, and the standard deviation of the frame start time.


| Return | Type | Description |
| --- | --- | --- |
| frametime | `number?` |  |
| frametime_stddev | `number?` |  |
| framestarttime_stddev | `number?` |  |


    
When the game is not connected to a server, all three values are **nil**.


  

  

### `netchan.GetInstance`

```lua
netchan.GetInstance(): userdata?
```

Returns a pointer to the net channel.


    


**Warning:** 
Use this pointer only with FFI. The pointer is owned by the connection. Do not keep it after the
game disconnects from the server.


  

  

<a id="netchan-FLOW-Value"></a>
### `netchan.FLOW.Value`

A table with one value for each direction of traffic. Use `netchan.FLOW` as the index. `[0]` is the value for outgoing traffic and `[1]` is the value for incoming traffic.


  

### `netchan.FLOW`

The direction of traffic. Use it as the index of a `netchan.FLOW.Value`.


    

### `netchan.FLOW`


| Name | Value | Description |
| --- | --- | --- |
| OUTGOING | 0 |  |
| INCOMING | 1 |  |
