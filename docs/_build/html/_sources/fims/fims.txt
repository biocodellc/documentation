.. FIMS 

.. _biocode-fims-commons: https://github.com/biocodellc/biocode-fims-commons
.. _biocode-fims-fuseki: https://github.com/biocodellc/biocode-fims-fuseki
.. _biocode-fims-sequences: https://github.com/biocodellc/biocode-fims-sequences
.. _biscicol-fims: https://github.com/biocodellc/biscicol-fims
.. _fuseki: https://jena.apache.org/documentation/serving_data/
.. _`BiSciCol site`: http://www.biscicol.org/
.. _`GeOMe site`: http://www.geome-db.org/
.. _`GeOMe documentation`: https://www.geome-db.org/docs/helpDocumentation.pdf
.. _`NMNH FIMS documentation`: https://nmnh-fims.si.edu/fims/docs/FIMS-NMNH-Help_Master.pdf
.. _`BiSciCol FIMS installation`: http://biscicol.org/index.jsp
.. _`http://n2t.net/ark:/21547/R2MBIO56`: http://n2t.net/ark:/21547/R2MBIO56


User Documentation
==============================

This document contains some general information for FIMS users to help explain how FIMS is organized.
since each FIMS installation has its own set of user-documentation, refer to the help documentation provided with each 
FIMS installation's homepage or project-specific help.  

The FIMS system is organized around a central "network", which is composed of a group of projects that belong to this network.  A project defines a set of data held in common by a group of contributors.  The data from a single project shares common concepts, attributes, and validation rules.  It is owned by a project administrator user who has the power to set validation rules, concept mappings, and users that are permitted to share data under the project.  New projects are created infrequently and require the project administator to create and modify.

Projects contain many expeditions.  Each user can create an expedition representing a unique set of data which may correspond to metadata for samples
residing in a 96 well plate, data from a single day of collecting, or any other organizing concept.  Expeditions work best if they are limited to less
than 1,000 records per spreadsheet, however, larger numbers of records per expedition are possible.  Each expedition has a unique name that you assign to it
and which can be referred to later for modifying or querying data.

All expeditions contain one or more resources.  How many resources exist per expedition is defined by the project itself.  Most projects currently have just
one resource per project.  Examples of resources may be collecting events, specimens, or tissue samples.  
