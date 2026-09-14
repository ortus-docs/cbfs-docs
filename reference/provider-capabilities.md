# Provider Capabilities

CBFS keeps the common API consistent, but storage backends cannot offer identical behavior.

| Capability | Local | RAM | S3 |
| --- | :---: | :---: | :---: |
| File CRUD and append/prepend | Yes | Yes | Yes |
| Directory operations | Yes | Yes | Object-prefix semantics |
| File and directory listings | Yes | Yes | Yes |
| `getAsBinary()` | Yes | Yes | Yes |
| `upload()` | Yes | No | No |
| `stream()` / `streamOf()` | Yes | No | No |
| `glob()` | Yes | No | Yes |
| Symbolic links | Yes | No | No |
| Unix `chmod()` | Yes | No-op/unsupported | No |
| Temporary URLs | Local URL | Not applicable | Signed URL |
| Persistent visibility | Filesystem | In memory | Object metadata/ACL |
| `extendedInfo()` | Yes | No | No |

* **Local** supports uploads, Java NIO streams, symbolic links, permission checks, and extended metadata.
* **RAM** is useful for tests and ephemeral data, but has no local filesystem path or upload semantics.
* **S3** maps files and directories to objects and prefixes. Operations are network requests and may use the provider cache.

See the [Local](../getting-started/providers/local-provider.md), [RAM](../getting-started/providers/ram-provider.md), and [S3](../getting-started/providers/s3-provider.md) setup pages.
