# Raw

Although no special privilege is needed to use these functions, access control is applied at the inode database level.

### classes

Returns a list of all data classes together with readable titles. Requires version 4.3-406 or later.

```
{
   "linuxdvb_rotor_gotox" : "TV Adapters - SatConfig - GOTOX Rotor",
   "dvb_mux" : "DVB multiplex",
   "profile-libav-mpegts" : "MPEG-TS/av-lib",
   "epggrab_mod" : "EPG Grabber",
   "esfilter" : "Elementary stream filter",
   "mpegts_network" : "DVB Inputs - Networks",
   "caclient_capmt" : "CAPMT (Linux Network DVBAPI)",
   "channeltag" : "Channel Tags",
   "codec_profile_libopus" : "libopus",
   "linuxdvb_frontend_isdb_t" : "TV Adapters - Linux ISDB-T Frontend",
   ...
}
```

### raw/export

* `class` One of the class names returned by [classes](raw.md#classes).
* `uuid` A single uuid or JSON array of uuids.

Returns data about the selected object(s). The information is the same as returned by the corresponding `grid` function (where available) but without the selection and filtering options provided by that function.

### raw/import

* `node` A JSON object or array of objects.

Objects being imported must have a uuid and must already exist in the database.
