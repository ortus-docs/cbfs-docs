# Disk Service

cbfs includes a Disk Service object you can use to register and interact with your disks.

The full API for the Disk Service can be found in the [API Docs](https://apidocs.ortussolutions.com/#/coldbox-modules/cbfs/).

## Injection DSL

The cbfs module registers a WireBox injection DSL that you can use to inject objects from the module.

```javascript
// Injects the DiskService
diskService = getInstance( "cbfs" );
property name="diskService" inject="cbfs";

diskService = getInstance( "DiskService@cbfs" );
property name="diskService" inject="DiskService@cbfs";

// Injects the entire disks record structure
disks = getInstance( "cbfs:disks" );
property name="disks" inject="cbfs:disks";

// Injects a specific disk by name
tempDisk = getInstance( "cbfs:disks:{name}" );
tempDisk = getInstance( "cbfs:disks:temp" );
property name="tempDisk" inject="cbfs:disks:temp";
```

## Helper Method

The cbfs module registers a helper method called `cbfs( diskName )` that you can use in your handlers, layouts, and views.

```javascript
// SomeHandler.cfc
component {
    function index( event, rc, prc ) {
        var storage = cbfs( "RamDisk" );
        var files = storage.allFiles();
    }
}
```

## Core Methods

### count()

Returns the count of registered disks.

### defaultDisk()

Return an instance of the default disk defined in your [configuration](configuration.md).

### get( name )

Returns requested disk instance. Throws 'InvalidDiskException' if the disk is not registered.

### getDiskRecord( name )

Returns struct of details for a disk.

### has( name )

Returns true if the disk has been registered with the provided name.

### names()

Returns an array of registered disk names.

### register( name, provider, properties, override )

Registers a new disk. If a disk has already been configured with the same name, then it will not be updated unless you specify `override=true`.

### shutdown()

Unregisters and shuts down all disks managed by the DiskService.

### tempDisk()

Returns the temporary disk.

### unregister( name )

Unregisters a disk. Throws 'InvalidDiskException' if the disk is not registered.
