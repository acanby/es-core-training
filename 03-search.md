Search
------

Searching via Lucene query string is not recommended.
- Difficult to read, hard to debug
- Use Query DSL instead.

Match query is the search box tool. Consider it like a google search.
query_string json will search in an all index. Can specify a specific index to use, ie message: "my value"

Filters are not able to do full text search, and cannot handle relevence. Mainly a binary query (true/false).

Sort needs to load everything required into memory. This is dependent on the size of the dataset, and the query being run.
Sort by default returns result in sorted order
Search will load into memory all documents then exclude, meaning a small query will still return all results and then filter



