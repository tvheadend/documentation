# EPGgrab

Manipulate EPG grabbers. ADMIN privilege is required for these functions except for epggrab/channel/list.

### epggrab/channel/list

Lists the EPG grabber channels, ie those appearing in Configuration -> Channel / EPG -> EPG Grabber Channels, together with the available option fields and the selections chosen.

```
{
   "entries" : [
    {
      "uuid": "fffe86fe9b43bdc58b607f811ee44fad",
      "id": "fffe86fe9b43bdc58b607f811ee44fad",
      "text": "opentv-skyuk-3618: opentv-skyuk-3618 (OpenTV: Sky UK)",
      "caption": "Channels / EPG - EPG Grabber Channels",
      "class": "epggrab_channel",
      "event": "epggrab_channel",
      "params": [
        {
          "id": "enabled",
          "type": "bool",
          "caption": "Enabled",
          "description": "Enable/disable EPG data for the entry.",
          "default": false,
          "group": 1,
          "value": true
        },
        {
          "id": "modid",
          "type": "str",
          "caption": "Module ID",
          "description": "Module ID used to grab EPG data.",
          "default": "",
          "rdonly": true,
          "hidden": true,
          "group": 1,
          "value": "opentv-skyuk"
        },
        {
          "id": "module",
          "type": "str",
          "caption": "Module",
          "description": "Name of the module used to grab EPG data.",
          "default": "",
          "rdonly": true,
          "nosave": true,
          "group": 1,
          "value": "OpenTV: Sky UK"
        },
        {
          "id": "path",
          "type": "str",
          "caption": "Path",
          "description": "Data path (if applicable).",
          "default": "",
          "rdonly": true,
          "nosave": true,
          "group": 1,
          "value": ""
        },
        {
          "id": "updated",
          "type": "time",
          "caption": "Updated",
          "description": "Date the EPG data was last updated (not set for OTA grabbers).",
          "default": 0,
          "rdonly": true,
          "nosave": true,
          "group": 1,
          "value": 0
        },
        {
          "id": "id",
          "type": "str",
          "caption": "ID",
          "description": "EPG data ID.",
          "default": "",
          "group": 1,
          "value": "opentv-skyuk-3618"
        },
        {
          "id": "name",
          "type": "str",
          "caption": "Name",
          "description": "Service name found in EPG data.",
          "default": "",
          "group": 1
        },
        {
          "id": "names",
          "type": "str",
          "caption": "Names",
          "description": "Additional service names found in EPG data.",
          "default": "",
          "group": 1,
          "value": ""
        },
        {
          "id": "number",
          "type": "s64",
          "caption": "Number",
          "description": "Channel number as defined in EPG data.",
          "default": 0,
          "group": 1,
          "intsplit": 1000000,
          "value": 172
        },
        {
          "id": "icon",
          "type": "str",
          "caption": "Icon",
          "description": "Channel icon as defined in EPG data.",
          "default": "",
          "group": 1
        },
        {
          "id": "channels",
          "type": "str",
          "caption": "Channels",
          "description": "Channels EPG data is used by.",
          "list": 1,
          "enum": {
            "type": "api",
            "uri": "channel/list",
            "event": "channel",
            "params": {
              "all": 1,
              "numbers": 1
            }
          },
          "group": 1,
          "value": [
            "2aae489c6a59abc9b0584c96b8300adb"
          ]
        },
        {
          "id": "only_one",
          "type": "bool",
          "caption": "Once per auto channel",
          "description": "Only use this EPG data once when automatically determining what EPG data to set for a channel.",
          "default": false,
          "group": 1,
          "value": false
        },
        {
          "id": "update",
          "type": "int",
          "caption": "Channel update options",
          "description": "Options used when updating channels.",
          "list": 1,
          "advanced": true,
          "enum": [
            {
              "key": "update_icon",
              "val": "Icon"
            },
            {
              "key": "update_chnum",
              "val": "Number"
            },
            {
              "key": "update_chname",
              "val": "Name"
            }
          ],
          "value": []
        },
        {
          "id": "comment",
          "type": "str",
          "caption": "Comment",
          "description": "Free-form text field, enter whatever you like.",
          "default": "",
          "group": 1
        }
      ]
    }
  ]
}
```

### epggrab/channel/class

Lists the parameters, descriptions, options and defaults for the GUI screen Configuration -> Channel/EPG -> EPG Grabber Channels.

### epggrab/channel/grid

Gives details of the EPG grabber channels, ie from Configuration -> Channel / EPG -> EPG Grabber Channels. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details.

```
{
  "entries": [
    {
      "uuid": "280f57f849ce2360f3cc413223cc28a4",
      "enabled": true,
      "modid": "opentv-skyuk",
      "module": "OpenTV: Sky UK",
      "path": "",
      "updated": 0,
      "id": "opentv-skyuk-5602",
      "names": "",
      "number": 506,
      "channels": [
        "4e523d1471e66f64a2837b2cbb3e9c5f"
      ],
      "only_one": false,
      "update": []
    },
    ...
  ],
  "total": 279
}
```

### epggrab/module/list

List EPG Grabber Modules, as shown in the GUI screen Configuration -> Channel/EPG -> EPG Grabber Modules.

```
{
   "entries" : [
      {
         "uuid" : "13ba822c654b492183fbd462cd2700f6",
         "title" : "External: XMLTV",
         "status" : "epggrabmodNone"
      }, ...
   ]
}
```

### epggrab/config/load

Lists the parameters, options, defaults and current settings for the EPG grabber, ie Configuration -> Channel / EPG -> EPG Grabber. See [Load Parameters](common-parameters.md#load-parameters) for parameter details.

### epggrab/config/save

Updates the EPG Grabber configuration from an object in the same format as provided by [epggrab/config/load](epggrab.md#epggrab-config-load).

* `node` The JSON object.

### epggrab/ota/trigger

Queues a run of the OTA EPG grabber.

* `trigger` Delay in seconds before the run starts. Minimum is one second, maximum is one week.

### epggrab/internal/rerun

Run the internal EPG grabbers immediately.

* `rerun` Not used but must be an integer greater than zero.
