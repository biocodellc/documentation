.. _configuration_files:

Configuration Files
======================

GEOME has a network level configuratino file which defines network level rules and all available data properties and entities.  Each project has its own configuration file as well which supplements the GEOME network configuration file.  All configuration files are written in JSON This is where the :ref:`projects` specific configuration is
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
