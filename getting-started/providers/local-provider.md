# Local Provider

Use the local provider to store files in a local filesystem where your application is running.

## Configuration

```json
moduleSettings = {
	"cbfs": {
		// The default disk with a reserved name of 'default'
		"defaultDisk" : "myStorage",
		// Register the disks on the system
		"disks"       : {
			// Your default application storage
			"myStorage" : {
				"provider"   : "Local",
				"properties" : { "path" : "#controller.getAppRootPath()#.myStorage" }
			}
		}
	},
};
```
