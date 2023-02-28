---
description: The local provider leverages the Java Non Block io package.
---

# Local Provider

Use the local provider to store files in a local filesystem where your application is running.  Behind the scenes it leverages the Java `nio` package to provide concurrency, atomicity, and non-blocking operations.

## Configuration

### Example

<pre class="language-json" data-title="config/ColdBox.cfc"><code class="lang-json">moduleSettings = {
<strong>  "cbfs": {
</strong>	// The default disk with a reserved name of 'default'
	"defaultDisk" : "myStorage",
	// Register the disks on the system
	"disks"       : {
	  // Your default application storage
	  "myStorage" : {
		"provider"   : "Local",
		"properties" : { 
			"path" : "#controller.getAppRootPath()#.myStorage",
			"diskUrl" : function(){
				return variables.controller
					.getRequestService()
					.getContext()
					.getHtmlBaseUrl()
					&#x26; "storage/.mystorage/";
			}
		}
	  }
	}
  }
};
</code></pre>

### Properties

When configuring your local disks, the following properties are available:

| Property           | Type      | Default  | Description                                                                                                                                   |
| ------------------ | --------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `autoExpand`       | `Boolean` | false    | If **true**, it will use an `expandPath()` on the path property. Else it leaves it as is.                                                     |
| `diskUrl`          | `http(s)` | `null`   | The public disk Url.  This is used to create file URLs and temporary URLs. This should point to the root path but in a web-accessible format. |
| `path`             | `string`  | --       | The relative or absolute path of where to store the file system.                                                                              |
| `uploadMimeAccept` | `string`  | \*       | The mime types which are accepted via the upload method. Defaults to all.                                                                     |
| `visibility`       | `string`  | `public` | The default visibility when creating files.  Available options are `public, private, readonly`                                                |
