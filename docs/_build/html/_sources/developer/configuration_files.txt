.. _configuration_files:

XML Configuration File
======================

Each project contains its own xml configuration file. This is where the :ref:`projects` specific configuration is
specified. This includes :ref:`resources`, attributes, validation rules, and relations.

Attributes
----------

DataType
^^^^^^^^

Each attribute may specify a ``dataType``\ . A dataType can be specified to provide additional validation,
and in the case of date, datetime, and time, can be used for data formatting. This is especially helpful
for standardizing the data to aid in querying and analysis.

The following ``dataType`` are supported:

* String (default if not specified)
* Integer
* Float
* Date

  * must specify ``dataformat`` as well

* Time

  * must specify ``dataformat`` as well

* Datetime

  * must specify ``dataformat`` as well
