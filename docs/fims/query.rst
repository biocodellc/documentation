.. query

.. _ElasticSearch Analysis: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/analysis.html
.. _ElasticSearch QueryString Query: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html
.. _ElasticSearch Docs: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#query-string-syntax
.. _boolean operators: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_boolean_operators
.. _grouping: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_grouping
.. _range: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_ranges
.. _fuzziness: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_fuzziness
.. _proximity searches: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_proximity_searches
.. _boosting: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_boosting
.. _regular expressions: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_regular_expressions
.. _leading wildcard queries: https://www.elastic.co/guide/en/elasticsearch/reference/5.1/query-dsl-query-string-query.html#_wildcards

FIMS Queries
============

FIMS provides a custom query syntax to help you find the data you need. The FIMS Query DSL is built upon the `ElasticSearch QueryString Query`_.

By default, the query terms are executed against all columns in the project. To execute a query against a specific column,
you can construct the query in the form ``columnName:query``.

The `text`_ query ``japan`` would return all results where a column contains the word ``japan``. Where as the `text`_ query
``column1:japan`` would return all results where **column1** contains the word ``japan``.

All queries can be constructed using the `boolean operators`_ *must*, *must_not*, and *should*. These are similar, although
not equivalent, to the mysql operators *AND*, *NOT*, and *OR* respectively. The default operator is the *should* operator. The operators
*must* and *must_not* are represented by prefixing the query expression with **+** and **-** respectively.

If there is only 1 *should* term (ex query. ``japan``), this is effectively a *must* query, and would return all results
where a column contains the word ``japan``. However the query ``japan australia`` will return all results where a column
contains the word ``japan`` **or** the word ``australia``.

The query ``+expedition:myExpedition -japan`` would return all results in the *expedition* ``myExpedition`` which do not
contain the word ``japan``.

Complex queries can be constructed using `grouping`_.

See the `ElasticSearch Docs`_ for more information regarding the query syntax.

Below you will find more information about the supported queries.

Supported Queries
-----------------

The following queries are supported:

* `text`_
* `phrase`_
* `range`_
* `expedition`_
* `_exists_`_
* `fuzziness`_
* `proximity searches`_
* `boosting`_

We **do not** support the following:

* `regular expressions`_
* `leading wildcard queries`_

.. _text:

text query
^^^^^^^^^^

This the default query, and will perform a search on the :ref:`tokenized <tokenization>` version of the uploaded data.


.. _phrase:

phrase query
^^^^^^^^^^^^

This query will perform an exact match on the uploaded data. This is done by surrounding your query term in quotes.

The query ``column1:"exact phrase"`` will return all results where ``column1`` has the exact value ``exact phrase``.


.. _expedition:

expedition query
^^^^^^^^^^^^^^^^
This query is will filter the results based on the expedition that they belong to.

The query ``+expedition:myExpedition`` would return everything uploaded under ``myExpedition``

.. _`_exists_`:

_exists_ query
^^^^^^^^^^^^^^

This query returns results where a column has a value.

The query ``_exists_:column1`` would return all results where ``column1`` has a value.


.. _tokenization:

Tokenization
------------

Text fields go through a tokenization process before they are indexed. Currently the tokenization process splits words
on any non-letter character or camelCase. The tokens are then lowercased and further processed to remove any possessives
and plurals.

Tokenization Ex::

    "manyDonkeys" -> ["many", "donkey"]

The above result would match the following queries::

    many

    manyMore

    many Donkeys

    manyDonkeys

    DONKEYS

    donkey


However it will not match::

    manydonkeys

For more information, you can view the `ElasticSearch Analysis`_. Our current anlyzer settings
can be found :ref:`here <elastic_search_config-analyzer>`.