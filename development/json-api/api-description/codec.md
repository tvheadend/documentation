# Codec

ADMIN privilege is required for all of these functions except codec\_profile/list.

### codec/list

Lists available codecs and their properties. This is a very verbose list.

### codec\_profile/class

Lists the text strings, options and defaults used when configuring codec profiles.

### codec\_profile/create

Add a new codec profile.

* `class` The name of the codec profile.
* `conf` A JSON object describing the codec profile.

### codec\_profile/list

```
{
   "entries" : [
      {
         "uuid" : "d3f76d002a895f5c65dd57715d169399",
         "title" : "webtv-vorbis (WEBTV codec Vorbis)",
         "status" : "codecEnabled"
      },
      {
         "status" : "codecEnabled",
         "title" : "webtv-aac (WEBTV codec AAC)",
         "uuid" : "77e7184d6ade386137f553de0687254d"
      },
      {
         "title" : "webtv-h264 (WEBTV codec H264)",
         "status" : "codecEnabled",
         "uuid" : "eb7281ade724c77d23add9223bc2a480"
      }
   ]
}
```
