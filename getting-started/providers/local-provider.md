# Local Provider

Use the local provider to store files in a local filesystem where your application is running.

## Configuration

### Example

{% code title="config/ColdBox.cfc" %}
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
{% endcode %}

### Properties

When configuring your local disks, the following properties are available:

| Property         | Type    | Default | Description                                                                         |
| ---------------- | ------- | ------- | ----------------------------------------------------------------------------------- |
| path             | string  | --      | The relative or absolute path of where to store the file system.                    |
| autoExpand       | Boolean | false   | If true, it will use an expandPath() on the path property. Else it leaves it as is. |
| uploadMimeAccept | string  | \*      | The mime types which are accepted via the upload method. Defaults to all.           |
