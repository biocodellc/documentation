.. types_of_identifiers

Types Of Identifiers
======================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources.  The three types of identifiers are described below. 

Each FIMS system installation must use its own name assigning authority number and register with California Digital Library's EZID service to mint Archival Resource Keys (ARKs).  

Expedition identifiers
----------------------
 * resourceType: http://purl.org/dc/dcmitype/Collection
 * Mutable, representing the most current version of a particular spreadsheet 
 * Metadata:
    * expeditionCode  
    * expeditionTitle 
    * userId (who created this expedition)
    * ts  (when loaded)
    * projectId (project this belongs to)
    * public (public or not)

Dataset identifiers
-------------------
 * resourceType: http://purl.org/dc/dcmitype/Dataset
 * Immutable
 * Belongs to a specific expedition
 * Metadata:
    * webAddress (where this dataset can be found, in its native format, depending on installation)
    * userId (who uploaded this dataset)
    * doi (an optional doi, in addition to the created ARK)
    

Resource identifiers
--------------------
 * resourceType: defined in configuration file
 * Belongs to an expedition.    Multiple resources may be specified for each expedition.
 * Implements suffix-passthrough feature to identify individual resources within each dataset. For example, a single "Material Sample" identifier is created for each expedition.  If the expedition has 1000 rows representing physical samples, 1000 identifiers can be resolved by appending a locally unique suffix on to the Resource Identifier root.
 * A resource identifier plus the locally unique primary key loaded for the most recent dataset in an expedition forms the globally unique identifier for a particular resource. 

