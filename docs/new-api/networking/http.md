> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# HTTP


<a id="http-1"></a>

## http  — global table


Sends HTTP requests. Every request runs in the background, and the response is passed to
`callback` when it arrives.

Add `http` to the `requirements` in `extension.json` before you call `require("http")`.

You can leave out `options`. So `http.Get(url, callback)` and `http.Get(url, options, callback)`
both work. A value in the place of `options` that is not a table, such as `false`, counts as no
options.

A callback runs only if the script is still loaded when the response arrives. When another
script is turned on or off, or a developer script is saved, all scripts are reloaded and the
callbacks that are waiting are dropped. In that case the `shutdown` callback of the script
receives `"refresh"` or `"reload"`, and the script can send the request again.

A script can have at most 64 requests that have not finished. Past that, a new request throws
an error and is not sent.

A header name that is not a string throws an error. A header name or value that contains CR, LF
or NUL also throws an error. An option key that is not listed in `http.Options` is ignored, and
the request is still sent. In a developer script, an unknown key also adds a warning to the
errors of the script, once for each key.

Redirects are followed. Only the `http` and `https` schemes are allowed. Certificates are always
checked.

Market scripts cannot send requests to the computer of the user or to a private network. Such
requests fail with the `"blocked"` error.


  

### `http.Get`

```lua
http.Get(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `GET` request.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

### `http.Head`

```lua
http.Head(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `HEAD` request. The server returns only the headers, so the body of the response is empty.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

### `http.Post`

```lua
http.Post(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `POST` request.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

### `http.Put`

```lua
http.Put(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `PUT` request.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

### `http.Delete`

```lua
http.Delete(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `DELETE` request.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

### `http.Patch`

```lua
http.Patch(url: string[, options: http.Options], callback: http.Callback)
```

Sends a `PATCH` request.


| Parameter | Type | Description |
| --- | --- | --- |
| url | `string` | The URL of the request. |
| options? | `http.Options` | The options of the request. |
| callback | `http.Callback` | The function that receives the response when the request is finished. |


  

<a id="httpcookies"></a>
### `http.Cookies`

```lua
http.Cookies(): http.Cookies
```

Creates a new cookie container. Pass it in `options.cookie` of a request.


  

<a id="http-Error"></a>
### `http.Error`

The reason why no response arrived.

Accepted values for ``:


| Value | Type / default | Description |
| --- | --- | --- |
| "blocked" |  | The address is on the computer of the user or on a private network. Market scripts cannot send requests there. |
| "resolve" |  | The host name could not be found. |
| "connect" |  | The connection to the server failed. |
| "timeout" |  | The request took longer than `timeout`, or the connection stalled. |
| "tls" |  | The secure connection failed, for example because of a bad certificate. |
| "too_large" |  | The body of the response was larger than 64 MB. |
| "bad_url" |  | The URL is not valid, or its scheme is not `http` or `https`. |
| "failed" |  | Any other error. |


  

<a id="http-Callback"></a>
### `http.Callback`


| Parameter | Type | Description |
| --- | --- | --- |
| response | `http.Response` |  |


## http.Response — object type

The response to a request. `status` is `0` only when `error` is set. An HTTP error status such
as `404` is still a response, so `error` is `nil` for it.


  

### `http.Response.body`

The body of the response.


  

### `http.Response.error`

The reason why no response arrived. It is `nil` when a response arrived.


  

### `http.Response.status`

The HTTP status code. It is `0` when no response arrived.


## http.Authorization — object type


  

### `http.Authorization.password`


  

### `http.Authorization.username`


## http.Options — object type


  

### `http.Options.authorization`

The user name and password for HTTP authentication.


  

### `http.Options.cookie`

A cookie container. Its cookies are sent with the request, and the cookies from the response are added to it.


  

### `http.Options.headers`

The request headers, with header names as keys.


  

### `http.Options.json`

A JSON string to send as the body. It sets the `Content-Type: application/json` header. When `json` is set, `params` is ignored.


  

### `http.Options.params`

The parameters, as a table of names and values or as a string that is already encoded. For `POST`, `PUT` and `PATCH` they are sent in the body as form data. For other methods they are added to the query string of the URL. A string that contains CR, LF or NUL throws an error.


  

### `http.Options.timeout`

The time limit for the whole request, in seconds. The default is `30`. The value is clamped to the range from `1` to `300`.


## http.Cookie — object type


  

### `http.Cookie.expire`

The time the cookie expires, as a Unix timestamp in seconds.


  

### `http.Cookie.host`


  

### `http.Cookie.name`


  

### `http.Cookie.path`

The path of the cookie. The default is `"/"`.


  

### `http.Cookie.secure`

`true` to send the cookie only over HTTPS.


  

### `http.Cookie.subdomains`

`true` to also send the cookie to subdomains of `host`.


  

### `http.Cookie.value`


## http.Cookies — object type

A container for cookies. It holds cookies to send with requests, and it collects the cookies
that servers return. Use the same container for several requests to keep the cookies between
them. Create a container with `http.Cookies`.


  

### `http.Cookies:Set`

```lua
http.Cookies:Set(cookie: http.Cookie)
```

Adds a cookie to the container. If `expire` is `0`, the cookie is a session cookie.


| Parameter | Type | Description |
| --- | --- | --- |
| cookie | `http.Cookie` | The cookie to add. |


    
Throws an error if a string field contains CR, LF, NUL or TAB.
