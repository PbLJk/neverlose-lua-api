> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Cloud


<a id="cloud-1"></a>

## cloud  — global table


Gets information about the user account, the running script, and the loaded config. Also
gives access to the files that are shipped with the script.


  

### `cloud.GetUser`

```lua
cloud.GetUser(): cloud.User
```

Returns information about the user who is logged in. Other code can fake this information, so do not use it for security checks.


  

### `cloud.GetUsername`

```lua
cloud.GetUsername(): string
```

Returns the login name of the user who is logged in. Other code can fake this name, so do not use it for security checks.


  

### `cloud.GetScript`

```lua
cloud.GetScript(): cloud.Item
```

Returns information about the script that is running.


  

### `cloud.GetConfig`

```lua
cloud.GetConfig(): cloud.Item
```

Returns information about the config that is loaded.


    
Throws an error if no config is loaded. No config is loaded when the client starts, until the
first config is applied. The error is also thrown if the loaded config was removed. Wrap the
call in `pcall` if your code can run at these times.


  

  

### `cloud.ReadResource`

```lua
cloud.ReadResource(name: string): string
```

Returns the full path on disk to a file or folder that is shipped with the running script, such as an image or a sound. Returns an empty string if the script has no file or folder with that name.


| Parameter | Type | Description |
| --- | --- | --- |
| name | `string` | The name of the file or folder, relative to the root folder of the script. |


| Return | Type | Description |
| --- | --- | --- |
|  | `string` | The full path on disk, or an empty string. |


    
`name` is relative to the root folder of the script. For a developer script, the path points
into the folder of the script. For a market script, the file is first extracted to a temporary
folder. If `name` is a folder, every file in it is extracted. So the folder on disk has the
same files for both kinds of script.

`filesystem.List`, `filesystem.Read` and `filesystem.Info` accept the returned path. They also
accept other paths in the files of the script that are built from it, such as its parent
folder. This also works for market scripts.


  


## cloud.User — object type

Information about the user who is logged in.


  

### `cloud.User.avatar`

The avatar image.


  

### `cloud.User.license`

The license code of the account.


  

### `cloud.User.name`

The login name.


## cloud.Item — object type

Information about a script or a config.


  

### `cloud.Item.author`

The author of the item.


  

### `cloud.Item.id`

The ID of the item in the cloud. It stays the same across sessions. A developer script is not in the cloud, so its ID is valid only for the current session. Do not save the ID of a developer script.


  

### `cloud.Item.is_market`

`true` if the item comes from the market.


  

### `cloud.Item.modify_time`

The time the item was last modified, as a Unix timestamp in seconds.


  

### `cloud.Item.name`

The name of the item.
