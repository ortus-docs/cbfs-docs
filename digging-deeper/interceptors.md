# Interception Points

There are [ColdBox interception points](https://coldbox.ortusbooks.com/the-basics/interceptors) announced when working with CBFS disks, directories, and files. You can use them to log file access, secure folders, and add application behavior.

Each example shows the BoxLang class first and the equivalent CFML class second.

## cbfsOnDiskStart

Invoked after a disk has been started. CBFS manages disk startup automatically.

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class {
    function cbfsOnDiskStart( disk ) {
        // Handle the event.
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```cfml
component {
    function cbfsOnDiskStart( disk ) {
        // Handle the event.
    }
}
```
{% endtab %}
{% endtabs %}

## cbfsOnDiskShutdown

Invoked after a disk has been shut down. CBFS manages disk shutdown automatically.

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class {
    function cbfsOnDiskShutdown( disk ) {
        // Handle the event.
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```cfml
component {
    function cbfsOnDiskShutdown( disk ) {
        // Handle the event.
    }
}
```
{% endtab %}
{% endtabs %}

## File events

The file events are `cbfsOnFileCreate`, `cbfsOnFileMove`, `cbfsOnFileCopy`, `cbfsOnFileDelete`, and `cbfsOnFileInfoRequest`. Each receives the affected `file`.

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class {
    function cbfsOnFileCreate( file ) {}
    function cbfsOnFileMove( file ) {}
    function cbfsOnFileCopy( file ) {}
    function cbfsOnFileDelete( file ) {}
    function cbfsOnFileInfoRequest( file ) {}
}
```
{% endtab %}
{% tab title="CFML" %}
```cfml
component {
    function cbfsOnFileCreate( file ) {}
    function cbfsOnFileMove( file ) {}
    function cbfsOnFileCopy( file ) {}
    function cbfsOnFileDelete( file ) {}
    function cbfsOnFileInfoRequest( file ) {}
}
```
{% endtab %}
{% endtabs %}

## Directory events

The directory events are `cbfsOnDirectoryMove`, `cbfsOnDirectoryCreate`, `cbfsOnDirectoryCopy`, and `cbfsOnDirectoryDelete`.

{% tabs %}
{% tab title="BoxLang" %}
```boxlang
class {
    function cbfsOnDirectoryMove( source, destination, disk ) {}
    function cbfsOnDirectoryCreate( directory, disk ) {}
    function cbfsOnDirectoryCopy( source, destination, disk ) {}
    function cbfsOnDirectoryDelete( directory, disk ) {}
}
```
{% endtab %}
{% tab title="CFML" %}
```cfml
component {
    function cbfsOnDirectoryMove( source, destination, disk ) {}
    function cbfsOnDirectoryCreate( directory, disk ) {}
    function cbfsOnDirectoryCopy( source, destination, disk ) {}
    function cbfsOnDirectoryDelete( directory, disk ) {}
}
```
{% endtab %}
{% endtabs %}
