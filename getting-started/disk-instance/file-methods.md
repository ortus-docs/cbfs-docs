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

### copy( source, destination )

Copy a file from one destination to another.

### create( path, contents, visibility, metadata, overwrite, mode )

Create a file on the disk.

### delete( path, throwOnMissing )

Delete a file or an array of file paths. If a file does not exist, `false` will be returned.

### exists( path )

Validate if a file or directory exists.

### get( path )

Get the contents of a file.

### getAsBinary( path )

Get the contents of a file as binary, such as an executable or image.

### missing( path )

Validate if a file or directory doesn't exist.

### move( source, destination )

Move a file from one destination to another.

### prepend( path, contents, metadata, throwOnMissing )

Prepend contents to the beginning of a file. This method can be a costly operation for local disk storage.

### touch( path, createPath )

Create a new empty file if it does not exist.
