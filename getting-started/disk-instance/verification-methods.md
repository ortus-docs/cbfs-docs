# Verification Methods

### isExecutable

Returns true if the file is executable.

```javascript
/**
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 */
boolean function isExecutable( required path );

// Example
if ( disk.isFile( "myFile.txt" ) ) {}
```

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
if ( disk.isFile( "myFile.txt" ) ) {}
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
var isReadable = disk.isReadable( "myFile.txt" );
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
if ( disk.isWritable( "myFile.txt" ) ) {
    // write to the file
}
```

