# File Object

The CBFS File object gives you simplied access to the disk API.

To create a new file object, you an use:

```javascript
var file = disk.file( "some/path/somefile.txt" );
```

Then you can access any of the api methods documented here. Enjoy!

```javascript
var file = disk.file( "somefile.txt" )
                .create( "some contents" )
                .append( "append contents" );
                
var mimeType = file.mimeType(); // returns 'text/plain'
```

## append

Append contents to the end of a file.

<pre class="language-javascript"><code class="lang-javascript"><strong>/**
</strong> * @contents       The contents of the file to append
 * @metadata       Struct of metadata to store with the file
 * @throwOnMissing Boolean flag to throw if the file is missing. Otherwise it will be created if missing.
 *
 * @return File
 *
 * @throws cbfs.FileNotFoundException
 */
function append(
	required contents,
	struct metadata        = {},
	boolean throwOnMissing = false
);
</code></pre>

## checksum

Generate checksum for a file in different hashing algorithms.

```javascript
/**
 * Generate checksum for a file in different hashing algorithms
 *
 * @algorithm Default is MD5, but SHA-1, SHA-256, and SHA-512 can also be used.
 *
 * @throws cbfs.FileNotFoundException
 */
string function checksum( algorithm = "MD5" );
```

## chmod

Sets the access attributes of the file on Unix based disks.

<pre class="language-javascript"><code class="lang-javascript"><strong>/**
</strong> * @mode Access mode, the same attributes you use for the Linux command `chmod`
 * @return File
 */
function chmod( required string mode );
</code></pre>

## copy

Copy a file from one destination to another.

```javascript
/**
* @destination The end destination path
* @overwrite   Flag to overwrite the file at the destination, if it exists. Defaults to true.
*
* @return File  - returns the copied file object
*
* @throws cbfs.FileNotFoundException - When the source doesn't exist
* @throws cbfs.FileOverrideException - When the destination exists and no override has been provided
*/
function copy(
   required destination,
   boolean overwrite = true
);
```

## create

Creates a file on the disk.

```javascript
/**
 * @contents   The contents of the file to store
 * @visibility The storage visibility of the file, available options are `public, private, readonly` or a custom data type the implemented driver can interpret
 * @metadata   Struct of metadata to store with the file
 * @overwrite  Flag to overwrite the file at the destination, if it exists. Defaults to true.
 * @mode       Applies to *nix systems. If passed, it overrides the visbility argument and uses these octal values instead
 *
 * @return File
 *
 * @throws cbfs.FileOverrideException - When a file exists and no override has been provided
 */
function create(
	required contents,
	string visibility,
	struct metadata   = {},
	boolean overwrite = true,
	string mode
);
```

## delete

Delete a file or an array of file paths. If a file does not exist a `false` will be shown for its return.

```javascript
/**
 * @throwOnMissing Boolean to throw an exception if the file is missing.
 *
 * @return boolean
 *
 * @throws cbfs.FileNotFoundException
 */
boolean function delete( boolean throwOnMissing = false );
```

## exists

Validate if a file exists.

```javascript
/**
* @path The file path to verify
*/
boolean function exists();
```

## extension

Extract the extension from the file path.

```javascript
string function extension();
```

## get

Get the contents of a file.

```javascript
/**
* @return The contents of the file
*
* @throws cbfs.FileNotFoundException
*/
any function get();
```

## info

Return information about the file. Will contain keys such as lastModified, size, path, name, type, canWrite, canRead, isHidden and more depending on the provider used.

```javascript
/**
* @return A struct of file metadata according to provider
*
* @throws cbfs.FileNotFoundException
*/
struct function info();
```

## isExecutable

Returns true if the file is executable.

```javascript
/**
* @throws cbfs.FileNotFoundException - If the filepath is missing
* 
* @return Boolean
*/
boolean function isExecutable();
```

## isHidden

Returns true if the file is hidden.

```javascript
/**
* @throws cbfs.FileNotFoundException - If the filepath is missing
* 
* @return Boolean
*/
boolean function isHidden();
```

## isReadable

Returns true if the file is readable.

```javascript
/**
* @return Boolean
*/
boolean function isReadable();
```

## isSymbolicLink

Returns true if the file is a symbolic link.&#x20;

```javascript
/**
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 * @return Boolean
 */
boolean function isSymbolicLink();
```

## isWritable

Returns true if the file is writable.

```javascript
/**
* @return Boolean
*/
boolean function isWritable();
```

## lastModified

Retrieve the file's last modified timestamp.

```javascript
/**
* @throws cbfs.FileNotFoundException
*/
function lastModified();
```

## mimeType

Retrieve the file's mime type.

```javascript
/**
 * Retrieve the file's mimetype
 * @return String
 * @throws cbfs.FileNotFoundException
 */
function mimeType();
```

## move

Move a file from one destination to another.

```javascript
/**
 * @destination The end destination path
 *
 * @return File - the moved file object
 *
 * @throws cbfs.FileNotFoundException - When the source doesn't exist
 * @throws cbfs.FileOverrideException - When the destination exists and no override has been provided
 */
function move(
	required destination,
	boolean overwrite = true
);
```

## prepend

Prepend contents to the beginning of a file. This is a very expensive operation for local disk storage.

```javascript
/**
* @contents       The contents of the file to prepend
* @metadata       Struct of metadata to store with the file
* @throwOnMissing Boolean flag to throw if the file is missing. Otherwise it will be created if missing.
*
* @return File
*
* @throws cbfs.FileNotFoundException
*/
function prepend(
   required contents,
   struct metadata        = {},
   boolean throwOnMissing = false
);
```

## setVisibility

Set the storage visibility of a file. Available options are `public`, `private`, `readonly` or a custom data type the implemented driver can interpret.

```javascript
/**
* @visibility The storage visibility of the file, available options are `public, private, readonly` or a custom data type the implemented driver can interpret
*
* @return File
*/
function setVisibility( required string visibility );
```

## size

Returns the size of a file (in bytes). The size may differ from the actual size on the file system due to compression, support for sparse files, or other reasons.

```javascript
/**
 * @throws cbfs.FileNotFoundException
 */
numeric function size();
```

## stream

Return a Java stream of the file using non-blocking IO classes. The stream will represent every line in the file so you can navigate through it. This method leverages the `cbstreams` library used accordingly by implementations (https://www.forgebox.io/view/cbstreams)

```javascript
/**
 * @return Stream object: See https://apidocs.ortussolutions.com/coldbox-modules/cbstreams/1.1.0/index.html
 */
function stream(){
        arguments.path = getPath();
        return getDisk().stream( argumentCollection=arguments );
};
```

## touch

Create a new empty file if it does not exist.

```javascript
/**
* @createPath if set to false, expects all parent directories to exist, true will generate necessary directories. Defaults to true.
*
* @return File
*
* @throws cbfs.PathNotFoundException
*/
function touch( boolean createPath = true );
```

## visibility

Get the storage visibility of a file. The return format can be a string of `public`, `private`, `readonly` or a custom data type the implemented driver can interpret.

```javascript
/**
* @return String
*/
string function visibility();
```
