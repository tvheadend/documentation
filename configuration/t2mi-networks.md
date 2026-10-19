# T2-MI Networks

Some providers deliver a complete DVB-T multiplex inside a single PID of a
satellite transponder, rather than broadcasting it terrestrially. The inner
multiplex is either wrapped in T2-MI baseband frames (ETSI TS 102 773) or
carried as a plain transport stream (data piping, ETSI EN 301 192), and it is
often scrambled. The Abertis/Cellnex regional DTT feeds on Hispasat 30°W work
this way.

A T2-MI network lets Tvheadend receive those inner services directly, without
an external decapsulation tool. It is available when Tvheadend is built with
T2-MI support (the default; disable with `--disable-t2mi` at configure time).

## How it works

A T2-MI network does not tune a transponder itself. Instead you point it at one
or more source muxes that already exist in another network (typically your
DVB-S/S2 transponders). Tvheadend looks at the services on those muxes, finds
the ones that carry a T2-MI or piped stream, and creates one inner multiplex for
each carrier.

Each inner multiplex subscribes to the carrier service on the source mux. The
stream therefore passes through the normal service and descrambler path first,
so a scrambled carrier is descrambled exactly like any other service. Only then
is the inner transport stream extracted and handed back to Tvheadend, where it
is scanned and its services are mapped to channels like those of any other mux.

## Setting one up

1. Create a network of type **T2-MI Network**.
2. In **Source muxes**, select the transponders that carry the feed.
3. Scan the network. Tvheadend discovers the carriers, creates an inner
   multiplex for each one, and scans those for services.

For feeds that do not use a T2-MI descriptor, leave **Detect private-stream
carriers** enabled so private data streams are treated as carriers.

An inner multiplex whose carrier temporarily disappears is kept, so its services
and channel mappings survive a change in the feed. Inner multiplexes are removed
only when their source mux is removed or the T2-MI network is deleted. Set
**Network discovery** to Disable to stop new carriers being added automatically.

## Related

Feature pull request: [tvheadend/tvheadend#2199](https://github.com/tvheadend/tvheadend/pull/2199)
