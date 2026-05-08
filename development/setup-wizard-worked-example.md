---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Setup Wizard Worked Example

### Introduction

Almost every TVH system will be slightly different. These worked examples are taken from a system configured for English with dual DVB-T/DVB-C tuners with only DVB-T tuners connected. One IPTV playlist was also loaded.  They should be used as a guide as to what to expect rather than definitive documentation.

#### hello

`/api/wizard/hello/load`

```json
{
  "entries": [
    {
      "uuid": "00000000000000000000000000000000",
      "id": "00000000000000000000000000000000",
      "text": "00000000000000000000000000000000",
      "caption": "Welcome",
      "class": "wizard_hello",
      "event": "wizard_hello",
      "params": [
        {
          "id": "ui_lang",
          "type": "str",
          "caption": "Language",
          "description": "Select the default user interface language. This can be overridden later in \"Access Entries\" on a per-user basis.",
          "default": "",
          "enum": {
            "type": "api",
            "uri": "language/ui_locale"
          },
          "group": 1,
          "value": ""
        },
        {
          "id": "epg_lang1",
          "type": "str",
          "caption": "Language 1",
          "description": "Select high priority (default) EPG language.",
          "default": "",
          "enum": {
            "type": "api",
            "uri": "language/locale"
          },
          "group": 2,
          "value": ""
        },
        {
          "id": "epg_lang2",
          "type": "str",
          "caption": "Language 2",
          "description": "Select medium priority EPG language.",
          "default": "",
          "enum": {
            "type": "api",
            "uri": "language/locale"
          },
          "group": 2,
          "value": ""
        },
        {
          "id": "epg_lang3",
          "type": "str",
          "caption": "Language 3",
          "description": "Select low priority EPG language.",
          "default": "",
          "enum": {
            "type": "api",
            "uri": "language/locale"
          },
          "group": 2,
          "value": ""
        },
        {
          "id": "icon",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "static/img/logobig.png"
        },
        {
          "id": "description",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "__Welcome to Tvheadend, Your TV Streaming Server and Video Recorder__ \n\nLet's start by configuring the basic language settings. Please select the default user interface and EPG language(s).\n\n* This wizard is optional, and can be cancelled at any time, but recommended for new users.\n* Running this wizard on existing configurations is NOT a good idea as it may lead to confusion, misconfiguration and unexpected features! ;)\n* The wizard will restart and reload the interface in your chosen language, unfortunately not all translations are available/complete.\n* If you get stuck at any point and need a little more information, press [Help].\n"
        },
        {
          "id": "page_next_login",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        }
      ],
      "meta": {
        "caption": "Welcome",
        "class": "wizard_hello",
        "event": "wizard_hello",
        "groups": [
          {
            "number": 1,
            "name": "Web interface"
          },
          {
            "number": 2,
            "name": "EPG Language (priority order)"
          }
        ],
        "props": [
          {
            "id": "ui_lang",
            "type": "str",
            "caption": "Language",
            "description": "Select the default user interface language. This can be overridden later in \"Access Entries\" on a per-user basis.",
            "default": "",
            "enum": {
              "type": "api",
              "uri": "language/ui_locale"
            },
            "group": 1
          },
          {
            "id": "epg_lang1",
            "type": "str",
            "caption": "Language 1",
            "description": "Select high priority (default) EPG language.",
            "default": "",
            "enum": {
              "type": "api",
              "uri": "language/locale"
            },
            "group": 2
          },
          {
            "id": "epg_lang2",
            "type": "str",
            "caption": "Language 2",
            "description": "Select medium priority EPG language.",
            "default": "",
            "enum": {
              "type": "api",
              "uri": "language/locale"
            },
            "group": 2
          },
          {
            "id": "epg_lang3",
            "type": "str",
            "caption": "Language 3",
            "description": "Select low priority EPG language.",
            "default": "",
            "enum": {
              "type": "api",
              "uri": "language/locale"
            },
            "group": 2
          },
          {
            "id": "icon",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "description",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_next_login",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          }
        ]
      }
    }
  ]
}
```

The properties involving languages provide an ENUM with a URI from which to obtain validation data for the GUI drop-down list.

`/api/wizard/hello/save`

The following shows the response for selecting English (GB) as the UI language and French, German and Indonesian as the EPG language preferences.

```json
{
  "ui_lang": "eng_GB",
  "epg_lang1": "fre",
  "epg_lang2": "ger",
  "epg_lang3": "ind",
  "uuid": "00000000000000000000000000000000"
}
```

#### login

`/api/wizard/login/load`

```json
{
  "entries": [
    {
      "uuid": "00000000000000000000000000000000",
      "id": "00000000000000000000000000000000",
      "text": "00000000000000000000000000000000",
      "caption": "Access Control",
      "class": "wizard_login",
      "event": "wizard_login",
      "params": [
        {
          "id": "network",
          "type": "str",
          "caption": "Allowed network",
          "description": "Enter allowed network prefix(es). You can enter a comma-separated list of prefixes here.",
          "default": "",
          "group": 1,
          "value": ""
        },
        {
          "id": "admin_username",
          "type": "str",
          "caption": "Admin username",
          "description": "Enter an administrator username. Note: do not use the same username as the superuser backdoor account.",
          "default": "",
          "group": 2,
          "value": ""
        },
        {
          "id": "admin_password",
          "type": "str",
          "caption": "Admin password",
          "description": "Enter an administrator password.",
          "default": "",
          "group": 2,
          "value": ""
        },
        {
          "id": "username",
          "type": "str",
          "caption": "Username",
          "description": "Enter a non-admin user username.",
          "default": "",
          "group": 3,
          "value": ""
        },
        {
          "id": "password",
          "type": "str",
          "caption": "Password",
          "description": "Enter a non-admin user password.",
          "default": "",
          "group": 3,
          "value": ""
        },
        {
          "id": "icon",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "static/img/logobig.png"
        },
        {
          "id": "description",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "__Enter Access Control Details to Secure Your System__ \n\nThe first part of this covers the network details for address-based access to the system; for example, 192.168.1.0/24 to allow local access only to 192.168.1.x clients, or 0.0.0.0/0 or empty value for access from any system.\n\nThis works alongside the second part, which is a familiar username/password combination, so provide these for both an administrator and regular (day-to-day) user.\n"
        },
        {
          "id": "page_prev_hello",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "page_next_network",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        }
      ],
      "meta": {
        "caption": "Access Control",
        "class": "wizard_login",
        "event": "wizard_login",
        "groups": [
          {
            "number": 1,
            "name": "Network access"
          },
          {
            "number": 2,
            "name": "Administrator login"
          },
          {
            "number": 3,
            "name": "User login"
          }
        ],
        "props": [
          {
            "id": "network",
            "type": "str",
            "caption": "Allowed network",
            "description": "Enter allowed network prefix(es). You can enter a comma-separated list of prefixes here.",
            "default": "",
            "group": 1
          },
          {
            "id": "admin_username",
            "type": "str",
            "caption": "Admin username",
            "description": "Enter an administrator username. Note: do not use the same username as the superuser backdoor account.",
            "default": "",
            "group": 2
          },
          {
            "id": "admin_password",
            "type": "str",
            "caption": "Admin password",
            "description": "Enter an administrator password.",
            "default": "",
            "group": 2
          },
          {
            "id": "username",
            "type": "str",
            "caption": "Username",
            "description": "Enter a non-admin user username.",
            "default": "",
            "group": 3
          },
          {
            "id": "password",
            "type": "str",
            "caption": "Password",
            "description": "Enter a non-admin user password.",
            "default": "",
            "group": 3
          },
          {
            "id": "icon",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "description",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_prev_hello",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_next_network",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          }
        ]
      }
    }
  ]
}

```

`/api/wizard/login/save`

```json
{
  "network": "1.2.3.4",
  "admin_username": "admin_username",
  "admin_password": "admin_password",
  "username": "user_username",
  "password": "user_password",
  "uuid": "00000000000000000000000000000000"
}
```

#### network

`/api/wizard/network/load`

```json
{
  "entries": [
    {
      "uuid": "00000000000000000000000000000000",
      "id": "00000000000000000000000000000000",
      "text": "00000000000000000000000000000000",
      "caption": "Tuner and Network",
      "class": "wizard_network",
      "event": "wizard_network",
      "params": [
        {
          "id": "icon",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "static/img/logobig.png"
        },
        {
          "id": "description",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "__Tuner and Network__ \n\nNow let's get your tuners configured. Go ahead and select a network for each of the tuners you would like to use. If you don't assign a network to a tuner it __won't__ be used.\n"
        },
        {
          "id": "page_prev_login",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "page_next_muxes",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "tuner1",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 1,
          "value": "IPTV #1"
        },
        {
          "id": "tunerid1",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "c2de754ac46e3ae8cf106893a4303a96"
        },
        {
          "id": "network1",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "iptv_auto_network",
              "val": "IPTV Automatic Network"
            }
          ],
          "group": 1,
          "value": ""
        },
        {
          "id": "tuner2",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 2,
          "value": "IPTV #2"
        },
        {
          "id": "tunerid2",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "abf7a884f404c9a312d5961ab03eb7de"
        },
        {
          "id": "network2",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "iptv_auto_network",
              "val": "IPTV Automatic Network"
            }
          ],
          "group": 2,
          "value": ""
        },
        {
          "id": "tuner3",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 3,
          "value": "Silicon Labs Si2168 #3 : DVB-T #0"
        },
        {
          "id": "tunerid3",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "4217276d79bbc105263891a33e99492f"
        },
        {
          "id": "network3",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "dvb_network_dvbt",
              "val": "DVB-T Network"
            }
          ],
          "group": 3,
          "value": ""
        },
        {
          "id": "tuner4",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 4,
          "value": "Silicon Labs Si2168 #3 : DVB-C #0"
        },
        {
          "id": "tunerid4",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "8ed6c0459881d74195df4083ca0deb21"
        },
        {
          "id": "network4",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "dvb_network_dvbc",
              "val": "DVB-C Network"
            }
          ],
          "group": 4,
          "value": ""
        },
        {
          "id": "tuner5",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 5,
          "value": "Silicon Labs Si2168 #2 : DVB-T #0"
        },
        {
          "id": "tunerid5",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "95be60337c2dc0e39c64044a4195fcf6"
        },
        {
          "id": "network5",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "dvb_network_dvbt",
              "val": "DVB-T Network"
            }
          ],
          "group": 5,
          "value": ""
        },
        {
          "id": "tuner6",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "rdonly": true,
          "group": 6,
          "value": "Silicon Labs Si2168 #2 : DVB-C #0"
        },
        {
          "id": "tunerid6",
          "type": "str",
          "caption": "Tuner",
          "description": "Name of the tuner.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "5bf4087180193d42b4d597b84c2da382"
        },
        {
          "id": "network6",
          "type": "str",
          "caption": "Network type",
          "description": "Select an available network type for this tuner.",
          "default": "",
          "enum": [
            {
              "key": "dvb_network_dvbc",
              "val": "DVB-C Network"
            }
          ],
          "group": 6,
          "value": ""
        }
      ],
      "meta": {
        "caption": "Tuner and Network",
        "class": "wizard_network",
        "event": "wizard_network",
        "groups": [
          {
            "number": 1,
            "name": "Network 1"
          },
          {
            "number": 2,
            "name": "Network 2"
          },
          {
            "number": 3,
            "name": "Network 3"
          },
          {
            "number": 4,
            "name": "Network 4"
          },
          {
            "number": 5,
            "name": "Network 5"
          },
          {
            "number": 6,
            "name": "Network 6"
          }
        ],
        "props": [
          {
            "id": "icon",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "description",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_prev_login",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_next_muxes",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "tuner1",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 1
          },
          {
            "id": "tunerid1",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network1",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 1
          },
          {
            "id": "tuner2",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 2
          },
          {
            "id": "tunerid2",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network2",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 2
          },
          {
            "id": "tuner3",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 3
          },
          {
            "id": "tunerid3",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network3",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 3
          },
          {
            "id": "tuner4",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 4
          },
          {
            "id": "tunerid4",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network4",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 4
          },
          {
            "id": "tuner5",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 5
          },
          {
            "id": "tunerid5",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network5",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 5
          },
          {
            "id": "tuner6",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "rdonly": true,
            "group": 6
          },
          {
            "id": "tunerid6",
            "type": "str",
            "caption": "Tuner",
            "description": "Name of the tuner.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "network6",
            "type": "str",
            "caption": "Network type",
            "description": "Select an available network type for this tuner.",
            "default": "",
            "group": 6
          }
        ]
      }
    }
  ]
}

```

`/api/wizard/network/save`

```json
{
  "network1": "iptv_auto_network",
  "network2": "",
  "network3": "dvb_network_dvbt",
  "network4": "",
  "network5": "dvb_network_dvbt",
  "network6": "",
  "uuid": "00000000000000000000000000000000",
  "undefined": "5bf4087180193d42b4d597b84c2da382"
}
```

#### muxes

`/api/wizard/muxes/load`

```json
{
  "entries": [
    {
      "uuid": "00000000000000000000000000000000",
      "id": "00000000000000000000000000000000",
      "text": "00000000000000000000000000000000",
      "caption": "Predefined Muxes",
      "class": "wizard_muxes",
      "event": "wizard_muxes",
      "params": [
        {
          "id": "icon",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "static/img/logobig.png"
        },
        {
          "id": "description",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "__Assign Predefined Muxes to Networks__ \n\nTo save you from manually entering muxes, Tvheadend includes predefined mux lists. Please select an option from the list for each network.\n\nPre-defined lists are not always up-to-date, this generally isn't a problem provided that one of the muxes in list is active, and contains network information. \n\n__If you don't see any options below, you need to go back and assign a network type to a tuner.__\n"
        },
        {
          "id": "page_prev_network",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "page_next_status",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "network1",
          "type": "str",
          "caption": "Network",
          "default": "",
          "rdonly": true,
          "group": 1,
          "value": "DVB-T Network"
        },
        {
          "id": "networkid1",
          "type": "str",
          "caption": "Network",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "3c80c7dc8ca5aeaf7d9c4b2ea22b4562"
        },
        {
          "id": "muxes1",
          "type": "str",
          "caption": "Pre-defined muxes",
          "default": "",
          "enum": {
            "type": "api",
            "uri": "dvb/scanfile/list",
            "stype": "none",
            "params": {
              "type": "dvbt"
            }
          },
          "group": 1,
          "value": ""
        },
        {
          "id": "network2",
          "type": "str",
          "caption": "Network",
          "description": "Name of the network.",
          "default": "",
          "rdonly": true,
          "group": 2,
          "value": "IPTV Automatic Network"
        },
        {
          "id": "networkid2",
          "type": "str",
          "caption": "Network",
          "description": "ID of the network.",
          "default": "",
          "noui": true,
          "persistent": true,
          "value": "d767846acf49663e0fae45211226669a"
        },
        {
          "id": "muxes2",
          "type": "str",
          "caption": "URL",
          "description": "URL of the M3U playlist.",
          "default": "",
          "group": 2,
          "value": ""
        }
      ],
      "meta": {
        "caption": "Predefined Muxes",
        "class": "wizard_muxes",
        "event": "wizard_muxes",
        "groups": [
          {
            "number": 1,
            "name": "Network 1"
          },
          {
            "number": 2,
            "name": "Network 2"
          },
          {
            "number": 3,
            "name": "Network 3"
          },
          {
            "number": 4,
            "name": "Network 4"
          },
          {
            "number": 5,
            "name": "Network 5"
          },
          {
            "number": 6,
            "name": "Network 6"
          }
        ],
        "props": [
          {
            "id": "icon",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "description",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_prev_network",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_next_status",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "network1",
            "type": "str",
            "caption": "Network",
            "default": "",
            "rdonly": true,
            "group": 1
          },
          {
            "id": "networkid1",
            "type": "str",
            "caption": "Network",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "muxes1",
            "type": "str",
            "caption": "Pre-defined muxes",
            "default": "",
            "group": 1
          },
          {
            "id": "network2",
            "type": "str",
            "caption": "Network",
            "description": "Name of the network.",
            "default": "",
            "rdonly": true,
            "group": 2
          },
          {
            "id": "networkid2",
            "type": "str",
            "caption": "Network",
            "description": "ID of the network.",
            "default": "",
            "noui": true,
            "persistent": true
          },
          {
            "id": "muxes2",
            "type": "str",
            "caption": "URL",
            "description": "URL of the M3U playlist.",
            "default": "",
            "group": 2
          }
        ]
      }
    }
  ]
}

```

`/api/wizard/muxes/save`

```json
{
  "muxes1": "dvbt/au/dvb-t_au-Sydne",
  "muxes2": "file:///home/dmc/development/TVH/empty/iptvtest.m3u",
  "uuid": "00000000000000000000000000000000",
  "undefined": "d767846acf49663e0fae45211226669a"
}
```

#### status

`/api/wizard/status/progress?_dc=[timestamp]`

A `status` request is issued at regular intervals until `progress` = `1`.

```json
{"progress":0,"muxes":30,"services":0}
```

```json
{"progress":0.5666666666666666,"muxes":30,"services":68}
```

```json
{"progress":1,"muxes":30,"services":80}
```

#### mapping

`/api/wizard/mapping/load`

```json
{
  "entries": [
    {
      "uuid": "00000000000000000000000000000000",
      "id": "00000000000000000000000000000000",
      "text": "00000000000000000000000000000000",
      "caption": "Service Mapping",
      "class": "wizard_mapping",
      "event": "wizard_mapping",
      "params": [
        {
          "id": "mapall",
          "type": "bool",
          "caption": "Map all services",
          "description": "Automatically map all available services to channels.",
          "default": false,
          "value": false
        },
        {
          "id": "provtags",
          "type": "bool",
          "caption": "Create provider tags",
          "description": "Create and associate a provider tag to created channels.",
          "default": false,
          "value": false
        },
        {
          "id": "nettags",
          "type": "bool",
          "caption": "Create network tags",
          "description": "Create and associate a network tag to created channels.",
          "default": false,
          "value": false
        },
        {
          "id": "icon",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "static/img/logobig.png"
        },
        {
          "id": "description",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": "__Map Services to Channels__ \n\nIn order for your frontend client(s) (such as Kodi, Movian, and similar) to see/play channels, you must first map discovered services to channels. If you would like Tvheadend to do this for you, check the 'Map all services' option below.\n\n__You can skip this step (do not check 'Map all services') and map services to channels manually.__\n"
        },
        {
          "id": "page_prev_status",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        },
        {
          "id": "page_next_channels",
          "type": "str",
          "caption": "",
          "default": "",
          "rdonly": true,
          "noui": true,
          "value": ""
        }
      ],
      "meta": {
        "caption": "Service Mapping",
        "class": "wizard_mapping",
        "event": "wizard_mapping",
        "props": [
          {
            "id": "mapall",
            "type": "bool",
            "caption": "Map all services",
            "description": "Automatically map all available services to channels.",
            "default": false
          },
          {
            "id": "provtags",
            "type": "bool",
            "caption": "Create provider tags",
            "description": "Create and associate a provider tag to created channels.",
            "default": false
          },
          {
            "id": "nettags",
            "type": "bool",
            "caption": "Create network tags",
            "description": "Create and associate a network tag to created channels.",
            "default": false
          },
          {
            "id": "icon",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "description",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_prev_status",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          },
          {
            "id": "page_next_channels",
            "type": "str",
            "caption": "",
            "default": "",
            "rdonly": true,
            "noui": true
          }
        ]
      }
    }
  ]
}

```

`/api/wizard/mapping/save`

```json
{
  "mapall": true,
  "provtags": true,
  "nettags": true,
  "uuid": "00000000000000000000000000000000"
}
```

The following appear out of order, nonetheless, that is the order in which the wizard executed them.

`/api/wizard/cancel?_dc=[timestamp]`

`/api/wizard/channels/save?node={"uuid":"00000000000000000000000000000000"}`
