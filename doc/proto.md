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

each network participant has their own version of the wider network that it generates from tested nodeinfos and which reachability descriptors were reachable.
there is no consensus, only a claimed view of the wider network that is atested by the node.
collectively the network should be able to see a most agreed upon slice of the wider network.
this is not meant to be an authorative source of truth due to sybil, but merely a suggestion or hint for clients using the network.

a client bootstraps into the network from an out of band specified seed node that is set by the configuration of the client.
the client will use this bootstrap node as a source of hints for bootstrapping the wider network.
bootstrap nodes are manually defined by the user's configuration because of sybil concerns, it is not meant to be automatically set.
when a client first connects to the bootstrap nodes it downloads each node's reachability info that it generated from testing.
clients also use these bootstrap nodes as explicitly pinned edge connections to build paths over too.
once the client has enough nodeinfos it will start to build paths.
