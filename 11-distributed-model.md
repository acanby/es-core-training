Distributed Model
=================

Two types of pinging to find other nodes:
- Multicast - publish message
- Unicast - list of seed nodes to grow network

Set minimum_master_nodes to help prevent split clusters (split_brain). Set this to > 1 to ensure when a node is isolated it doesn't make its own cluster and elect itself as master. It will ping until the network returns, or the timeout is reached.


