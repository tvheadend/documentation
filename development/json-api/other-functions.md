# Other Functions

This section describes other functions which can be accessed via HTTP. They are not part of the HTTP API and so are not preceded by 'api'.

Unless otherwise stated no special privilege is needed to use these functions.

### comet/poll

Returns a JSON object containing data used by the Tvheadend UI, including the disk space utilisation.

The "freediskspace" and "totaldiskspace" figures relate to the disk partition holding the recorder Storage Path, "useddiskspace" is the total size of all files stored below that point. These figures may not give the actual storage situation if there are multiple storage devices and mount points.

```
curl  "http://192.168.0.1:9981/comet/poll" | jq

{
  "boxid": "1cee949b52c05872fdb24c8bc2dccc0a41fdb33b",
  "messages": [
    {
      "notificationClass": "accessUpdate",
      "uilevel": "expert",
      "theme": "blue",
      "quicktips": 1,
      "chname_num": 0,
      "chname_src": 0,
      "date_mask": "",
      "label_formatting": 0,
      "username": "",
      "address": "192.168.0.1",
      "dvr": 1,
      "admin": 1,
      "time": 1709799071,
      "cookie_expires": 2047,
      "ticket_expires": 300,
      "info_area": "login,storage,time",
      "freediskspace": 608234205184,
      "useddiskspace": 135222628776,
      "totaldiskspace": 861450428416
    },
    {
      "notificationClass": "setServerIpPort",
      "ip": "192.168.0.1",
      "port": 9981
    }
  ]
}
```

See [WebSocket](websocket.md) for a WebSocket interface to this function.

### dvrfile

Downloads a previously-recorded file. Called with the UUID of the recording. Requires appropriate privilege (DVR or streaming).

```
http://192.168.0.1:9981/dvrfile/968ecf2073e4ec2e45c0ad534acdd4bf
```

### epgsave

Flushes the contents of the EPG to disk.

### eventinfo

Used by simple.html.

### favicon.ico

Downloads an icon file. The filename is hard-coded in the source; on installation it is usually placed at `/usr/share/tvheadend/src/webui/static/img/logo.png`.

### HDHomeRun

These functions are only available if HDHomeRun Server has been compiled into Tvheadend. The first two are documented in [https://info.hdhomerun.com/info/http\_api](https://info.hdhomerun.com/info/http_api), the others are required by Plex.

* discover.json
* lineup.json
* lineup\_status.json
* lineup.post
* device.xml

### imagecache

Outputs an image from the image cache. Requires streaming, recording or web interface privilege.

```
$ curl  http://192.168.0.1:9981/imagecache/<image-number>
```

### markdown

Used to download help files.

### ping

Available on version 4.3-2124 and later. Provides a simple way to check that the server is alive. No authentication is needed to use this function.

```
curl http://192.168.0.1:9981/ping
PONG
```

### play

This function acts as a front-end to the `dvrfile` and `stream` functions. It is invoked using the following forms:

```
http://192.168.0.1:9981/play/stream/channelnumber/<channelnumber>
http://192.168.0.1:9981/play/stream/mux/cc23a085f4ff2cb41a8f58ad85570fde
http://192.168.0.1:9981/play/dvrfile/968ecf2073e4ec2e45c0ad534acdd4bf
```

The function examines the 'User-Agent' string sent by the client. If the user-agent is on a preset list (or is not present), data transfer starts immediately; if not then a playlist is returned to the client.

The User-Agent list is "MPlayer", "curl/", "wget/", "TVHeadend", "Lavf" and any string containing "shoutcastsource".

If `ticket` is added to the URL, for example:

```
http://192.168.0.1:9981/play/ticket/stream/channelnumber/<channelnumber>
```

the url in the returned playlist will contain an authentication ticket, removing any need to enter credentials in order to access the data. However the ticket is only valid for five minutes so the playlist cannot be re-used after that time.

When playing streams, the parameters for the underlying stream function can also be used.

### playlist

This is a complex function which outputs lists of content available from the server, in various formats and filtered in several ways. The syntax for invoking the function depends on the required output and not all combinations of inputs are valid.

**Note:** The hostname portion of the URLs returned within the resulting playlist, for example m3u, will be the same as the hostname supplied with the http request.

#### List all tags

```
$ curl http://192.168.0.1:9981/playlist/tags
```

See below for sample output.

#### List all channels or recordings

```
$ curl http://192.168.0.1:9981/playlist/y/x/channels
$ curl http://192.168.0.1:9981/playlist/y/recordings
```

The value of \<x> in the URL specifies the format of the output. The options are `e2`, `m3u` or `satip`, with `m3u` the default if the item is omitted. For recordings only `m3u` is available.

For channels, a parameter `sort` can be added. This can take the value 'name' or 'numname', to sort the output by channel name or channel number respectively.

See below for notes including the values of \<y> in the URL, and sample outputs.

#### List filtered channels or recordings

```
$ curl http://192.168.0.1:9981/playlist/y/x/channelid/<channelid>
$ curl http://192.168.0.1:9981/playlist/y/x/channelnumber/<channelnumber>
$ curl http://192.168.0.1:9981/playlist/y/x/channelname/<channelname>
$ curl http://192.168.0.1:9981/playlist/y/x/channel/<channelUUID>
$ curl http://192.168.0.1:9981/playlist/y/x/tagid/<tagid>
$ curl http://192.168.0.1:9981/playlist/y/x/tagname/<tagname>
$ curl http://192.168.0.1:9981/playlist/y/x/tag/<tagUUID>

$ curl http://192.168.0.1:9981/playlist/y/dvrid/<dvr_id>
```

The value of \<x> in the URL specifies the format of the output. The options are `e2`, `m3u` or `satip`, with `m3u` the default if the item is omitted. For recordings only `m3u` is available.

See below for notes including the values of \<y> in the URL, and sample outputs.

#### Notes

The list of recordings includes all entries in the DVR logs, including failed and missed recordings and recordings to be made in the future (ie timers). Unplayable recordings have 'bandwidth=0' in the output.

The value of \<y> in the URLs, if supplied, specifies whether the channel list or playlist should include authentication in the URL. If \<y> is `ticket`, each entry includes an access-control 'ticket' - these tickets are only valid for five minutes, they are different for each channel/recording listed, and calling the playlist again will output a different set of tickets.

Alternatively, if Persistent Authentication is in use (TVHeadend versions > 4.3.1485), the value of \<y> may be set to `auth`. The auth code must be appended to the URL as a parameter, eg.

`$ curl http://192.168.0.1:9981/playlist/auth/tags?auth=8ef7aa08e516060ca4330730c60e00d5b5174920`

#### Sample outputs

```
$ curl  http://192.168.0.1:9981/playlist/tags
#EXTM3U
#EXTINF:-1 logo="",HDTV
http://192.168.0.1:9981/playlist/tagid/1267929608?profile=pass
#EXTINF:-1 logo="",Radio channels
http://192.168.0.1:9981/playlist/tagid/1970563711?profile=pass
...

$ curl  http://192.168.0.1:9981/playlist/channels
#EXTINF:-1 tvg-id="90a325df8d683eb014cf0abf56943e8d" tvg-chno="1005",CNN
http://192.168.0.1:9981/stream/channelid/1596302224?profile=pass
#EXTINF:-1 tvg-id="c44d3390a7b5ecb59a074fff73a6b532" tvg-chno="2000",BBC R4 FM
http://192.168.0.1:9981/stream/channelid/271797700?profile=pass
...

$ curl  http://user:pass@192.168.0.1:9981/playlist/ticket/channels
#EXTINF:-1 tvg-id="4d422960b4d45e8e007eaa8b3bf58190" tvg-chno="69",QUEST+1
http://192.168.0.1:9981/stream/channelid/1613316685?ticket=5609a7022c1a7b5f8ac8b22aff2638a3efd78cdc&profile=pass
#EXTINF:-1 tvg-id="85f9c040b03cd5496a2d950b2380d793" tvg-chno="70",Quest Red+1
http://192.168.0.1:9981/stream/channelid/1086388613?ticket=d89df723230fa791e11b1e17cc1962e55fe73230&profile=pass
...

$ curl  http://192.168.0.1:9981/playlist/e2/channelname/QUEST
#NAME QUEST
#SERVICE 1:0:0:0:0:0:0:0:0:0:http://192.168.1.1:9981/stream/channelid/344789476&profile=pass:QUEST
#DESCRIPTION QUEST

$ curl  http://192.168.0.1:9981/playlist/satip/channelname/QUEST
#EXTINF:-1,QUEST
http://192.168.1.1:9981/stream/channelid/344789476?profile=pass

$ curl  http://192.168.1.0:9981/playlist/recordings
#EXTM3U
#EXTINF:1800,The Repair Shop
#EXT-X-TARGETDURATION:1800
#EXT-X-STREAM-INF:PROGRAM-ID=da01a7de69dfd8d09241c045d6fbaeb6,BANDWIDTH=5115
#EXT-X-PROGRAM-DATE-TIME:2018-03-23T18:30:00+0000
http://192.168.0.1:9981/dvrfile/da01a7de69dfd8d09241c045d6fbaeb6
#EXTINF:1800,The Hitchhiker's Guide to the...
#EXT-X-TARGETDURATION:1800
#EXT-X-STREAM-INF:PROGRAM-ID=74cb4b64f55afca54725d8ab0a3d3e00,BANDWIDTH=0
#EXT-X-PROGRAM-DATE-TIME:2018-04-05T18:30:00+0100
http://192.168.0.1:9981/dvrfile/74cb4b64f55afca54725d8ab0a3d3e00
```

### pvrinfo

Used by [simple.html](other-functions.md#simple.html).

### redir

Used internally for theme selection?

### satip\_server

Outputs one of two files describing the SAT>IP server and the services available from it. SAT>IP server must be compiled into Tvheadend.

```
$ curl  http://192.168.0.1:9981/satip_server/desc.xml
$ curl  http://192.168.0.1:9981/satip_server/satip.m3u
```

### simple.html

A rudimentary user interface to TVHeadend. It shows the contents of the recorder log (both completed and future recordings) and allows entries to be cancelled or deleted. A search box allows the EPG to be scanned for matching entries; clicking on an entry opens an information page which contains a button allowing the event to be recorded. Requires RECORDER privilege.

### special/srvid2

Outputs details of encrypted services. Each item contains:

* Service ID
* CA ID
* CA provider ID
* Service name
* Service type
* Service provider name

```
2968:0B00|TRP 1|TV||ASTRA
177B:0963,0961,0960|Crime+Inv+1|TV||ASTRA
0E1F:0963,0961,0960|Virgin Two|TV||ASTRA
13FB:0963,0961,0960|VICE|TV||ASTRA
2584:0963,0961,0960|Virgin One+1|TV||ASTRA
1789:0963,0961,0960|Real Lives+1|TV||ASTRA
15AE:0963,0961,0960|History+1|TV||ASTRA
15AF:0963,0961,0960|History2|TV||ASTRA
15AD:0963,0961,0960|History|TV||ASTRA
15B3:0963,0961,0960|Nat Geo Wild|TV||ASTRA
15B1:0963,0961,0960|Nat Geo+1|TV||ASTRA
15B0:0963,0961,0960|Nat Geo|TV||ASTRA
```

### state

Outputs the TVHeadend version number and a (text) list of channels. This function requires Admin privilege.

The binary hash is only filled-in if the server runs on an x86 processor.

```
$ curl  'http://user:pass@192.168.0.1:9981/state'

Tvheadend 4.3-1215~g5782d8c14-dirty  Binary SHA1: 0000000000000000000000000000000000000000

Channels
----------------------------------------------
tru TV (13183175)
  refcount = 0
  number = 156
  icon = <none set>

ITV3 (54665543)
  refcount = 0
  number = 114
  icon = <none set>
...
```

### status.xml

Outputs the current status of the server, including CPU load average, recordings in progress (or minutes to the next recording) and the number of active subscriptions. Needs 'Web interface' or 'Recorder' privilege.

```
<?xml version="1.0"?>
 <currentload>
  <systemload>0.000000,0.000000,0.000000</systemload>
  <recordings>
   <recording>
    <next>465</next>
   </recording>
  </recordings>
  <subscriptions>0</subscriptions>
 </currentload>
```

```
<?xml version="1.0"?>
<currentload>
 <systemload>0.390000,0.090000,0.030000</systemload>
 <recordings>
  <recording>
   <start>
    <date>2020/05/24</date>
    <time>09:00</time>
    <unixtime>1590307200</unixtime>
    <extra_start>60</extra_start>
   </start>
   <stop>
    <date>2020/05/24</date>
    <time>13:00</time>
    <unixtime>1590321600</unixtime>
    <extra_stop>300</extra_stop>
   </stop>
   <title>Soft Rock Classics! 1980-1989</title>
   <status>Recording</status>
  </recording>
 </recordings>
 <subscriptions>1</subscriptions>
</currentload>
```

### stream

Starts the streaming of live data from a channel, service or mux. The parameters which can be applied depend on the source:

```
 http://192.168.0.1:9981/stream/channelid/<chid>
 http://192.168.0.1:9981/stream/channel/<uuid>
 http://192.168.0.1:9981/stream/channelnumber/<channelnumber>
 http://192.168.0.1:9981/stream/channelname/<channelname>
```

* `profile`. The streaming profile to use. If the specified profile does not exist or can not be used the 'htsp' profile is used if available.
* `qsize`. Streaming buffer size. Default is 1500000 bytes.
* `User-Agent`. Use unknown.

```
 http://192.168.0.1:9981/stream/service/<uuid>
```

* `profile`. The streaming profile to use. If the specified profile does not exist or can not be used the 'htsp' profile is used if available.
* `qsize`. Streaming buffer size. Default is 1500000 bytes.
* `descramble`. If set to 0 Tvheadend does not descramble the service.
* `emm`. Unknown. Default is 0, set to 1 to activate.
* `User-Agent`. Use unknown.

```
 http://192.168.0.1:9981/stream/mux/<muxid>
```

* `qsize`. Streaming buffer size. Default is 10000000 bytes.
* `pids`. A comma-separated list of pids to stream, or the word 'all' to stream the raw mux. The default is to stream all.

### udpstream

Controls the streaming of live data from a channel or service to a UDP address and port. This function requires Tvheadend version 4.3.2038 or later.

The following parameters are mandatory:

* `address`. The IP address of the device to receive the UDP stream.
* `port`. The destination port address.

The remaining parameters for the `start` function depend on the source:

```
 http://192.168.0.1:9981/udpstream/<start|stop>/channelid/<chid>
 http://192.168.0.1:9981/udpstream/<start|stop>/channel/<uuid>
 http://192.168.0.1:9981/udpstream/<start|stop>/channelnumber/<channelnumber>
 http://192.168.0.1:9981/udpstream/<start|stop>/channelname/<channelname>
```

* `profile`. The streaming profile to use. If the specified profile does not exist or can not be used a 'Not Allowed' error is output.
* `qsize`. Streaming buffer size. Default is 1500000 bytes.
* `User-Agent`. Use unknown.

```
 http://192.168.0.1:9981/udpstream/<start|stop>/service/<uuid>
```

* `profile`. The streaming profile to use. If the specified profile does not exist or can not be used a 'Not Allowed' error is output.
* `qsize`. Streaming buffer size. Default is 1500000 bytes.
* `descramble`. If set to 0 Tvheadend does not descramble the service.
* `emm`. Default is 0, set to 1 to activate.
* `User-Agent`. Use unknown.

### xmltv

Outputs the EPG in XML format, filtered in various ways.

```
$ curl http://192.168.0.1:9981/xmltv/channelid/<channelid>
$ curl http://192.168.0.1:9981/xmltv/channelnumber/<channelnumber>
$ curl http://192.168.0.1:9981/xmltv/channelname/<channelname>
$ curl http://192.168.0.1:9981/xmltv/channel/<channelUUID>
$ curl http://192.168.0.1:9981/xmltv/tagid/<tagid>
$ curl http://192.168.0.1:9981/xmltv/tagname/<tagname>
$ curl http://192.168.0.1:9981/xmltv/tag/<tagUUID>
```

The final variation lists the complete EPG together with a channel list. Example:

```
$ curl  http://192.168.0.1:9981/xmltv/channels

<?xml version="1.0" encoding="utf-8" ?>
<!DOCTYPE tv SYSTEM "xmltv.dtd">
<tv generator-info-name="TVHeadend-4.3-1670~ge37c696de-dirty" source-info-name="tvh-Tvheadend">
<channel id="7e7b77801531c803f5ce8f4d5003f44c">
  <display-name>Channel 5+1</display-name>
</channel>
...
<programme start="20181231151500 +0000" stop="20181231161500 +0000" channel="7e7b77801531c803f5ce8f4d5003f44c">
  <title lang="eng">Dirty Dancing</title>
  <desc lang="eng">Classic starring Patrick Swayze and Jennifer Grey. A spoiled 17-year-old learns a lot about life from the hotel dance instructor during a family summer holiday. (1987)[S]</desc>
  <category lang="en">Movie / Drama</category>
</programme>
...
</tv>
```

If Persistent Authentication is in use (TVHeadend versions > 4.3.1485), the auth code must be appended to the URL as a parameter.
