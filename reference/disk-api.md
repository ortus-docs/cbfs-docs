# Disk API

`IDisk` is the common provider contract. All providers expose the core operations below; providers may add capabilities documented in the [provider matrix](provider-capabilities.md).

## File operations

| Method | Description |
| --- | --- |
| `create(path, contents, visibility, metadata={}, overwrite=true, mode)` | Creates or replaces a file. |
| `createFromFile(source, directory, name, visibility, overwrite=true, deleteSource=false)` | Creates a file from an existing source path. |
| `setVisibility(path, visibility)` / `visibility(path)` | Sets or reads provider-specific visibility. |
| `prepend(path, contents, metadata={}, throwOnMissing=false)` | Writes contents before the current contents. |
| `append(path, contents, metadata={}, throwOnMissing=false)` | Writes contents after the current contents. |
| `copy(source, destination, overwrite=true)` / `move(...)` | Copies or moves a file. |
| `get(path)` / `getAsBinary(path)` | Reads text/structured contents or binary contents. |
| `exists(path)` / `missing(path)` | Tests path existence. S3 also supports `exists(path, force)`. |
| `delete(path, throwOnMissing=false)` | Deletes one path or an array of paths. |
| `touch(path, createPath=true)` | Creates an empty file. |

## Utility and verification methods

`url`, `temporaryUrl`, `download`, `size`, `lastModified`, `mimeType`, `info`, `checksum`, `name`, `extension`, `chmod`, and `createSymbolicLink` provide URL, metadata, hashing, path, permission, and link operations. Verification methods are `isFile`, `isDirectory`, `isWritable`, `isReadable`, `isExecutable`, `isHidden`, and `isSymbolicLink`.

Missing files and directories generally throw `FileNotFoundException` or `DirectoryNotFoundException`; see [Errors](errors.md).

## Directory methods

| Method | Description |
| --- | --- |
| `createDirectory(directory, createPath=true, ignoreExists=true)` | Creates a directory. |
| `copyDirectory(source, destination, recurse=false, filter, createPath=true)` | Copies a directory, optionally recursively and with a wildcard or closure filter. |
| `moveDirectory(source, destination, createPath=true)` | Moves a directory. |
| `deleteDirectory(directory, recurse=true, throwOnMissing=false)` | Deletes one or more directories. |
| `cleanDirectory(directory, throwOnMissing=false)` | Removes contents without removing the directory itself. |
| `contents(directory, filter, sort, recurse=false, type="all")` | Lists files and directories. |
| `allContents(...)` | Recursive `contents()`. |
| `files(...)` / `allFiles(...)` | Lists files, optionally recursively. |
| `directories(...)` / `allDirectories(...)` | Lists directories, optionally recursively. |
| `filesMap(...)` / `allFilesMap(...)` | Lists file metadata structs. |
| `contentsMap(...)` / `allContentsMap(...)` | Lists file contents. Use carefully with large files. |
| `glob(pattern)` | Finds paths matching a glob pattern where supported. |
