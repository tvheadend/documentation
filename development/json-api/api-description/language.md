# Language

### language/list

Produces a list of all known languages and their three-letter ISO639-3 codes. The list is hard-coded within the Tvheadend source.

```
{
   "entries" : [
      {
         "val" : "Undetermined",
         "key" : "und"
      },
      {
         "key" : "aar",
         "val" : "Afar"
      },
      {
         "val" : "Abkhazian",
         "key" : "abk"
      }, ...
   ]
}
```

### language/locale

Produces a similar list to language/list but also including the full RFC3066 locale reference for those locales which have been compiled into Tvheadend.

<pre><code>{
  "entries" : [
  ...
<strong>    {
</strong>      "key": "elx",
      "val": "Elamite"
    },
    {
      "key": "eng",
      "val": "English"
    },
    {
      "key": "eng_US",
      "val": "English (US)"
    },
    {
      "key": "eng_GB",
      "val": "English (GB)"
    },
    {
      "key": "epo",
      "val": "Esperanto"
    }, ...
  ]
}
</code></pre>

### language/ui\_locale

Produces a list in the same format as language/locale but containing only those locales which are supported by TVHeadend (ie have translations available).
