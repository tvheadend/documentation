# Common Parameters

### Grid parameters

API calls which end in `/grid`, with the exception of epg/events/grid, have a common set of parameters:

* `start` First entry to include. Default is the first (0).
* `limit` Number of entries to include. **Default is 50** - use a large number to get all.
* `filter` A JSON object describing the filter(s) to be applied. See Grid Filters below for syntax.
* `sort` Name of the field to sort the records by. A case-sensitive sort is used.
* `dir` if `sort` is specified then `dir=desc` produces a reverse sort.

#### Grid filters

A filter can be applied to the output using a JSON object. The syntax is:

```
filter=[
            {
                "field" : "<fieldname>",
                "type"  : "string|numeric|boolean",
                "value" : "<value>",
                "comparison" : "gt|lt|eq",
                "intsplit" : <intsplit>
             }, ...
        ]
```

The "comparison" field is only used with numeric data. A "gt" comparison actually matches on greater-or-equal, and "lt" on less-or-equal.

Boolean values must be specified as "0" or "1" (NOT "true" or "false"). A (case-insensitive) regular expression match is used for strings.

The "intsplit" field is used for integer variables which are used to store a quotient and remainder, and defines how the bits of the variable are allocated.

Multiple filters can be applied to a query ONLY if they refer to different fields, so for example it is not possible to query for EPG events having start times between two values.

### Load parameters

API calls which end in `/load`, with the exception of epg/events/load, have a common set of parameters:

* `meta` If > 0 an extra data structure is output, mostly related to the format of the GUI screen where the information is presented. Default is 0.
* `list` This parameter selects which items in the params array are to be output, based on the value of the 'id' field. Multiple entries can be selected, separated by commas, colons or semicolons. A '-' in front of an entry deselects that item (and implicitly selects all others).
