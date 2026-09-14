# Disk Service

The Disk Service is the registry and factory for configured disks. Inject it with `cbfs` or `DiskService@cbfs`, or use the `cbfs()` helper.

## Methods

| Method | Returns | Description |
| --- | --- | --- |
| `get(name)` | `IDisk` | Lazily creates and starts a registered disk. Throws `InvalidDiskException` for an unknown name. |
| `getDiskRecord(name)` | `struct` | Returns the registration blueprint, including provider, properties, and lifecycle timestamps. |
| `register(name, provider, properties={}, override=false)` | `DiskService` | Registers a disk blueprint. Existing registrations are preserved unless `override=true`. |
| `unregister(name)` | `DiskService` | Shuts down a created disk and removes its registration. |
| `has(name)` / `missing(name)` | `boolean` | Tests whether a disk name is registered. |
| `names()` | `array` | Returns registered names sorted case-insensitively. |
| `count()` | `numeric` | Returns the number of registered disks. |
| `defaultDisk()` | `IDisk` | Resolves the disk named by `moduleSettings.defaultDisk`. |
| `tempDisk()` | `IDisk` | Resolves the reserved `temp` disk. |
| `registerAppDisks()` | `DiskService` | Registers disks from application settings. |
| `registerModuleDisks()` | `DiskService` | Registers disks contributed by loaded modules. |
| `shutdown()` | `DiskService` | Unregisters and shuts down every registered disk. |

## Lazy startup

`register()` stores configuration only. A provider is instantiated and started on the first `get()` call, so registration does not open provider connections immediately.

```javascript
diskService.register(
    name       = "archive",
    provider   = "S3",
    properties = { defaultBucketName : "my-archive" }
);

archive = diskService.get( "archive" );
```
