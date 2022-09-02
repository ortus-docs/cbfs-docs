# Stream Methods

### stream

Returns a Java stream of the file using non-blocking IO classes. The stream will represent every line in the file so you can navigate through it.

```javascript
/**
 * @path The path to read all the files with
 *
 * @return Stream object: See https://apidocs.ortussolutions.com/coldbox-modules/cbstreams/1.1.0/index.html
 */
function stream( required path );

// Example
disk.stream( expandPath( "datadump.txt" ) );
```
