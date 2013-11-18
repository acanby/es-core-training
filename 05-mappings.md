Advanced Search & Mappings
==========================

Setup a mapping when you create an index, or later. Add down the track, can only add, not remove existing mappings.

Type mapping - multi_field. Allows you to index the same field in different ways in the same document.

ElasticSearch stores the source of an index by default. This is compressed, and can usually be left as the default. DO NOT store source fields as this is not necessary.

Setting dynamic to false will cause unmapped data to be ignored. Setting to strict will throw an error when new data is found.

Multi field access will infer a default field to be that with the same name. Ie user.name and user.raw, user will by default return the value of user.name, unless otherwise specified

_all field has its own analyzer, does not relate to any of the specified analyzers for fields.
_all index can bel disabled, which would save a significant amount of space.

If you don't specify a timestamp, it will use now() automatically. Can also be configured to pick up the value from the database.

Cheaper to delete whole index and recreate rather than mark for deletion and rebuild segments. (Only if starting from scratch, and useful for limited time)

_score on a match_all query is meaningless, as all documents should return a score of 1

High cardinality strings are expensive when building indexes/reverse indexes. 
ElasticSearch automatically chooses the most optimal structure based on the field nature, considering: data type, single/multi valued, number of uniques, maximum value.

Don't do deep pagination, it requires n possible values returned from each shard. Say page 10000, you need 100000 from each shard, to discard 490000. Google doesn't even go past 100, and what data do you have that necessitates it?

Search type = COUNT will do exactly that, and return a count with no additional data.

SCAN is an efficent way of getting all documents, or a subset of (with filters). This is optimised at the Lucene level also.

Queries - important for relevance
Filters - no scoring, typically cacheable yes/no answers
Default execution is filters first, then queries, to limit parsing required.

Clauses
* Must - must match
* Must_not - must not match
* Should - doesn't have to match, but if it does it gets a higher score.

Slop - the number of words allowed to appear within a phrase before a match is considered invalid. Ie slop=0 search quick fox on terms quick brown fox would not be founf. Changing slop to 1 or more would work in this case. Remember that all words are required.

Phrase_prefix - poor mans auto complete. Do not use for this purpose! Use Suggesters API instead. Will give Did you mean ...? searches etc.


