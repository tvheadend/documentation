# DVR

This section includes functions to manipulate recorder objects; timers, autorecs and recordings. Unless noted otherwise, RECORDER privilege is required for all these functions - the 'Basic' tick-box in the 'Video Recorder' drop-down on the Access Entry screen. Other tick-boxes will be needed for some functions.

### dvr/config/class

Lists the text strings, options and defaults used when configuring the DVR capability within TVH (ie Configuration -> Recording). Requires either RECORDER or ADMIN privilege.

### dvr/config/grid

Lists the configuration sets available for the TVH server together with their options. Configurations are identified by their `name` parameter; the default config has the name blank. Requires either RECORDER or ADMIN privilege.

```
{
   "total" : 1,
   "entries" : [
      {
         "cache" : 2,
         "storage-mfree" : 1000,
         "autorec-maxsched" : 0,
         "whitespace-in-title" : false,
         "time-in-title" : false,
         "channel-dir" : false,
         "epg-running" : true,
         "name" : "",
         "episode-in-title" : false,
         "profile" : "af143f0983fd4e91953fb859c5561984",
         "clean-title" : false,
         "pre-extra-time" : 0,
         "uuid" : "4e3a1e1cacd2d559c129e7b90f6c986e",
         "day-dir" : false,
         "subtitle-in-title" : false,
         "epg-update-window" : 86400,
         "title-dir" : false,
         "warm-time" : 30,
         "windows-compatible-filenames" : false,
         "autorec-maxcount" : 0,
         "removal-days" : 2147483647,
         "storage-mused" : 0,
         "tag-files" : true,
         "clone" : true,
         "omit-title" : false,
         "enabled" : true,
         "storage" : "/mnt/tvheadend",
         "date-in-title" : false,
         "channel-in-title" : false,
         "post-extra-time" : 0,
         "skip-commercials" : false,
         "rerecord-errors" : 0,
         "file-permissions" : "0664",
         "retention-days" : 2147483646,
         "charset" : "ASCII",
         "pri" : 2,
         "directory-permissions" : "0775",
         "pathname" : "$t$n.$x"
      }
   ]
}
```

### dvr/config/create

Creates a new configuration set. Requires ADMIN privilege.

* `name` configuration name. Must be supplied and cannot be blank
* `conf` parameter set, passed as a JSON object

### dvr/entry/class

Lists the text strings, options and defaults used when editing an upcoming recording.

### dvr/entry/grid

Lists all of the recordings that TVH knows about, ie it combines the output of `grid_upcoming`, `grid_finished`, `grid_failed` and `grid_removed`. Use the `status` parameter to tell them apart.

See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details, and note the default is to return only the first 50 items.

### dvr/entry/grid\_upcoming

Lists all of the currently-scheduled recordings. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details, and note the default is to return only the first 50 items.

* `duplicates` Set to 0 to exclude duplicate timers. Default is 1.

The data is derived from the EPG when the timer was scheduled. From version 4.3.1013 the item "disp\_extratext" is included to deal with the inconsistent use of "subtitle" and "summary" fields by broadcasters.

The values of `start_real` and `stop_real` take into account the recorder padding and warm-up time currently set.

The value of `rating_label_uuid` points to a current parental rating label record.

```
{
  "entries": [
    {
      "uuid": "bc85208b236701a63568cb62d5506e08",
      "enabled": true,
      "create": 1561451356,
      "watched": 0,
      "start": 1562099400,
      "start_extra": 0,
      "start_real": 1562099340,
      "stop": 1562103000,
      "stop_extra": 0,
      "stop_real": 1562103000,
      "duration": 3600,
      "channel": "9a20ebf5ec10a3c49c2c021cc2698ecc",
      "channelname": "BBC TWO HD",
      "image": "",
      "fanart_image": "",
      "title": {
        "eng": "Inside the Bank of England"
      },
      "disp_title": "Inside the Bank of England",
      "disp_subtitle": "",
      "summary": {
        "eng": "1/2. Filmed with unprecedented access, this episode goes inside the Bank to show how it prints our cash, ensures our money holds its value and sets the UKs interest rate. [S,AD] [HD]"
      },
      "disp_summary": "1/2. Filmed with unprecedented access, this episode goes inside the Bank to show how it prints our cash, ensures our money holds its value and sets the UKs interest rate. [S,AD] [HD]",
      "description": {
        "eng": "1/2. Filmed with unprecedented access, this episode goes inside the Bank to show how it prints our cash, ensures our money holds its value and sets the UKs interest rate. [S,AD] [HD]"
      },
      "disp_description": "1/2. Filmed with unprecedented access, this episode goes inside the Bank to show how it prints our cash, ensures our money holds its value and sets the UKs interest rate. [S,AD] [HD]",
      "disp_extratext": "1/2. Filmed with unprecedented access, this episode goes inside the Bank to show how it prints our cash, ensures our money holds its value and sets the UKs interest rate. [S,AD] [HD]",
      "pri": 6,
      "retention": 0,
      "removal": 0,
      "playposition": 0,
      "playcount": 0,
      "config_name": "4e3a1e13acd2d5a9c129e7b00f6c986e",
      "owner": "tvheadend",
      "creator": "tvheadend",
      "filename": "",
      "errorcode": 0,
      "errors": 0,
      "data_errors": 0,
      "dvb_eid": 3842,
      "noresched": false,
      "norerecord": false,
      "fileremoved": 0,
      "uri": "crid://fp.bbc.co.uk/m/4586",
      "autorec": "24fcfd056fc32b86f0abd9fc6a57d17d",
      "autorec_caption": "Inside the Bank of England (Inside the Bank of England - Created from EPG query)",
      "timerec": "",
      "timerec_caption": "",
      "parent": "",
      "child": "",
      "content_type": 2,
      "copyright_year": 0,
      "broadcast": 295634,
      "episode_disp": "",
      "url": "",
      "filesize": 0,
      "status": "Scheduled for recording",
      "sched_status": "scheduled",
      "duplicate": 0,
      "first_aired": 0,
      "comment": "Auto recording: Inside the Bank of England - Created from EPG query",
      "category": [],
      "credits": {},
      "keyword": [],
      "genre": [
        32
      ],
      "age_rating": 11,
      "rating_label_saved": "PG,
      "rating_icon_saved": "file:///my/file/location/acma-pg.png",
      "rating_country_saved": "AUS",
      "rating_authority_saved": "ACMA",
      "rating_label_uuid": "a82438515ecc857dbf2509517ff3fe40",
      "rating_icon": "imagecache/37",
      "rating_label": "PG"
    }, ...
  ],
  "total": 4
}
```

### dvr/entry/grid\_finished

Lists recordings which have completed and which are still in the TVH logs. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details, and note the default is to return only the first 50 items.

The values of `start_real` and `stop_real` take into account the recorder padding and warm-up time **currently** set - not the values which were set when the recording was made. If this is a segmented recording (a programme split into two or more parts with for example a news bulletin in between) the value of `stop_real` is the end time of the final segment, while `stop` is the end time of he first segment.

Because legislation can change over time, the value of `rating_label_uuid` is blank for finished DVR entries, the 'saved' tags should be used instead.

```
{
  "entries": [
    {
      "uuid": "07ac8ed6d7d8744a4217c7b7005d5d7a",
      "enabled": true,
      "create": 1581300276,
      "watched": 0,
      "start": 1581937200,
      "start_extra": 0,
      "start_real": 1581937110,
      "stop": 1581940800,
      "stop_extra": 0,
      "stop_real": 1581940800,
      "duration": 3600,
      "channel": "16460c1b17ee679e0fc3cdb851edd294",
      "channel_icon": "imagecache/223",
      "channelname": "YESTERDAY",
      "image": "",
      "fanart_image": "",
      "title": {
        "eng": "Abandoned Engineering"
      },
      "disp_title": "Abandoned Engineering",
      "disp_subtitle": "",
      "disp_summary": "",
      "description": {
        "eng": "Pyramiden Norway: A town with a supernatural atmosphere, a collection of imposing buildings in southern Australia, and the remains of curious-looking basins emerging from the waves. [AD,S]"
      },
      "disp_description": "Pyramiden Norway: A town with a supernatural atmosphere, a collection of imposing buildings in southern Australia, and the remains of curious-looking basins emerging from the waves. [AD,S]",
      "disp_extratext": "Pyramiden Norway: A town with a supernatural atmosphere, a collection of imposing buildings in southern Australia, and the remains of curious-looking basins emerging from the waves. [AD,S]",
      "pri": 6,
      "retention": 0,
      "removal": 0,
      "playposition": 0,
      "playcount": 0,
      "config_name": "1ccca1a328ecdcab3f88640dda5b6209",
      "owner": "linvdr",
      "creator": "linvdr",
      "filename": "/video/tvheadend/Abandoned Engineering-4.ts",
      "errorcode": 0,
      "errors": 0,
      "data_errors": 0,
      "dvb_eid": 0,
      "noresched": true,
      "norerecord": false,
      "fileremoved": 0,
      "uri": "crid://onid-2/QQK596",
      "autorec": "",
      "autorec_caption": "",
      "timerec": "",
      "timerec_caption": "",
      "parent": "",
      "child": "",
      "content_type": 2,
      "copyright_year": 0,
      "broadcast": 0,
      "episode_disp": "",
      "url": "dvrfile/07ac8ed6d7d8744a4217c7b7005d5d7a",
      "filesize": 997310108,
      "status": "Completed OK",
      "sched_status": "completed",
      "duplicate": 0,
      "first_aired": 0,
      "comment": "Auto recording: New: Abandoned Engineering - Created from EPG query",
      "category": [],
      "credits": {},
      "keyword": [],
      "genre": [],
      "age_rating": 13,
      "rating_label_saved": "M",
      "rating_icon_saved": "file:///my/file/location/acma-m.png",
      "rating_country_saved": "AUS",
      "rating_authority_saved": "ACMA",
      "rating_label_uuid": "",
      "rating_icon": "imagecache/35",
      "rating_label": "M"
    }, ...
  "total": 101
}
```

### dvr/entry/grid\_failed

Lists failed recordings. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details.

If you merge the 'failed' and 'completed' recordings into a single list, the only way to tell which list the entries originally came from is by using the `status` field.

```{
   "total" : 1,
   "entries" : [
      {
         "parent" : "",
         "channelname" : "BBC Four HD",
         "start" : 1513112400,
         "stop_real" : 1513116000,
         "description" : {
            "eng" : "2/3. Series in which Sam Willis reveals stories of invasion in Britain, including the Barbary Corsaire pirates and the tale of King Louis the Lion, who invaded in the 13th century. [HD] [S]"
         },
         "comment" : "Auto recording: Created from EPG query",
         "disp_title" : "New: Invasion! with Sam Willis",
         "child" : "",
         "uri" : "crid://fp.bbc.co.uk/247LP4",
         "image" : "",
         "dvb_eid" : 62795,
         "autorec_caption" : " (Created from EPG query)",
         "removal" : 0,
         "url" : "dvrfile/22d9847b550b8fe9e39e01bda2e41777",
         "owner" : "tvheadend",
         "copyright_year" : 0,
         "playposition" : 0,
         "filename" : "/video/tvheadend/New: Invasion! with Sam Willis.ts",
         "start_real" : 1513112355,
         "start_extra" : 0,
         "duration" : 3600,
         "category" : [],
         "creator" : "tvheadend",
         "playcount" : 0,
         "sched_status" : "completed",
         "status" : "Too many data errors",
         "autorec" : "5cf012bf5c78e23d3c89c59c172414cb",
         "errors" : 0,
         "norerecord" : false,
         "broadcast" : 0,
         "noresched" : true,
         "keyword" : [],
         "config_name" : "ffb7136480e16dac47c8e71bd7686537",
         "disp_subtitle" : "2/3. Series in which Sam Willis reveals stories of invasion in Britain, including the Barbary Corsaire pirates and the tale of King Louis the Lion, who invaded in the 13th century. [HD] [S]",
         "enabled" : true,
         "stop_extra" : 0,
         "pri" : 6,
         "retention" : 0,
         "subtitle" : {
            "eng" : "2/3. Series in which Sam Willis reveals stories of invasion in Britain, including the Barbary Corsaire pirates and the tale of King Louis the Lion, who invaded in the 13th century. [HD] [S]"
         },
         "disp_description" : "2/3. Series in which Sam Willis reveals stories of invasion in Britain, including the Barbary Corsaire pirates and the tale of King Louis the Lion, who invaded in the 13th century. [HD] [S]",
         "fileremoved" : 0,
         "filesize" : 2171129092,
         "credits" : {},
         "title" : {
            "eng" : "New: Invasion! with Sam Willis"
         },
         "content_type" : 2,
         "genre" : [],
         "errorcode" : 0,
         "stop" : 1513116000,
         "channel_icon" : "",
         "data_errors" : 510410,
         "timerec" : "",
         "channel" : "7bd448424af369b19f22511b1ece023c",
         "uuid" : "22d9847b550b8fe9e39e01bda2e41777",
         "timerec_caption" : "",
         "first_aired" : 0,
         "duplicate" : 0
      }
   ]
}
```

### dvr/entry/grid\_removed

Lists removed recordings. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details.

Under some circumstances an unsuccessful recording may appear here rather than under failed recordings. For example when EIT-based accurate recording is being used and the 'running' status is never received.

If TVH is configured to delete the log record when a recording is deleted this function will not return them.

### dvr/entry/create

Creates a new timer from a JSON object.

* `conf` The JSON object describing the timer. Items not specified are derived from the default profile of the user. An example of the minimum useful JSON is shown below.

```
{
   "start":1509397200,
   "stop":1509400800,
   "channelname":"Channel 5",
   "title":{
      "eng":"Paddington Station 24/7"
   },
   "subtitle":{"eng":"More real-life dramas..."}
}
```

The function returns the uuid of the created timer on success.

It is also possible using this function to add a file created elsewhere into the TVH database as a completed recording. Items needed in the JSON are:

```
{
    "enabled": true,
    "start": 1509000000,
    "stop":  1509003600,
    "channelname": "local file",
    "title": {
        "eng": "my title"
    },
    "subtitle": {
        "eng": "filename: my video"
    },
    "description": {
        "eng": "my description"
    },
    "comment": "added by tvh_addfile.py",
    "files": [
        {
            "filename": "/full/path/to/videofile.ts"
        }
    ]
}
```

It is important that the start and stop times are in the past, otherwise TVH will try to create a timer to record the event. _(Thanks to "ullix tv" for this information.)_ Also note that the ability to add a pre-recorded file is unintended behaviour - see [Caution](../#caution).

### dvr/entry/create\_by\_event

Creates a new timer using details from the EPG. Input parameters are:

* `config_uuid` this is the `uuid` parameter from the output of [dvr/config/grid](dvr.md#dvr-config-grid)
* `event_id` this is the `eventId` parameter for the event, taken from [epg/events/grid](epg.md#epg-events-grid)

### dvr/entry/rerecord/toggle, dvr/entry/rerecord/deny, dvr/entry/rerecord/allow

These functions provide the same capability as the Re-record button in Digital Video Recorder -> Finished Recordings. "Allow" sets the recording to be re-done, "deny" cancels a scheduled rerecording, "toggle" reverses the rerecord state.

* `uuid` the `uuid` of the finished or failed recording, or a JSON object containing an array of uuids.

### dvr/entry/stop

Gracefully stops a running recording.

* `uuid` The `uuid` value from the timer's entry in dvr/entry/grid.

### dvr/entry/cancel

Deletes a timer or aborts a running recording.

* `uuid` The `uuid` value from the timer's entry in dvr/entry/grid.

If the timer is running, the recording is kept on disk but classified as a 'failed' recording.

**NOTE** To delete a series use [idnode/delete](idnode.md#idnode-delete), passing parameter `uuid` from the entry in [dvr/timerec/grid](dvr.md#dvr-timerec-grid). As with the UI, deleting a series deletes all pending timers for that series.

### dvr/entry/prevrec/toggle, dvr/entry/prevrec/set, dvr/entry/prevrec/unset

These three functions affect the "previously recorded" status of a timer. If set, either directly or via a call to the toggle function, the timer is marked as completed and the file flagged as deleted. If unset, a new timer is created.

These functions provide the same capability as the Previously Recorded button in Digital Video Recorder -> Upcoming/Current Recordings. It can be used to 'hide' re-runs to prevent them being re-recorded.

### dvr/entry/remove

Removes a completed recording from storage.

* `uuid` The recording's `uuid` value from [dvr/entry/grid\_finished](dvr.md#dvr-entry-grid\_finished).

### dvr/entry/filemoved

Informs TVH that a recording has been relocated (by external means) within the filesystem. Requires ADMIN privilege.

* `src` The original full path to the file
* `dst` The new full path to the file

### dvr/entry/move/finished

Move a **finished** recording entry to the "Finished Recordings" category, presumably from "Failed Recordings". The actual file is not moved.

* `uuid` The `uuid` of the entry, or an array of entries passed as a JSON object.

### dvr/entry/move/failed

Move a **finished** recording entry to the "Failed Recordings" category, presumably from "Finished Recordings". The actual file is not moved.

* `uuid` The `uuid` of the entry, or an array of entries passed as a JSON object.

### dvr/autorec/class

Lists the text strings, options and defaults used when creating or editing a series timer.

### dvr/autorec/grid

Lists autorecs (series timers). See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details.

```
{
   "entries" : [
      {
         "record" : 0,
         "pri" : 6,
         "channel" : "a931256950c3f8aa5c5416cd36175e13",
         "content_type" : 0,
         "retention" : 0,
         "fulltext" : false,
         "start_window" : "Any",
         "serieslink" : "crid://www.five.tv/R5HP0",
         "config_name" : "4e3a1e13acd2d5a9c129e7b00f6c986e",
         "maxduration" : 0,
         "removal" : 0,
         "start_extra" : 0,
         "stop_extra" : 0,
         "maxcount" : 0,
         "owner" : "tvheadend",
         "weekdays" : [
            1,
            2,
            3,
            4,
            5,
            6,
            7
         ],
         "uuid" : "f2c30b9757e66567bf2d8ec6de60314c",
         "creator" : "tvheadend",
         "tag" : "",
         "maxsched" : 0,
         "comment" : "Created from EPG query",
         "start" : "Any",
         "btype" : 0,
         "brand" : "",
         "enabled" : true,
         "season" : "",
         "minduration" : 0,
         "title" : "New: Paddington Station 24/7"
      }, ...
   ],
   "total" : 9
}
```

### dvr/autorec/create

Create a new series timer by specifying search parameters. To create a timer using CRIDs use [dvr/autorec/create\_by\_series](dvr.md#dvr-autorec-create\_by\_series).

* `conf` A JSON object specifying the selection parameters for the timer.
* `config_uuid` The `uuid` parameter from the output of [dvr/config/grid](dvr.md#dvr-config-grid). Parameter `config_name` may be passed instead.

### dvr/autorec/create\_by\_series

Creates a new series timer using CRIDs. Input parameters are:

* `config_uuid` The `uuid` parameter from the output of [dvr/config/grid](dvr.md#dvr-config-grid)
* `event_id` The `eventId` parameter for one event in the series, taken from [epg/events/grid](epg.md#epg-events-grid)

**NOTE** To delete a series use [idnode/delete](idnode.md#idnode-delete), passing parameter `uuid` from the entry in [dvr/autorec/grid](dvr.md#dvr-autorec-grid). As with the UI, deleting a series deletes all pending timers for that series.

### dvr/timerec/class

Lists the text strings, options and defaults used when creating or editing a time-based recording.

### dvr/timerec/grid

Lists time-based recordings. See [Grid Parameters](common-parameters.md#grid-parameters) for parameter details.

```
{
   "total" : 1,
   "entries" : [
      {
         "name" : "My Timerec",
         "title" : "Time-%F_%R",
         "enabled" : true,
         "channel" : "7bd448424af369b19f22511b1ece023c",
         "retention" : 0,
         "config_name" : "ffb7136480e16dac47c8e71bd7686537",
         "creator" : "tvheadend",
         "uuid" : "458251fe1963a9967e5b83e8f2a680e6",
         "weekdays" : [
            2,
            4
         ],
         "pri" : 6,
         "owner" : "tvheadend",
         "stop" : "19:30",
         "start" : "19:00",
         "removal" : 0
      }
   ]
}
```

### dvr/timerec/create

Create a new time-based timer.

* `conf` A JSON object specifying the selection parameters for the timer.

A JSON object is returned containing the UUID of the timerec.
