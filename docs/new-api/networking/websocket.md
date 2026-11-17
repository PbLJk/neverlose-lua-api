> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# WebSocket


<a id="websocket-1"></a>

## websocket  — global table


Opens WebSocket connections. A connection stays open, and it passes what happens to the
callbacks that you give to `websocket.Connect`.

Add `websocket` to the `requirements` in `extension.json` before you call
`require("websocket")`.

You can leave out `options`. So `websocket.Connect(url, callbacks)` and
`websocket.Connect(url, options, callbacks)` both work. A value in the place of `options` that is
not a table, such as `false`, counts as no options.

Market scripts can connect only to `wss://` URLs on public addresses. Developer scripts can also
use `ws://` URLs and connect to the computer of the user or to a private network. For a `wss://`
URL, the certificate of the server must be valid for its host name.

Callbacks run only while the script is loaded. All scripts are reloaded together. So when
another script is turned on or off, or a developer script is saved, every open socket is closed
with code `1001`, and none of its callbacks run again. In that case the `shutdown` callback of
the script receives `"refresh"` or `"reload"`, and the script can connect again when it runs.

A socket stays open as long as the script is loaded, even if no variable holds its
`websocket.Socket` any more.

A script can have at most 16 sockets that are not closed. Past that, `websocket.Connect` throws
an error. A message can be at most 64 MB. At most 64 callbacks of one socket run in one frame,
and the rest run in the next frames. If 4096 messages or 64 MB of messages are waiting for the
script, the socket is closed with the `"overflow"` error.

A socket does not reconnect by itself, and it does not send pings to the server. To find a
connection that stopped working without a close, send a message on a timer and wait for a reply.

An option key or a callback key that is not listed below is ignored. In a developer script, an
unknown key also adds a warning to the errors of the script, once for each key.


  

### `websocket.Connect`

```lua
websocket.Connect(url: string[, options: websocket.Options], callbacks: websocket.Callbacks): websocket.Socket
```

Starts to connect and returns at once. Everything that happens after that is passed to `callbacks`. This includes a failure to connect.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL to connect to. It must start with `wss://`. Developer scripts can also use `ws://`. |
| options? | `websocket.Options` | The options of the connection. |
| callbacks | `websocket.Callbacks` | The functions to call when something happens on the connection. |


    
Throws an error in these cases. A callback is not a function. A header name is not a string, or
it is not a valid HTTP token. A header value contains CR, LF or NUL. A subprotocol is not a valid
HTTP token. A header is `Host`, `Upgrade`, `Connection` or starts with `Sec-WebSocket-`. The
handshake sets these headers itself.


  

  

<a id="websocket-Error"></a>
### `websocket.Error`

The reason why a connection failed or was lost.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "blocked" |  | The address is on the computer of the user or on a private network. Market scripts cannot connect there. |
| "resolve" |  | The host name could not be found. |
| "connect" |  | The connection to the server failed. |
| "timeout" |  | The connection or the handshake took too long. |
| "tls" |  | The secure connection failed, for example because of a bad certificate. |
| "too_large" |  | A message was larger than 64 MB. |
| "bad_url" |  | The URL is not valid, or its scheme is not `wss`. Developer scripts can also use `ws`. |
| "handshake" |  | The server replied, but it did not accept a WebSocket connection. |
| "lost" |  | The connection was lost without a closing handshake. |
| "overflow" |  | Messages arrived faster than the script handled them, and too many messages were waiting. |
| "failed" |  | Any other error. |


  

<a id="websocket-State"></a>
### `websocket.State`


Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "connecting" |  | The connection is not open yet. |
| "open" |  | The connection is open. Messages can be sent and received. |
| "closing" |  | `Close` was called, and the closing handshake has started. |
| "closed" |  | The connection is closed. |


## websocket.Options — object type


  

### `websocket.Options.headers`

Extra headers to send with the handshake request.


  

### `websocket.Options.protocols`

One or more subprotocols to offer to the server.


## websocket.Callbacks — object type

All callbacks are optional. Each callback receives the socket as its first argument.

`close` is always the last callback of a socket, and it is called exactly once, whether the
connection opened or not. When the connection failed or was lost, `error` is called just
before `close`.


  

### `websocket.Callbacks.close`

Called when the connection is closed. `code` is `1006` when the server did not send a close frame.


  

### `websocket.Callbacks.error`

Called when the connection failed or was lost.


  

### `websocket.Callbacks.message`

Called when a message arrives. `is_binary` is `true` for a binary message.


  

### `websocket.Callbacks.open`

Called when the connection is open. `protocol` is the subprotocol that the server chose, or `""` if it chose none.


## websocket.Socket — object type

A connection that `websocket.Connect` opened.


  

### `websocket.Socket:Send`

```lua
websocket.Socket:Send(data: string[, binary: boolean]): boolean
```

Sends a message. Returns `true` if the message was queued to be sent.


| Parameter | Type | Description |
| --- | --- | --- |
| data | `string` | The message to send. |
| binary? | `boolean` | `true` to send a binary message. The default is `false`, which sends a text message. |


| Return | Type | Description |
| --- | --- | --- |
| sent | `boolean` |  |


    
Returns `false` and sends nothing in these cases. The socket is not open, which includes the
time before `open` is called. A text message is not valid UTF-8. More than 64 MB is still
waiting to be sent.


  

  

### `websocket.Socket:Close`

```lua
websocket.Socket:Close([code: integer, reason: string])
```

Closes the connection. The `close` callback is called when the closing handshake is done. If the socket is still connecting, `open` is not called. If the socket is already closing or closed, this function does nothing.


| Parameter | Type | Description |
| --- | --- | --- |
| code? | `integer` | The close code. The default is `1000`. |
| reason? | `string` | The reason for closing, as text. |


    
Throws an error if `code` is not `1000` and not in the range from `3000` to `4999`. Also throws
an error if `reason` is longer than 123 bytes. If `reason` is not valid UTF-8, it is not sent.


  

  

### `websocket.Socket:State`

```lua
websocket.Socket:State(): websocket.State
```

Returns the state of the connection.
