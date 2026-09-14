# File Object

A File object binds a relative path to a disk and forwards file operations fluently. Create one with `disk.file( "path/to/file.txt" )`.

| Method | Returns | Description |
| --- | --- | --- |
| `create(contents, visibility, metadata={}, overwrite=true, mode)` | `File` | Creates the file. |
| `setVisibility(visibility)` | `File` | Updates visibility. |
| `visibility()` | `string` | Reads visibility. |
| `prepend(contents, metadata={}, throwOnMissing=false)` | `File` | Prepends contents. |
| `append(contents, metadata={}, throwOnMissing=false)` | `File` | Appends contents. |
| `copy(destination, overwrite=true)` | `File` | Copies and returns a File for the destination. |
| `move(destination, overwrite=true)` | `File` | Moves and returns a File for the destination. |
| `get()` | `any` | Reads contents. |
| `delete(throwOnMissing=false)` | `boolean` | Deletes the bound path. |
| `download()` | `string` | Sends the file to the browser. |
| `touch(createPath=true)` | `File` | Creates an empty file. |
| `size()` / `lastModified()` | `numeric` / date | Returns file size or modification time. |
| `mimeType()` / `info()` | `string` / `struct` | Returns type or provider metadata. |
| `checksum(algorithm="MD5")` | `string` | Returns a checksum. |
| `name()` / `extension()` | `string` | Returns path components. |
| `chmod(mode)` | `File` | Sets Unix-style permissions where supported. |
| `isWritable()` / `isReadable()` | `boolean` | Checks access. |
| `isExecutable()` / `isHidden()` / `isSymbolicLink()` | `boolean` | Checks file attributes. |
| `exists()` / `missing()` | `boolean` | Checks whether the bound path exists. |
| `url()` / `temporaryUrl(expiration)` | `string` | Builds a public or temporary URL. |

Mutating methods return the File object where noted, allowing chains such as `disk.file( "a.txt" ).create( "a" ).append( "b" )`.
