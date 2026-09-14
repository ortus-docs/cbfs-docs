# Configuration

CBFS reads configuration from `moduleSettings.cbfs`.

```javascript
moduleSettings = {
    cbfs : {
        defaultDisk : "default",
        disks : {
            default : {
                provider : "Local",
                properties : {
                    path : "#controller.getAppRootPath()#.storage"
                }
            }
        }
    }
};
```

| Setting | Default | Description |
| --- | --- | --- |
| `defaultDisk` | `default` | Disk returned by `defaultDisk()`. |
| `disks` | `default`, `public`, and `temp` Local disks | Application disk blueprints. |

Each disk has a `provider` and provider-specific `properties`. `provider` can be `Local`, `Ram`, `S3`, a WireBox id, or a provider class path.

## Environment variables

The built-in Local disks use these system settings when present: `CBFS_DEFAULT_DISK_PATH`, `CBFS_PUBLIC_DISK_PATH`, and `CBFS_TEMP_DISK_PATH`.

## Provider properties

Common Local properties include `path` and `diskUrl`; S3 properties include `accessKey`, `secretKey`, `awsDomain`, `awsRegion`, `defaultBucketName`, `cacheLookups`, `defaultACL`, and `defaultStorageClass`. See the provider pages for the complete list.

A module can contribute disks under `cbfs.disks`, or use `cbfs.globalDisks` for a disk registered without a module namespace. Keep credentials in environment variables or a secrets manager.
