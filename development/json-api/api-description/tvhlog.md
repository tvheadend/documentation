# Tvhlog

ADMIN privilege is required for these functions.

### tvhlog/config/load

Lists the details, descriptions, defaults and current values of the items in the GUI screen Configuration -> Debugging -> Configuration -> Settings. See [Common Parameters](common-parameters.md) for details of selection parameters.

### tvhlog/config/save

**Untested.** Updates the server from an object in the format produced by [tvhlog/config/load](tvhlog.md#tvhlog-config-load).

* `node` The JSON object.

### tvhlog/subsystem/grid

List the subsystems available for trace and debug operations.

Also see [Debugging / Trace options](../../../appendices/debugging.md) and [CLI / Debug Options](../../../appendices/cli-commands.md#debug-options).

```
{
    "entries": [
        {
            "id": 1,
            "subsystem": "START",
            "description": "START",
            "trace": true,
            "debug": false
        },
         . . . . . . .
        {
            "id": 103,
            "subsystem": "ratinglabels",
            "description": "Rating Labels",
            "trace": false,
            "debug": true
        }
    ],
    "traceCount": 12,
    "debugCount": 42,
    "totalCount": 103
}
```

* `id` - The internal enum for this subsystem.  These values may change between systems depending upon the application version and the options used at compile-time but are otherwise constant.
* `subsystem` - The name of the subsystem.  These values are to be used in the WebUI when enabling trace/debug operations.
* `description` - The locale-aware description of the subsystem.
* `trace` - `True` if this subsystem is currently being traced.
* `debug` - `True` if this subsystem is currently being debugged.
* `traceCount` - The number of subsystems with `trace` currently set to `true`.
* `debugCount` - The number of subsystems with `debug` currently set to `true`.
* `totalCount` - The total number of subsystems.

**Note 1:**  Users may enter a special `all` subsystem (not listed) instead of nominating each subsystem individually in the WebUI.  This condition can be detected if `traceCoount` and/or `debugCount` is equal to `totalCount`.

**Note 2:** As at April 2024, the `id` field is informational only.  It is provided to facilitate future API development.
