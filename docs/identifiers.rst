.. Identifers

Identifiers
=================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources (described below).  "Shoulders" (borrowed from the EZID terminology)
are minted and encoded/decoded to correspond to Integer values in the database.  All Shoulders
end with the integer "2" and use the following character based codes for translation:

`ABCDEFGHIJKLMNPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz`

Each FIMS system installation must use its own name assigning authority number and register with California Digital Library's EZID service to mint Archival Resource Keys (ARKs).  

All of the following types of identifiers are represented as ARKs and registered with the CDL's EZID service:

Expedition identifiers
--------------------
 * Mutable, representing the most current version of a particular spreadsheet 
 * Metadata:
    * expeditionCode  
    * expeditionTitle 
    * userId (who created this expedition)
    * ts  (when loaded)
    * projectId (project this belongs to)
    * public (public or not)

Dataset identifiers
--------------------
 * Immutable
 * Belongs to a specific expedition
 * Metadata:
    * webAddress (where this dataset can be found, in its native format, depending on installation)
    * userId (who uploaded this dataset)
    * doi (an optional doi, in addition to the created ARK)
    

Resource identifiers
--------------------
 * Belongs to an expedition.    Multiple resources may be specified for each expedition.
 * Implements suffix-passthrough feature to identify individual resources within each dataset. For example, a single "Material Sample" identifier is created for each expedition.  If the expedition has 1000 rows representing physical samples, 1000 identifiers can be resolved by appending a locally unique suffix on to the Resource Identifier root.
 * A resource identifier plus the locally unique primary key loaded for the most recent dataset in an expedition forms the globally unique identifier for a particular resource. 
