.. Implementations 

Implementations
===============

.. _`BiSciCol`: http://biscicol.org/
.. _`NMNH`: http://nmnh-fims.si.edu/

Refer to documentation for particular projects that utilize the FIMS system for instructions on using the interface.  This documentation focuses on development for back-end components and more generally on topics that all implementations share, such as minting globally unique identifiers.  Here we describe just the BiSciCol implementation to show how one possible FIMS implementation may be used.

BiSciCol 
--------
The `BiSciCol`_ implementation uses a triplestore data storage engine, a dedicated EZID name assigning authority number, and supports a number of different projects that use this implementation directly:

 * Barcode of Wildlife sites (currently Kenya, Mexico, Nigeria, South Africa)
 * University and Jepson Herbarium
 * Diversity of the IndoPacific (DIPNet)
 * New York Botanical Garden

Instances calling some portion of BiSciCol services but running their own interfaces:
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 * Amphibian Disease Portal  (in development: this instance will only mint expedition identifiers and use validation services)
 * Automated Reef Monitoring System Project (in development: substitutes a mysql data storage engine for the triplestore data storage)



