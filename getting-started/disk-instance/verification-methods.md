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



### isWritable

Returns true if the file is writable.

```javascript
if ( disk.isWritable( path="myFile.txt" ) ) {
    // write to the fileava
}
```

