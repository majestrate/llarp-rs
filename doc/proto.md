every network participant has a distinct nodedb which is a loose collection of nodeinfo descriptors (nodeinfos) built up by participants in the network.

nodeinfos are retained by participants given sufficient reachability is sustained.
each node participating in routing floodfills its nodeinfo to the network and existing participants test connectivity it advertises.


a nodeinfo is represented as an ASN1 sequence of the following in order defined:

* a network id bytestring
* a protocol version bytestring
* an ed448 public identity signing key 
* a 64 bit unix timestamp of when the node started at
* an uptime counter integer that incremenets every 30 minutes
* a sequence of reachability desecriptors
* a signature of the above data signed by the identity key

each time the uptime counter increments the node resigns the nodeinfo and floods it to the network.
the network then retests connectivity for each of the reachability descriptors given.

each network participant has their own version of the wider network that it generates from tested nodeinfos and which reachability descriptors were reachable. there is no consensus, only a claimed view of the wider network that is atested by the node. collectively the network should be able to see a most agreed upon slice of the wider network but this is not meant to be an authorative source of truth due to sybil, merely a suggestion or hint.


