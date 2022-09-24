# Module Configuration

If you are creating your own ColdBox modules, you can create disks from those modules in the configure() lifecycle method in ModuleConfig.cfc.

```javascript

component {
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
