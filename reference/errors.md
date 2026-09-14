# Errors

| Exception | When it is raised |
| --- | --- |
| `cbfs.InvalidDiskException` | A disk name is requested before it is registered. |
| `cbfs.IncorrectDslException` | A WireBox DSL definition is not supported. |
| `cbfs.FileNotFoundException` | A required file is missing. |
| `cbfs.DirectoryNotFoundException` | A required directory is missing. |
| `cbfs.DirectoryExistsException` | A directory exists and `ignoreExists=false`. |
| `cbfs.FileOverrideException` | An operation would replace a file while overwrite is disabled. |
| `cbfs.PathNotFoundException` | A required parent path is missing. |
| `UnsupportedOperationException` | A provider cannot implement an operation such as symbolic links. |

Most mutating methods are tolerant where practical. `delete()` can return a false result for a missing path unless `throwOnMissing=true`; `append()` and `prepend()` create the file unless `throwOnMissing=true`. Check the method reference before relying on a default.

```javascript
try {
    disk.delete( "reports/old.csv", true );
} catch ( any error ) {
    if ( error.type == "cbfs.FileNotFoundException" ) {
        // Decide whether a missing file is acceptable.
    } else {
        rethrow;
    }
}
```

S3 operations can also raise errors from the underlying `s3sdk` client or remote service. Preserve useful error detail in logs without exposing credentials or signed URLs.
