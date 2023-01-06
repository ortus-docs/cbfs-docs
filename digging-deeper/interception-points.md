# Interception Points

There are [ColdBox interception points](https://coldbox.ortusbooks.com/the-basics/interceptors) that are announced when working with CBFS disks, directories, and files that you can use. These can be used to provide additional functionality in your applications such as logging file access, securing folders, and more.

## cbfsOnDiskStart

Invoked after a disk has been started.

{% hint style="info" %}
CBFS automatically manages the starting of disks.
{% endhint %}

```javascript
component {
      function cbfsOnDiskStart( disk ) {
            //java...
      }
}
```

## cbfsOnDiskShutdown

{% hint style="info" %}
CBFS automatically manages the shutdown of disks.
{% endhint %}

Invoked after a disk has been shutdown.

```javascript
component {
      function cbfsOnDiskShutdown( disk ) {
            //java...
      }
}
```

## cbfsOnFileCreate

Invoked when a file is created.

```javascript
component {
    function cbfsOnFileCreate( file ) {
 
    }
}
```

## cbfsOnFileMove

Invoked when a file is moved.

```javascript
component {
    function cbfsOnFileMove( file ) {
 
    }
}
```

## cbfsOnFileCopy

Invoked when a file is copied.

```javascript
component {
    function cbfsOnFileCopy( file ) {
 
    }
}
```

## cbfsOnFileDelete

Invoked when a file is deleted.

```javascript
component {
    function cbfsOnFileDelete( file ) {
        
    }
}
```

## cbfsOnFileInfoRequest

Invoked when info or extended info is requested on a file.

```javascript
component {
    function cbfsOnFileInfoRequest( file ) {
    
    }
}
```

## cbfsOnFileMove

Invoked when a file is moved.

```javascript
component {
    function cbfsOnFileMove( file ) {
        
    }
}
```

## cbfsOnDirectoryMove

Invoked when a directory is moved.

<pre class="language-javascript"><code class="lang-javascript"><strong>component {
</strong>    function cbfsOnDirectoryMove( source, destination, disk ) {
    
    }
}
</code></pre>

## cbfsOnDirectoryCreate

Invoked when a directory is created.

```javascript
component {
    function cbfsOnDirectoryCreate( directory, disk ) {
    
    }
}
```

## cbfsOnDirectoryCopy

Invoked when a directory is copied.

```javascript
component {
    function cbfsOnDirectoryCopy( source, destination, disk ) {
    
    }
}
```

## cbfsOnDirectoryDelete

Invoked when a directory is deleted.

```javascript
component {
    function cbfsOnDirectoryDelete( directory, disk ) {
    
    }
}
```
