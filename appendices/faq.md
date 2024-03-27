# FAQ

### Q: How do I get a playlist for all my channels? <a href="#q-how-do-i-get-a-playlist-for-all-my-channels" id="q-how-do-i-get-a-playlist-for-all-my-channels"></a>

Tvheadend can generate a playlist of all your mapped services (channels). You can download it from the webui at `http://<ip>:<port>/playlist`, e.g. `http://192.168.0.2:9981/playlist`.

### Q: Why am I getting a playlist when trying to view/stream a channel? <a href="#q-why-am-i-getting-a-playlist-when-trying-to-viewstream-a-channel" id="q-why-am-i-getting-a-playlist-when-trying-to-viewstream-a-channel"></a>

By default Tvheadend’s _Play_ links are playlists, although not all players accept them (e.g. Media Player Classic Home Cinema). You can bypass this by removing the `/play/` path from the url.

### Q: Tvheadend has scanned for services but some rows in the Service Name column are blank, is that normal? <a href="#q-tvheadend-has-scanned-for-services-but-some-rows-in-the-service-name-column-are-blank-is-that-norm" id="q-tvheadend-has-scanned-for-services-but-some-rows-in-the-service-name-column-are-blank-is-that-norm"></a>

Yes, not all services are given a name by providers. These services are usually hidden for a reason and may be used for things like encrypted guide data for set-top boxes, interactive services, and so on. If you do not see any service names at all this may indicate an issue with your hardware or configuration.

### Q: I get a blank page when trying to view the web interface! <a href="#q-i-get-a-blank-page-when-trying-to-view-the-web-interface" id="q-i-get-a-blank-page-when-trying-to-view-the-web-interface"></a>

This usually happens when Tvheadend is installed incorrectly. On Debian and Ubuntu systems check  the web interface path `/usr/share/tvheadend/src/webui/static/` exists and isn’t empty. On other distros the path may be different.

### Q: Why can’t I see my tuners in Tvheadend’s interface? <a href="#q-why-cant-i-see-my-tuners-in-tvheadends-interface" id="q-why-cant-i-see-my-tuners-in-tvheadends-interface"></a>

This is normally because they are not installed properly. Check syslog/dmesg (e.g. `dmesg | grep dvb`) and see that you have startup messages that indicate whether or not the tuners have initialized properly. Similarly, check `/dev/dvb` to see if the block device files used to communicate with the tuner have been created correctly?. The other major cause of this issue is when you run Tvheadend as a user that does not have permissions to access the tuners, e.g. not a member of the _video_ group.
