# EPG

Functions to query the Electronic Program(me) Guide.

### epg/events/grid

Query the EPG and optionally apply filters.

* `lang` 3-letter ISO639 language code. If not supplied, the language configured for the user is entered; otherwise the system default.
* `mode` If set to the string `now` then only events currently playing are listed.
* `title` A (case-insensitive) string which must appear in the title to be listed.
* `fulltext` If set to 1 then the `title` string must match exactly. Default is 0.
* `channel` The channel to show events from, specified either by channel name or uuid. Must be an exact match to the data from [channel/list](channel.md#channel-list), otherwise all channels are returned.
* `channelTag` The (single) channel tag to show events from, specified either by name or uuid. Must be an exact match to the data from [channeltag/list](channel.md#channeltag-list), otherwise all tags are returned.
* `durationMin` Shortest event to be listed (seconds).
* `durationMax` Longest event to be listed (seconds).
* `contentType` Integer representing the genre to be listed - see [epg/content\_type/list](epg.md#epg-content_type-list).
* `filter` A JSON object describing the filter(s) to be applied. See [Grid Filters](common-parameters.md#grid-filters) for the syntax. String filters can only be applied to the 'channelName', 'title', 'subtitle', 'summary', 'description' and 'extraText' fields.
* `sort` The key to be sorted by. Default is to sort by 'start'.
* `dir` If `sort` is specified, setting 'dir' to 'desc' reverses the sort order
* `start` First record to be listed from the database, default is 0.
* `limit` Number of records to list. **Default is 50** - use a very large number to get all.
* `new` If set to 1 then only events marked as 'new' will be included. Default is 0. The EPG source must identify 'new' events for this filter to work.
* `cat1, cat2, cat3` XMLTV provides more details of the event category than the OTA EPG, and these parameters can be used to filter by XMLTV category. See [Channel-Category](channel.md#channelcategory-list).

EPG sources differ in the information which they provide, and there are many more information items possible than are included in the example below. Any items which have no data available will be omitted.

```
{
   "totalCount" : 18575,
   "entries" : [
      {
         "eventId": 5229882,
         "episodeUri": "crid://www.itv.com/1002485413",
         "serieslinkUri": "crid://www.itv.com/ebshd48582",
         "channelName": "ITV HD",
         "channelUuid": "fd22bbade9093bd1fedf6ce87d75f9a0",
         "channelNumber": "3",
         "start": 1747148400,
         "stop": 1747152000,
         "title": "Tipping Point",
         "summary": "Ben Shephard hosts the quiz show in which three players take on an extraordinary machine in the hope of winning a cash jackpot. [S,HD]",
         "widescreen": 1,
         "subtitled": 1,
         "hd": 1,
         "genre": [
           48
         ],
         "nextEventId": 5229883
         "ageRating" : 9,
         "ratingLabel" : "PG,
         "ratingLabelIcon" : "imagecache/37"
      }, ...
   ]
}
```

If the event is scheduled to be recorded, these extra items will appear:

```
      "dvrUuid": "f01433995f76d60f3b32d38fb18f541a",
      "dvrState": "scheduled",
```

Other possible values for `dvrState` are "recording", "completed", "completedError", "completedWarning" and "completedRerecord". The 'completed' values can only be present if the recording stopped before the scheduled stop time.

### epg/events/alternative

Lists alternative broadcasts of the same event.

* `eventId` Identifier of the event, eg taken from [epg/events/grid](epg.md#epg-events-grid).
* `lang` 3-letter ISO639 language code. If not supplied, the language configured for the user is entered; otherwise the system default.

The function looks for broadcasts having the same eventId, rather than using event CRIDs. It does not work on UK DVB-T.

This function does not work on TVH versions older than 4.2.4-5 or 4.3-589.

### epg/events/related

Lists broadcasts related to the given event.

* `eventId` Identifier of the event, eg taken from [epg/events/grid](epg.md#epg-events-grid).
* `lang` 3-letter ISO639 language code. If not supplied, the language configured for the user is entered; otherwise the system default.

The function looks for events having the same series link ID as the given event, ie part of the same series of broadcasts. It therefore relies on the EPG provider filling in these details.

Note that the series link ID is unique to an individual set of broadcasts; if the series is repeated on a different channel (or at a different time) the series link will be different.

This function does not work on TVH versions older than 4.2.4-5 or 4.3-589.

From version 4.3.1711, if the given event does not have a series link ID, events in the EPG having the same title are returned.

### epg/events/load

Lists details of specific event(s).

* `eventId` Identifier of the event, or a JSON array of event Ids.

The common parameters which apply to other 'load' functions do not work here.

```
{
   "entries" : [
      {
         "eventId": 5229882,
         "episodeUri": "crid://www.itv.com/1002485413",
         "serieslinkUri": "crid://www.itv.com/ebshd48582",
         "channelName": "ITV HD",
         "channelUuid": "fd22bbade9093bd1fedf6ce87d75f9a0",
         "channelNumber": "3",
         "start": 1747148400,
         "stop": 1747152000,
         "title": "Tipping Point",
         "summary": "Ben Shephard hosts the quiz show in which three players take on an extraordinary machine in the hope of winning a cash jackpot. [S,HD]",
         "widescreen": 1,
         "subtitled": 1,
         "hd": 1,
         "genre": [
           48
         ],
         "nextEventId": 5229883
         "ageRating" : 9,
         "ratingLabel" : "PG,
         "ratingLabelIcon" : "imagecache/37"
      }
   ],
   "totalCount" : 1
}

```

### epg/brand/list

A 'Brand' is a commonly-available show, eg "Simpsons". What constitutes a 'Brand' is up to the EPG provider.

**This function was removed in version 4.3.1059.**

### epg/content\_type/list

Lists the Content Type IDs extracted from ETSI EN 300 468 together with their descriptions. The Content Type ID appears in the output of [epg/events/grid](epg.md#epg-events-grid) as "Genre". IDs described as 'Reserved' or 'User Defined' in the specification are given the description of the previous ID instead.

* `full` If set to 0 (the default) only the broad categories defined by `content_nibble_level_1` in the specification are listed. If set to 1 all categories are listed.

```
{
   "entries" : [
      {
         "val" : "",
         "key" : 0
      },
      {
         "val" : "Movie / Drama",
         "key" : 16
      },
      {
         "key" : 17,
         "val" : "Detective / Thriller"
      }, ...
   ]
}
```
