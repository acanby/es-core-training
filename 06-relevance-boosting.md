Relevance and Boosting
======================

Relevance - how well does a document match a query?
- The more a term occurs in a document, it generally means it is more important (excluding stop words for example)

Inverse Document Frequency - the less the term appears in the index as a whole, the more relevant or important it is.

Shorter ocuments likely to be more relevant than longer documents

_explain helps analyze results and shows the weightings applied to get the results. This can be helpful for debugging search results.

Influence relevance by boosting. This essentially says give x field more importance over y & z.
Not recommended to boost fields at index time. This stores the data in your index at a given boost, which may not be appropriate for certain queries. Must reindex to update these boost parameters.
Better to do boosting at query time to ensure that boosts are applied only to fields which need them, and only at a time which is suitable/logical.
Document level boosting is suitable for indexing time. There is no way to do document boosting at query time.

Boost_factor - does not normalize the boost value, it is purely a mulitiplier.

Use the appropriate way to access field values
- doc['popularity'] - loads from the field cache, very fast.
- _source.popularity - loads from the _source, slow and heavy.
- _fields['popularity'] - loads from the stored fields, could be quicker than _source but still heavy and slow compared with doc notation.

