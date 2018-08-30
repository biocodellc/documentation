.. query

.. _psql tokenization: https://www.postgresql.org/docs/9.5/static/textsearch-intro.html#TEXTSEARCH-INTRO_CONFIGURATIONS

FIMS Queries
============

FIMS provides a custom sql-like query syntax to help you find the data you need.

By default, the query terms are executed against all columns in the project. To execute a query against a specific column,
you can construct the query in the form ``columnName:query``.

The `full text search`_ query ``japan`` would return all results where a column contains the word ``japan``. Where as the `full text search`_ query
``column1:japan`` would return all results where **column1** contains the word ``japan``.

All queries can be constructed using the sql operators *AND*, *OR*, and *NOT* as well as groupings within `()`;

The query ``_expeditions_:myExpedition and not japan`` would return all results in the *expedition* ``myExpedition`` which do not
contain the word ``japan``.

Below you will find more information about the supported queries.

Supported Queries
-----------------

The following queries are supported:

* `full text search`_
* `comparison`_
* `project`_
* `expedition`_
* `exists`_
* `like`_
* `phrase`_
* `range`_
* `select`_

.. _`full text search`:

full text search
^^^^^^^^^^^^^^^^

This the default query, and will perform a search on the :ref:`tokenized <tokenization>` version of the uploaded data.

 ``col1:value`` - will perform a fts on ``col1`` for ``value``
 ``col1:val*`` - will perform a fts on ``col1`` for words starting with ``val``
 ``value`` - will preform a fts on all columns for ``value``
 
.. _comparison:

comparison
^^^^^^^^^^

This query is used to compare 2 values. The following operators are supported:

NOTE: for correct comparison results when using ``<``, ``<=``, ``>``, ``>=``, the Attribute dataType should be one of (Integer, Float, Date, Datetime, Time).
This can be set via the project configuration. Talk to your project administrator about this.

 ``=`` - equals  
 ``<>`` - not equals  
 ``>`` - greater then
 ``>=`` - greater then or equal to
 ``<`` - less then
 ``<=`` - less then or equal to

.. _project:

project query
^^^^^^^^^^^^^^^^
This query is will filter the results based on the project(s) that they belong to.

The query ``_projects_:1`` would return everything uploaded under project ``1``
The query ``_projects_:[1, 2]`` would return everything uploaded under project ``1`` or ``2``

.. _expedition:

expedition query
^^^^^^^^^^^^^^^^
This query is will filter the results based on the expedition(s) that they belong to. Note: as expeditions are only unique within a project, 
you most likely want to specify a project query as well.

The query ``_expeditions_:myExpedition`` would return everything uploaded under ``myExpedition``
The query ``_expeditions_:[myExpedition1, myExpedition2]`` would return everything uploaded under ``myExpedition1`` or ``myExpedition2``

.. _expedition:

.. _`_exists_`:

_exists_ query
^^^^^^^^^^^^^^

This query returns results where a column has a value.

The query ``_exists_:column1`` would return all results where ``column1`` has a value.
The query ``_exists_:[column1, column2]`` would return all results where ``column1`` or ``column2`` has a value.

.. _like:

like query
^^^^^^^^^^

This query performs a sql ``ILIKE`` (case-insensitive ``LIKE``) query.

``col1:"%value"`` - ``col1 ILIKE '%value'``

.. _phrase:

phrase query
^^^^^^^^^^

This query performs a sql ``ILIKE`` (case-insensitive ``LIKE``) query.

``col1:"some value"`` - ``col1 ILIKE '%some value%'``


.. _range:

range query
^^^^^^^^^^^

This is a shorthanded way to perform a comparison query.

NOTE: for correct comparison results, the Attribute dataType should be one of (Integer, Float, Date, Datetime, Time)
This can be set via the project configuration. Talk to your project adminstrator about this.

``col1:[1 TO 10]`` - ``>= 1 AND <= 10``
``col1:[1 TO 10}`` - ``>= 1 AND < 10``
``col1:{1 TO 10}`` - ``> 1 AND < 10``
``col1:{* TO 100]`` - ``<= 100``

.. _select:

select query
^^^^^^^^^^^^

Used to select related parent/child data along with the queried entity. The provided value should be the conceptAlias of the Entity to select.
The provided conceptAlias' do need to be related to the query entity, but do not need to be directly related. For example, if you are querying a
parent entity, you can also select the grandChildren and the grandParents. Any combination of related entities can be selected.

NOTE: ``_select`` queries should not be preceded/followed by `and` or `or` keywords and can not be preceded by the `not` keyword.

``_select_:parentEntity`` - selects both child and parent entity results for the query
``_select_:[parentEntity, grandParentEntity]`` - selects both child and parent entity results for the query

.. _tokenization:

Tokenization
------------

Text fields go through a tokenization process before they are indexed. This process attempts to breakdown text into words
and numbers as well as converting words to their normalized form.

Tokenization Ex::

    "many donkeys" -> ["many", "donkey"]

For more information, you can view the `psql tokenization`_.