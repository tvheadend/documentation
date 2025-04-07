# HTTPS access via Reverse Proxy

Tvheadend currently (as at April 2025) only supports the HTTP protocol natively.  To access TVH via HTTPS, an external reverse proxy server is required to convert the incoming HTTPS request to HTTP and forward it to TVH.

In order for TVH to recognise that it is operating behind a HTTPS reverse proxy server, the proxy server must be configured to add the `X-Forwarded-Proto: https` header to the request forwarded to TVH.

Adding this header will ensure that documents that contain a TVH URL, such as `M3U` files, will be prefixed with correct protocol identifier.
