# transport-fanout

The egress edge: one zone tick, filtered by each subscriber's interest and written to it as back-to-back fixed-size entity records.

## What it is for

The gateways terminate client transport on the way in; this is the way out. It is driven by the zone tick rather than by an arriving packet, and it does its work per subscriber rather than per connection. Entity packets stay fixed-size binary records with no per-packet framing, so a subscriber recovers the record count by division. Delivery goes through a sink function pointer, so a caller can pass a socket writer or a counter.

It is a library rather than a process: a caller supplies the tick and the sink.

## Build and run

The build needs two generated headers: the predictive BVH from `interactor-spatial-oracle` and the entity packet codec from `contract-entity-packet`. Point the `WEFT_GEN_DIR` build setting at the directory holding them; without it, the build skips the library.

## Licence

MIT, as LICENSE and CITATION.cff state. The public header's SPDX tag says Apache-2.0, which disagrees with them.
