# Disk Service

cbfs includes a Disk Service object you can use to register and interact with your disks.

The full API for the Disk Service can be found in the [API Docs](https://apidocs.ortussolutions.com/#/coldbox-modules/cbfs/).

## Injection DSL

```javascript
// Injects the DiskService
diskService = getInstance( "cbfs" );
property name="diskService" inject="cbfs";

// Injects the entire disks record structure
disks = getInstance( "cbfs:disks" );
property name="disks" inject="cbfs:disks";

// Injects a specific disk by name
tempDisk = getInstance( "cbfs:disks:{name}" );
tempDisk = getInstance( "cbfs:disks:temp" );
property name="tempDisk" inject="cbfs:disks:temp";
```

The `cbfs` module also registers a WireBox injection DSL that you can use to inject objects from the module:

## Core Methods

### get( name )

Returns requested disk instance. Throws 'InvalidDiskException' if the disk is not registered.

### has( name )

Returns true if the disk has been registered with the provided name.

### register( name, provider, properties, override )

Registers a new disk. If a disk has already been configured with the same name, then it will not be updated unless you specify `override=true`.

### unregister( name )

Unregisters a disk. Throws 'InvalidDiskException' if the disk is not registered.

### shutdown()

Unregisters and shuts down all disks managed by the DiskService.

### getDiskRecord( name )

Returns struct of details for a disk.

### names()

Returns an array of registered disk names.

### count()

Returns the count of registered disks.

### defaultDisk()

Return an instance of the default disk defined in your [configuration](configuration.md).

### tempDisk()

Returns the temporary disk.
