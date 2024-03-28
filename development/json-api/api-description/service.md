# Service

ADMIN privilege is required to use all of these functions.

### service/mapper/load

Lists the descriptions, options, current values and defaults of the GUI screen Configuration -> DVB Inputs -> Services. -> Map Services.

Further API functions for manipulating DVB services are in the MPEGts section.

### service/mapper/save

**Untested.** Set the Service Mapper options.

* `node` Unknown, possibly the value of `class`.

### service/mapper/stop

Stops a running service mapper operation.

### service/mapper/status

Provides the same output as Status -> Service Mapper in the TVH GUI.

```
{
   "ignore" : 0,
   "ok" : 0,
   "fail" : 0,
   "total" : 0
}
```

### service/list

Lists available services. "Available" services includes those which are disabled or encrypted.

* `enum` If set to 1 (as an integer without quotes) a short-form list is output containing each service's uuid and name. If set to 0 (the default) a verbose list is generated.
* `list` If `enum` is not 1 this parameter selects which items in the `params` array are to be output, based on the value of the 'id' field. Multiple ids can be selected, separated by commas, colons or semicolons. A '-' in front of an id deselects that item (and implicitly selects all others).

```
curl http://192.168.0.1:9981/api/service/list?enum=1 | jq
{
  "entries": [
    {
      "key": "0172dacd8860f567057a3a2a4ae5533b",
      "val": "Sandy/522MHz/BBC Radio London"
    },
    {
      "key": "01badd8ba1b947976237a5310ad46c75",
      "val": "Sandy/746MHz/5USA+1"
    }, ...
  ]
}
```

```
{
curl http://192.168.0.1:9981/api/service/list?list=enabled,encrypted | jq
  "entries": [
    {
      "uuid": "0172dacd8860f567057a3a2a4ae5533b",
      "id": "0172dacd8860f567057a3a2a4ae5533b",
      "text": "Sandy/522MHz/BBC Radio London",
      "caption": "DVB Inputs - Services",
      "class": "mpegts_service",
      "event": "service",
      "params": [
        {
          "id": "enabled",
          "type": "bool",
          "caption": "Enabled",
          "description": "Enable/Disable service.",
          "default": false,
          "value": false
        },
        {
          "id": "encrypted",
          "type": "bool",
          "caption": "Encrypted",
          "description": "The service's encryption status.",
          "default": false,
          "rdonly": true,
          "nosave": true,
          "value": false
        }
      ]
    }, ...
  ]
}
```

`raw/export?class=service` provides a simpler version of the same information (but including the streams data), however the API call is about 50% slower.

```
curl  "http://192.168.0.1:9981/api/raw/export?class=service"|jq
[
  {
    "sid": 8258,
    "lcn": 3,
    "lcn_minor": 0,
    "lcn2": 0,
    "srcid": 0,
    "svcname": "ITV1",
    "cridauth": "www.itv.com",
    "dvb_servicetype": 1,
    "dvb_ignore_eit": false,
    "prefcapid": 0,
    "prefcapid_lock": 0,
    "force_caid": 0,
    "pts_shift": 0,
    "created": 1473842950,
    "last_seen": 1683534676,
    "enabled": false,
    "auto": 0,
    "priority": 0,
    "s_type_user": -1,
    "verified": 1,
    "pcr": 1701,
    "pmt": 1700,
    "stream": [
      {
        "pid": 1701,
        "type": "MPEG2VIDEO",
        "position": 0
      },
      {
        "pid": 1702,
        "type": "MPEG2AUDIO",
        "position": 0,
        "language": "eng",
        "audio_type": 0,
        "audio_version": 2
      },
      {
        "pid": 1703,
        "type": "MPEG2AUDIO",
        "position": 0,
        "language": "eng",
        "audio_type": 3,
        "audio_version": 2
      },
      {
        "pid": 1731,
        "type": "DVBSUB",
        "position": 0,
        "language": "eng",
        "compositionid": 2,
        "ancillartyid": 2
      }
    ],
    "uuid": "ff05eed5b10a3b072356158688252f03"
  },
...
]
```

### service/streams

Lists the streams comprising the service.

* `uuid` uuid of the service. This parameter is mandatory; it is not possible to list all services.

```
curl http://192.168.0.1:9981/api/service/streams?uuid=01badd8ba1b947976237a5310ad46c75 | jq
{
  "name": "Sandy/746MHz/5USA+1",
  "streams": [
    {
      "pid": 2121,
      "type": "PCR"
    },
    {
      "pid": 1025,
      "type": "PMT"
    },
    {
      "index": 1,
      "pid": 2121,
      "type": "H264",
      "language": "",
      "width": 0,
      "height": 0,
      "duration": 0,
      "aspect_num": 0,
      "aspect_den": 0
    },
    {
      "index": 2,
      "pid": 2122,
      "type": "AAC",
      "language": "eng",
      "audio_type": 0
    },
    {
      "index": 3,
      "pid": 2124,
      "type": "AAC",
      "language": "eng",
      "audio_type": 3
    },
    {
      "index": 4,
      "pid": 2123,
      "type": "DVBSUB",
      "language": "eng",
      "composition_id": 2,
      "ancillary_id": 2
    }
  ],
  "fstreams": [
    {
      "index": 1,
      "pid": 2121,
      "type": "H264",
      "language": "",
      "width": 0,
      "height": 0,
      "duration": 0,
      "aspect_num": 0,
      "aspect_den": 0
    },
    {
      "index": 2,
      "pid": 2122,
      "type": "AAC",
      "language": "eng",
      "audio_type": 0
    },
    {
      "index": 3,
      "pid": 2124,
      "type": "AAC",
      "language": "eng",
      "audio_type": 3
    },
    {
      "index": 4,
      "pid": 2123,
      "type": "DVBSUB",
      "language": "eng",
      "composition_id": 2,
      "ancillary_id": 2
    }
  ]
}
```

### service/removeunseen

Remove services which have not been seen recently. This call carries out the same action as Configuration -> DVB Inputs -> Services -> Maintenance in the TVH GUI.

* `days` The number of unseen days before deletion. The default is 7 days, the minimum is 5 days.
* `type` If set to `pat` the action is the same as "Remove unseen services (PAT/SDT)" in the GUI. Otherwise the action is the same as "Remove all unseen services".

An empty JSON object is always returned.
