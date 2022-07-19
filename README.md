---
description: cbfs is a module for ColdBox that provides abstractions to any file system.
---

# Introduction

The `cbfs` module will enable you to abstract **ANY** filesystem within your ColdBox applications. You can configure as many disks as you wish which represent file systems in your application. Each disk is backed by a storage provider and configurable within your ColdBox application.

## Installation

Use CommandBox CLI to install:

```
box install cbfs

# Install bleeding edge version
box install cbfs@be
```

## System Requirements

* Lucee 5+
* Adobe ColdFusion 2016 (Deprecated)
* Adobe ColdFusion 2018+

## Versioning

`cbfs` is maintained under the [Semantic Versioning](https://semver.org) guidelines as much as possible. Releases will be numbered with the following format:

```
<major>.<minor>.<patch>
```

And constructed with the following guidelines:

* Breaking backward compatibility bumps the major (and resets the minor and patch)
* New additions without breaking backward compatibility bumps the minor (and resets the patch)
* Bug fixes and misc changes bumps the patch

## License

The ColdBox Platform, cbfs is open source and licensed under the [Apache 2](http://www.apache.org/licenses/LICENSE-2.0.html) License.

* Copyright by Ortus Solutions, Corp
* ColdBox, CacheBox, Wirebox, LogBox are registered trademarks by Ortus Solutions, Corp

##
