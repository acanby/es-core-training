Distributed Model
=================

Two types of pinging to find other nodes:
- Multicast - publish message
- Unicast - list of seed nodes to grow network

Set minimum_master_nodes to help prevent split clusters (split_brain). Set this to > 1 to ensure when a node is isolated it doesn't make its own cluster and elect itself as master. It will ping until the network returns, or the timeout is reached.

Client nodes can be added as light weight load balancers. Can also talk to a localhost instance which forwards to an appropriate node.
Master nodes can be run on small boxes, as they do not suffer from data constraints. They are purely managing the cluster if configured as a dedicated master.

All elasticsearch networking operations are evented, ie non blocking.

Trying to GET a document which was indexed with a routing value requires that you specify the routing value for the GET request. This will otherwise mean you have a 1/shards chance of hitting the right shard, which negates the benefit of adding a routing value.

Replication write consistency by default is using a quorum: N/2 + 1.
