# Creating a Mux Dump

## Introduction

A 'Mux Dump' is a special recording where Tvheadend records the entire transmission of a single broadcaster rather than just a specific channel. Mux dumps can be useful for development and debugging purposes.

For most purposes, a mux dump lasting between 1 and 2 minutes should be suitable, however, if you are requested to provide a mux dump, ask the requester to indicate how long the mux dump should be for their purposes.

## Performing a Mux Dump

In order to perform a mux dump, you first have to obtain the UUID of the mux that you wish to dump. The [UUID](development/object-id-representation.md) is a block of text, 32 characters long, containing only numbers and lower case letters.

### Finding the UUID

### WebUI Methods

There are many ways to do this, however, one of the easiest is to use the WebUI to navigate to '`Configuration - DVB Inputs - Muxes`'. For each mux listed, there will be a 'Play' icon.

The process will be different between specific browsers, however, the 'Play' icon will always point to a link that contains the UUID of the mux somewhere.

* Simply moving your mouse cursor over this icon should show the link destination, containing the mux UUID, somewhere in the browser window.
* Right-clicking on the icon and selection 'Copy link' (or similar) should place some text into your clipboard that contains the UUID.\
  \
  For example: `http://<TVH_IP>:9981/play/ticket/stream/mux/176838fd011c233adfa42d8a07f9ddba?title=177.5MHz%20%2F%20DVB-T%20Network` \
  \
  Using this method, the UUID is '176838fd011c233adfa42d8a07f9ddba' can can be located between '/mux/' and the question mark.
* Also, right-clicking on the icon and selecting 'Save link as' (or similar) should provide you with a prompt for a file name. The default file name provided by your browser should contain the UUID of the mux.\
  \
  For example: `d32ef9ef9c67e0552465f6a86caf1d77.m3u` \
  \
  Using this method, the UUID is 'd32ef9ef9c67e0552465f6a86caf1d77' and consists of all of the characters before the '.m3u' in the file name.

#### API Direct Method

A list (in JSON format) of all muxes known to the system can be obtained by issuing the following [API](development/json-api/api-description/mpegts.md#mpegts-mux-grid) command:

`http://<TVH_IP>:9981/api/mpegts/mux/grid`

This list will contain all muxes, enabled and disabled, successfully tuned or not. Each JSON object will represent one mux. You will need to search through this list for the mux on the frequency that you seek and then take note of the UUID associate with that frequency.

### Creating the Mux Dump

#### VLC

If you already have VLC configured as your default m3u application, simply click on the 'Play' icon described above and once VLC starts, press the 'Record' icon in VLC. Manually stop the recording after the required duration has elapsed.

Even if VLC is not your default m3u application, you can still use VLC by opening the '`Media - Open Network Stream`' and pasting the link to the mux that you wish to dump as follows:

`http://<TVH_IP>:9981/stream/mux/<MUX_UUID>`

**Hint:** If you used the 'Copy link' method described above, you can simply paste that link directly into the '`Network URL`' requested by VLC.

#### Linux Command Line - curl

The following curl command will dump 90 seconds of the specified mux.

`curl -m 90 http://<TVH_IP>:9981/stream/mux/<MUX_UUID> > sample_file.ts`

#### Linux Command Line - wget

The following wget command initiate a dump of the specified mux. However, the dump will have to be manually stopped using CTRL-C when the required time has elapsed.

`wget http://<TVH_IP>:9981/stream/mux/<MUX_UUID> -O sample_file.ts`

### Transferring the Mux Dump

A mux dump file is normally too large to email or post to the forum.  It is up to the requester and user to agree a method for transferring the file.  There are, however, several free peer-to-peer file transfer options to choose from.
