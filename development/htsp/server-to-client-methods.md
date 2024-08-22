# Server to Client methods

### channelAdd

A new channel has been created on the server.

Message fields:\


```
channelId          u32   required   ID of channel.
channelNumber      u32   required   Channel number, 0 means unconfigured.
channelNumberMinor u32   optional   Minor channel number (Added in version 13).
channelName        str   required   Name of channel.
channelIcon        str   optional   URL to an icon representative for the channel
                                    (For v8+ clients this could be a relative /imagecache/ID URL
                                     intended to be fed to fileOpen() or HTTP server)
                                    (For v15+ clients this could be a relative imagecache/ID URL
                                     intended to be fed to fileOpen() or HTTP server)
eventId            u32   optional   ID of the current event on this channel.
nextEventId        u32   optional   ID of the next event on the channel.
tags               u32[] optional   Tags this channel is mapped to.
services           msg[] optional   List of available services (Added in version 5)
```

Service fields:\


```
name               str   required   Service name
type               str   required   Service type
caid               u32   optional   Encryption CA ID
caname             str   optional   Encryption CA name
providername       str   optional   Service provider (Added in version 38)
```

### channelUpdate

Same as channelAdd, but all fields (except channelId) are optional.

### channelDelete

A channel has been deleted on the server.

Message fields:\


```
channelId          u32   required   ID of channel.
```

***

### tagAdd

A new tag has been created on the server.

Message fields:\


```
tagId              u32   required   ID of tag.
tagName            str   required   Name of tag.
tagIndex           u32   optional   Index value for sorting (default by from min to max) (Added in version 18).
tagIcon            str   optional   URL to an icon representative for the channel.
tagTitledIcon      u32   optional   Icon includes a title
members            u32[] optional   Channel IDs of those that belong to the tag
```

### tagUpdate

Same as tagAdd, but all fields (except tagId) are optional.

### tagDelete

A tag has been deleted from the server.

Message fields:\


```
tagId              u32   required   ID of tag.
```

***

### dvrEntryAdd

(Added in version 4)

A new recording has been created on the server.

Message fields:\


```
id                 u32   required   ID of dvrEntry.
channel            u32   optional   Channel of dvrEntry.
start              s64   required   Time of when this entry was scheduled to start recording.
stop               s64   required   Time of when this entry was scheduled to stop recording.
startExtra         s64   required   Extra start time (pre-time) in minutes (Added in version 13).
stopExtra          s64   required   Extra stop time (post-time) in minutes (Added in version 13).
retention          s64   required   DVR Entry retention time in days (Added in version 13).
priority           u32   required   Priority (0 = Important, 1 = High, 2 = Normal, 3 = Low, 4 = Unimportant, 5 = Not set) (Added in version 13).
eventId            u32   optional   Associated EPG Event ID (Added in version 13).
autorecId          str   optional   Associated Autorec UUID (Added in version 13).
timerecId          str   optional   Associated Timerec UUID (Added in version 18).
contentType        u32   optional   Content Type (like in the DVB standard) (Added in version 13).
title              str   optional   Title of recording
subtitle           str   optional   Subtitle of recording (Added in version 20).
summary            str   optional   Short description of the recording (Added in version 6).
description        str   optional   Long description of the recording.
state              str   required   Recording state
error              str   optional   Plain english error description (e.g. "Aborted by user").
owner              str   optional   Name of the entry owner (Added in version 18).
creator            str   optional   Name of the entry creator (Added in version 18).
subscriptionError  str   optional   Subscription error string (Added in version 20).
streamErrors       str   optional   Number of recording errors (Added in version 20).
dataErrors         str   optional   Number of stream data errors (Added in version 20).
path               str   optional   Recording path for playback.
files              msg   optional   All recorded files for playback (Added in version 21).
dataSize           s64   optional   Actual file size of the last recordings (Added in version 21).
enabled            u32   optional   Enabled flag (Added in version 23).
ageRating          u32   optional   Minimum age rating (Added in version 36).
ratingLabel        str   optional   Parental rating label text (Added in version 37).
ratingIcon         str   optional   Parental rating label icon (Added in version 37).
```

Valid values for state:\


```
TODO
```

Valid values for subscriptionError:\


```
noFreeAdapter            No free adapter for this service.
scrambled                Service is scrambled.
badSignal                Bad signal status.
tuningFailed             Tuning of this service failed.
subscriptionOverridden   Subscription overridden by another one.
muxNotEnabled            No mux enabled for this service.
invalidTarget            Recording/livestream cannot be saved to filesystem or recording/streaming configuration is incorrect.
userAccess               User does not have access rights for this service.
userLimit                Maximum number of streaming connections set in user's profile reached.
```

### dvrEntryUpdate

Message fields:\


```
Same as dvrEntryAdd, but all fields (except id) are optional.
```

### dvrEntryDelete

(Added in version 4)

A recording has been deleted from the server.

Message fields:\


```
id                 u32   required   ID of recording to delete.
```

***

### autorecEntryAdd

(Added in version 13)

A new autorec recording has been created on the server.

Message fields:\


```
id                 str   required   ID (string!) of dvrAutorecEntry.
enabled            u32   required   If autorec entry is enabled (activated).
name               str   required   Name of the autorec entry (Added in version 18).
minDuration        u32   required   Minimal duration in seconds (0 = Any).
maxDuration        u32   required   Maximal duration in seconds (0 = Any).
retention          u32   required   Retention time (in days).
daysOfWeek         u32   required   Bitmask - Days of week (0x01 = Monday, 0x40 = Sunday, 0x7f = Whole Week, 0 = Not set).
priority           u32   required   Priority (0 = Important, 1 = High, 2 = Normal, 3 = Low, 4 = Unimportant, 5 = Not set).
approxTime         u32   required   Minutes from midnight (up to 24*60).
start              s32   required   Exact start time (minutes from midnight) (Added in version 18).
startWindow        s32   required   Exact stop time (minutes from midnight) (Added in version 18).
startExtra         s64   required   Extra start minutes (pre-time).
stopExtra          s64   required   Extra stop minutes (post-time).
title              str   optional   Title.
fulltext           u32   optional   Fulltext flag (Added in version 20).
directory          str   optional   Forced directory name (Added in version 19).
channel            u32   optional   Channel ID.
owner              str   optional   Owner of this autorec entry (Added in version 18).
creator            str   optional   Creator of this autorec entry (Added in version 18).
dupDetect          u32   optional   Duplicate detection (see addAutorecEntry) (Added in version 20).
```

### autorecEntryUpdate

(Added in version 13)

Message fields:\


```
Same as autorecEntryAdd but all fields (except id) are optional.
```

#### autorecEntryDelete (Added in version 13)

Message fields:\


```
id                 str   required   Autorec Entry ID (string!)
```

***

### timerecEntryAdd

(Added in version 18)

A new autorec recording has been created on the server.

Message fields:\


```
title              str   required   Title for the recordings.
directory          str   optional   Forced directory name (Added in version 19).
enabled            u32   required   Title for the recordings.
name               str   required   Name for this timerec entry.
configName         str   required   DVR Configuration Name / UUID.
channel            u32   required   Channel ID.
daysOfWeek         u32   optional   Bitmask - Days of week (0x01 = Monday, 0x40 = Sunday, 0x7f = Whole Week, 0 = Not set).
priority           u32   optional   Priority (0 = Important, 1 = High, 2 = Normal, 3 = Low, 4 = Unimportant, 5 = Not set).
start              u32   required   Minutes from midnight (up to 24*60) for the start of the time window (including)
stop               u32   required   Minutes from modnight (up to 24*60) for the end of the time window (including, cross-noon allowed)
retention          u32   optional   Retention in days.
owner              str   optional   Owner of this timerec entry.
creator            str   optional   Creator of this timerec entry.
```

### timerecEntryUpdate

(Added in version 18)

Message fields:\


```
Same as timerecEntryAdd but all fields (except id) are optional.
```

### timerecEntryDelete

(Added in version 18)

Message fields:\


```
id                 str   required   Timerec Entry ID (string!)
```

***

### eventAdd

(Added in version 6)

Message fields:\


```
eventId            u32   required   Event ID
channelId          u32   required   The channel this event is related to.
start              u64   required   Start time of event, UNIX time.
stop               u64   required   Ending time of event, UNIX time.
title              str   optional   Title of event.
summary            str   optional   Short description of the event (Added in version 6).
description        str   optional   Long description of the event.
serieslinkId       u32   optional   Series Link ID (Added in version 6).
episodeId          u32   optional   Episode ID (Added in version 6).
seasonId           u32   optional   Season ID (Added in version 6).
brandId            u32   optional   Brand ID (Added in version 6).
contentType        u32   optional   DVB content code (Added in version 4, Modified in version 6*).
ageRating          u32   optional   Minimum age rating (Added in version 6).
starRating         u32   optional   Star rating (1-5) (Added in version 6).
firstAired         s64   optional   Original broadcast time, UNIX time (Added in version 6).
seasonNumber       u32   optional   Season number (Added in version 6).
seasonCount        u32   optional   Show season count (Added in version 6).
episodeNumber      u32   optional   Episode number (Added in version 6).
episodeCount       u32   optional   Season episode count (Added in version 6).
partNumber         u32   optional   Multi-part episode part number (Added in version 6).
partCount          u32   optional   Multi-part episode part count (Added in version 6).
episodeOnscreen    str   optional   Textual representation of episode number (Added in version 6).
image              str   optional   URL to a still capture from the episode (Added in version 6).
dvrId              u32   optional   ID of a recording (Added in version 5).
nextEventId        u32   optional   ID of next event on the same channel.
ratingLabel        str   optional   Parental rating label text (Added in version 37).
ratingIcon         str   optional   Parental rating label icon (Added in version 37).
```

* \*contentType previously had the major DVB category in the bottom 4 bits,\
  however in v6 this has been changed to properly match DVB, so top 4 bits\
  as major category and bottom 4 bits has sub-category. Clients requesting\
  v5 or lower will get the old output.

### eventUpdate

(Added in version 6)

Message fields:\


```
Same as eventAdd but all fields (except eventId) are optional.
```

### eventDelete

(Added in version 6)

Message fields:\


```
eventId            u32   required   Event ID
```

***

### initialSyncCompleted

(Added in version 2)

Sent after all the initial metadata has been sent when session has been set to async mode.

Message fields:\


```
```

***

### subscriptionStart

Asynchronous message output when a new subscription is successfully started.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
streams            msg[] required   Array of messages with stream information
sourceinfo         msg   optional   Source information.
```

Stream message fields:\


```
index              u32   required   Index for this stream
type               str   required   Type of stream
meta               bin   optional   Codec metadata (private data, libav - extradata) (Added in version 17)
language           str   optional   Language for stream
Video components only:
width              u32   optional   Width of video in pixels
height             u32   optional   Height of video in pixels
aspect_num         u32   optional   Aspect ratio numerator (Added in version 5) *Can be incorrect and should not be relied upon*
aspect_den         u32   optional   Aspect ratio denonminator (Added in version 5) *Can be incorrect and should not be relied upon*
Audio components only:
audio_type         u32   optional   Audio type - 0=Normal; 1=Clean effects; 2=Hearing impaired; 3=Visually impaired commentary; 4-255=Reserved (Added in version 11)
channels           u32   optional   Number of audio channels (Added in version 5)
rate               u32   optional   Audio bitrate (Added in version 5)
Subtitle components only:
composition_id     u32   optional   ??? (Added in version 5)
ancillary_id       u32   optional   ??? (Added in version 5)
```

Sourceinfo message fields:\


```
adapter            str   optional   Adapter name
mux                str   optional   Transponder name
network            str   optional   Network name
provider           str   optional   Provide name (like 'Sky UK')
service            str   optional   Service name
satpos             str   optional   Satellite position name (Added in version 20).
```

Video Stream types:\


```
MPEG2VIDEO                    MPEG2 video, meta field is present (configuration blocks)
H264                          H264 video, meta field is present (configuration blocks)
HEVC                          HEVC video, meta field is present (configuration blocks)
```

Audio Stream types:\


```
MPEG2AUDIO                    MPEG2 audio (MP2)
AC3                           AC3 audio
AAC                           ADTS framed AAC (one AAC packet per ADTS frame), meta field is present (MPEG4 config)
EAC3                          Enhanced AC3 audio
VORBIS                        Vorbis audio, meta field is present with the main vorbis header
```

Subtitle Stream types:\


```
TELETEXT                      ???
DVBSUB                        ???
```

### subscriptionGrace

Notifies client about the grace timeout (timeout for stream activation). It can be issues multiple times.\
For example a configuration with satellite rotors requires more than 120 seconds to tune, so users\
should be notified..

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
graceTimeout       u32   required   Grace timeout in seconds.
```

### subscriptionStop

A subscription has been stopped.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
status             str   optional   Error message if subscription stopped unexpectedly.
subscriptionError  str   optional   Subscription error code (Added in version 20).
```

Valid values for subscriptionError:\


```
see dvrEntryAdd
```

### subscriptionSkip

(Added in version 9)

A subscription has been skipped.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
error              u32   optional   The last skip command caused an error.
absolute           u32   optional   Indicates the output is absolute (Note: should always be 1 at the moment)
time               u64   optional   The time the subscription has skipped to.
size               u64   optional   The position in the file we've skipped to (Note: not currently used).
```

### subscriptionSpeed

(Added in version 9)

A subscription's playback speed has changed.

This can happen even without a speed request, should playback reach either end of the buffer.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
speed              u32   required   The new speed of the subscription
```

### subscriptionStatus

Subscription status update.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
status             str   optional   English clear text of error status. Absence of this field means that the status is OK. 
subscriptionError  str   optional   Subscription error code (Added in version 20).
```

Valid values for subscriptionError:\


```
see dvrEntryAdd
```

### queueStatus

The queueStatus message is sent every second during normal data delivery.

The transmit scheduler have different drop thresholds for different frame types.

If congestion occurs it will favor dropping B-frames before P-frames before I-frames.\
All audio is recognized as I-frames.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
packets            u32   required   Number of data packets in queue.
bytes              u32   required   Number of bytes in queue.
delay              u32   optional   Estimated delay of queue (in µs).
Bdrops             u32   required   Number of B-frames dropped
Pdrops             u32   required   Number of P-frames dropped
Idrops             u32   required   Number of I-frames dropped
delay              s64   required   Delta between first and last DTS (Added in version 9)
```

### signalStatus

The signalStatus message is sent every second during normal data delivery.

The optional fields may not have been implemented or may not be supported by the active adapter.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
feStatus           str   required   Frontend status.
feSNR              u32   optional   Signal to noise ratio.
feSignal           u32   optional   Signal status percentage.
feBER              u32   optional   Bit error rate.
feUNC              u32   optional   Uncorrected blocks.
```

### timeshiftStatus

Provide status every second about the timeshift buffer.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
full               u32   required   Indicates whether the buffer is full
shift              s64   required   Current position relative to live
start              s64   optional   PTS of the first frame in the buffer
end                s64   optional   PTS of the last frame in the buffer
```

### muxpkt

Streaming data.

Message fields:\


```
subscriptionId     u32   required   Subscription ID.
frametype          u32   required   Type of frame as ASCII value: 'I', 'P', 'B'
stream             u32   required   Stream index. Corresponds to the streams reported in the subscriptionStart message.
dts                s64   optional   Decode Time Stamp in µs.
pts                s64   optional   Presentation Time Stamp in µs.
duration           u32   required   Duration of frame in µs.
payload            bin   required   Actual frame data.
```
