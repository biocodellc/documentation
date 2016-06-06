.. FIMS Introduction

Introduction
===================

Biocode-FIMS is used for data validation, expedition planning, and data management for field-based surveys enabling tracking physical objects including organisms, soil cores, water samples, and sub-samples.  If you would like to start your own Biocode FIMS project, you can either download and install the relevant modules (all freely available) or contact the owner of the 
`BiSciCol FIMS installation`_ code site to see if you can be added as a project to this installation.


Biocode FIMS Web Application
*******************

Biocode FIMS has multiple running instances, in support of a variety of field-based sampling projects.  
An example of how the FIMS components work together is running at the `BiSciCol homepage`_.   The biscicol-fims_ codebase 
is one example of a FIMS implementation which features data validation, a graph-based data storage engine, assignment of globally unique identifiers for expeditions, datasets, and every defined sample and process.  Project administrators to control and validate specific fields, while allowing users to add their own data to spreadsheet templates.   

For developers: All Biocode FIMS installations use the biocode-fims-commons_ code repository and may include 
also the biocode-fims-fuseki_ codebase for working with triples.

.. _biocode-fims-commons: https://github.com/biocodellc/biocode-fims-commons
.. _biocode-fims-fuseki: https://github.com/biocodellc/biocode-fims-fuseki
.. _biscicol-fims: https://github.com/biocodellc/biscicol-fims
.. _fuseki: https://jena.apache.org/documentation/serving_data/
.. _`BiSciCol homepage`: http://biscicol.org/
.. _`BiSciCol FIMS installation`: http://biscicol.org/index.jsp

How FIMS is organized
-------------

The following sections describe how data is stored in the FIMS system.  See the identifiers section for more information how identifiers are applied at each level.

Projects
+++++++++++

A project defines a set of data held in common by a group of contributors.  The data from a single project shares common concepts, attributes, and validation rules.  It is owned by a project administrator user who has the power to set validation rules, concept mappings, and users that are permitted to share data under the project.  New projects are created infrequently and require super-user status to create (currently the owner of BCID site itself).   However, once created, project values can be edited by an assigned project administrator.

To create a new project, please contact the BCID owner.

Expeditions
+++++++++++

Projects contain many expeditions. An Expedition refers to a group of datasets and is associated with a project. Users may freely create expeditions.

Datasets
+++++++++++

Expeditions contain many datasets.  A dataset typically refers to an excel spreadsheet.  When loaded through the associated Biocode-FIMS expeditions, a reference to this dataset is stored as part of the Biocode-FIMS BCID system with a unique ARK.  When a dataset is created, it is given a unique code, which is owned by the user that first uploaded it.  This user may choose, to re-load this dataset again, in which case a new reference will be loaded here.

Resources
+++++++++++

All expeditions contain one or more resources.  A special resource identifier is created for each of the expedition resources.  For example, a project cataloging tissue
samples may choose to define a resource for the tissue itself, a resource for the collecting event data associated with the tissue, and an identification 
resource containing information about the taxonomic name associated with the tissue.  Or, a project may choose to simply bundle all of this information into a single resource 
describing all of this data.
