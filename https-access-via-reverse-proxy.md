# HTTPS access via Reverse Proxy

In order to access Tvheadend behind a reverse proxy server and still be able to stream services or recordings, it is necessary for the reverse proxy server to add or modify some headers in the HTTP request forwarded to TVH.

### X-Forwarded-Proto:

Tvheadend currently (as at April 2025) only supports the HTTP protocol natively.  To access TVH via HTTPS, an external reverse proxy server is required to convert the incoming HTTPS request to HTTP and forward it to TVH.

In order for TVH to recognise that it is operating behind a HTTPS reverse proxy server, the proxy server must be configured to add the `X-Forwarded-Proto: https` header to the request forwarded to TVH.

Adding this header will ensure that documents that contain a TVH URL, such as `M3U` files, will be prefixed with correct protocol identifier.

### Host: / X-Forwarded-Host:

The public-facing host name, port number and path returned by TVH within documents such as an `M3U` can also be modified.  As TVH only recognises the `X-Forwarded-Host:`header when the `Host:`header is not present, it is recommended that only the `Host:`header be modified by the proxy in for following format:

`Host: <External host>[:<External port>][/<External path>]`
