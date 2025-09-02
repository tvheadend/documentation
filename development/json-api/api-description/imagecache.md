# Imagecache

Functions controlling the configuration of the Image Cache. ADMIN privilege is required for all of these functions.

Before version 4.3.1660, these functions were only available if Image Cache support was included at compile time.

### imagecache/config/load

Lists the current values, defaults and descriptions of the parameters used to configure the image cache.

```
{
   "entries" : [
      {
         "caption" : "Configuration - Image Cache",
         "params" : [
            {
               "caption" : "Enabled",
               "description" : "Select whether or not to enable caching. Note, even with this disabled you can still specify local (file://) icons and these will be served by the built-in webserver.",
               "id" : "enabled",
               "default" : false,
               "type" : "bool",
               "value" : false
            },
            {
               "default" : false,
               "id" : "ignore_sslcert",
               "type" : "bool",
               "value" : false,
               "description" : "Ignore invalid/unverifiable (expired, self-certified, etc.) certificates",
               "caption" : "Ignore invalid SSL certificate"
            },
            {
               "caption" : "Expire time",
               "description" : "The time in days after the cached URL will be removed. The time starts when the URL was lastly requested. Zero means unlimited cache (not recommended).",
               "type" : "u32",
               "value" : 7,
               "id" : "expire",
               "default" : 0
            },
            {
               "description" : "How frequently the upstream provider is checked for changes.",
               "caption" : "Re-fetch period (hours)",
               "id" : "ok_period",
               "default" : 0,
               "type" : "u32",
               "value" : 168
            },
            {
               "description" : "How frequently a failed image fetch is retried.",
               "caption" : "Re-try period (hours)",
               "value" : 24,
               "type" : "u32",
               "id" : "fail_period",
               "default" : 0
            }
         ],
         "class" : "imagecache",
         "text" : "00000000000000000000000000000000",
         "event" : "imagecache"
      }
   ]
}
```

### imagecache/config/save

TODO

### imagecache/config/clean

Delete all files from the image cache and re-load, in the same way as Configuration -> General -> Image Cache -> Clean Image (icon) Cache in the GUI.

* `clean` Required parameter, must be 1 - the value is not used.

### imagecache/config/trigger

Trigger a re-load of the image cache, in the same way as Configuration -> General -> Image Cache -> Re-fetch Images in the GUI.

* `trigger` Required parameter, must be 1 - the value is not used.
