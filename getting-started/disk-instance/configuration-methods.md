# Configuration Methods

## getIdentifier

Returns the unique UUID identifier for this disk.

```javascript
var identifier = disk.getIdentifier(); // returns GUID
```

## hasStarted

Returns true if the disk has been started up, false if not.

```javascript
if ( !disk.hasStarted() ) {
    // Email Luis
}
```
