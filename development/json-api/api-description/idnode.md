# idnode

_These function provide direct access to the internal data structures of TVHeadend. Attempting to modify these internal structures may have unwanted effects including loss of data._

Information is held within TVHeadend in a key-value database. The key for each record is a random 128-bit value called a uuid. The value is a data structure which can be represented in JSON format. The record is called an idnode.

The content of each idnode depends on what it represents; this is indicated by the value of the `class` parameter.

Although no special privilege is required to call these functions, access control is applied to the data items being referenced.

### idnode/load

Read the value of one or more idnode records. One (and only one) of these parameters must be specified:

* `uuid` The uuid (or JSON-structured list of uuids) to read.
* `class` The class of records to read, ie one of the classes returned by classes.

If `uuid` is given, the data to be returned may be qualified by setting one of these parameters to an integer greater than zero:

* `meta` Include meta-data (default values and descriptions of the data items).
* `grid` Return a brief summary of the records.

If `class` is given, setting the parameter `enum` to an integer value greater than zero returns only a set of key-value pairs.

In both cases the `list` parameter can be used to select which items are to be output, based on the value of the 'id' field. Multiple entries can be selected, separated by commas, colons or semicolons. A '-' in front of an entry deselects that item (and implicitly selects all others).

### idnode/save

Update an existing idnode.

* `node` The JSON object (or array of objects) containing the update.

Each update must contain the `uuid` item. Other items supplied replace those in the idnode; they are not merged.

Fields within an idnode may be read-only; for this reason it may not be possible to take the data from idnode/load and use it as input to idnode/save _(thanks to Poul Kalff for this information)_. To check the read-only status of a field, use idnode/class and check for a 'rdonly' flag.

### idnode/tree

Read information held in a tree structure (eg for tuner devices).

* `uuid` The uuid of the starting point in the tree structure, or the special value 'root'.
* `root` The uuid of the head of the tree structure. Required if `uuid` = 'root'.

### idnode/class

List information about a specified class; mostly metadata used to configure the TVHeadend UI.

* `name` The name of the class, ie one of the values returned by classes.

### idnode/delete

Delete one or more records.

* `uuid` The uuid (or a JSON-formatted list) of the record(s) to be deleted.

### idnode/moveup

### idnode/movedown
