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

## getName

Returns the name of the disk.

```javascript
var name = disk.getName(); // returns name like 'tempDisk'
```

## getProperties

Returns the settings for the disk.

### startup( name, properties = {} )

Start up a disk provider with the instance data it needs to start up. It must ensure that it sets the "started" variable to true to operate.

### shutdown()

cbfs invokes this method before the cbfs module is unloaded or during application reinit. You can implement this method as you see fit to shut down connections, sockets, etc.

