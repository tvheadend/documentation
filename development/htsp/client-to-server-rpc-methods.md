---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Client to Server (RPC) methods

### hello

Used to identify the client toward the server and to get the session challenge used to hash passwords into digests. The client can request a different version of the HTSP protocol with this method. If no 'hello' message is sent the server assumes latest version is to be used.

Client/Server should select lowest common version, if this is not possible connection should be terminated.

Request message fields:\


{% code fullWidth="false" %}
```
htspversion        u32   required   Client preferred HTSP version.
clientname         str   required   Client software name.
clientversion      str   required   Client software version.
```
{% endcode %}

Reply message fields:

```
htspversion        u32   required   The server supports all versions of the protocol up to and including this number.
servername         str   required   Server software name.
serverversion      str   required   Server software version.
servercapability   str[] required   Server capabilities (Added in version 6)
challenge          bin   required   32 bytes randomized data used to generate authentication digests
webroot            str   optional   Server HTTP webroot (Added in version 8)
                                    Note: any access to TVH webserver should include this at start of URL path
```

Note: possible values for servercapability\[]:\


{% code fullWidth="false" %}
```
cwc                Descrambling available
v4l                Analogue TV available
linuxdvb           Linux DVB API available
imagecache         Image caching available
timeshift          Timeshifting available (Added in version 9).
```
{% endcode %}

### authenticate

This can be used to issue authentication without doing anything else.\
If no privileges are gained it will return with 'noaccess' set to 1.

Request message fields:\


```
None   
```

Reply message fields:\


{% code fullWidth="false" %}
```
noaccess           u32   optional   If set to 1, no privileges were granted.
```
{% endcode %}

***

### api

(Added in version 24)

This is a proxy to HTTP API.

Request message fields:\


{% code fullWidth="false" %}
```
args               msg[] optional   HTTP arguments
path               str   required   HTTP path
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
response           msg[] required   Structured response (like in JSON HTTP replies)
```
{% endcode %}

**Note:** To execute the HTTP API command `http://TVH:9981/api/channel/grid` set the `path` to `channel/grid`.  A string containing the raw JSON response will be returned.

Also see: [JSON API](../json-api/).

***

### getDiskSpace

(Added in version 3)

Return diskspace status from Tvheadend's PVR storage

Request message fields:\


```
None
```

Reply message fields:\


{% code fullWidth="false" %}
```
freediskspace      s64   required   Bytes available.
totaldiskspace     s64   required   Total capacity.
```
{% endcode %}

Also see: [JSON API 'comet/poll'](../json-api/other-functions.md).

### getSysTime

(Added in version 3)

Return system time on the server.

Request message fields:\


```
None
```

Reply message fields:\


{% code fullWidth="false" %}
```
time               s64  required   UNIX time.
timezone           s32  required   Hours west of GMT. (deprecated, does not work reliable, use gmtoffset instead)
gmtoffset          s32  optional   Minutes east of GMT.
```
{% endcode %}

***

### enableAsyncMetadata

When this is enabled the client will get continuous updates from the server about added, update or deleted channels, tags, dvr and epg entries.

An interactive application that presents the user with information about these things should probably enable this and the implement the various server to client methods.

Request message fields:\


{% code fullWidth="false" %}
```
epg                u32   optional   Set to 1, to include EPG data in async, implied by epgMaxTime (Added in version 6).
lastUpdate         s64   optional   Only provide metadata that has changed since this time (Added in version 6).
epgMaxTime         s64   optional   Maximum time to return EPG data up to (Added in version 6)
language           str   optional   RFC 2616 compatible language list (Added in version 6)
```
{% endcode %}

Reply message fields:\


```
None
```

Once the reply as been sent the initial data set will be provided, and then updates will arrive asynchronously after that. The initial data dump is sent using the following messages:

{% code fullWidth="false" %}
```
tagAdd                   optional
channelAdd               optional
tagUpdate                optional
dvrEntryAdd              optional
eventAdd                 optional   (Added in version 6)
initialSyncComplete      required
```
{% endcode %}

***

### getChannel

(Added in version 14)

Request information about the given channel.

Request message fields:\


{% code fullWidth="false" %}
```
channelId          u32   required   Channel ID.
```
{% endcode %}

Reply message fields:\


```
see channelAdd
```

Also see: [JSON API Channel](../json-api/api-description/channel.md)

***

### getEvent

Request information about the given event. An event typically corresponds to a program on a channel.

The language field in the request allows preference for languages to be requested for the various string fields.

Request message fields:\


{% code fullWidth="false" %}
```
eventId            u32   required   Event ID.
language           str   optional   RFC 2616 compatible language list (Added in version 6)
```
{% endcode %}

Reply message fields:\


```
see eventAdd
```

Also see: [JSON API EPG](../json-api/api-description/epg.md)

### getEvents

(Added in version 4)

Request information about a set of events. If no options are specified the entire EPG database will be returned.

Request message fields:\


{% code fullWidth="false" %}
```
eventId            u32   optional   Event ID to begin from (Optional since version 6)
channelId          u32   optional   Channel ID to get data for (Added in version 6)
numFollowing       u32   optional   Number of events to add (Optional since version 6)
maxTime            u64   optional   Maximum time to return data up to (Added in version 6)
language           str   optional   RFC 2616 compatible language list (Added in version 6)
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
events             msg[] required   List of events, using response message fields from eventAdd
```
{% endcode %}

### epgQuery

(Added in version 4)

Query the EPG (event titles) and optionally restrict to channel/tag/content type.

Request message fields:\


{% code fullWidth="false" %}
```
query              str   required  Title regular expression to search for
channelId          u32   optional  [[ChannelId]] to restrict search to
tagId              u32   optional  [[TagId]] to restrict search to
contentType        u32   optional  DVB content type to restrict search to
minduration        u32   optional  Minimal duration in seconds (Added in version 13)
maxduration        u32   optional  Maximal duration in seconds (Added in version 13)
language           str   optional  RFC 2616 compatible language list for title (Added in version 6)
full               u32   optional  Output full event list rather than just IDs
```
{% endcode %}

Reply message fields:

if full == 1\


{% code fullWidth="false" %}
```
events             msg[] optional   List of events, using response message fields from eventAdd
```
{% endcode %}

else

{% code fullWidth="false" %}
```
eventIds           u32[] optional  List of eventIds that match the query
```
{% endcode %}

### getEpgObject

Get detailed EPG Object info.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required  Object ID
type               u32   optional  Object type
```
{% endcode %}

Reply message fields:

```
TODO
```

***

### getDvrConfigs

(Added in version 16)

Return a list of DVR configurations.

Reply message fields:\


{% code fullWidth="false" %}
```
dvrconfigs         msg[]      optional   Supported DVR configurations.
```
{% endcode %}

Message fields:\


{% code fullWidth="false" %}
```
uuid               str        required   DVR configuration ID
name               str        required   DVR configuration Name
comment            str        required   DVR configuration Comment
```
{% endcode %}

Also see: [JSON API DVR](../json-api/api-description/dvr.md)

### addDvrEntry

(Added in version 4)

Create a new DVR entry. Either eventId or channelId, start and stop must be specified.

Request message fields:\


{% code fullWidth="false" %}
```
eventId            u32   optional   Event ID (Optional since version 5).
channelId          u32   optional   Channel ID (Added in version 5)
start              s64   optional   Time to start recording (Added in version 5)
stop               s64   optional   Time to stop recording (Added in version 5)
retention          u32   optional   Retention time in days (Added in version 13)
creator            str   optional   Name of the event creator (Added in version 5, obsoleted in version 18 - applications are not allowed to change credential)
priority           u32   optional   Recording priority (Added in version 5)
startExtra         s64   optional   Pre-recording buffer in minutes (Added in version 5)
stopExtra          s64   optional   Post-recording buffer in minutes (Added in version 5)
title              str   optional   Recording title, if no eventId (Added in version 6)
subtitle           str   optional   Recording subtitle, if no eventId (Added in version 20)
description        str   optional   Recording description, if no eventId (Added in version 5)
configName         str   optional   DVR configuration name or UUID
enabled            u32   optional   Enabled flag (Added in version 23).
ageRating          u32   optional   Minimum age rating (Added in version 36).
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was added, 0 otherwise
id                 u32   optional   ID of created DVR entry
error              str   optional   English clear text of error message
```
{% endcode %}

### updateDvrEntry

(Added in version 5)

Update an existing DVR entry.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   DVR Entry ID
channelId          u32   optional   New channel ID (Added in version 22)
start              s64   optional   New start time
stop               s64   optional   New stop time
title              str   optional   New entry title
subtitle           str   optional   New entry subtitle (Added in version 21)
description        str   optional   New entry description (Added in version 6)
startExtra         s64   optional   New pre-record buffer (Added in version 6)
stopExtra          s64   optional   New post-record buffer (Added in version 6)
configName         str   optional   New DVR configuration name or UUID
retention          u32   optional   Retention in days (Added in version 13)
priority           u32   optional   Recording priority (Added in version 13)
enabled            u32   optional   Enabled flag (Added in version 23).
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if update as successful, otherwise 0
error              str   optional   Error message if update failed
```
{% endcode %}

### cancelDvrEntry

(Added in version 5)

Cancel an existing recording, but don't remove the entry from the database.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   dvrEnryId to delete
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            int   required   1 if entry was cancelled
error              str   optional   Error message if cancellation failed
```
{% endcode %}

### deleteDvrEntry

(Added in version 4)

Delete an existing DVR entry from the database.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   DVR Entry ID
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was removed
error              str   optional   Error message if the delete fails
```
{% endcode %}

### getDvrCutpoints

(Added in version 12)

Get DVR cutpoints.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   DVR Entry ID
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
cutpoints          msg[] optional   List of cutpoint entries, if a file is found and has some valid data.
```
{% endcode %}

Cutpoint fields:\


{% code fullWidth="false" %}
```
start              u32   required   Cut start time in ms.
end                u32   required   Cut end time in ms.
type               u32   required   Action type: 
                                      0=Cut, 1=Mute, 2=Scene, 
                                      3=Commercial break.
```
{% endcode %}

***

### addAutorecEntry

(Added in version 13)

Create a new Autorec DVR entry. Title must be specified.

Request message fields:\


{% code fullWidth="false" %}
```
enabled            u32   optional   Enabled flag (Added in version 19).
title              str   required   Title for the recordings.
fulltext           u32   optional   Full text flag (Added in version 20).
directory          str   optional   Forced directory name - missing or empty = auto (Added in version 19).
name               str   optional   Name of this autorec entry (Added in version 18).
configName         str   optional   DVR Configuration Name / UUID.
channelId          u32   optional   Channel ID.
minDuration        u32   optional   Minimal duration in seconds (0 = Any).
maxDuration        u32   optional   Maximal duration in seconds (0 = Any).
daysOfWeek         u32   optional   Bitmask - Days of week (0x01 = Monday, 0x40 = Sunday, 0x7f = Whole Week, 0 = Not set).
priority           u32   optional   Priority (0 = Important, 1 = High, 2 = Normal, 3 = Low, 4 = Unimportant, 5 = Not set).
approxTime         u32   optional   Minutes from midnight (up to 24*60) (window +- 15 mintes) (Obsoleted from version 18).
start              s32   optional   Minutes from midnight (up to 24*60) for the start of the time window (including) (Added in version 18).
startWindow        s32   optional   Minutes from modnight (up to 24*60) for the end of the time window (including, cross-noon allowed) (Added in version 18).
startExtra         s64   optional   Extra start minutes (pre-time).
stopExtra          s64   optional   Extra stop minutes (post-time).
dupDetect          u32   optional   Dup Detect (0 = all, 1 = diff episode, 2 = diff subtitle, 3 = diff description, 4 = once per week, 5 = once per day) (Added in version 20).
comment            str   optional   User Comment.
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was added, 0 otherwise
id                 str   optional   ID (string!) of created autorec DVR entry
error              str   optional   English clear text of error message
```
{% endcode %}

### deleteAutorecEntry

(Added in version 13)

Delete an existing autorec DVR entry from the database.

Request message fields:\


{% code fullWidth="false" %}
```
id                 str   required   Autorec DVR Entry ID (string!)
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was removed
error              str   optional   Error message if the delete fails
```
{% endcode %}

***

### addTimerecEntry

(Added in version 18)

Create a new Timerec DVR entry. Title must be specified.

Request message fields:\


{% code fullWidth="false" %}
```
enabled            u32   optional   Enabled flag (Added in version 19).
title              str   required   Title for the recordings.
directory          str   optional   Forced output directory name (Added in version 19).
name               str   optional   Name for this timerec entry.
configName         str   optional   DVR Configuration Name / UUID.
channelId          u32   optional   Channel ID.
daysOfWeek         u32   optional   Bitmask - Days of week (0x01 = Monday, 0x40 = Sunday, 0x7f = Whole Week, 0 = Not set).
priority           u32   optional   Priority (0 = Important, 1 = High, 2 = Normal, 3 = Low, 4 = Unimportant, 5 = Not set).
start              u32   optional   Minutes from midnight (up to 24*60) for the start of the time window (including)
stop               u32   optional   Minutes from modnight (up to 24*60) for the end of the time window (including, cross-noon allowed)
retention          u32   optional   Retention in days. 
comment            str   optional   User Comment.
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was added, 0 otherwise
id                 str   optional   ID (string!) of created timerec DVR entry
error              str   optional   English clear text of error message
```
{% endcode %}

### deleteTimerecEntry

(Added in version 18)

Delete an existing timerec DVR entry from the database.

Request message fields:\


{% code fullWidth="false" %}
```
id                 str   required   Timerec DVR Entry ID (string!)
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
success            u32   required   1 if entry was removed
error              str   optional   Error message if the delete fails
```
{% endcode %}

***

### getTicket

(Added in version 5)

Get a ticket to allow access to a channel or recording via HTTP

Request message fields:\


{% code fullWidth="false" %}
```
channelId          u32  optional   Channel to gain access for
dvrId              u32  optional   DVR file to gain access for
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
path               str  required   The full path for access URL (no scheme, host or port)
ticket             str  required   The ticket to pass in the URL query string
```
{% endcode %}

### subscribe

Request subscription to the given channel.

Request message fields:\


{% code fullWidth="false" %}
```
channelId          u32   required   ID for channel. 
subscriptionId     u32   required   Subscription ID. Selected by client. This value is not interpreted by the server in any form. 
                                    The value is used from now on in all messages related to the subscription.
weight             u32   optional   Weighting of this subscription (same as recording priority).
90khz              u32   optional   Request PTS/DTS in default 90kHz timebase, default is 1MHz (Added in version 7)
normts             u32   optional   Request PTS/DTS normalisation (Added in version 7)
                                    Note: this will mean missing timestamps are added, first packet should be ~0 and will always be an i-frame.
                                    Note: this is implied if timeshiftPeriod is enabled
                                    Note: from version 17, this is always enabled and this parameter is ignored.
queueDepth         u32   optional   Change the default packet queue lengths, default 500000 bytes (Added in version 7)
                                    Note: I-frame depth is 3*queueDepth, P-frame is 2*queueDepth and B-frame is queueDepth
timeshiftPeriod    u32   optional   The number of seconds to keep in the timeshift buffer (Added in version 9)
                                    Note: this may be bounded by server configuration settings
profile            str   optional   Select stream profile (Added in version 16).
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
90khz              u32   optional   Indicates 90khz timestamps will be used
normts             u32   optional   Indicates timestamps will be normalised (and fixed)
timeshiftPeriod    u32   optional   The actual timeshiftPeriod to be used
```
{% endcode %}

### unsubscribe

Stop a subscription.

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32   required   Subscription ID.
```
{% endcode %}

Reply message fields:\


```
None
```

### subscriptionChangeWeight

(Added in version 5)

Change the weight of an existing subscription

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32   required   Subscription ID.
weight             u32   optional   The new subscription weight.
```
{% endcode %}

Reply message fields:\


```
None
```

### subscriptionSkip

(Added in version 9)

Skip a timeshift enabled subscription. The response will be asynchronous subscriptionSkip().

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32   required   Subscription ID.
absolute           u32   optional   The skip request is absolute
time               u64   optional   Specify skip using time (units are as for PTS)
size               u64   optional   Specify skip using size (Not currently used)
```
{% endcode %}

Reply message fields:\


```
None
```

### subscriptionSeek

(Added in version 9)

Synonym for subscriptionSkip

### subscriptionSpeed

(Added in version 9)

Set the playback speed for the subscription. The response will be asynchronous subscriptionSpeed().

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32   required   Subscription ID.
speed              u32   required   Specify speed (0=pause, 100=1x fwd, -100=1x backward)
```
{% endcode %}

Reply message fields:\


```
None
```

### subscriptionLive

(Added in version 9)

Return a timeshifted session to live. Reply will be asynchronous subscriptionSkip().

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32   required   Subscription ID.
```
{% endcode %}

Reply message fields:\


```
None
```

### subscriptionFilterStream

(Added in version 12)

Enable or disable specified streams by index.

Request message fields:\


{% code fullWidth="false" %}
```
subscriptionId     u32        required   Subscription ID.
enable             list[u32]  optional   Enable stream indexes
disable            list[u32]  optional   Disable (filter out) stream indexes
```
{% endcode %}

Reply message fields:\


```
None
```

***

### getProfiles

(Added in version 16)

Return a list of stream profiles (configurations).

Reply message fields:\


{% code fullWidth="false" %}
```
profiles           msg[]      optional   Supported profiles
```
{% endcode %}

Message fields:\


{% code fullWidth="false" %}
```
uuid               str        required   Profile ID
name               str        required   Profile Name
comment            str        required   Profile Comment
```
{% endcode %}

### getCodecs

(Added in version 11, Removed in version 16)

Return a list of encoders (codecs).

Reply message fields:\


{% code fullWidth="false" %}
```
encoders           list[str]  optional   Supported encoders
```
{% endcode %}

### fileOpen

(Added in version 8)

Open a file within the Tvheadend file system. This is now the preferred method (in place of HTTP) for accessing recordings.

Accessing recordings via HTSP will overcome the limitations of standard HTTP streaming which cannot handle both skipping and growing files (i.e. in-progress recordings) at the same time.

Request message fields:\


{% code fullWidth="false" %}
```
file               str   required   File path to open
```
{% endcode %}

Valid file paths:\


{% code fullWidth="false" %}
```
/dvrfile/ID        will open the file associated with DVR entry ID
/imagecache/ID     will open the file associated with imagecache entry ID (Note: only works for HTSPv10+)
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   The file handle used for further file operations
size               u64   optional   The size of the file in bytes
mtime              u64   optional   The last time the file was modified
```
{% endcode %}

### fileRead

(Added in version 8)

Read data from a file.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   The file handle used for further file operations
size               u64   required   The amount of data to read
offset             u64   optional   Offset into the file to read (default is current position)
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
data               bin   required   The data read from the file (size may be less than requested)
```
{% endcode %}

### fileClose

(Added in version 8)

Close an opened file.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   The file handle to be closed
```
{% endcode %}

Reply message fields:\


```
None
```

### fileStat

(Added in version 8)

Get status of a file.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   The file handle to be stat'd
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
size               u64   optional   The size of the file in bytes
mtime              u64   optional   The last time the file was modified
```
{% endcode %}

### fileSeek

(Added in version 8)

Seek to position in a file.

Request message fields:\


{% code fullWidth="false" %}
```
id                 u32   required   The file handle to be stat'd
offset             u64   required   The position to seek in the file
whence             str   required   Where to seek relative to (default=SEEK_SET)
```
{% endcode %}

Note: valid values for whence\


{% code fullWidth="false" %}
```
SEEK_SET           Seek relative to start of file
SEEK_CUR           Seek relative to current position in file
SEEK_END           Seek relative (backwards) to end of file
```
{% endcode %}

Reply message fields:\


{% code fullWidth="false" %}
```
offset             u64   optional   The new absolute position within the file
```
{% endcode %}
