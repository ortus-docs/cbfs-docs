# Disk Instance

### append( path, contents, metadata, throwOnMissing )

Append contents to the end of a file.

### copy( source, destination )

Copy a file from one destination to another.

### create( path, contents, visibility, metadata, overwrite, mode )

Create a file on the disk.

### delete( path, throwOnMissing )

Delete a file or an array of file paths. If a file does not exist a `false` will be shown for it's return.

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

### setVisibility( path, visibility )

Set the storage visibility of a file. The available visibility options are `public, private, readonly` or a custom data type the implemented driver can interpret.

### touch( path, createPath )

Create a new empty file if it does not exist.

### visibility( path )

Returns the storage visibility of a file.&#x20;

The return format can be a string of `public, private, readonly` or a custom data type the implemented driver can interpret.











