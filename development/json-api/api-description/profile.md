# Profile

ADMIN privilege is required to use these functions except for profile/list.

### profile/list

Lists the available stream profiles (visible in the GUI at Configuration -> Stream -> Stream Profiles) together with their uuids.

* `all` A user with ADMIN privilege can use this parameter to see details of every profile even if the profile is disabled or they do not have access to them.
* `htsp` If set to 1, list only HTSP profiles. Default is 0 (list all).

```
{
   "entries" : [
      {
         "val" : "webtv-h264-vorbis-mp4",
         "key" : "1c1f404622fbe9e6133eec69b7c7da6e"
      },
      {
         "val" : "matroska",
         "key" : "03663b00383b34a6ce2a621733388bf5"
      },
      {
         "val" : "webtv-h264-aac-mpegts",
         "key" : "b90da9e0bc0633515b261714a966910d"
      },
      {
         "val" : "webtv-vp8-vorbis-webm",
         "key" : "b171e3a1d2b576e61b8df418e13c5f4a"
      },
      {
         "key" : "8405e0911b97b795d4cd2cddc322dd7f",
         "val" : "webtv-h264-aac-matroska"
      },
      {
         "key" : "b436b4d6bf606fc9954a1fd3dcebe6a8",
         "val" : "audio"
      },
      {
         "val" : "pass",
         "key" : "af143f0b83fd4e919e3fbf05c5561984"
      }
   ]
}
```

To get the contents of a stream profile use [raw/export](raw.md#raw-export), passing it the stream profile's uuid.

### profile/class

Lists the options, defaults and descriptions of configuration parameters (Configuration -> Stream -> Stream Profiles) in the GUI.

### profile/builders

Lists the options, defaults and descriptions of configuration parameters when adding a new stream profile (Configuration -> Stream -> Stream Profiles -> Add) in the GUI.

### profile/create

Create a new stream profile.

* `class`
* `conf` A JSON object containing details of the new profile.
