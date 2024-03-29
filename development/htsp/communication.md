# Communication

This communication is currently implemented by using htsmsg's. All strings are encoded as UTF-8.

There are two distinct ways for communication within HTSP.

Apart from this there is a number of messages that needs to be exchanged during login, see the login section below.

### RPC Communication

There is a normal RPC way of doing things. I.e. the client sends a request and the server responds with a reply. All the RPC methods are listed below as the 'Client to Server' methods. Apart from all message fields listed within each message type the client can add an additional field:

RPC request extra fields:\


```
seq              int  optional   Sequence number. This field will be echoed back by the server in the reply.
username         str  optional   Username, in combination with 'digest' this can be used to raise the privileges
                                 for the session in combination with invocation of a method. 
digest           bin  optional   Used to raise privileges.
```

The followings field should be used by the client to match the reply with the request.\
All replies are guaranteed to arrive in the same order as the requests.\
Even so, probably the best way to implement the request-reply client is by taking advantage of the 'seq' field.

RPC reply extra fields:\


```
seq              int  optional   Sequence number. Same as in the request.
error            str  optional   If present an error has occurred and the text describes the error.
noaccess         int  optional   If present and set to '1' the user is prohibited from invoking the method due to 
                                 access restrictions. 
```

### Streaming Communication

For streaming of live TV and various related messages the server will continuously push data to the client.\
These messages are referred to as asynchronous messages and always have the 'method' field set and never have the 'seq' field set.\
Also, the client can enable an additional asyncMetadata mode and by doing so it will be notified by the server when meta data changes. (EPG updates, creation of channels and tags, etc).

### Authentication

In Tvheadend, each method has an associated access restriction. Currently there is only one restriction (Streaming). However, this may change in the future.

Privileges for these restrictions may be granted in two ways: Username + Password and/or Source IP address.\
Therefore it is possible to gain permissions to the system without entering a username and password.\
While this is really useful it also complicates the authentication schema a bit.\
Upon connect the initial privileges will be raised based on the source address.

Before any username / password based authentication has taken place the client must have\
obtained a challenge (which stays fixed for the session). This is done via the 'hello' method.

In principle it's possible to use two different authentication idioms with HTSP.\
Depending on how your application works one or another may be more suitable.\
While they do not really differ from a protocol point of view it's worth mentioning a bit about them here:

### Initial Login Authentication

The client performs all of its authentication using the 'login' method.

It may choose to send:

* Username and password: Privileges will be raised based on these credentials.
* Username only: Privileges will be based on just the source address. The username will be used for various logging purposes.
* Nothing: Privileges will be based on just the source address.

If no privileges are granted after the login message has been received by the server (i.e. both network and username + password based)\
the server will reply with 'noaccess' set to 1. A client that only employs initial login should honor this flag and ask the\
user for a username + password and retry by using the 'authenticate' method. I.e. it should not send the 'login' method again.

### On-Demand Authentication

The client performs all of its authentication when it needs to.

When using this method, the client will check every RPC reply for the 'noaccess' field.\
If it set to 1 it whould ask the user for username + password and retry the request but also\
add 'username' and 'digest' to the original message. (See _RPC request extra fields_ above)

Typically it would not send a username or digest during login.
