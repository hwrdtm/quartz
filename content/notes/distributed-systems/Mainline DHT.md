---
title: Mainline DHT
---
This is a Kademlia-based distributed hash table used by BitTorrent clients to find peers via the BitTorrent protocol. It is used for distributed tracking of peers, as opposed to the previously used method of relying on trackers to find peers, which is a centralized approach as it relies on specific servers to provide that information.

Each BitTorrent client is a peer and is therefore running a "node" that also stores partially replicated state as part of this DHT.

# Resources

https://en.wikipedia.org/wiki/Mainline_DHT

Protocol Specs: https://www.bittorrent.org/beps/bep_0005.html