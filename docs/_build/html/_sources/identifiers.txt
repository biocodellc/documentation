.. Identifers

Identifiers
=================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources (described below).  Each FIMS system installation must use its own name assigning authority number and register with California Digital Library's EZID service to mint Archival Resource Keys (ARKs).  

All of the following types of identifiers are represented as ARKs and registered with the CDL's EZID service:

Expedition identifiers
-------------------------
 * Mutable, representing the most current version of a particular spreadsheet 
 * Metadata:
    * expeditionCode  
    * expeditionTitle 
    * userId (who created this expedition)
    * ts  (when loaded)
    * projectId (project this belongs to)
    * public (public or not)

Dataset identifiers
-------------------------
 * Immutable
 * Belongs to a specific expedition
 * Metadata:
    * webAddress (where this dataset can be found, in its native format, depending on installation)
    * userId (who uploaded this dataset)
    * doi (an optional doi, in addition to the created ARK)
    

Resource identifiers
-------------------------
 * Belongs to an expedition.    Multiple resources may be specified for each expedition.
 * Implements suffix-passthrough feature to identify individual resources within each dataset. For example, a single "Material Sample" identifier is created for each expedition.  If the expedition has 1000 rows representing physical samples, 1000 identifiers can be resolved by appending a locally unique suffix on to the Resource Identifier root.
 * A resource identifier plus the locally unique primary key loaded for the most recent dataset in an expedition forms the globally unique identifier for a particular resource. 

BCID Resolution System
-------------------------
The BCID Resolution system resolves BCID identifiers that are passed through the Name-to-thing resolver (http://nt2.net/).  All BCID groups identifiers are registered with EZID.  EZID redirects requests to the BCID resolver which has resolution capabilities and features.  The Behaviour of the BCID resolver is explained in the following chart.

.. image:: https://raw.githubusercontent.com/biocodellc/documentation/master/docs/IdentifierService.png

Table 1 notes
 * **graph value** is whether data has been loaded into the FIMS system
 * **suffixpassthrough** is a boolean indicating whether or not this ID supports suffix passthrough.
 * **has specified redirection target** indicates whether or a redirection target has been specified for this URL.

