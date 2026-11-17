> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# File System


## filesystem — global table

Provides access to the game's working directory at `%steamdir%/steamapps/cs2/game/bin/win64/`,
the SearchPaths at `game/csgo/`, `game/core/`, `csgo_addons`, and `csgo_community_addons`,
and the directory used by `cloud.ReadResource`. Attempting to access any other paths will throw an error.

Paths for the game's directories should be relative paths.

See [https://developer.valvesoftware.com/wiki/VPK\_(file\_format)](https://developer.valvesoftware.com/wiki/VPK_\(file_format\)) for how game content is managed by CS2.

The files in the path returned by `cloud.ReadResource` cannot be modified. `filesystem.List` will show
cloud files that are not yet extracted, and `filesystem.Info` will return the time the cloud script was modified at.


  

### `filesystem.Read`

```lua
filesystem.Read(path: string[, is_binary: boolean]): string?
```

Reads a file and returns all of its contents. If the file is not in the working directory, the SearchPaths are checked. Returns **nil** if the file cannot be opened.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path to the file, relative to the working directory. |
| is_binary? | `boolean` | Whether to read the file in binary mode. The default is `false`. |


  

### `filesystem.Write`

```lua
filesystem.Write(path: string, contents: string[, is_binary: boolean]): boolean
```

Writes `contents` to a file and replaces any content that the file already has. If the file cannot be opened in the working directory, the SearchPaths are tried. Returns `true` if all of the data was written, and `false` otherwise.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path to the file, relative to the working directory. |
| contents | `string` | The data to write. |
| is_binary? | `boolean` | Whether to write the file in binary mode. The default is `false`. |


  

### `filesystem.Delete`

```lua
filesystem.Delete(path: string)
```

Deletes a file. If the file does not exist, nothing happens. Throws an error if the file exists but cannot be deleted.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path to the file, relative to the working directory. |


  

### `filesystem.Folder`

```lua
filesystem.Folder(path: string)
```

Creates a directory at the given path. If the directory already exists, nothing happens. The parent directory must already exist, or an error is thrown.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path of the directory to create, relative to the working directory. |


  

### `filesystem.List`

```lua
filesystem.List(path: string[, filter: string]): string[]
```

Returns the names of the entries in a directory. You can pass a wildcard pattern to keep only the names that match it. In the pattern, `*` matches any number of characters and `?` matches exactly one character.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path to the directory, relative to the working directory. |
| filter? | `string` | The wildcard pattern that names must match. If it is not given, all names are returned. |


    
Throws an error if the path is not an existing directory.


  

  

### `filesystem.Info`

```lua
filesystem.Info(path: string): filesystem.Info.Result
```

Returns the times and the size of a file. Throws an error if the file does not exist.


| Parameter | Type | Description |
| --- | --- | --- |
| path | `string` | The path to the file, relative to the working directory. |


## filesystem.Info.Result — object type

The file information returned by `filesystem.Info`.


  

### `filesystem.Info.Result.atime`

The time of the last access, as a Unix timestamp.


  

### `filesystem.Info.Result.ctime`

The time of creation, as a Unix timestamp.


  

### `filesystem.Info.Result.mtime`

The time of the last modification, as a Unix timestamp.


  

### `filesystem.Info.Result.size`

The size of the file in bytes.
