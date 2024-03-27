# Debugging

## Trace Options <a href="#trace-options" id="trace-options"></a>

The following options can be passed to tvheadend to provide detailed debugging information while the application is running. Trace debugging has to be enabled at build time with`--enable-debugging` and can be specified in a CLI command, e.g. `tvheadend -u hts -g video --trace <module>` or in the web interface (_Configuration -> Debugging_).

Multiple options can be used, e.g. `–-trace cwc,dvr,linuxdvb`

```
all
access
bouquet
capmt
cwc
descrambler
diseqc
dvbcam
dvr
eit
en50221
epg
epggrab
fastscan
fsmonitor
gtimer
htsp
httpc
idnode
linuxdvb
main
mkv
mpegts
opentv
parser
pass
psi
satip
satips
scanfile
sdt
service
service_mapper
settings
subscription
tcp
thread
time
timeshift
transcode
tsfile
tvhdhomerun
upnp
```
