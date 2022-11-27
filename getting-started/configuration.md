# Configuration

In your `config/ColdBox.cfc` create a cbfs structure within the `moduleSettings` key. Here you will define your storage disks and global settings for the cbfs storage services.

{% hint style="info" %}
Each provider has its own configuration properties. Please review this book for additional information on each provider.
{% endhint %}

```javascript
moduleSettings = {
	cbfs: {
		// The default disk with a reserved name of 'default'
		"defaultDisk" : "myStorage",
		// Register the disks on the system
		"disks"       : {
			// Your default application storage
			"myStorage" : {
				provider   : "Local",
				properties : { path : "#controller.getAppRootPath()#.myStorage" }
			},
			// An S3 disk point use Digital Ocean Spaces
			"S3" : {
				"provider": "S3",
				"properties": {
					"visibility": "public", // can be 'public' or 'private'
					"path": "",
					"accessKey": "",
					"secretKey": "",
					"awsDomain": "digitaloceanspaces.com",
					"awsRegion": "sfo3",
					"defaultBucketName": "myDOSpace",
					"signatureType": "v4"
				}
			}
		}
	},
};
```

## Default Disk

You can use the `defaultDisk` setting to point it to a registered disk by name. Every time you use the default operations, it will be based upon this setting.

<pre class="language-javascript"><code class="lang-javascript"><strong>function configure() {
</strong><strong>	moduleSettings = {
</strong>		cbfs: {
			// Set disk named 'default' as the default disk.
			"defaultDisk" : "default",
			"disks"       : {
				"myStorage" : {
					provider   : "Local",
					properties : { path : "#controller.getAppRootPath()#.mystorage" }
				}
			}
		},
	};
}</code></pre>

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

### Ram

The `ram` provider has a shortcut of `Ram` or it can be fully referenced via its WireBox ID `RamProvider@cbfs`. It also does not have any configuration properties.

### S3

The `s3` disk provider has a shortcut of `S3` and can be used to create a storage disk with any AWS S3 compatible API.  This provider uses all of the available properties of the [S3SDK](https://github.com/coldbox-modules/s3sdk#coldbox-module) which pass through to the instance when the disk is created. Additional properties are:&#x20;

| Property       | Type   | Default  | Description                                                                                             |
| -------------- | ------ | -------- | ------------------------------------------------------------------------------------------------------- |
| `publicDomain` | string | ---      | Will be the public domain in URLs generated - for example, when using a CDN distribution via CloudFront |
| `visibility`   | string | `public` | Whether the contents of the disk are public (world read ) or private                                    |
| `bucketName`   | string | ---      | The bucket name, within which this disk operates.                                                       |
