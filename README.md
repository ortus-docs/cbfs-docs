---
description: cbfs is a module for ColdBox that provides abstractions to any file system.
---

# Introduction

<figure><img src=".gitbook/assets/CleanShot 2022-08-29 at 14.02.25.png" alt=""><figcaption></figcaption></figure>

The `cbfs` module will enable you to abstract **ANY** filesystem within your ColdBox applications. You can configure as many disks as you wish to represent file systems in your application. Each disk is backed by a storage provider and configurable within your ColdBox application.

## Storage Providers

The available storage providers are:

* `Local` - A local file system storage provider.
* `Ram` - An in-memory file storage provider.
* `S3` - An Amazon S3, Rackspace, Digital Ocean, or Google Cloud Storage provider. (Beta)
* `CacheBox` - Leverages ANY caching engine as a virtual file system. If you use a distributed cache like Couchbase, Redis, or Mongo, you will have a distributed file system.

## System Requirements

* Lucee 5+
* Adobe ColdFusion 2016 (Deprecated)
* Adobe ColdFusion 2018+

## Versioning

`cbfs` is maintained under the [Semantic Versioning](https://semver.org) guidelines as much as possible. We number releases in the following format:

```
<major>.<minor>.<patch>
```

And constructed with the following guidelines:

* Breaking backward compatibility bumps the major (and resets the minor and patch)
* New additions without breaking backward compatibility bump the minor (and reset the patch)
* Bug fixes and misc changes bump the patch

## License

The ColdBox Platform, cbfs is open source and licensed under the [Apache 2](http://www.apache.org/licenses/LICENSE-2.0.html) License.

* Copyright by Ortus Solutions, Corp
* ColdBox, CacheBox, Wirebox, and LogBox are registered trademarks by Ortus Solutions, Corp.

##
