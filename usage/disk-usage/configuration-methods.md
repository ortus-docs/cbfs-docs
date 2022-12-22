# Configuration Methods

{% hint style="info" %}
The configuration methods are most commonly used by cbfs internally to startup and shutdown disks. You should only have to call these methods directly for advanced use cases.
{% endhint %}

## hasStarted

Returns true if the disk has been started up, false if not.

```javascript
if ( !disk.hasStarted() ) {
    // Email Luis
}
```

## getIdentifier

Returns the unique UUID identifier for this disk.

```javascript
var identifier = disk.getIdentifier(); // returns GUID
```

## getName

Returns the name of the disk.

```javascript
var name = disk.getName(); // returns name defined in ColdBox.cfc
```

## getProperties

Returns the settings for the disk.

```javascript
var properties = disk.getProperties(); // returns struct

var isCDrive = properties.path == "C:\" ? true : false;
```

## shutdown

cbfs invokes this method before the cbfs module is unloaded or during application reinit. You can implement this method as you see fit to shut down connections, sockets, etc.

```javascript
if ( disk.hasStarted() ) {
    disk.shutdown(); // No disk for you.
}
```

## startup

Start up a disk provider with the instance data it needs to start up. It must ensure that it sets the "started" variable to true to operate.

```javascript
disk.startup( name="myDisk", properties={
    "path": "C:\somepath"
} );
```

