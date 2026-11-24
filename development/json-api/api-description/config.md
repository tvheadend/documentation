# Config

ADMIN privilege is required for all of these functions except config/capabilities and serverinfo.

### config/capabilities

Returns a list of some compile-time options which were used to build the software. Requires either 'Web Interface' or 'HTSP Interface' privilege.

```
[
   "caclient",
   "tvadapters",
   "imagecache",
   "timeshift",
   "trace",
   "libav"
]
```

### config/load

Lists the details, descriptions, defaults and current values of the items in the GUI screen Configuration -> General -> Base. See [Common Parameters](common-parameters.md) for details of selection parameters.

### config/save

**Untested.** Updates the server from an object in the format produced by [config/load](config.md#config-load).

* `node` The JSON object.

### memoryinfo/class

Lists the details and descriptions of items in the TVH GUI screen Configuration -> Debugging -> Memory Information Entries.

### memoryinfo/grid

Lists details of in-memory objects. See [Common Parameters](common-parameters.md) for details of selection parameters.

```
{
   "entries" : [
      {
         "peak_count" : 17154,
         "name" : "EPG Broadcasts",
         "uuid" : "a1af1bc4f29ba28104e71a540465f250",
         "count" : 17154,
         "peak_size" : 6235792,
         "size" : 6235792
      },
      {
         "peak_count" : 3285,
         "peak_size" : 369303,
         "count" : 3285,
         "size" : 369303,
         "name" : "EPG Series Links",
         "uuid" : "823a78a3bcd05b688c59871455da6399"
      },
      {
         "count" : 11514,
         "peak_size" : 5015593,
         "size" : 5015593,
         "name" : "EPG Episodes",
         "uuid" : "5c666eea1ec3de4bbb9a11f60116b258",
         "peak_count" : 11514
      }, ...
   ],
   "total" : 19
}
```

### pathlist

Lists all of the api functions supported by the server.

```
[
   "access/entry/class",
   "access/entry/create",
   "access/entry/grid",
   "access/entry/userlist", ...
]
```

### serverinfo

Lists information about the server including the software and api version numbers. "Build\_timestamp" is only available from version 4.3-2911.

```
{
  "sw_version": "4.3-2964~gfce1dbfff-dirty",
  "api_version": 20,
  "name": "Tvheadend",
  "webroot" : "/testserver",
  "capabilities": [
    "caclient",
    "tvadapters",
    "trace"
  ],
  "build_timestamp": "2026-11-24T14:34:12+0000"
}
```

### serverinfo/build

Lists the input and output of the configure step of the server build. Requires version 4.3.2911 or later. The output string contains embedded newline characters which have been removed here for readability.

```
{
  "build_config": "Configure arguments:
    --prefix=/usr --disable-libav --disable-libvpx --disable-libvpx_static --enable-libx265 --disble-libx264_static --disable-libx265_static --disable-libvorbis --disable-libvorbis_static --disable-libtheora_static --disable-libtheora --disable-libopus --disable-libopus_static --disable-ffmpeg_static --disable-libfdkaac-static --disable-hdhomerun_static --disable-hdhomerun_client --disable-hdhomerun_server --disable-satip_server --disable-satip_client --disable-imagecache --enable-dvbscan --disable-cwc --disable-cccam --disable-capmt --disable-constcw --enable-ddci --enable-iptv --disable-avahi
    Compiler:
      Using C compiler:                        cc
        Build for arch:                          aarch64
        Binaries:
          Using PYTHON:                            python
          Using GZIP:                              gzip
          Using BZIP2:                             bzip2
        Options:
          pie                                      yes
          ccdebug                                  no
          cardclient                               no
          cwc                                      no
          cccam                                    no
          capmt                                    no
          constcw                                  no
          linuxdvb                                 yes
          satip_server                             no
          satip_client                             no
          hdhomerun_client                         no
          hdhomerun_server                         no
          hdhomerun_static                         no
          iptv                                     yes
          tsfile                                   yes
          dvbscan                                  yes
          timeshift                                yes
          trace                                    yes
          avahi                                    no
          zlib                                     yes
          libav                                    no
          vue_build                                yes
          vue_cache                                no
          ffmpeg_static                            no
          libx264                                  yes
          libx264_static                           yes
          libx265                                  yes
          libx265_static                           no
          libvpx                                   no
          libvpx_static                            no
          libtheora                                no
          libtheora_static                         no
          libvorbis                                no
          libvorbis_static                         no
          libfdkaac                                no
          libfdkaac_static                         yes
          libopus                                  no
          libopus_static                           no
          nvenc                                    no
          vaapi                                    no
          mmal                                     no
          omx                                      no
          inotify                                  yes
          epoll                                    yes
          pcre                                     no
          pcre2                                    yes
          uriparser                                no
          ccache                                   no
          tvhcsa                                   no
          bundle                                   no
          pngquant                                 no
          kqueue                                   no
          dbus_1                                   yes
          android                                  no
          gtimer_check                             no
          slow_memoryinfo                          no
          libsystemd_daemon                        no
          pcloud_cache                             yes
          ddci                                     yes
          cclang_threadsan                         yes
          gperftools                               no
          execinfo                                 yes
          W_unused_result                          yes
          f_stack_protector                        yes
          f_stack_protector_strong                 yes
          f_stack_check                            yes
          f_PIE                                    yes
          strlcat                                  yes
          strlcpy                                  yes
          fdatasync                                yes
          getloadavg                               yes
          atomic32                                 yes
          atomic64                                 yes
          atomic_time_t                            yes
          atomic_ptr                               yes
          bitops64                                 yes
          lockowner                                yes
          qsort_r                                  yes
          time_ld                                  yes
          gmtoff                                   yes
          recvmmsg                                 yes
          sendmmsg                                 yes
          ifnames                                  yes
          py_gzip                                  yes
          bin_pkg_config                           yes
          bin_xgettext                             yes
          bin_msgmerge                             yes
          bin_gzip                                 yes
          bin_bzip2                                yes
          ssl                                      yes
          linuxdvbapi                              yes
          linuxdvb_ca                              yes
          inotify_h                                yes
          inotify_init1                            yes
          epoll_create1                            yes
          mpegts                                   yes
          mpegts_dvb                               yes  
        Packages:
          openssl                                  4.1.0
          zlib                                     1.4
          libpcre2-8                               10.49
          dbus-1                                   1.16.4
        Installation paths:
          Prefix:                                  /usr
          Binaries:                                ${prefix}/bin
          Libraries:                               ${prefix}/lib
          Data files:                              ${prefix}/share
          Man pages:                               ${datadir}/man"
}

```
