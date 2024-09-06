# Protocol Changes

#### This information may be outdated. If you have some spare time, please to through the commit History and add the changes to the documentation.

#### v42

* added comment field to addDvrEntry, updateDvrEntry, autorecEntryAdd, autorecEntryUpdate, timerecEntryAdd, timerecEntryUpdate&#x20;

#### v41

* added full UUID to channelAdd, tagAdd and dvrEntryAdd
* added ratingAuthority and ratingCountry to dvrEntryAdd and eventAdd

#### v40

* added DVR configuration UUID to dvrEntryAdd, dvrEntryUpdate, autorecEntryAdd, autorecEntryUpdate, timerecEntryAdd, timerecEntryUpdate

#### v39

* added broadcast type to autorec DVR entry

#### v38

* added service provider name to channelAdd -> services

#### v37

* added ratingLabel to EPG & DVR entries
* added ratingIcon to EPG & DVR entries

#### v36

* added ageRating to DVR entries

#### v26..35

TODO

#### v25

* added updateAutorecEntry and updateTimerecEntry
* (and other changes not yet documented here)

#### v23..24

* added descrambleInfo (not yet documented here)

#### v22..23

* extended addDvrEntry, updateDvrEntry, dvrEntryAdd method
  * added enabled
* extended getSysTime
  * added gmtoffset

#### v21..22

* extended updateDvrEntry method
  * added channelId

#### v20..v21

* dvrEntry structures
  * added files msg (multiple files) to the files field
  * added dataSize field to show actual (last) file size in dvrEntry updates
* epg events - added subtitle field

#### v19..v20

* dvrEntry structures
  * added subscriptionError, streamErrors, dataErrors fields
  * added subtitle fields
* autorecEntry structures
  * added dupDetect and fulltext fields
* added errors fields to the stream status
* added satpos to the subscription start
* added subscriptionError field to subscriptionStatus server-to-client method

#### v18..v19

* autorec/timerec structures
  * added directory field (forced output directory)
  * added enabled field

#### v17..v18

* added addTimerecEntry, deleteTimerecEntry methods
* added timerecEntryAdd, timerecEntryUpdate, timerecEntryDelete server-to-client methods
* extended addAutorecEntry method
  * added start/startWindow/name fields
  * added owner/creator fields
  * obsoleted creator field
* extended dvrEntryAdd, dvrEntryUpdate
  * added timerecId field
  * added owner/creator fields
* extended addAutorecEntry, deleteAutorecEntry methods
  * added start/startWindow fields
  * obsoleted approxTime
  * added name/owner/creator fields
* extended autorecEntryAdd, autorecEntryUpdate server-to-client methods
  * fields like for addAutorecEntry
* extended getTag method
  * added tagIndex field

#### v16..v17

* extended subscriptionStart server-to-client method
  * added meta field
* changed H264 meta data handling (codec meta data are in the meta field only in start message)
* VORBIS and AAC codecs have codec specific meta data in the meta field in start message
* changed subscribe method
  * the normts is always active and the parameter is ignored

#### v15..v16

* added getProfiles, getDvrConfigs methods
* removed getCodecs methods
* extended subscribe method
  * add profile field

#### v14..v15

* extended channelAdd, channelUpdate server-to-client methods
  * the channelIcon URL can be relative 'imagecache/%d' or '/imagecache/%d'
* extended getChannel method
  * the channelIcon URL can be relative 'imagecache/%d' or '/imagecache/%d'

#### v13..v14

* added getChannel method

#### v12..v13

* added addAutorecEntry method
* added deleteAutorecEntry method
* added autorecEntryAdd, autorecEntryUpdate, autorecEntryDelete server-to-client methods
* extended channelAdd server-to-client method
  * added channelNumberMinor (for {major}.{minor} channel numbers)
* extended dvrEntryAdd and dvrEntryUpdate server-to-client methods
  * added eventId, autorecId, startExtra, stopExtra, retention, priority, contentType fields
* extended addDvrEntry method
  * added retention
* extended updateDvrEntry method
  * added retention, priority
* extended epgQuery method
  * added minduration, maxduration
* added subscriptionGrace server-to-client method

#### v11..v12

* added subscriptionFilterStream method
* added getDvrCutpoints method

#### v10..v11

* added audio\_type in the subscriptionStart server-to-client method
* added getCodecs method

