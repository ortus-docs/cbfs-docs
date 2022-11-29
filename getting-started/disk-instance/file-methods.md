# File Methods

### append

Append contents to the end of a file.

```javascript
/**
 * @path           The file path to use for storage
 * @contents       The contents of the file to append
 * @metadata       Struct of metadata to store with the file
 * @throwOnMissing Boolean flag to throw if the file is missing. Otherwise it will be created if missing.
 *
 * @return LocalProvider
 *
 * @throws cbfs.FileNotFoundException
 */
function append(
	required string path,
	required contents,
	struct metadata        = {},
	boolean throwOnMissing = false
);
```

### copy

Copy a file from one destination to another.

```javascript
/**
 * @source      The source file path
 * @destination The end destination path
 * @overwrite   Flag to overwrite the file at the destination, if it exists. Defaults to true.
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.FileNotFoundException - When the source doesn't exist
 * @throws cbfs.FileOverrideException - When the destination exists and no override has been provided
 */
function copy(
	required source,
	required destination,
	boolean overwrite = true
);
```

### create

Create a file on the disk.

```javascript
/**
 * @path       The file path to use for storage
 * @contents   The contents of the file to store
 * @visibility The storage visibility of the file, available options are `public, private, readonly` or a custom data type the implemented driver can interpret
 * @metadata   Struct of metadata to store with the file
 * @overwrite  Flag to overwrite the file at the destination, if it exists. Defaults to true.
 * @mode       Applies to *nix systems. If passed, it overrides the visbility argument and uses these octal values instead
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.FileOverrideException - When a file exists and no override has been provided
 */
function create(
	required path,
	required contents,
	string visibility = "public",
	struct metadata   = {},
	boolean overwrite = true,
	string mode
);
```

### upload

Uploads a file directly in to disk storage

```javascript
/**
 * Uploads a file in to the disk
 *
 * @fieldName The file field name
 * @directory the directory on disk to upload to
 * @fileName  optional file name on the disk
 * @overwrite whether to overwrite ( defaults to false )
 */
function upload(
	required fieldName,
	required directory,
	string fileName,
	string overwrite = false
);
```

### delete

Delete a file or an array of file paths. If a file does not exist, `false` will be returned.

```javascript
/**
 * @path           A single file path or an array of file paths
 * @throwOnMissing Boolean to throw an exception if the file is missing.
 *
 * @return boolean or struct report of deletion
 *
 * @throws cbfs.FileNotFoundException
 */
boolean function delete( required any path, boolean throwOnMissing = false );
```

### exists

Validate if a file exists.

```javascript
/**
 * @path The file path to verify
 */
boolean function fileExists( required string path );
```

### missing

Validate if a file doesn't exist.

```javascript
/**
 * @path The file path to verify
 */
boolean function fileMissing( required string path );
```

### get

Get the contents of a file.

```javascript
/**
 * @path The file path to retrieve
 *
 * @return The contents of the file
 *
 * @throws cbfs.FileNotFoundException
 */
any function get( required path );
```

### getAsBinary

Get the contents of a file as binary, such as an executable or image.

```javascript
/**
 * @path The file path to retrieve
 *
 * @return A binary representation of the file
 *
 * @throws cbfs.FileNotFoundException
 */
any function getAsBinary( required path );
```

### move

Move a file from one destination to another.

```javascript
/**
 * @source      The source file path
 * @destination The end destination path
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.FileNotFoundException - When the source doesn't exist
 * @throws cbfs.FileOverrideException - When the destination exists and no override has been provided
 */
function move(
	required source,
	required destination,
	boolean overwrite = true
);
```

### prepend

Prepend contents to the beginning of a file. This method can be a costly operation for local disk storage.

```javascript
/**
 * @path           The file path to use for storage
 * @contents       The contents of the file to prepend
 * @metadata       Struct of metadata to store with the file
 * @throwOnMissing Boolean flag to throw if the file is missing. Otherwise it will be created if missing.
 *
 * @return LocalProvider
 *
 * @throws cbfs.FileNotFoundException
 */
function prepend(
	required string path,
	required contents,
	struct metadata        = {},
	boolean throwOnMissing = false
);
```

### touch

Create a new empty file if it does not exist.

```javascript
/**
 * @path       The file path
 * @createPath if set to false, expects all parent directories to exist, true will generate necessary directories. Defaults to true.
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.PathNotFoundException
 */
function touch( required path, boolean createPath = true );
```
