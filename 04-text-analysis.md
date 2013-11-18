Text Analysis
=============

Grammar
* Stemming - jumps, jumping, jumped all boil down to jump
* Interchangeable - quick, fast, etc. Aka synonyms.
* Stop words - The, and, a, is. Words which provide no meaning.

toLower() all words before removing stop words, as this will cut the stop word list size dramatically. 

Test analyzers usng the _analyze tokeniser
eg: curl -XPOST 'localhost:9200/_analyze?tokenizer=keyword&filters=lowercase' -d 'New York' -> returns the query parsed with the given tokenizer.

Not recommended to add tokenizers to config files, requies restarting when changes made.

ICUTokenizer knows how to handle Unicode languages, eg Thai. 
These tokenizers are available as a plugin, as they almost double the size of elasticsearch to download.

UAX URL Email tokenizer will work like a standard tokenizer, but maintains URLs and Email addresses. They are stored properly, and no attempt to split is made.

NGram view - window into a word of varying size, eg window size 2 would return foo bar = [fo,oo,ba,ar]
Edge NGram is the same as NGram but anchored to the beginning of a word. Useful for type ahead searching. Foo Bar would return [f,fo,foo,b,ba,bar]


1.0 removes the stopword analyzer as a default analyzer. Updaters need to rebuild index, as existing indexes will use existing stopword filter


