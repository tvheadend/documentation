# Bouquet

ADMIN privilege is required for all of these functions.

### bouquet/class

Lists the text strings, options and defaults used when configuring bouquets within TVH (ie Configuration -> Channel/EPG -> Bouquets).

### bouquet/create

Create a new bouquet.

* `conf` Object describing the new bouquet. An element `ext_url` is required; presumably in the format of the `source` element in bouquet/grid.

### bouquet/detach

Removes the link from a channel to the bouquet that it is part of.

* `uuid` uuid(s) of channels to detach.

### bouquet/grid

Lists details of bouquets. For details of the parameters and selection criteria which can be applied, see Commmon Parameters.

```
{
   "entries" : [
      "uuid": "0d5677d5c370705f3cd3fb53665bc62c",
      "enabled": false,
      "maptoch": false,
      "mapopt": [],
      "chtag": [],
      "chtag_ref": "",
      "name": "Scotland G2: Scotland/BorderSco",
      "ssl_peer_verify": false,
      "ext_url_period": 60,
      "source": "dvb-freesat://dvbs,28.2E,0119,62",
      "services": {},
      "services_seen": 63,
      "services_count": 0,
      "comment": "11428H in Freesat",
      "lcn_off": 0
    }, ...
  ],
  "total": 303
}
```

### bouquet/list

Lists names and bouquets. The list excerpted below is coded into tvheadend.

```
{
   "entries" : [
      {
         "key" : "e7ddb611669a6a612846415946272f89",
         "val" : "Canal Digitaal SD"
      }, ...
   ]
}
```

### bouquet/scan

Scan (using an available tuner) one or more bouquets to find their channels. The channel list is NOT returned, just an empty JSON object.

* `uuid` uuid(s) of bouquet(s) to scan.
