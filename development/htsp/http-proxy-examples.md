# HTTP Proxy Examples

The HTSP `api` method can be used as a proxy to access the HTTP/JSON API.  This allows HTSP-only clients access to any JSON feature, including JSON-only features.\
\
Data exchanged to and from the TVH server is achieved by encapsulating the required HTTP/JSON parameters within the HTSP message.\
\
TVH expects to receive encapsulated JSON data and will respond with a HTSP map representing the JSON data returned.

Also see: [JSON API](../json-api/).

## HTSP `API` Syntax Summary

Request:

```
args               msg[] optional   HTTP arguments
path               str   required   HTTP path
```

Reply:

```
response           msg[] required   JSON response 
```

## Simple Request

To execute the HTTP API command:\
`http://TVH:9981/api/channel/grid`\
\
Set the `path` field to `channel/grid` and send the request.  The `args` field is not required.\
\
The response will be a HTSP `map` containing an element named `response`.  This element will be a `map` containing the JSON response presented as HTSP elements.

## Intermediate Request

To execute the HTTP API command:\
`http://TVH:9981/api/channel/grid?sort=number&dir=desc`\
\
Set the path to `channel/grid` as in the previous example.\
\
The `arg` field must be set to type `map`, and in this example, contain two `str` elements.\
\
Map `str` element named `sort` should contain the value `number` and map `str` element named `dir` should contain the value `desc`.

## Advanced Request

To execute the HTTP API command:\
`http://TVH:9981/api/dvr/entry/create`\
\
Set the path to `dvr/entry/create`.\
\
As with the previous example, the `args` field must be set to type `map`.\
\
**Method 1 - JSON String**\
\
Create a JSON string containing the properties required to complete the request as detailed in the [JSON API documentation](../json-api/).  In this example, to create a new DVR entry.\
\
Within that `map`, create a `str` element named `conf` that contains the required JSON string.\
\
**Method 2 - HTSP Map**\
\
Instead of creating a JSON string, create a HTSP `map` where each element name matches the name of the JSON property and contains the required property value.\
\
`args` should be a `map` that contains another `map` named `conf` that contains another `map` with the required JSON data represented as HTSP elements.
