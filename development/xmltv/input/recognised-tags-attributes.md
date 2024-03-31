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
</programme>
```

Multiple instances of some tags like 'actor' or 'category' or 'rating' may be present.
