# WebSocket

Tvheadend has a websocket interface on port 9981. It is used by the UI to provide 'live' actions and updates, avoiding the need to refresh the screen.

### Example Code

The example below creates a WebSocket connection to the Tvheadend server and listens for updates.

```
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <title>Websocket Test</title>
    <script>
      let socket = new WebSocket("ws://192.168.0.1:9981/comet/ws");
      socket.onmessage = function(event) {
        let message = event.data;
        let messageElem = document.createElement('div');
        messageElem.textContent = message;
        document.getElementById('messages').prepend(messageElem);
      }
    </script>
  </head>
  <body>
    <header></header>
    <main>
      <div id="messages"></div>
    </main>
    <footer></footer>
  </body>
</html>
```

### Output

Tvheadend transmits messages on the Websocket interface asynchronously, when either a event occurs or in some cases at scheduled intervals. The output format is JSON.

Each message contains a key "messages" whose value is an array of message objects. Each message object contains a key "notificationClass" which specifies the source of the message, and a series of message-specific key-value pairs.

```
{
  "messages": [
    {
      "freediskspace": 607828439040,
      "useddiskspace": 135628398200,
      "totaldiskspace": 861450428416,
      "notificationClass": "diskspaceUpdate"
    },
    {
      "notificationClass": "logmessage",
      "logtxt": "2024-03-06 11:06:14.444 subscription: 00D5: \"HTTP\" subscribing on channel \"DMAX\", weight: 100, adapter: \"DVB-T #0\", network: \"Sandy\", mux: \"690MHz\", service: \"DMAX\", profile=\"pass\", hostname=\"192.168.1.2\", client=\"VLC/3.0.20 LibVLC/3.0.20\""
    },
    {
      "id": 213,
      "start": 1709723174,
      "errors": 0,
      "state": "Running",
      "hostname": "192.168.1.2",
      "client": "VLC/3.0.20 LibVLC/3.0.20",
      "title": "HTTP",
      "channel": "DMAX",
      "service": "DVB-T #0/Sandy/690MHz/DMAX",
      "pids": [
        1011,
        2401,
        2402,
        2403,
        2404
      ],
      "profile": "pass",
      "in": 57716,
      "out": 57716,
      "total_in": 57716,
      "total_out": 57716,
      "updateEntry": 1,
      "notificationClass": "subscriptions"
    }
  ]
}
```
