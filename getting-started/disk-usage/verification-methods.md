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
if ( disk.isExecutable( "myFile.txt" ) ) {
    // Execute the file
}
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
if ( disk.isFile( "myFile.txt" ) ) {
    // Read the file
}
```

### isHidden

Returns true if the file is hidden.

```javascript
/**
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 */
boolean function isHidden( required path );

// Example
if ( !disk.isHidden( "myFile.txt" ) ) {
    // Read the file
}
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
if ( disk.isReadable( "myFile.txt" ) ) {
    // Read the file
}
```

### isSymbolicLink

Returns true if the file is a symbolic link.

```javascript
/**
 * Is the file is a symbolic link
 *
 * @path The file path
 *
 * @throws cbfs.FileNotFoundException - If the filepath is missing
 */
boolean function isSymbolicLink( required path );

// Example
if ( !disk.isSymbolicLink( "myFile.txt" ) ) {
    // Read the file
}
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
    // Write to the file
}
```

