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

# Episode Numbering

TVH accepts three episode numbering schemes via XMLTV.

* onscreen
* dd\_progid
* xmltv\_ns

```xml
<episode-num system="onscreen">S01E01</episode-num>
```

Set the 'episodeOnscreen' property of the EPG event to the value provided. TVH treats this value as free-form plain-text and no additional series or episode parsing is performed.

**Note:** If an 'episode-num' tag exists with a 'system' attribute set to 'onscreen', the tag's value will override the EPG event's 'episodeOnscreen' property regardless of the series or episode numbers parsed from other 'episode-num' tags. However, the other properties, for example 'seasonNumber' are set correctly. The 'onscreen' override occurs regardless of the sequence of the 'episode-num' tags.

```xml
<episode-num system="dd_progid">SH00012345.0000</episode-num>
```

Set the 'serieslinkUri' property to "ddprogid://xmltv/SH00012345.0000". No additional series or episode parsing is performed.

```xml
<episode-num system="dd_progid">EP00012345.0001</episode-num>
```

Set the 'episodeUri' property to "ddprogid://xmltv/EP00012345.0001". Set the 'serieslinkUri' property to "ddprogid://xmltv/EP00012345". Set the 'episodeNumber' property to 1. Set the 'episodeOnscreen' property to "e01".

```xml
<episode-num system="xmltv_ns">1/16.3/25.1/2</episode-num>
```

Set the 'seasonNumber' property to 2.\
Set the 'seasonCount' property to 16.\
Set the 'episodeNumber' property to 4.\
Set the 'episodeCount' property to 25.\
Set the 'partNumber' property to 2.\
Set the 'partCount' property to 2.\
Set the 'episodeOnscreen' property to "s02.e04".

**Note:** In a number pair separated by a slash, the first number is **zero-based** and the second number is **1-based**. Episode 8 of 12 is represented by '7/12'.  Series/episode/part numbers are always **zero-based** when appearing alone.

```xml
<episode-num system="xmltv_ns">1/15.3/24</episode-num>
```

Set the 'seasonNumber' property to 2.\
Set the 'seasonCount' property to 15.\
Set the 'episodeNumber' property to 4.\
Set the 'episodeCount' property to 24.\
Set the 'episodeOnscreen' property to "s02.e04".

```xml
<episode-num system="xmltv_ns">2.4</episode-num>
```

Set the 'seasonNumber' property to 3.\
Set the 'episodeNumber' property to 5.\
Set the 'episodeOnscreen' property to "s03.e05".

**Note:** The property names in the above examples refer to the HTML/JSON API.

More details on the XMLTV format can be found here: [https://wiki.xmltv.org/index.php/XMLTVFormat](https://wiki.xmltv.org/index.php/XMLTVFormat) and here: [https://github.com/XMLTV/xmltv/blob/master/xmltv.dtd](https://github.com/XMLTV/xmltv/blob/master/xmltv.dtd).
