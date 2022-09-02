# Utility Methods

### checksum

Generates a checksum for a file in different hashing algorithms.

```javascript
/**
 * @path      The file path
 * @algorithm Default is MD5, but SHA-1, SHA-256, and SHA-512 can also be used.
 *
 * @throws cbfs.FileNotFoundException
 */
string function checksum( required path, algorithm = "MD5" );

// Example
disk.checksum( expandPath( "myFile.txt" ), "SHA-256" );
```

### chmod

Sets the access attributes of the file on Unix-based disks.

```javascript
/**
 * @path The file path
 * @mode Access mode, the same attributes you use for the Linux command `chmod`
 *
 * @return cbfs.models.IDisk
 */
function chmod( required string path, required string mode );

// Example
disk.chmod( expandPath( "myFile.txt" ), "600" );
```

### createSymbolicLink

```
/**
	 * Create a symbolic link in the system if it supports it.
	 *
	 * The target parameter is the target of the link. It may be an absolute or relative path and may not exist. When the target is a relative path then file system operations on the resulting link are relative to the path of the link.
	 *
	 * @link   The path of the symbolic link to create
	 * @target The target of the symbolic link
	 *
	 * @return cbfs.models.IDisk
	 *
	 * @throws cbfs.FileNotFoundException    - if the target does not exist
	 * @throws UnsupportedOperationException - if the implementation does not support symbolic links
	 */
	function createSymbolicLink( required link, required target ){
		variables.files[ arguments.link ] = ensureRecordExists( arguments.target )
			.duplicate()
			.append( { symbolicLink : true } );
		return this;
	}
```

### extension

```
	/**
	 * Extract the extension from the file path
	 *
	 * @path The file path
	 */
	string function extension( required path ){
		return listLast( this.name( arguments.path ), "." );
	}
```

### info

```
/**
	 * Return information about the file.  Will contain keys such as lastModified, size, path, name, type, canWrite, canRead, isHidden and more
	 * depending on the provider used
	 *
	 * @path The file path
	 *
	 * @return A struct of file metadata according to provider
	 *
	 * @throws cbfs.FileNotFoundException
	 */
	struct function info( required path ){
		return ensureRecordExists( arguments.path );
	}
```

### lastModified

```
/**
	 * Retrieve the file's last modified timestamp
	 *
	 * @path The file path location
	 *
	 * @throws cbfs.FileNotFoundException
	 */
	function lastModified( required path ){
		return ensureRecordExists( arguments.path ).lastModified;
	}
```

### mimeType

```
/**
	 * Retrieve the file's mimetype
	 *
	 * @path The file path location
	 *
	 * @throws cbfs.FileNotFoundException
	 */
	function mimeType( required path ){
		return getMimeType( ensureRecordExists( arguments.path ).path );
	}
```

### size

```
/**
 * Retrieve the size of the file in bytes
 *
 * @path The file path location
 *
 * @throws cbfs.FileNotFoundException
 */
numeric function size( required path ){
	return len( get( arguments.path ) );
}
```

### temporaryURI

```
/**
 * Get a temporary uri for the given file
 *
 * @path       The file path to build the uri for
 * @expiration The number of minutes this uri should be valid for.
 *
 * @throws cbfs.FileNotFoundException
 */
string function temporaryUri( required path, numeric expiration ){
	return this.uri( arguments.path ) & "?expiration=#arguments.expiration#";
}
```

### uri

```
	/**
	 * Get the uri for the given file
	 *
	 * @path The file path to build the uri for
	 *
	 * @throws cbfs.FileNotFoundException
	 */
	string function uri( required string path ){
		return ensureRecordExists( arguments.path ).path;
	}
```
