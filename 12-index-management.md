Index Management
================

Index will automatically be created for you unless you specify otherwise in the config.

Mappings can be inherited. Use the _default_ keyword to define the root.

Templates can be used as default configurations for named types. Can specify a wildcard prefix to define what this template applies to, for example te* will match anything beginning with te

Close an unused index to free file handles etc, using the _close endpoint. Reverse the operation using the _open. Can take a couple of minutes to do this if you do not flush the index before closing it.

Disable the refresh interval by setting to value -1. This is useful when inserting a lot of data.

Optimize - don't usually want to call it when being used actively. Only call on old data which is not going to change. This is not throttled so be careful in production.

Aliases can point to a single index or multiple indicies. Calling an index method on an alias which points to multiple aliases will fail, as it doesn't know which to operate on.
Renaming an alias is done by using the _aliases endpoint, by specifying a remove and add in the same call. This is done atomically.
