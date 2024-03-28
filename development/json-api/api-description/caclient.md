# Caclient

API calls related to Conditional Access. ADMIN privilege is necessary for all of these functions.

### caclient/builders

Lists the text strings, options and defaults used when configuring Conditional Access devices within TVH (ie Configuration -> CAs -> Add).

### caclient/class

Lists the text strings, options and defaults used when configuring Conditional Access within TVH (ie Configuration -> CAs).

### caclient/create

Create a new CA instance.

* `class` Name of the class to create, ie one of the classes listed by caclient/builders.
* `conf` A JSON object describing the new device.

### caclient/list

List CA clients.

```
{
   "entries" : [
      {
         "title" : "Linux DVB CAM (CI/CI+)",
         "status" : "caclientNone",
         "uuid" : "7f435a73b190419cc6e69e3956c50549"
      }
   ]
}
```
