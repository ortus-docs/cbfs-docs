# File Object

## create

Creates a file on the disk.

```javascript
/**
 * @contents   The contents of the file to store
 * @visibility The storage visibility of the file, available options are `public, private, readonly` or a custom data type the implemented driver can interpret
 * @metadata   Struct of metadata to store with the file
 * @overwrite  Flag to overwrite the file at the destination, if it exists. Defaults to true.
 * @mode       Applies to *nix systems. If passed, it overrides the visbility argument and uses these octal values instead
 *
 * @return File
 *
 * @throws cbfs.FileOverrideException - When a file exists and no override has been provided
 */
function create(
	required contents,
	string visibility,
	struct metadata   = {},
	boolean overwrite = true,
	string mode
);
```
