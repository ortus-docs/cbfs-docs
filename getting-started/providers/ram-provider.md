---
description: The RAM provider leverages memory allocation for its file-system
---

# RAM Provider

Use the RAM provider to store files within available RAM.

{% hint style="warning" %}
The trade-off with the RAM provider is that IO operations will be performed incredibly fast, but you are limited to the available RAM that's been allocated to run your CFML application.&#x20;
{% endhint %}

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
				"provider"   : "RAM",
				"properties" : {}
			}
		}
	},
};
```
{% endcode %}

### Properties

When configuring your RAM disks, the following properties are available:

| Property           | Type     | Default | Description                                                               |
| ------------------ | -------- | ------- | ------------------------------------------------------------------------- |
| `uploadMimeAccept` | `string` | \*      | The mime types which are accepted via the upload method. Defaults to all. |
