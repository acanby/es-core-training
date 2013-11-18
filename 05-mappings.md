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


