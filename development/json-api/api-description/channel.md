# Channel

Functions to query and manipulate the list of channels.

A TVH user can only see via the API those channels which have been enabled and to which access has been allowed. However a user with ADMIN privilege can use the parameter `all=1` to see details of every channel, channeltag and category even if they do not have access to them.

### channel/class

Lists the text strings, options and defaults used when configuring channels within TVH (ie Configuration -> Channel/EPG -> Channel -> Add).

### channel/create

Creates a new channel. Requires ADMIN privilege.

* `conf` A JSON object containing details of the new channel.

### channel/grid

Lists details of channels. For details of the parameters and selection criteria which can be applied, see Grid Parameters.

```
{
   "entries" : [
      {
         "dvr_pst_time" : 0,
         "enabled" : true,
         "epgauto" : true,
         "autoname" : true,
         "name" : "BBC RB 1",
         "number" : 601,
         "tags" : [
            "21d5fe751062c4d99997d6cb48f43c55",
            "1a2a61c4374cedb1fc29417f1a517446"
         ],
         "services" : [
            "9b0e2e103a373350f5e99cda6dd3f055"
         ],
         "epg_running" : -1,
         "epggrab" : [],
         "uuid" : "ae63d3b40fbfab610f49290abc189472",
         "bouquet" : "",
         "dvr_pre_time" : 0
      }, ...
   ],
   "total" : 104
}
```

### channel/list

Lists the names and uuids of all known channels. For disabled channels the channel name is enclosed in braces.

These parameters were added at version 4.3-905:

* `numbers` If non-zero, the LCN appears before the channel name, separated by a space. Default is zero.
* `sources` If non-zero, the source appears after the channel name, in square brackets and separated by a space. Default is zero.
* `sort` Either `name` to sort by channel name, or `numname` to sort by LCN then by name (default). The name sort is case-sensitive.

```
{
   "entries" : [
      {
         "val" : "Channel 5+1",
         "key" : "7e7b77801531c803f5ce8f4d5003f44c"
      }, ...
   ]
}
```

### channel/rename

Renames a channel. Only available from version 4.3.652. Requires ADMIN privilege.

* `from` The current name of the channel.
* `to` The new name of the channel.

### channeltag/class

Lists the text strings, options and defaults used when configuring channels within TVH (ie Configuration -> Channel/EPG -> Channel Tags -> Add).

### channeltag/create

Creates a new channel tag. Requires ADMIN privilege.

* `conf` A JSON object containing details of the new channel tag.

### channeltag/grid

Lists details of channel tags. For details of the parameters and selection criteria which can be applied, see Grid Parameters.

```
{
   "total" : 5,
   "entries" : [
      {
         "index" : 0,
         "private" : false,
         "icon_public_url" : "",
         "internal" : false,
         "name" : "Radio",
         "titled_icon" : false,
         "enabled" : true,
         "uuid" : "3479ac5a48d6680fc37d8b411cf0e2e8",
         "icon" : "",
         "comment" : ""
      }, ...
   ]
}
```

### channeltag/list

Lists the names and uuids of all channel tags.

```
{
   "entries" : [
      {
         "key" : "3479ac5a48d6680fc37d8b411cf0e2e8",
         "val" : "Radio"
      }, ...
   ]
}
```

### channelcategory/list

**Untested.** Return a list of the categories of events which appear in the current EPG and which the user is permitted to see. Used internally to populate the 'Category 1-3' drop-down boxes in DVR -> Autorecs -> Add (Expert view only). The function only works if the EPG is sourced from XMLTV.
