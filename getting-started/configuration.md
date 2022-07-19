# Configuration

In your config/ColdBox.cfc create a cbfs structure within the moduleSettings key. Here you will define your storage disks and global settings for the cbfs storage services.

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
