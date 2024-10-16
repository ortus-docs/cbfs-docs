# Directory Methods

### allContents

Get an array listing of all files and directories in a directory using recursion.

```javascript
/**
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
);
```

### allContentsMap

Get an array of content from all the files from a specific directory with recursion.

```javascript
/**
 * @directory The directory
 * @filter    A string wildcard or a lambda/closure that receives the file path and should return true to include it in the returned array or not.
 * @sort      Columns by which to sort. e.g. Directory, Size DESC, DateLastModified.
 *
 * @throws cbfs.DirectoryNotFoundException
 */
array function allContentsMap( required directory, any filter, sort );
```

### allDirectories

Get an array of all directories in a directory using recursion.

```javascript
/**
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
);
```

### allFiles

Get an array of all files in a directory using recursion. This is a shortcut to files() with a recursion argument.

```javascript
/**
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
);
```

### allFilesMap

Get an array of structs of all recursive files in a directory and their appropriate information map: attributes, dateLastModified, directory, link, name, size, etc.

<pre class="language-javascript"><code class="lang-javascript">/**
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
<strong>);
</strong></code></pre>

### buildDiskPath

Builds the path on the provided disk from its root + incoming path with normalization, cleanup, and canonicalization.

```javascript
/**
 * @path The path on the disk to build
 *
 * @return The canonical path on the disk
 */
function buildDiskPath( required string path );
```

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

### contents

Get an array listing of all files and directories in a directory.

```javascript
/**
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
);
```

### contentsMap

Get an array of content from all the files from a specific directory.

```javascript
/**
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
);

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

### directories

Get an array of all directories in a directory.

```javascript
/**
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
);
```

### directoryExists

Validates that a directory does exists.

```javascript
/**
 * Validate if a directory exists
 *
 * @path The directory to verify
 */
boolean function directoryExists( required string path )
```

### directoryMissing

Validates that a directory does not exists.

```javascript
/**
 * Validate if a directory exists
 *
 * @path The directory to verify
 */
boolean function directoryExists( required string path )
```

### files

Get an array of all files in a directory.

```javascript
/**
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
);
```

### filesMap

Get an array of structs of all files in a directory and their appropriate information map: attributes, dateLastModified, directory, link, name, size, etc.\


```javascript
/**
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
);
```

### isDirectory

Returns a boolean determining if a path is a directory or not.

```javascript
/**
 * @path The directory path
 *
 * @return true if the file is a directory; false if the file does not exist, is not a directory, or it cannot be determined if the file is a directory or not.
 */
boolean function isDirectory( required path );
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

