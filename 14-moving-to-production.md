Moving to Production
====================

Install either via zip, deb/rpm or using Chef/Puppet

All configuration (almost) have sensible defaults. Ensure that you move the location of your elasticsearch data.
Set discovery.zen.minimum_master_nodes to avoid a splitbrain. Use in tandem with timeout for master election.

Stay below 30gb allocation for Xmx, the JVM can compress pointers from 64bit to 32bit pointers.
Make sure the process does not swap. Set bootstrap.mlockall=true in the config and also ulimit -l unlimited.

Ubuntu does not use /etc/security/limits, enable this in /etc/pam.d by removing the commenting on the lines for security config.

Field Data
----------

- Load using the doc prefix
- Needed to be loaded to provide fast execution times
- Do not facet on analyzed data - use multi_field
- Monitored using node status API

If you get an OutOfMemoryException, you need to kill the node. Unknown state at this point. Consider upping ES_HEAP_SIZE.

Watch for memory usage which is not freeing quickly. This is likely to cause an issue sooner rather than later.
Increase file descriptors allocated to elasticsearch, somewhere around 64000 (default is 1024). Check to see if set correctly using ulimit -m (I think?)

Nodes are highly concurrent and and will easily use all cores of a machine.
Consider SSD or provisioned IOPS (on Amazon). Also consider RAID for spinning disks etc.

Monitoring cluster health
-------------------------

- Green - all shards are allocated
- Yellow - all primary shards are allocated, some replicas are not (might be coming up)
- Red - not all primary shards are allocated.

Red health cluster is still functional. All but the bad shards will work as normal. Issues will only persist for bad shards.

Use up to Java 1.7.0_25, _40 has issues with index corruption.

When using HTTP prefer persistent connections to limit overhead. 
