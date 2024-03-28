# Config

ADMIN privilege is required for all of these functions except config/capabilities.

### config/capabilities

Returns a list of some compile-time options which were used to build the software. Requires either 'Web Interface' or 'HTSP Interface' privilege.

```
[
   "caclient",
   "tvadapters",
   "imagecache",
   "timeshift",
   "trace",
   "libav"
]
```

### config/load

Lists the details, descriptions, defaults and current values of the items in the GUI screen Configuration -> General -> Base. See [Common Parameters](common-parameters.md) for details of selection parameters.

### config/save

**Untested.** Updates the server from an object in the format produced by [config/load](config.md#config-load).

* `node` The JSON object.

### memoryinfo/class

Lists the details and descriptions of items in the TVH GUI screen Configuration -> Debugging -> Memory Information Entries.

### memoryinfo/grid

Lists details of in-memory objects. See [Common Parameters](common-parameters.md) for details of selection parameters.

```
{
   "entries" : [
      {
         "peak_count" : 17154,
         "name" : "EPG Broadcasts",
         "uuid" : "a1af1bc4f29ba28104e71a540465f250",
         "count" : 17154,
         "peak_size" : 6235792,
         "size" : 6235792
      },
      {
         "peak_count" : 3285,
         "peak_size" : 369303,
         "count" : 3285,
         "size" : 369303,
         "name" : "EPG Series Links",
         "uuid" : "823a78a3bcd05b688c59871455da6399"
      },
      {
         "count" : 11514,
         "peak_size" : 5015593,
         "size" : 5015593,
         "name" : "EPG Episodes",
         "uuid" : "5c666eea1ec3de4bbb9a11f60116b258",
         "peak_count" : 11514
      }, ...
   ],
   "total" : 19
}
```

### pathlist

Lists all of the api functions supported by the server.

```
[
   "access/entry/class",
   "access/entry/create",
   "access/entry/grid",
   "access/entry/userlist", ...
]
```

### serverinfo

Lists information about the server including the software version number.

```
{
   "api_version" : 19,
   "webroot" : "/testserver",
   "name" : "Tvheadend",
   "capabilities" : [
      "caclient",
      "tvadapters",
      "trace",
      "libav"
   ],
   "sw_version" : "4.3-943~g9b85e7b7c-dirty"
}
```
