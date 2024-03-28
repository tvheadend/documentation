# API Description

TVHeadend provides the API using the HTTP protocol, by default via port 9981 though this can be changed in the TVH config. API functions appear as pseudo-files under the /api/ root of the server filesystem, with parameters passed to the function via either the GET or POST methods.

The call must include a username and password with access permissions to carry out the requested task. The user must also have the ACCESS\_WEB\_INTERFACE privilege, either directly or inherited from an earlier '\*' user. In other words the "Web interface" box must be ticked on the Access Entries screen; without this all calls will fail with a "403 Forbidden" error.

If TVHeadend has been started with the '--http\_root' qualifier, the HTTP root must be included in the URL, thus eg

`http://admin:admin@192.168.3.45:9981/myHttpRoot/api/serverinfo`

The server does not check that all parameters supplied are valid in the context of the request; unexpected items are ignored. Parameters not in the expected format or not containing the expected data may also be ignored.

The response from TVH follows the HTTP protocol and includes an HTTP/1.1 header with status code. If an error occurs the response is in HTML, for example:

```
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<HTML><HEAD>
<TITLE>404 Not Found</TITLE>
</HEAD><BODY>
<H1>404 Not Found</H1>
</BODY></HTML>
```

The error returned is generic and does not indicate the source of the problem. Authentication failures (incorrect user/pass) will return "401 Unauthorized", lack of privilege "403 Forbidden", non-existent API functions "404 Not Found", incorrect or missing parameters generally "400 Bad Request".

Data is usually returned as JSON, without any CR or LF characters - the examples given have been 'prettified' using json\_pp or jq to make them easier to read. Functions which perform an action rather than return data will return an empty JSON object on successful completion.
