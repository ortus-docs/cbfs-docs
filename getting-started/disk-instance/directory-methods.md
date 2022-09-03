# Directory Methods

### cleanDirectory

Empty the specified directory of all files and folders.

```javascript
/**
 * @directory      The directory
 * @throwOnMissing Throws an exception if the directory does not exist, defaults to false
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.DirectoryNotFoundException
 */
function cleanDirectory( required directory, boolean throwOnMissing = false );
```

### copyDirectory

Copies a directory to a destination. The 'filter' argument can be a closure and lambda with the format function(path ).

```javascript
/**
 * @source      The source directory
 * @destination The destination directory
 * @recurse     If true, copies all subdirectories, otherwise only files in the source directory. Default is false.
 * @filter      A string file extension filter to apply like *.jpg or server-*.json or a lambda/closure that receives the file path and should return true to copy it.
 * @createPath  If false, expects all parent directories to exist, true will generate all necessary directories. Default is true.
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.DirectoryNotFoundException - When the source directory does not exist
 */
function copyDirectory(
	required source,
	required destination,
	boolean recurse = false,
	any filter,
	boolean createPath = true
);
```

### createDirectory

Create a new directory.

```javascript
/**
 * @directory    The directory path to be created
 * @createPath   Create parent directory paths when they do not exist. The default is true
 * @ignoreExists If false, it will throw an error if the directory already exists, else it ignores it if it exists. This should default to true.
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.DirectoryExistsException - If the directory you are trying to create already exists and <code>ignoreExists</code> is false
 */
function createDirectory(
	required directory,
	boolean createPath   = true,
	boolean ignoreExists = true
);
```

### deleteDirectory

Delete one or more directory locations.

```javascript
/**
 * @directory      The directory or an array of directories
 * @recurse        Recurse the deletion or not, defaults to true
 * @throwOnMissing Throws an exception if the directory does not exist, defaults to false
 *
 * @return A boolean value or a struct of booleans determining if the directory paths got deleted or not.
 *
 * @throws cbfs.DirectoryNotFoundException
 */
boolean function deleteDirectory(
	required string directory,
	boolean recurse        = true,
	boolean throwOnMissing = false
);

```

### isDirectory

Returns boolean determining if a path is a directory or not.

```javascript
/**
 * @path The directory path
 *
 * @return true if the file is a directory; false if the file does not exist, is not a directory, or it cannot be determined if the file is a directory or not.
 */
boolean function isDirectory( required path ){
	return variables.jFiles.isDirectory( buildJavaDiskPath( arguments.path ), [] );
};
```

### moveDirectory

Move or rename a directory.

```javascript
/**
 * @source      The source directory
 * @destination The destination directory
 * @createPath  If false, expects all parent directories to exist, true will generate all necessary directories. Default is true.
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.DirectoryNotFoundException          - When the source does not exist
 */
function moveDirectory(
	required source,
	required destination,
	boolean createPath = true
);
```

```javascript

/**
 * Get an array listing of all files and directories in a directory.
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @recurse   Recurse into subdirectories, default is false
 * @type      Filter the result to only include files, directories, or both. ('file|files', 'dir|directory', 'all'). Default is 'all'
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function contents(
	required directory,
	any filter,
	sort,
	boolean recurse  = false,
	type             = "all",
	boolean absolute = false
){
	// If missing throw or ignore
	if ( missing( arguments.directory ) ) {
		throw(
			type    = "cbfs.DirectoryNotFoundException",
			message = "Directory [#arguments.directory#] not found."
		);
	}

	// Move to nio later
	return directoryList(
		buildDiskPath( arguments.directory ), // path
		arguments.recurse, // recurse
		"path", // listinfo
		isNull( arguments.filter ) ? "" : arguments.filter, // filter
		isNull( arguments.sort ) ? "" : arguments.sort, // sort
		arguments.type // type
	).map( function( item ){
		return absolute ? arguments.item : arguments.item.replace( variables.properties.path, "" );
	} );
}

/**
 * Get an array listing of all files and directories in a directory using recursion
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @type      Filter the result to only include files, directories, or both. ('file|files', 'dir|directory', 'all'). Default is 'all'
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allContents(
	required directory,
	any filter,
	sort,
	type             = "all",
	boolean absolute = false
){
	arguments.recurse = true;
	return contents( argumentCollection = arguments );
}

/**
 * Get an array of all files in a directory.
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @recurse   Recurse into subdirectories, default is false
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function files(
	required directory,
	any filter,
	sort,
	boolean recurse  = false,
	boolean absolute = false
){
	arguments.type = "file";
	return contents( argumentCollection = arguments );
};

/**
 * Get an array of all directories in a directory.
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @recurse   Recurse into subdirectories, default is false
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function directories(
	required directory,
	any filter,
	sort,
	boolean recurse  = false,
	boolean absolute = false
){
	arguments.type = "Dir";
	return contents( argumentCollection = arguments );
};

/**
 * Get an array of all files in a directory using recursion, this is a shortcut to the `files()` with recursion
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allFiles(
	required directory,
	any filter,
	sort,
	boolean absolute = false
){
	arguments.type    = "File";
	arguments.recurse = true;
	return contents( argumentCollection = arguments );
};

/**
 * Get an array of all directories in a directory using recursion
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @absolute  Local provider only: We return relative disk paths by default. If true, we return absolute paths
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allDirectories(
	required directory,
	any filter,
	sort,
	boolean absolute = false
){
	arguments.type    = "Dir";
	arguments.recurse = true;
	return contents( argumentCollection = arguments );
}

/**
 * Get an array of structs of all files in a directory and their appropriate information map:
 * - Attributes
 * - DateLastModified
 * - Directory
 * - Link
 * - Name
 * - Size
 * - etc
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @recurse   Recurse into subdirectories, default is false
 * @extended  Default of false produces basic file info, true, produces posix extended info.
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function filesMap(
	required directory,
	any filter,
	sort,
	boolean recurse  = false,
	boolean extended = false
){
	return files( argumentCollection = arguments ).map( function( item ){
		return extended ? extendedInfo( arguments.item ) : info( arguments.item );
	} );
};

/**
 * Get an array of structs of all recursive files in a directory and their appropriate information map:
 * - Attributes
 * - DateLastModified
 * - Directory
 * - Link
 * - Name
 * - Size
 * - etc
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @extended  Default of false produces basic file info, true, produces posix extended info.
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allFilesMap(
	required directory,
	any filter,
	sort,
	boolean extended = false
){
	arguments.recurse = true;
	return filesMap( argumentCollection = arguments );
};

/**
 * Get an array of content from all the files from a specific directory
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 * @recurse   Recurse into subdirectories, default is false
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function contentsMap(
	required directory,
	any filter,
	sort,
	boolean recurse = false
){
	return files( argumentCollection = arguments ).map( function( item ){
		return {
			"path"     : arguments.item,
			"contents" : get( arguments.item ),
			"size"     : size( arguments.item )
		};
	} );
};

/**
 * Get an array of content from all the files from a specific directory with recursion
 *
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allContentsMap( required directory, any filter, sort ){
	arguments.recurse = true;
	return contentsMap( argumentCollection = arguments );
};

/**
 * This function builds the path on the provided disk from it's root + incoming path
 * with normalization, cleanup and canonicalization.
 *
 * @path The path on the disk to build
 *
 * @return The canonical path on the disk
 */
function buildDiskPath( required string path ){
	var pathTarget = normalizePath( arguments.path );
	return pathTarget.startsWith( variables.properties.path ) ? pathTarget : getCanonicalPath(
		variables.properties.path & "/#pathTarget#"
	).reReplace( "\/$", "" );
}
```
