# General

HTSP is a TCP based protocol primarily intended for streaming of live TV and related meta data such as channels, group of channels (called tags in HTSP) and electronic program guide (EPG) information.

The transmission and reception of a channel over HTSP is referred to as a subscription. A single HTSP session can handle as many concurrent subscriptions as the bandwidth and CPU permits.

The HTSP server in tvheadend has a payload-aware scheduler for prioritizing more important packets (such as I-frames) before less important ones (such as B-frames). This makes HTSP suitable for long-distance transmissions and/or paths with non-perfect delivery.\
(It has been tested with a server in Stockholm and the client in Berlin).

For information about the HTSP wire format please refer to the following page: [htsmsg-binary-format.md](htsmsg-binary-format.md "mention")

If you're looking to develop a new client, there are several existing client implementations from which you might be able to gain knowledge:

* [Kodi](https://github.com/kodi-pvr/pvr.hts)
* [Showtime](https://github.com/andoma/showtime/tree/master/src/backend/htsp)
* [TVHGuide](https://github.com/john-tornblom/TVHGuide)
* [PyHTSP](https://github.com/adamsutton/tvheadend/tree/master/lib/py/tvh/htsp.py) (This is a demo client and is WIP, it has limited functionality).



