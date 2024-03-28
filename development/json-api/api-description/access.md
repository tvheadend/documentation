# Access

Functions to list and manipulate access controls. With the exception of access/entry/userlist, ADMIN privilege is required to use these functions.

### access/entry/class

Lists the text strings, options and defaults used when configuring access controls within the TVH GUI (ie Configuration -> Users -> Access Entries).

### access/entry/create

Creates a new user from a JSON object.

* `conf` The JSON object describing the new user.

### access/entry/grid

Lists users and their privileges. See [Common Parameters](common-parameters.md) for details of selection parameters.

```
{
  "entries": [
    {
      "uuid": "59c300295cbf01e53f096242fd5b8ffc",
      "index": 1,
      "enabled": true,
      "username": "*",
      "prefix": "192.168.1.0/24,127.0.0.1/32",
      "change": [
        "change_rights",
        "change_chrange",
        "change_chtags",
        "change_dvr_configs",
        "change_profiles",
        "change_conn_limit",
        "change_lang",
        "change_lang_ui",
        "change_theme",
        "change_uilevel"
      ],
      "uilevel": -1,
      "uilevel_nochange": -1,
      "lang": "eng_GB",
      "langui": "eng_GB",
      "themeui": "blue",
      "streaming": [
        "basic",
        "advanced",
        "htsp"
      ],
      "profile": [],
      "dvr": [
        "basic",
        "htsp",
        "all",
        "all_rw",
        "failed"
      ],
      "htsp_anonymize": false,
      "dvr_config": [
        "4e3a1e13acd2d5a9c129e7b00f6c986e"
      ],
      "webui": true,
      "admin": false,
      "conn_limit_type": 0,
      "conn_limit": 0,
      "channel_min": 0,
      "channel_max": 0,
      "channel_tag_exclude": false,
      "channel_tag": [],
      "comment": "Wildcard",
      "wizard": false
    },
  ]
}
```

### access/entry/userlist

Outputs a list of usernames. The "\*" user and any users with a zero-length name are excluded.

The function is used internally to populate the "Owner" dropdown in Digital Video Recorder -> Finished Recordings -> Edit. It MUST be called by a user without ADMIN privileges, otherwise an empty list is returned.

```
{
   "entries" : [
      {
         "key" : "myUserName",
         "val" : "myUserName"
      }, ...
   ]
}
```

### ipblock/entry/class

Lists the text strings, options and defaults used when configuring access controls within the TVH GUI (ie Configuration -> Users -> IP Blocking Records).

### ipblock/entry/create

Creates a new IP-based access record.

* `conf` The JSON object describing the access record.

### ipblock/entry/grid

Lists IP-block records. See [Common Parameters](common-parameters.md) for details of selection parameters.

```
{
   "entries" : [
      {
         "prefix" : "10.0.0.0/8",
         "enabled" : true,
         "comment" : "Don't allow guests",
         "uuid" : "95a81ed085a1d1a9d8647400a878594d"
      }
   ],
   "total" : 1
}
```

### passwd/entry/class

Lists the text strings, options and defaults used when configuring access controls within the TVH GUI (ie Configuration -> Users -> Passwords).

### passwd/entry/create

Creates a new password record.

* `conf` The JSON object describing the record.

### passwd/entry/grid

Lists passwords for users. Note that "password" is in clear-text while "password2" is base64-encoded with a static prefix. See [Common Parameters](common-parameters.md) for details of selection parameters.

```
{
   "total" : 1,
   "entries" : [
      {
         "password" : "XxXxXxXx",
         "uuid" : "2fa9ebf7e421a537ac032a6905134137",
         "username" : "xxxxxx",
         "enabled" : true,
         "wizard" : true,
         "password2" : "Base64EncodedPassword"
      }, ...
   ]
}
```

If authentication for the user is by persistent token (requires TVHeadend > 4.3.1500) the entry has some extra fields:

```
{
   "total" : 1,
   "entries" : [
      {
         "password" : "",
         "uuid" : "2fa9ebf7e421a537ac032a6905134137",
         "username" : "xxxxxx",
         "enabled" : true,
         "wizard" : true,
         "password2" : "Base64EncodedPassword"
         "auth": [
            "enable"
         ],
         "authcode": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
   ]
}
```
