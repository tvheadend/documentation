# Examples

These examples (and any other use of the API which passes username and password in the URL) will only work if TVheadend is configured to use 'basic' or 'basic and digest' authentication.

#### curl

Parameters passed to TVH using the GET method must be URI-encoded:

`curl 'http://user:pass@localhost:9981/api/epg/events/grid?limit=999&channel=BBC%20ONE'`

Alternatively use the POST Method:

`curl --data 'limit=999&channel=BBC ONE' 'http://user:pass@localhost:9981/api/epg/events/grid'`

To make the output more human-readable, pipe it through json\_pp (included in the perl package on many distributions) or jq.

#### PHP

This simple example lists some details about upcoming timers, sorted in date order. To work through a PHP-enabled web server, the PHP.INI setting "allow\_url\_fopen" must be ON.

```
<!DOCTYPE html>
<html>
 <head>
  <title>TVH PHP test</title>
  <meta http-equiv="content-type" content="text/html; charset=utf-8">
  <style>
    table, th, td {
      border: 1px solid black;
    }
  </style>
 </head>
 <body>
  <table>
   <tr><th>Date</th><th>Start</th><th>End</th><th>Title</th></tr>
<?php
        $timers = get_timers();
        foreach($timers as $t) {
          $start = strftime("%H:%M", $t["start"]);
          $stop = strftime("%H:%M", $t["stop"]);
          $date = strftime("%a %e/%m", $t["start"]);
          echo "<tr><td>$date</td><td>$start</td><td>$stop</td><td>{$t['disp_title']}</td></tr>";
        }

        function get_timers() {
          $url = "http://admin:admin@your.server:9981/api/dvr/entry/grid_upcoming?sort=start";
          $json = file_get_contents($url);
          $j = json_decode($json, true);
          $ret = &$j["entries"];
          return $ret;
        }
?>
  </table>
 </body>
</html>

```

For an example of what can be done with the API in PHP see https://github.com/dave-p/TVHadmin.

#### Javascript

It is a 'feature' of Javascript that a script can only access remote content from the same source (IP and port number) as the script was loaded from. Hence to call the TVHeadend API from Javascript, the script must be hosted on TVHeadend's built-in web server. To do this, place your script in `/usr/share/tvheadend/src/webui/static`; it can then be accessed from URL `http://user:pass@your.server:9981/static/`. _Note that this is unintended behaviour and may change in the future._

This example carries out the same task as the PHP example above. Your browser will prompt for the TVHeadend user and password.

```
<!DOCTYPE html>
<html>
<head>
  <title>TVH Javascript test</title>
  <meta http-equiv="content-type" content="text/html; charset=utf-8">
  <style>
    table, th, td {
      border: 1px solid black;
    }
  </style>
  <script>
    var getTimers = async function() {
      var url = "http://192.168.0.1:9981/api/dvr/entry/grid_upcoming?sort=start";
      const response = await fetch(url);
      const timers = await response.json();
      return timers.entries;
    }

    async function main() { 
      var timers = await getTimers(); 
      const table = document.getElementById("result");
      timers.forEach(function(entry) {
        var start = new Date(entry.start * 1000);
        var stop = new Date(entry.stop * 1000);
        row = table.insertRow();
        html = "<td>" + start.toLocaleDateString() +
             "</td><td>" + start.toLocaleTimeString() +
             "</td><td>" + stop.toLocaleTimeString() +
             "</td><td>" + entry.disp_title + "</td>";
        row.innerHTML = html;
      });
    } 
    main(); 
  </script>
</head>
<body>
  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Start</th>
        <th>End</th>
        <th>Title</th>
      </tr>
    </thead>
    <tbody id="result"></tbody>
  </table>
</body>
</html>
```

#### Python

This example produces the same output as the previous ones.

```
#!/usr/bin/env python3

import json
import time
import requests

def get_timers():
    ts_server = 'http://192.168.0.1:9981'
    ts_url = 'api/dvr/entry/grid_upcoming?sort=start'
    ts_user = 'admin'
    ts_pass = 'admin'
    ts_query = '%s/%s' % (
        ts_server,
        ts_url,
    )
    ts_response = requests.get(ts_query, auth=(ts_user, ts_pass))
    if ts_response.status_code != 200:
        print('<pre>Error code %d\n%s</pre>' % (ts_response.status_code, ts_response.content, ))
        return {}

    ts_json = json.loads(ts_response.text, strict=False)
    return ts_json['entries']

def main():
    print('''
<!DOCTYPE html>
<html>
 <head>
  <title>TVH Python test</title>
  <meta http-equiv="content-type" content="text/html; charset=utf-8">
  <style>
    table, th, td {
      border: 1px solid black;
    }
  </style>
 </head>
 <body>
  <table>
   <tr><th>Date</th><th>Start</th><th>End</th><th>Title</th></tr>
''')

    timers = get_timers()
    if len(timers):
        for timer in timers:
            start = time.localtime(timer['start'])
            print('<tr><td>%s</td><td>%s</td><td>%s</td><td>%s</td></tr>'
                % (time.strftime("%a %e/%m",start),
                   time.strftime("%H:%M",start),
                   time.strftime("%H:%M",time.localtime(timer['stop'])),
                   timer['disp_title'],
                ))
                
    print('''
  </table>
 </body>
</html>
''')


main()
```
