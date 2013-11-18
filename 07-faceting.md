Faceting
========

Faceting is calculated on the fly, and gives grouping information relative to the result set being worked upon.

Facets can be applied to a query result set, or on a global scale.

Possible to facet before or after filtering. This is useful when providing search filters and showing non matching groupings.

Typically use a mutli_field type instead of not analyzing a field when attempting to facet. This will leave New York as one item in the faceting, but leave it for proper analysis on the search query.
