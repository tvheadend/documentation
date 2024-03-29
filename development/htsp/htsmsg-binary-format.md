---
description: Message Structure
---

# HTSMSG Binary Format

A message can be of either **map** or **list** type. In a **map** each field has a name, in a **list** the members do not have names, but the order should be preserved.

The field types are:

<table><thead><tr><th width="111">Name </th><th width="70">ID </th><th>Description </th></tr></thead><tbody><tr><td>Map </td><td>1</td><td>Sub message of type map</td></tr><tr><td>S64 </td><td>2</td><td>Signed 64bit integer</td></tr><tr><td>Str </td><td>3</td><td>UTF-8 encoded string</td></tr><tr><td>Bin </td><td>4</td><td>Binary blob</td></tr><tr><td>List </td><td>5</td><td>Sub message of type list</td></tr></tbody></table>

All in all the message structure is quite similar to JSON but most notably; no **boolean** nor **null** type exist and HTSMSG supports **binary** objects.

## HTSMSG Binary Format

The binary format is designed to for back-to-back transmission of messages over a network (TCP) connection.

The root message must always be of type **map**.

### Root body

<table data-header-hidden><thead><tr><th width="111"></th><th width="171"></th><th></th></tr></thead><tbody><tr><td>Length</td><td>4 byte integer</td><td>Total length of message (not including this length field itself)</td></tr><tr><td>Body</td><td>HTSMSG-Field * N</td><td>Fields in the root body</td></tr></tbody></table>

### HTSMSG-Field

<table data-header-hidden><thead><tr><th width="146"></th><th width="136"></th><th></th></tr></thead><tbody><tr><td>Type</td><td>1 byte integer</td><td>Type of field (see field type IDs above)</td></tr><tr><td>Namelength</td><td>1 byte integer</td><td>Length of name of field. If a field is part of a list message this must be 0</td></tr><tr><td>Datalength</td><td>4 byte integer</td><td>Length of field data</td></tr><tr><td>Name</td><td>N bytes</td><td>Field name, length as specified by Namelength</td></tr><tr><td>Data</td><td>N bytes</td><td>Field payload, for details see below</td></tr></tbody></table>

#### Field encoding for type: map and list

The data is repeated HTSMSG-Fields exactly as the root body. Note the subtle difference in that for the root-message the length includes the 4 bytes of length field itself whereas in the field encoding the length written includes just the actual payload.

#### Field encoding for type: s64

Integers are encoded using a very simple variable length encoding. All leading bytes that are 0 is discarded. So to encode the value 100, datalength should be 1 and the data itself should be just one byte \[0x64]. To encode 1337; datalength=2, data=\[0x39 0x05].

Note that there is no sign extension in this encoding scheme so if you need to encode -1 you need to set datalength=8 and data = \[0xff 0xff 0xff 0xff 0xff 0xff 0xff 0xff]. This can certainly be thought of as a bug, but it is the way it is.

#### Field encoding for type: str

Datalength should be the length of the string (NOT including the null terminating character). Thus the null terminator should not be present in data either.

#### Field encoding for type: bin

Datalength should be the length of the binary object. Data is the binary object itself.
