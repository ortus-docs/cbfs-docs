# Disk Instance

## Core Methods

### getIdentifier()

Returns the unique UUID identifier for this disk.

### hasStarted()

Returns true if the disk has been started up, false if not.

### getName()

Returns the name of the disk.

### getProperties()

Returns the settings for the disk.

### startup( name, properties = {} )

Start up a disk provider with the instance data it needs to start up. It must ensure that it sets the "started" variable to true to operate.

### shutdown()

cbfs invokes this method before the cbfs module is unloaded or during application reinits. You can implement this method as you see fit to shut down connections, sockets, etc.

### create( path, contents, visibility, metadata, overwrite, mode )

Create a file on the disk.

### setVisibility( path, visibility )

Set the storage visibility of a file. The available visibility options are `public, private, readonly` or a custom data type the implemented driver can interpret.

### visibility( path )

Returns the storage visibility of a file.&#x20;

The return format can be a string of `public, private, readonly` or a custom data type the implemented driver can interpret.

### prepend( path, contents, metadata = {}, throwOnMissing = false )

Prepend contents to the beginning of a file. This method can be a costly operation for local disk storage.

### append( path, contents, metadata = {}, throwOnMissing = false )

Append contents to the end of a file.

### copy( source, destination )

Copy a file from one destination to another.

### move( source, destination )

Move a file from one destination to another.

### get( path )

Get the contents of a file.

### getAsBinary( path )

Get the contents of a file as binary, such as an executable or image.

### exists( path )

Validate if a file or directory exists.

### missing( path )

Validate if a file or directory doesn't exist.

### delete( path, throwOnMissing = false )

Delete a file or an array of file paths. If a file does not exist a `false` will be shown for it's return.

### touch( path, createPath = false )

Create a new empty file if it does not exist.











