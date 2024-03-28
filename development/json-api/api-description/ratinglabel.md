# RatingLabel

Functions to query and manipulate the list of parental rating labels ('G', 'M', 'PG', etc).

### ratinglabel/class

Lists the text strings, options and defaults used when configuring parental rating labels within TVH (ie Configuration -> Channel/EPG -> Rating Labels -> Add).

### ratinglabel/create

Creates a new parental rating label. Requires ADMIN privilege.

* `conf` A JSON object containing details of the new parental rating label.

### ratinglabel/grid

Lists details of parental rating labels. For details of the parameters and selection criteria which can be applied, see Grid Parameters.

```
{
   "entries" : [
      {
         "uuid : "a82438515ecc857dbf2509517ff3fe40",
         "enabled" : true,
         "country" : "AUS",
         "age" : 8,
         "display_age" : 11,
         "display_label" : "PG",
         "label" : "PG",
         "authority" : "ACMA",
         "icon" : "file:///my/file/location/acma-pg.png",
         "icon_public_url" : "imagecache/37"
      }, ...
   ],
   "total" : 9
}
```

### ratinglabel/list

Lists the names and uuids of all known parental rating labels.

```
{
   "entries" : [
      {
         "val" : "AUS",
         "key" : "7b1f8773747155ed7341c8328a037f28"
      }, ...
   ]
}
```

**Notes:**

* Parental rating labels were added to Tvheadend in December 2023.
* Processig of parental rating labels is **disabled** by default and can be enabled via Configuration -> Channel/EPG -> EPG Grabber.
* Tvheadend will automatically create a placeholder record as new labels are encountered.
* Parental rating label fields will not appear in other modules, (DVR, EPG) if the processing of parental rating labels is disabled.
