# Object ID Representation

The **JSON API** represents the unique identifier as a 32 byte character hexadecimal string.  For example: `90e9361f38c156df654ecd27b92f398c`.\
\
When **proxied** via the **HTSP** `api` method, the unique identifier is encoded as a 16 byte binary field.  When this field is represented as a hexadecimal string, it matches that used by the JSON API.\
\
The **HTSP API** represents the unique identifier of an object using an unsigned 32 bit big-endian integer.\
\
When represented as a hexadecimal string, the value matches the first 8 characters of the JSON unique identifier.\
\
When evaluated as binary data, it matches the first 4 bytes of the proxied JSON value.

**Mixing and Matching API Values**\
\
The following table summarises UUID handling by API.

<table><thead><tr><th width="148">API Used</th><th width="372">UUID Value Returned</th><th>Encoding</th></tr></thead><tbody><tr><td>JSON</td><td><code>90e9361f38c156df654ecd27b92f398c</code></td><td>String</td></tr><tr><td>Proxied JSON</td><td><code>0x90e9361f38c156df654ecd27b92f398c</code></td><td>Binary</td></tr><tr><td>HTSP</td><td><code>0x90e9361f</code></td><td>Binary</td></tr></tbody></table>
