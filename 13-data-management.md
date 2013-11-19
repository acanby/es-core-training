Data Management
===============

Overallocation allows for future expansion. Shards typically define max cluster size. These can be on one node, and then coped later. They cannot be created after index creation time.

Multiple indicies - searching one index with 50 shards is the same as searching 50 indexes with one shard, in terms of shards hit.

Max index size = num_of_shards * shard_size. Replicas do not factor into index size, though they need to be considered for space constraints on the box.

Search must hit all shards, so do not allocate too many.

Typical defaults can get you a long way, 5 shards is typically a good starting point to go a long way.


