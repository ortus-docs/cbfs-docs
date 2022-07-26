# Verification Methods

### isFile

Verifies if the passed path is an existent file.

```javascript
/**
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException
 */
boolean function isFile( required path );

// Example
if ( disk.isFile( path="myFile.txt" ) ) {}
```

### isReadable

Returns true if the file is readable.

```javascript
/**
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 */
boolean function isReadable( required path );

// Example
var isReadable = disk.isReadable( "myFile.txt" );va
```

### isWritable

Returns true if the file is writable.

```javascript
/**
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 */
boolean function isReadable( required path );

// Example
if ( disk.isWritable( path="myFile.txt" ) ) {
    // write to the file
}
```

