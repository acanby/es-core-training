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

Primary shard - first to receive data
Replica shard - 0 or more per Primary. Defaults to 1. Increases availability, will be promoted to primary should existing primary go down.
Replicas can also serve up queries.

Endpoints for the API typically use _ as a prefix, eg: _search

Field Data types
* Core - string, number, boolean, datetime, base64 enc
* Complex - array, object
* Other - inc geo-coding points

PUT vs POST
_id is optional, can also be extracted from a field in the document.
POST will autogenerate _id.

Index will be auto created by default, but can be disabled. Use action.auto_create_index: false to disable

_create operation - acts as an index-if-absent operation. Index will fail if the document does not exist.

Can request specific fields from the API if required. Add get param '?fields=field_name'
Can suggest that local copies are used in GET requests, as opposed to round robin. use ?preference=_local

Use verb HEAD to get an exists/does not exist status on an id passed into the API

When paired with a database, consider not versioning data stored within elasticsearch.
Each write operation will return the newest version number, (ie the worked on document)
Each write operation can accept a version number, which is the expected version to work on. If this number does not match the version found by elasticsearch, the operation will fail

Index requests are cached by elasticsearch, for around a minute. This is useful for requests which are near enough to simultaneous.

Updates
get-then-reindex to limit version conflicts and network roundtrips
retry_on_confluct specifies the number of times to retry an idempotent update
Updates will be retried if there is a version conflict between the get and update.
Only works if _source is stored (is enabled by default)
_update will update the document identified by the id in the url path. Existing data will be wrapped in a doc json block.
upsert param can be added to do an update if exists, create otherwise type operation.

Scripts can do anything that the elasticsearch user can do. They should typically be disabled for production use.

_mget will return multiple documents at once, limiting the overhead of HTTP.
