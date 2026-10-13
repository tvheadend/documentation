# Recognised Tags/Attributes

TVHeadEnd only recognises a subset of the total XMLTV schema.

```xml
<programme start="YYYYMMDDhhmmss +0000" stop="YYYYMMDDhhmmss +0000" channel="3">
	<title lang="en">Event title to display</title>
	<sub-title lang="en">Event sub-title to display</sub-title>
	<desc lang="en">Extended event description</desc>
	<summary lang="en">Event summary</summary>
	<category lang="en">Category name</category>
	<keyword lang="en">Keyword name</keyword>
	<credits>
		<actor>Actor's name</actor>
		<director>Director's name</director>
		<guest>Guest's name</guest>
		<presenter>Presenter's name</presenter>
		<writer>Writer's name</writer>
	</credits>
	<video>
		<colour>NO</colour>
		<aspect>Width:Height</aspect>
		<quality>HD|FHD|UHD|488|576|720|1080|1716|2160</quality>
	</video>
	<subtitles type="teletext|deaf-signed"/>
	<audio-described />
	<previously-shown start="2008-10-11"/>
	<premiere />
	<new />
	<episode-num system="onscreen|xmltv_ns|dd_progid">Episode number text</episode-num>
	<star-rating>
		<value>X/Y</value>
	</star-rating>
	<date>YYYY</date>
	<rating system="Name">
		<value>Rating displey text</value>
	</rating>
	<icon src="Icon URL" />
	<image type="poster" orient="P">https://example.org/poster.jpg</image>
	<image type="backdrop" orient="L">https://example.org/backdrop.jpg</image>
	<image type="still" orient="L">https://example.org/still.jpg</image>
</programme>
```

Multiple instances of some tags like 'actor' or 'category' or 'rating' may be present.

Four additional fields can be also extracted from non-standard locations using XPath-like syntax.

* ETSI Category (Genre) Code
* Unique Event ID
* SeriesLink (CRID)
* EpisodeLink (CRID)

See the 'External: XMLTV Grabber' module help text for more details.

## Programme images

Select the artwork to import in **Programme image types** (`image_types`) on
the internal or external XMLTV grabber module. The available types are `poster`,
`backdrop` and `still`; none are selected by default. This setting does not
change the existing programme `<icon>` handling. Person and character images
are not imported.

The `<image>` URL is the element's text, not a `src` attribute. Surrounding XML
whitespace is stripped and empty values are ignored. Tvheadend retains one URL
per selected type: the first poster, and the first explicitly landscape
(`orient="L"`) backdrop or still. If no image of that type is marked landscape,
the first one wins. The `size` and `system` attributes do not affect selection.
Tvheadend uses the declared orientation, not measured image dimensions.

Normal grabber priority and merge rules apply. A subsequent accepted programme
import can clear a previously imported type if it is missing from the source or
has been deselected. Changing the setting alone does not immediately remove
artwork from existing EPG events.

Priority applies to the broadcast, not separately to artwork. A lower-priority
XMLTV grabber cannot supplement images on a broadcast owned by a higher-priority
source. An accepted non-merge update from a source without typed images, such as
EIT, can clear them; merge updates can preserve omitted fields.

Selected images use the existing image cache and its settings. Additional types
can increase image requests and cache storage. Clients need support for the
separate [JSON EPG](../../json-api/api-description/epg.md#programme-images) or
[HTSP](../../htsp/server-to-client-methods.md#eventadd) fields to display them.
Typed images do not replace or automatically populate the programme icon.
