# MPEGts

Functions relating to DVB networks, multiplexes and services. Further service functions can be found in the Service section. ADMIN privilege is required for all these functions.

### mpegts/input/network\_list

Lists the network(s) associated with a given input device.

* `uuid` The uuid of the specific hardware device.

To find the input device uuid, use `hardware/tree?uuid=root`, then take the `id` value from the output and use it as the value of `uuid` in another call to hardware/tree. From the output of this function select the `id` corresponding to the specific front-end device required.

```
{
   "entries" : [
      {
         "key" : "c70bb0e55db15cf44c72a8acb49d5ed7",
         "val" : "Sandy"
      }
   ]
}
```

### mpegts/network/grid

Lists available networks. The standard parameters listed in Grid Parameters may be used. The items returned depend on the type of network - terrestrial, satellite, IPTV etc.

```
curl http://192.168.1.1:9981/api/mpegts/network/grid |jq 
{
  "entries": [
    {
      "uuid": "546f654e5e9abe67386f9ea3516987a3",
      "url": "file:///home/hts/iptvlist.m3u8",
      "channel_number": 0,
      "refetch_period": 60,
      "ssl_peer_verify": false,
      "tsid_zero": false,
      "remove_args": "",
      "ignore_path": 0,
      "scan_create": false,
      "service_sid": 1,
      "priority": 0,
      "spriority": 0,
      "max_streams": 0,
      "max_bandwidth": 0,
      "max_timeout": 15,
      "remove_scrambled": true,
      "enabled": true,
      "networkname": "iptv",
      "pnetworkname": "iptvlist",
      "nid": 0,
      "autodiscovery": 0,
      "bouquet": false,
      "skipinitscan": true,
      "idlescan": false,
      "sid_chnum": false,
      "ignore_chnum": false,
      "charset": "AUTO",
      "localtime": 0,
      "num_mux": 100,
      "num_svc": 100,
      "num_chn": 0,
      "scanq_length": 0,
      "wizard": false
    },
    {
      "uuid": "c9a4516fa61feef914de797a799f11d2",
      "orbital_pos": "28.2E",
      "enabled": true,
      "networkname": "Freesat",
      "pnetworkname": "ASTRA",
      "nid": 0,
      "autodiscovery": 2,
      "bouquet": false,
      "skipinitscan": false,
      "idlescan": false,
      "sid_chnum": false,
      "ignore_chnum": false,
      "charset": "AUTO",
      "localtime": 0,
      "num_mux": 79,
      "num_svc": 602,
      "num_chn": 193,
      "scanq_length": 0,
      "wizard": true
    }
  ],
  "total": 2
}

```

### mpegts/network/class

Lists the text strings, options and defaults used when configuring the DVB capability within TVH (ie Configuration -> DVB Inputs -> Networks).

### mpegts/network/builders

Lists the text strings, options and defaults used when configuring the DVB capability within TVH (ie Configuration -> DVB Inputs -> Network -> Add).

### mpegts/network/create

Create a new network.

* `class` Required. The class name matching the `class` item obtained from a call to mpegts/network/builders.
* `conf` Required. A JSON object containing the settings for this network.

### mpegts/network/mux\_class

Lists the text strings, options and defaults used when editing a multiplex using Configuration -> DVB Inputs -> Muxes -> Edit.

* `uuid` The value of `network_uuid` from a call to mpegts/mux/grid.

### mpegts/network/mux\_create

Create a mux for an existing network.

* `uuid` The uuid of the network containing this mux.
* `conf` A JSON object containing the settings for this mux. The contents will depend on the type of network.

A JSON object containing the UUID of the new mux is returned.

```
curl -d uuid=62d279b29fff2de0ff1245dad5154500 -d 'conf={"enabled":1,"epg":0,"epg_module_id":"","delsys":"DVBS","frequency":12440000,"symbolrate":29500000,"polarisation":"V","modulation":"QPSK","fec":"8/9","scan_state":0,"charset":"","rolloff":"AUTO","pilot":"AUTO","dvb_satip_dvbc_freq":0,"dvb_satip_dvbt_freq":0,"tsid_zero":false,"pmt_06_ac3":0,"eit_tsid_nocheck":false,"sid_filter":0,"stream_id":-1,"pls_mode":"ROOT","pls_code":1}'
 "http://192.168.0.1:9981/api/mpegts/network/mux_create"
```

### mpegts/network/scan

Triggers a scan of the requested network(s).

* `uuid` uuid(s) of the network(s) to scan. More than one may be given; they will be scanned in sequence.

### mpegts/mux/grid

Lists available multiplexes. The standard parameters listed in Grid Parameters may be used.

* `hidemode` If set to `all`, only enabled multiplexes are listed. The default is to show all multiplexes.

```
{
   "total" : 9,
   "entries" : [
      {
         "created" : 1508497835,
         "delsys" : "DVB-T",
         "scan_state" : 0,
         "tsid" : 24640,
         "scan_first" : 1508761027,
         "name" : "690MHz",
         "pnetwork_name" : "Cambs & Beds",
         "transmission_mode" : "8k",
         "sid_filter" : 0,
         "network_uuid" : "c70bb0e55db15cf44c72a8acb49d5ed7",
         "onid" : 9018,
         "num_svc" : 35,
         "eit_tsid_nocheck" : false,
         "num_chn" : 29,
         "hierarchy" : "NONE",
         "tsid_zero" : false,
         "pmt_06_ac3" : 0,
         "network" : "Sandy",
         "scan_last" : 1509267382,
         "bandwidth" : "8MHz",
         "fec_lo" : "NONE",
         "frequency" : 690000000,
         "constellation" : "QAM/64",
         "fec_hi" : "3/4",
         "epg" : 1,
         "guard_interval" : "1/32",
         "scan_result" : 1,
         "enabled" : 1,
         "uuid" : "0245c791efc3fa448c19db2f000d0d8f",
         "plp_id" : -1
      }, ...
   ]
}
```

### mpegts/mux/class

Lists the text strings, options and defaults used when configuring the DVB capability within TVH (ie Configuration -> DVB Inputs -> Muxes).

### mpegts/service/grid

Lists available mpegts services. The standard parameters listed in Grid Parameters may be used.

* `hidemode` The default is to show only services where the multiplex is enabled and the service has been verified. Setting this parameter to `all` also hides services which are not enabled, setting it to `none` shows all services.

```
curl http://192.168.1.1:9981/api/mpegts/service/grid | jq
{
   "entries" : [
      {
         "uuid": "105984f18272f0e05107b296a1ea9d2a",
         "network": "Freesat",
         "multiplex": "11914.5H",
         "multiplex_uuid": "bb4aaf3f77880e60bdfc6fd33fc4efc1",
         "sid": 5229,
         "lcn": 0,
         "lcn_minor": 0,
         "lcn2": 0,
         "srcid": 0,
         "svcname": "Sky Arts",
         "provider": "BSkyB",
         "dvb_servicetype": 1,
         "dvb_ignore_eit": false,
         "prefcapid": 0,
         "prefcapid_lock": 0,
         "force_caid": 0,
         "pts_shift": 0,
         "created": 1623526273,
         "last_seen": 1662095234,
         "enabled": true,
         "auto": 0,
         "channel": [
            "4e3dacb42fa6aff571ff2ce2d143d70d"
         ],
         "priority": 0,
         "encrypted": false,
         "caid": "",
         "s_type_user": -1
      }, ...
   ]
  "total": 908
}
```

`dvb_servicetype` can be used to determine what kind of service is being broadcast. The possibilities are:

* Radio: 0x02
* SD TV: 0x01, 0x16, 0x17, 0x18, 0x80, 0x96, 0xa8, 0xd3
* HD TV: 0x11, 0x19 - 0x1e, 0x91, 0xa0, 0xa4, 0xa6
* UHDTV: 0x1f

### mpegts/service/class

Lists the text strings, options and defaults used when configuring the DVB capability within TVH (ie Configuration -> DVB Inputs -> Services).

### mpegts/mux\_sched/class

Lists the text strings, options and defaults used when configuring the DVB capability within TVH (ie Configuration -> DVB Inputs -> Mux Schedulers).

### mpegts/mux\_sched/grid

List the entries as found under Configuration -> DVB Inputs -> Mux Schedulers. The standard parameters listed in Grid Parameters may be used.

```
{
   "entries" : [
      {
         "mux" : "93b544d663e5313b12991fe9926ae4af",
         "restart" : false,
         "enabled" : true,
         "uuid" : "feab6167cd0596388382441987f33678",
         "timeout" : 600,
         "cron" : "30 3 * * *"
      }
   ],
   "total" : 1
}
```

### mpegts/mux\_sched/create

**Untested.** Create a mux schedule, presumably from a structure similar to that from mpegts/mux\_sched/grid.

### dvb/orbitalpos/list

Lists orbital positions and the satellites occupying them. The list is distributed with tvheadend; satellite reception is not necessary to use this API.

```
{
   "entries" : [
      {
         "key" : "177W",
         "val" : "177W : NSS 9"
      }, ...
   ]
}
```

### dvb/scanfile/list

Lists the available frequency scan tables.

* `type` One of 'dvb-s', 'dvb-t', 'dvb-c', 'atsc-t', 'atsc-c', 'isdb-t'.
* `satpos` For dvb-s, the satellite position in degrees **multiplied by 10** with East positive (so 28.2E is written as 282). The position must be accurate within +/- 0.2 degrees.

This function requires the dvb-scan files to be present on the server. They are installed by default (in /usr/share/tvheadend/data/) but are omitted if configure argument '--disable-dvbscan' is used. Distributions may also choose to package them separately.

```
{
   "entries" : [
      {
         "val" : "> 28.2E:Astra",
         "key" : "dvb-s/geo/dvb-s_> 28.2E:Astra"
      }
   ]
}
```
