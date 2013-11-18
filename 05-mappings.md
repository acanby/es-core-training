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

Use range filters where possible. Not a good idea to use on Strings, as they will need to be brought into memory. Best usage for numbers.
Do range filters rather than queries.... it is either in the range or not. And you get caching for free.

Control prefix/wildcard search with a decent length prefix. Will speed up the query as it limits the permutations.

Fuzzy now quite efficient, used to be similar to prefix/wildcard. Now very suitable for usage. Looks for spellings up to 2 edits from the inputted word.

Filter naming can save space in the cache, but means you must do the logic to retrieve the cached bitset from the cache. Tradeoffs.
Filter on less changing items (eg on midnight for logging), and then cache based on the resultant subset. This will eliminate a large percentage of data, and still yeild acceptable performance.

Warmer API ensures that the segment is warmed or ready to go before it is exposed to search. This ensures that there is no JIT like process for the first user to hit the page
Warmers can be added to an existing index and will be run on new instances. Can be preconfigured to load specific data using queries etc.

When highlighting the original text needs to be available, using the source field. This is necessary as the analyzed value might not represent the data you want to display.
Three types of highlighters:
1. Highlighter
- no need for extra info during indexing, but does not support complex queries (will actually fail)
2. Fast Vector Highlighter
- Considerably increases the size of the index (somewhere around 2x)
- No need for re analysis of index
- Requires storing term vectors during indexing
- It is not fast? (Despite the name)
3. Postings highlighter (new)
- Needs quite a bit of setup
- Gives sentence based results
- Doesn't use the space of the FVH
- Is actually fast!

Highlighter type is automatically chosen. Will choose FVH if term vectors is enabled, otherwise default highlighter. Can pass in which one you would like (not sure?)
Highlighting can break HTML tags. Use a token which will *not* appear in the HTML, ie || to mark the positions where highlighting occurs. Then parse this into valid markup in your result to the client.

