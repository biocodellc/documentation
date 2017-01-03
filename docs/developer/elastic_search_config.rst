.. _elastic_search_config:

Following is information about configurations changes that are made when setting up a new ElasticSearch cluster

Dynamic Templates
=================

Creating dynamic templates allows us to modify the default index settings and mappings.

Analyzer
^^^^^^^^

We are currently using a custom default analyzer. To set this up, make a ``POST`` request to ``/_template/{template_name}`` with the following in the body::

    {
      "template" : "*",
      "settings" : {
        "index" : {
          "analysis" : {
            "analyzer" : {
              "default" : {
                "filter" : [
                  "word_delimiter",
                  "lowercase",
                  "asciifolding",
                  "kstem",
                  "stop"
                ],
                "char_filter" : [
                  "html_strip"
                ],
                "type" : "custom",
                "tokenizer" : "standard"
              }
            }
          }
        }
      }
    }

Index Aliases
=============

Indexes are created for each project. When creating an index, the format is ``{projectId}_{todays_date}``. Then we use index aliases to point to the latest index version.
The index alias format is ``{projectId}``. The advantage to this is that if we need to update any settings, mappings, etc we are able to reindex to existing
data and point the index alias to the updated index, without changing the index name.


