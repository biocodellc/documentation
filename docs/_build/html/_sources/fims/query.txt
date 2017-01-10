.. query

.. _Docs: https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis.html

Biocode FIMS ElasticSearch Query Information
============================================

Below you will find information about how queries are matched for Biocode FIMS implementations using ElasticSearch.

Querying
--------

Currently queries can be filtered on:

* expeditions
* columns
* full text search

columns
^^^^^^^

This is a ``{key}:{value}`` pair, where ``{key}`` is either a ``columnName`` or a ``columnUri`` defined in the project
configuration file (:ref:`config files <configuration_files>`) or `_all`_. When using ``{key}:{value}`` queries, the ``{value}`` is
an exact match.

.. _`_all`:

_all query
^^^^^^^^^^

The _all Query is a special query which performs a full text search across all columns in the project. This is a much
more lenient query compared to the exact match detailed above and follows the tokenization process detailed
:ref:`below <tokenization>`.

.. _tokenization:

Tokenization
------------

Currently the tokenization process splits words on any non-letter character or camelCase. The tokens are then lowercased
and further processed to remove any possessives and plurals.

Tokenization Ex::

    "manyDonkeys" -> ["many", "donkey"]

The above result match the following queries::

    _all=many

    _all=manyMore

    _all=many Donkeys

    _all=manyDonkeys

    _all=DONKEYS

    _all=donkey


However it will not match::

    _all=manydonkeys

For more information, you can view the Elastic Search Analysis Docs_. Our current anlyzer settings
can be found :ref:`here <elastic_search_config-analyzer>`.