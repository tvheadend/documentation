# Input

List details of input devices. ADMIN privilege is required for these functions.

### hardware/tree

Lists the parameters, options and settings for input devices.

* `uuid` (Required). If set to 'root', the top-level details of the input device(s) are shown. If the uuid of a device (obtained from the top-level details) is submitted, full information is shown similar to Configuration -> DVB Inputs -> TV Adaptors.
* `root` Function obscure.

```
[
   {
      "leaf" : 0,
      "uuid" : "efe25f71ce456f99bb5a1b600b2e8143",
      "class" : "linuxdvb_adapter",
      "params" : [
         {
            "nosave" : true,
            "caption" : "Active",
            "id" : "active",
            "default" : false,
            "rdonly" : true,
            "noui" : true,
            "value" : true,
            "type" : "bool"
         },
         {
            "caption" : "Device path",
            "type" : "str",
            "id" : "rootpath",
            "rdonly" : true,
            "default" : "",
            "value" : "/dev/dvb/adapter0",
            "description" : "Path used by the device."
         }
      ],
      "text" : "/dev/dvb/adapter0 [Montage Technology M88DS3103 #0]",
      "caption" : "LinuxDVB adapter",
      "id" : "efe25f71ce456f99bb5a1b600b2e8143",
      "event" : "linuxdvb_adapter"
   }
]
```

### hardware/satip/discover

Triggers a discovery process for SAT>IP servers, as Configuration -> General -> SAT>IP Server -> Discover SAT>IP Servers in the GUI. This function is only available if SAT>IP client functionality has been compiled into TVHeadend.

The `op` parameter must be set to `all`.

Example: `/api/hardware/satip/discover?op=all`
