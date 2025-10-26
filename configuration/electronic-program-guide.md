# Electronic Program Guide

Tvheadend has a built-in Electronic Program Guide (EPG). This is an in-memory database populated with information received over-the-air from DVB networks or from external XMLTV grabbers.

The EPG tab displays a filterable grid containing all events, sorted on start time:

!['Electronic Program Guide' Tab](https://tvheadend.readthedocs.io/en/latest/webui/docresources/epg.png)

## Menu Bar <a href="#menu-barbuttons" id="menu-barbuttons"></a>

The following functions are available:

### **Filtering  / Searching**

The EPG tool bar shows five input fields which are used to filter/search events. The form uses implicit AND between input fields. This means all filters must match for an event to be displayed.

<table><thead><tr><th width="246">Filter</th><th>Function</th></tr></thead><tbody><tr><td><strong>Search Title</strong></td><td>Display events that match the given title. The filter uses case-insensitive regular expressions. If you don’t know what a regular expression is, this simply means that you can type just parts of the title and filter on that - there’s no need for full, exact matching. If the fulltext checkbox is checked, the title text is matched against title, subtitle, summary and description.</td></tr><tr><td><strong>Filter Channel</strong></td><td>Display events from the selected channel. Channels in the drop down are ordered by name and can be filtered (by name) by typing in the box.</td></tr><tr><td><strong>Filter Tag</strong></td><td>Display events from channels which are included in the selected tag. Tags are used for grouping channels together - such as ‘Radio’ or ‘HDTV’ and are configured by the admin. Start typing a tag name to filter the list.</td></tr><tr><td><strong>Filter Content Type</strong></td><td>Display events that match the given content type tag. Most DVB networks classify their events into content groups. This field allows you to filter based on content type (e.g. “Sports” or “Game Show”). Supported tags are determined by your broadcaster. Again, simply start typing to filter the entries if you have a long list to choose from.</td></tr><tr><td><strong>Filter Duration</strong></td><td>Display events that fall between the given minimum and maximum durations. This allows you to filter for or against, say, a daily broadcast and a weekly omnibus edition of a programme, or only look for short news bulletins and not the 24-hour rolling broadcasts.</td></tr></tbody></table>

_Title_, _Channel_, _Tag_ and _Content Type_ are dependent on your configuration and on what your broadcaster sends. Options for the _Duration_ are as follows:

<table><thead><tr><th width="248">Filter Range</th><th>Example Purpose</th></tr></thead><tbody><tr><td>00:00:01 to 00:15:00</td><td>Very short news bulletins, children’s programmes, etc.</td></tr><tr><td>00:15:01 to 00:30:00</td><td>Short programmes, e.g. daily soap operas</td></tr><tr><td>00:30:01 to 01:30:00</td><td>Medium-length programmes, e.g. documentaries</td></tr><tr><td>01:30:01 to 03:00:00</td><td>Longer programmes, e.g. films</td></tr><tr><td>03:00:00 to no maximum</td><td>Very long programmes, e.g. major sporting events</td></tr></tbody></table>

For example: if you only want to see Movies from available HD channels you would select ‘HDTV’ in the _\[Filter tag…]_ field, and select ‘Movie / Drama’ in the _\[Filter content type…]_ field. You could then further limit the search to programmes between 1.5 - 3 hours by selecting ‘01:30:01 to 03:00:00’ in the _\[Filter duration…]_ field.

> The grid updates dynamically as you change filters. You do not need to press a ‘Search’ button.

You can clear a filter by deleting its contents or by selecting _‘(Clear filter)’_ on all filter fields except the Title filter. To clean all filters, press the _\[Reset All]_ button.

## **Buttons**

The following buttons are also available:

<table><thead><tr><th width="238">Button</th><th>Function</th></tr></thead><tbody><tr><td><strong>Reset All</strong></td><td>Clears all search filters</td></tr><tr><td><strong>Watch TV</strong></td><td>Launches Live TV via HTML5 video</td></tr><tr><td><strong>Create Autorec</strong></td><td>Creates an auto-recording rule based on the current filter criteria</td></tr><tr><td><strong>Help</strong></td><td>Display this help page</td></tr></tbody></table>

## Grid Items <a href="#grid-items" id="grid-items"></a>

The main grid items have the following functions:

* **Details**: Displays the current status of a recording event for the selected programme

<table><thead><tr><th width="108">Icon</th><th>Description</th></tr></thead><tbody><tr><td><img src="https://tvheadend.readthedocs.io/en/latest/webui/icons/clock.png" alt="Clock icon"></td><td>The programme is scheduled for recording</td></tr><tr><td><img src="https://tvheadend.readthedocs.io/en/latest/webui/icons/rec.png" alt="Recording icon"></td><td>The programme is currently recording</td></tr><tr><td><img src="https://tvheadend.readthedocs.io/en/latest/webui/icons/broadcast_details.png" alt="Broadcast details icon"></td><td>Click to call up more detailed information about an event</td></tr></tbody></table>

* **Progress** : A bar graph display of how far through a programme we currently are.
* **Title**: The programme main title. _You can automatically set a filter to the value of this field by clicking on it (e.g. click on ‘Daily News’ will automatically filter the whole grid to only show programmes with the same name)._
* **SubTitle**: The programme minor title or subtitle if included with EPG data. Some providers use this for a programme synopsis and not a true subtitle.
* **Episode**: Episode number, if given by your EPG provider.
* **Start Time**: The scheduled start time of the programme.
* **End Time**: The scheduled end time of the programme.
* **Duration**: The scheduled duration (i.e. start time to end time) of the programme.
* **Number**: The channel number of the broadcasting channel, if defined.
* **Channel**: The name of the broadcasting channel. _You can automatically set a filter to the value of this field by clicking on it (e.g. click on ‘Channel 4 HD’ will automatically filter the whole grid to only show programmes from that channel)._
* **Stars**: Rating (in stars) of the programme.
* **Age**: Age rating of the programme.
* **Content Type** : Any content/genre information as provided by the EPG provider. _You can automatically set a filter to the value of this field by clicking on it (e.g. click on ‘Movie/Drama’ will automatically filter the whole grid to only show programmes of the same type)._

## Event Details & Recording <a href="#event-details-and-recording" id="event-details-and-recording"></a>

If you click on a single event, a popup displays detailed information. You can schedule the event for recording by clicking on the _\[Record program]_ button. If the EPG provider includes series-link data the _\[Record series]_ button allows you to schedule recording of all entries in the series.

![EPG Detail 1](https://tvheadend.readthedocs.io/en/latest/webui/docresources/epg2.png)

For events without any series link information, an _\[Autorec]_ button will be provided to create a pseudo-series link using the autorec feature.

![EPG Detail 2](https://tvheadend.readthedocs.io/en/latest/webui/docresources/epg3.png)

When scheduling recording you can choose the DVR profile used for the recording or autorec rule. This will normally show _(default)_ but you can define different profiles in the **Configuration -> Recording -> Digital Video Recorder** tab. Profiles allow you to set, e.g. post-broadcast padding to accommodate a channel that always runs late, or a post-processing command to strip adverts from recordings made from a commercial channel.

The _\[Search IMDB]_ button runs a search against the programme title on on imdb.com, and _\[Play program]_ button. This downloads am XSPT or M3U playlist file (depending on startup options) and if your Operating System is correctly configured this will launch an appropriate player application. If not you will need to manually open (double-click) the playlist file to start watching.

Clock on the \[X] window button (top-right) to close the popup. The popup is not modal and will remain open and visible. You can open multiple detailed information popups at the same time.

## Autorecordings <a href="#autorecordings" id="autorecordings"></a>

To record all events matching a specific search query, e.g. to record a favourite show every week, press the _\[Create AutoRec]_ button in the top toolbar. A popup with details on the to-be-created "autorec" rule will be shown. To enable the rule, confirm it by clicking the \[Yes] button.

![Autorec Dialogue Box](https://tvheadend.readthedocs.io/en/latest/webui/docresources/autorecpopup.png)

Autorec rules are listed in the **Digital Video Recorder** tab. Edit the rule list if you want to temporarily disable an autorecording or make adjustments to the channel, tag, or similar rule criteria.

## Watch TV <a href="#watch-tv" id="watch-tv"></a>

Clicking the _\[Watch TV]_ button will open an HTML5 player pop-up where you can select the channel to open and stream profile to use. A transcoding stream profile is required to transcode the stream to a format that is supported by your browser, as browsers only support certain formats and codecs.

### **Supported Container Formats**

| Browser         |                                    MPEG-TS                                    |                                    MPEG-PS                                    |                                  Matroska                                 |                                    WebM                                   |
| --------------- | :---------------------------------------------------------------------------: | :---------------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
| Google Chrome   | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |
| Mozilla Firefox | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) |                                                                           | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |

### **Supported Video Codecs**

| Browser         |                                     MPEG2                                     |                                   H.264                                   |                                    VP8                                    |
| --------------- | :---------------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
| Google Chrome   | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |
| Mozilla Firefox | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) |                                                                           | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |

### **Supported Audio Codecs**

| Browser         |                                     MPEG2                                     |                                    DD (AC3)                                   |                                    AAC                                    |                                   Vorbis                                  |
| --------------- | :---------------------------------------------------------------------------: | :---------------------------------------------------------------------------: | :-----------------------------------------------------------------------: | :-----------------------------------------------------------------------: |
| Google Chrome   | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |
| Mozilla Firefox | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) | ![no](https://tvheadend.readthedocs.io/en/latest/webui/icons/exclamation.png) |                                                                           | ![yes](https://tvheadend.readthedocs.io/en/latest/webui/icons/accept.png) |
