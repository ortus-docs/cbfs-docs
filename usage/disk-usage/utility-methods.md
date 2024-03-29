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

Creates a symbolic link in the system if it supports it. The target parameter is the target of the link. It may be an absolute or relative path and may not exist. When the target is a relative path, then file system operations on the resulting link are relative to the path of the link.

```javascript
/**
 * @link   The path of the symbolic link to create
 * @target The target of the symbolic link
 *
 * @return cbfs.models.IDisk
 *
 * @throws cbfs.FileNotFoundException    - if the target does not exist
 * @throws UnsupportedOperationException - if the implementation does not support symbolic links
 */
function createSymbolicLink( required link, required target );

// Example
disk.createSymbolicLink( expandPath( "/symbolicPath" ), expandPath( "/myfolder" ) );
```

### extension

Extract the extension from the file path

```javascript
/**
 * @path The file path
 */
string function extension( required path );

// Example
disk.extension( someImagePath ); // returns '.jpg';

```

### info

Returns information about the file. Will contain keys such as lastModified, size, path, name, type, canWrite, canRead, isHidden, and more depending on the provider used.

```javascript
/**
 * @path The file path
 *
 * @return A struct of file metadata according to provider
 *
 * @throws cbfs.FileNotFoundException
 */
struct function info( required path );

// Example
disk.info( expandPath( "myFile.txt" ) );
```

### lastModified

Retrieves the file's last modified timestamp.

```javascript
/**
 * @path The file path location
 *
 * @throws cbfs.FileNotFoundException
 */
function lastModified( required path );

// Example
disk.lastModified( expandPath( "myFile.txt" ) );
```

### mimeType

Retrieves the file's mimetype.

```javascript
/**
 * @path The file path location
 *
 * @throws cbfs.FileNotFoundException
 */
function mimeType( required path );

// Example
disk.mimeType( expandPath( "myFile.jpg" ) ); // returns 'image/jpeg'
```

### size

Retrieves the size of the file in bytes.

```javascript
/**
 * @path The file path location
 *
 * @throws cbfs.FileNotFoundException
 */
numeric function size( required path );

// Example
disk.size( expandPath( "myFile.txt" ) ); // returns 2097152
```

### temporaryUrl

Gets a temporary URI for the given file.

```javascript
/**
 * @path       The file path to build the url for
 * @expiration The number of minutes this url should be valid for.
 * @responseHeaders A struct of headers to be forced for the HTTP response of GET requests.  Valid options are content-type, content-language, cache-control, content-disposition, content-encoding
 *
 * @throws cbfs.FileNotFoundException
 */
string function temporaryUrl( required path, numeric expiration, struct responseHeaders );

// Example
disk.temporaryUrl( expandPath( "myFile.txt", 60 ) );

```

With the S3 provider, you can specify a struct of response headers to control the URL constructed. For example, to generate a URL that ensures a file is returned with the MIME type 'text/plain', you could pass that into temporaryURL().

```javascript
disk.temporaryURL( path="somefile.txt", expiration=60, responseHeaders= {
    "content-type": "text/plain"
} );

# All arguments
disk.temporaryURL( path="somefile.txt", expiration=60, responseHeaders= {
    "content-type"        : "custom-type",
    "content-language"    : "custom-language",
    "cache-control"       : "custom-cache",
    "content-disposition" : "custom-disposition",
    "content-encoding"    : "custom-encoding"
} );
```

### url

Retrives the full url for a resource

```javascript
/**
 * Get the full url for the given file
 *
 * @path The file path to build the uri for
 *
 * @throws cbfs.FileNotFoundException
 */
string function url( required string path )
```

###
