.. Implementations 

Implementations
====================

.. _`BiSciCol`: http://biscicol.org/
.. _`NMNH`: http://nmnh-fims.si.edu/

BiSciCol Implementation
--------------------
The `BiSciCol`_ implementation uses a triplestore data storage engine, a dedicated EZID name assigning authority number, and supports a number of different projects that use this implementation directly:

 * Barcode of Wildlife sites (currently Kenya, Mexico, Nigeria, South Africa)
 * University and Jepson Herbarium
 * Diversity of the IndoPacific (DIPNet)
 * New York Botanical Garden

Instances calling some portion of BiSciCol services but running their own interfaces:
++++++++++++++++
 * Amphibian Disease Portal  (in development: this instance will only mint expedition identifiers and use validation services)
 * Automated Reef Monitoring System Project (in development: substitutes a mysql data storage engine for the triplestore data storage)

Smithsonian Institution National Museum of Natural Histrory
--------------------
The `NMNH`_  installation uses a dedicated EZID name assigning authority number, has its own web interface, and stores data as spreadsheets.  In addition, it offers services for notifying data managers of loaded datasets.



