---
description: Reference documentation for the CBFS public API
---

# Reference

Use this section as the lookup index for CBFS's public API. The [usage guides](../usage/disk-usage/README.md) explain common workflows; these pages describe public methods, arguments, return values, and provider-specific boundaries.

* [Disk Service](disk-service.md) - register, resolve, inspect, and shut down disks.
* [Disk API](disk-api.md) - the common `IDisk` contract shared by providers.
* [File Object](file-object.md) - the fluent wrapper returned by `disk.file()`.
* [Provider capabilities](provider-capabilities.md) - supported operations by provider.
* [Configuration](configuration.md) - module settings, disk definitions, and environment variables.
* [Integration and lifecycle](integration.md) - injection DSL, helper method, module disks, and events.
* [Errors](errors.md) - common exception types and handling guidance.
