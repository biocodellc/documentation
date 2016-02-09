.. FIMS Introduction

Introduction
===================

Biocode-FIMS is used for generating spreadsheet templates and validating data for field expeditions, typically involving 
genomic workflows and working with biological samples and sub-samples.  If you would like to start your own Biocode FIMS 
project, you can either download and install the source code or contact the owner of the 
Biocode FIMS code site to see if you can be added as a project to an existing installation.

Operation
*******************

Contained here is documentation for developers or anybody else wishing to understand how the FIMS system operates.  
FIMS is a modular application, and is broken down into components that 1) validate data, create spreadsheet templates, assigns identifers 
using request and responses serialized as JSON, 2) store 
data (either as triples, relational format, or as spreadsheets), 3) and front-end pieces for interacting with users with responses serialized typically
as HTML.

An example of how the FIMS componenets work together is running at the `BiSciCol homepage`_.   The biscicol-fims_ codebase 
is a specific FIMS implementation which includes jar files built by the biocode-fims-commons_ and  biocode-fims-fuseki_ codebases. 
Common functions and services are run by biocode-fims-commons_, creating
identifiers and interpretes validation rules while the biocode-fims-fuseki_ codebase sends data to the 
the fuseki_ triplestore, and handles features for querying data.

.. _biocode-fims-commons: https://github.com/biocodellc/biocode-fims-commons
.. _biocode-fims-fuseki: https://github.com/biocodellc/biocode-fims-fuseki
.. _biscicol-fims: https://github.com/biocodellc/biscicol-fims
.. _fuseki: https://jena.apache.org/documentation/serving_data/
.. _`BiSciCol homepage`: http://biscicol.org/

