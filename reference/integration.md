# Integration and Lifecycle

## Injection

| Injection | Value |
| --- | --- |
| `cbfs` | The Disk Service. |
| `cbfs:disks` | The registered disk record struct. |
| `cbfs:disks:{name}` | A named, lazily started disk. |

The service can also be injected as `DiskService@cbfs`.

## Helper

The `cbfs( diskName )` helper returns the Disk Service when no name is supplied, or a named disk when a name is supplied.

```javascript
storage = cbfs( "public" );
storage.file( "images/avatar.jpg" ).url();
```

## Module lifecycle

* On load, CBFS registers application disks.
* After aspects load, CBFS discovers disks contributed by other modules.
* On ColdBox shutdown, CBFS shuts down and unregisters all disks.
* Providers start lazily when first resolved by name.

## Interception points

CBFS exposes `cbfsOnDiskStart`, `cbfsOnDiskShutdown`, `cbfsOnFileCreate`, `cbfsOnFileMove`, `cbfsOnFileCopy`, `cbfsOnFileDelete`, `cbfsOnFileInfoRequest`, `cbfsOnDirectoryMove`, `cbfsOnDirectoryCreate`, `cbfsOnDirectoryCopy`, and `cbfsOnDirectoryDelete`.
