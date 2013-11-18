ElasticSearch & Lucene
======================

Inverted index (Shakespeare example)
--------------
1. Take all plays
2. Break them down word by word
3. For each word store the ids of the documents that contain it.
4. Sort all tokens (words)

Buffer is not inclufded in search until it is flushed to a segment (ie written to disk)

ElasticSearch adds a transaction log over the top of Lucene, to aid in maintaining state. On restart will replay transaction log to get back to previous state.

_flush will force a flush of the elasticsearch buffer.

_refresh will make the latest changes visible to search. Not committed, but still visible (which is lighter). Will do this by default once every 5 seconds.

Merge segments into one larger one, and delete those which are marked for deletion. The new segment is immutable.

Never write small parts, always sequential data. Limits write amplification. Good fit for SSD drives.


