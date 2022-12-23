---
description: Get up and running with cbfs in no time!
---

# Installation

Use [CommandBox CLI](https://www.ortussolutions.com/products/commandbox) to install:

```bash
install cbfs
```

To install the bleeding-edge version:

```bash
install cbfs@be
```

### Configuration

You can configure the module by adding a `cbfs` structure to the `moduleSettings` in your `config/Coldbox.cfc` file or you can create your own `config/modules/cbfs.cfc` configuration file if you are using ColdBox 7.  Below you can see the default configuration for cbfs.

{% code title="config/modules/cbfs.cfc" %}
```json
function configure(){
    return {
    	// The default disk with a reserved name of 'default'
	"defaultDisk" : "default",
	// Register the disks on the system
	"disks"       : {
		// Your default application storage : non-web accessible
		"default" : {
			provider   : "Local",
			properties : {
				path : getSystemSetting( "CBFS_DEFAULT_DISK_PATH", "#controller.getAppRootPath()#.cbfs" )
			}
		},
		// A public web-accessible storage located at /includes/public
		"public" : {
			provider   : "Local",
			properties : {
				path : getSystemSetting(
					"CBFS_PUBLIC_DISK_PATH",
					"#controller.getAppRootPath()#includes/public"
				),
				diskUrl : function(){
					return variables.controller
						.getRequestService()
						.getContext()
						.getHtmlBaseUrl() & "includes/public"
				}
			}
		},
		// A disk that points to the CFML Engine's temp directory
		"temp" : {
			provider   : "Local",
			properties : { path : getSystemSetting( "CBFS_TEMP_DISK_PATH", getTempDirectory() ) }
		}
	}
   };
}
```
{% endcode %}

### Pre-Configured Disks

By default, cbfs, comes pre-configured with 3 disks:

| Disk Name | Provider | Location                | Description                                             |
| --------- | -------- | ----------------------- | ------------------------------------------------------- |
| `default` | `Local`  | `{app}/.cbfs`           | A private location for assets                           |
| `public`  | `Local`  | `{app}/includes/public` | A public accessible location inside of your application |
| `temp`    | `Local`  | `{CF internal}`         | The Java temp internal directory                        |

#### Environment Variables

Please note that you can change the location of these disks by adding the configuration or you can easily do so using the following environment variables:

* `CBFS_DEFAULT_DISK_PATH`
* `CBFS_PUBLIC_DISK_PATH`
* `CBFS_TEMP_DISK_PATH`

### Default Disk

You can use the `defaultDisk` key to specify which disk will be the `default` in your system.  By `default` it's the `default` one :joy: which is not web-accessible and stored as `.cbfs` in your root application.

### Registering Disks

The `disks` structure is used to register disks in your application.  The `key` is the name of the disk which is a structure that each disk needs in order to be configured:

* **provider** : The name of the provider (if core) or a full CFC path or WireBox ID
* **properties** : A structure of configuration properties the disk requires (if any)

{% hint style="info" %}
Please check out the [providers ](providers/)section in order to see the properties and requirements for each one of them.
{% endhint %}
