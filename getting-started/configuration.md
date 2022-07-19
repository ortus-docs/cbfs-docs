# Configuration

In your `config/ColdBox.cfc` create a cbfs structure within the `moduleSettings` key. Here you will define your storage disks and global settings for the cbfs storage services.

{% hint style="info" %}
Each provider has its own configuration properties. Please review this book for additional information on each provider.
{% endhint %}

```javascript
moduleSettings = {
	cbfs: {
		// The default disk with a reserved name of 'default'
		"defaultDisk" : "default",
		// Register the disks on the system
		"disks"       : {
			// Your default application storage
			"default" : {
				provider   : "Local",
				properties : { path : "#controller.getAppRootPath()#.cbfs" }
			},
			// A disk that points to the CFML Engine's temp directory
			"temp" : {
				provider   : "Local",
				properties : { path : getTempDirectory() }
			}
		}
	},
};
```

## Default Disk

You can use the `defaultDisk` setting to point it to a registered disk by name. Every time you use the default operations, it will be based upon this setting.

## Disks

You can register as many disks as you want in the parent application using this structure. The `key` will be the name of the disk, and the value is a struct of:

* `provider` : The provider's short name, a WireBox ID, or a full CFC path.
* `properties` : A struct of properties that configures each provider.

By default, we register two disks in your ColdBox application.

| Disk    | Provider | Description                                                                                                                    |
| ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| default | Local    | By convention, it creates a `.cbfs` folder in the root of your application where all files will be stored.                     |
| temp    | Local    | Access to the Java temporary folder structure you can use for any type of generation that is not web-accessible and temporary. |

## Providers

The available providers are listed below with their appropriate properties to configure them.

### Local

The `local` provider has a shortcut of `Local` or it can be fully referenced via its WireBox ID `LocalProvider@cbfs`. The available properties are:



| Property     | Type    | Default | Description                                                                             |
| ------------ | ------- | ------- | --------------------------------------------------------------------------------------- |
| `path`       | string  | ---     | The relative or absolute path of where to store the file system.                        |
| `autoExpand` | boolean | false   | If true, it will use an `expandPath()` on the `path` property. Else it leaves it as is. |
