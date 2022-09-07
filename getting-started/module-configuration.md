# Module Configuration

Any ColdBox module can create disks in the configure() lifecycle method in ModuleConfig.cfc.

```javascript
component {

	/**
	 * Configure this module
	 */
	function configure(){
		settings = {
			// CBFS Module
			cbfs : {
				// Disks that will be namespaced with the module name @diskModule
				disks : {
					"temp" : { provider : "Ram" },
					"nasa" : { provider : "Ram" }
				},
				// No namespace in global spacing
				globalDisks : {
					// Should be ignored, you can't override if it exists
					"temp" : { provider : "Ram" },
					"nasa" : { provider : "Ram" }
				}
			}
		};
	}
	
}
```
