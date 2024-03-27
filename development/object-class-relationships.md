# Object Class Relationships

All configuration data within TVHeadEnd (TVH), is stored in object classes. A class may contain multiple objects representing a single configuration item each.

Examples include: channels, recordings, muxes, adapters, autorecs, etc.

Detailing every object class is beyond the scope of this document, however, a list of classes can be obtained via the JSON API as follows: http://\[TVH\_IP]:9981/api/classes

Any object within TVH can be addressed via its UUID ([Universally unique identifier](https://en.wikipedia.org/wiki/Universally\_unique\_identifier)).

The UUID is represented in the JSON API as a 32 hexadecimal character string (128 bit). In the HTSP API, an object’s ID is normally represented as an unsigned 32 bit integer that corresponds to the first four bytes (eight hex characters) of the UUID.

Please note: EPG event data is not stored or addressed using UUIDs, however, EPG event entries can contain links to UUIDs of configuration objects.

Objects can be linked to other objects via their UUIDs.

**For example:** To record a programme, the EPG entry will be linked to a ‘Channel’ object. That channel object will be linked to one or more ‘Service’ objects. Each service object will be linked to a ‘Mux’ object. Each mux object will be linked to a ‘Network’ object. Finally a network object will be linked to one or more ‘Adaptor’ objects.

The following diagram is not exhaustive, but serves to illustrate the relationship between various common object classes.

<figure><img src="../.gitbook/assets/TVH Object Relationships.jpg" alt=""><figcaption></figcaption></figure>

Objects are stored on disk in JSON-formatted files. These files are located with the subdirectories representing their configuration function and are named to match their UUID.

It is recommended that these files not be edited directly.
