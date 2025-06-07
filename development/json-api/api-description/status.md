# Status

Lists statistics of input sources and connections. ADMIN privilege is required for all these functions.

### status/connections

Lists currently-connected client devices.

```
{
   "totalCount" : 1,
   "entries" : [
      {
         "id" : 1,
         "started" : 1508668447,
         "server_port" : 9982,
         "server" : "x.x.x.x",
         "type" : "HTSP",
         "peer" : "x.x.x.y",
         "user" : "xxxxxx",
         "peer_port" : 57496
      }
   ]
}
```

### status/subscriptions

Lists currently-active subscriptions.

```
{
   "entries" : [
      {
         "errors" : 0,
         "title" : "epggrab",
         "in" : 85222,
         "total_in" : 25162474,
         "total_out" : 25162474,
         "id" : 75,
         "out" : 85222,
         "service" : "Silicon Labs Si2168 : DVB-T #0/Sandy/690MHz/Raw PID Subscription",
         "state" : "Running",
         "start" : 1508763840
      }
   ],
   "totalCount" : 1
}
```

### status/inputs

Lists statistics of input devices.

For DVB-T and DVB-S tuners at least, the signal and SNR values are only non-zero while TVH is actively using the device. Some items may be missing if the device is idle.

```
{
   "entries" : [
      {
         "ec_block" : 0,
         "uuid" : "20f11bcaaf93afb5fc13cce31278494e",
         "signal_scale" : 2,
         "weight" : 100,
         "cc" : 1,
         "ber" : 0,
         "tc_block" : 0,
         "input" : "Montage Technology M88DS3103 #0 : DVB-S #0",
         "tc_bit" : 0,
         "unc" : 0,
         "te" : 0,
         "bps" : 2257504,
         "subs" : 1,
         "ec_bit" : 0,
         "pids" : [
            0,
            1,
            16,
            17,
            18,
            269,
            5700,
            5701,
            5703,
            5704
         ],
         "stream" : "10773H in DVB-S Network",
         "snr" : 14149,
         "signal" : -75649,
         "snr_scale" : 2
      }
   ],
   "totalCount" : 1
}
```

The meaning of the statistics is below. Not all input sources provide all of the values.

|               |                                    |
| ------------- | ---------------------------------- |
| ber           | Bit Error Rate                     |
| bps           | Bandwidth (bits/second)            |
| cc            | Continuity Errors                  |
| ec\_bit       | Bit Error Count                    |
| ec\_block     | Block Error Count                  |
| pids          | List of pids present in the stream |
| signal        | Signal Strength (see below)        |
| signal\_scale | See below                          |
| snr           | Signal/Noise Ratio (see below)     |
| snr\_scale    | See below                          |
| stream        | Stream (multiplex) name            |
| subs          | Subscribers                        |
| tc\_bit       | Total Bit Error Count              |
| tc\_block     | Total Block Error Count            |
| te            | Transport Errors                   |
| unc           | Uncorrected Blocks                 |
| weight        | Weight                             |

For signal\_scale and snr\_scale, a value of 1 indicates that the corresponding signal or SNR reading is relative; 65535 = 100%. A value of 2 indicates the reading is absolute; 1000 = 1dB. A value of 0 indicates that the reading is not available or not valid.

The "pids" data is only present in TVH versions 4.3.1420 and later.

### status/inputclrstats

Resets the input counters to zero.

* `uuid` The uuid of the input device from [status/inputs](status.md#status-inputs). More than one uuid can be specified - syntax?

### connections/cancel



Disconnects one or more clients.

* `id` ids of the connections, obtained from [status/connections](status.md#status-connections). If set to 'all' then all connections are cancelled (new in 4.3.1680).

### status/activity

Provide information required for assessing the suitability for entering low-power mode and a suitable time for reawakening.  For example, then TVH is used as part of an appliance configuration.

```json
{
  "current_time": 1748659324,
  "next_activity": 1748659500,
  "activities": {
    "dvr": 1748764623,
    "ota_grabber": 1748659500,
    "int_grabber": 0,
    "mux_scheduler": 1748725200
  },
  "subscription_count": 1,
  "connection_count": 2
}
```

For finer analysis and control, the 'activities' property contains individual scheduling times for the following activities:

* DVR Recordings
* OTA EPG Grabber
* Internal EPG Grabber
* Mux Scheduler

Times are presented as standard Unix epoch values. A value of zero indicates that nothing for that activity type is currently scheduled.

It should be noted that the times provided are strictly from the point of view of TVH internal activities and that the calling program must take into account operating system and hardware boot times when determining the precise time to reawaken the system.

Times are only reported for the EPG grabbers if there are enabled grabbers of that type. Likewise, only enabled mux schedulers are reported.

DVR recordings in progress are also included, therefore, the reported DVR time may be in the past.

The connection and subscription counts are duplications of the summaries provided by the ‘status/connections’ and ‘status/subscriptions’ API calls and are included here in order to provide a single consolidated API call for assessing the suitability for entering low-power mode.

Requires v4.3-2405.
