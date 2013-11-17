ElasticSearch
=============

Introduction
------------

ES_HEAP_SIZE - JVM size, should be set. Typically to 50% of available ram on each box
Disable multicast for production

Ports used
* HTTP [9200-9300) chosen based on available ports
* Transport [9300-9400) as above, chosen based on available ports

Plugins
* Java requires restart
* Others do not
Ensure that each node has required plugins, they are not propogated.


