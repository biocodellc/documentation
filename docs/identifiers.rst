.. Identifers

Identifiers
=================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources.  The three types of identifiers are described below. 

Each FIMS system installation must use its own name assigning authority number and register with California Digital Library's EZID service to mint Archival Resource Keys (ARKs).  

Expedition identifiers
-------------------------
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
-------------------------
 * resourceType: http://purl.org/dc/dcmitype/Dataset
 * Immutable
 * Belongs to a specific expedition
 * Metadata:
    * webAddress (where this dataset can be found, in its native format, depending on installation)
    * userId (who uploaded this dataset)
    * doi (an optional doi, in addition to the created ARK)
    

Resource identifiers
-------------------------
 * resourceType: defined in configuration file
 * Belongs to an expedition.    Multiple resources may be specified for each expedition.
 * Implements suffix-passthrough feature to identify individual resources within each dataset. For example, a single "Material Sample" identifier is created for each expedition.  If the expedition has 1000 rows representing physical samples, 1000 identifiers can be resolved by appending a locally unique suffix on to the Resource Identifier root.
 * A resource identifier plus the locally unique primary key loaded for the most recent dataset in an expedition forms the globally unique identifier for a particular resource. 

BCID Resolution System
-------------------------
The Name-to-Thing resolver (http://n2t.net/) redirects requests to the BCID resolver.  The BCID resolver service enables users to specify forwarding targets by specifying webaddress targets for unique expeditions and datasets.  For resources, targets are defined in the project configuration file, so may be updated dynamically, depending on where the user wants to resolve specific resources.  The followin is a sketch of the resolution service:

The following illustration shows how BCIDs work with local identifiers, the world wide web, and EZID's name-to-thing resolution service.  A field researcher uses their own numbering system, in this casae an identifier labelled 'MBIO56', and uploads their data to FIMS, which assigns it to a resource category 'R2', which being part of the FIMS system has a name assigning authority number (NAAM) of 21547 under the ark: scheme, which is then registered with the Name-to-thing resolution service. Resolution requests coming through name-to-thing are re-directed to the BCID resolution service, which then either displays object metadata or redirects to a project specified web-page, depending on settings in the FIMS configuration file for this project.

.. image:: https://raw.githubusercontent.com/biocodellc/documentation/master/docs/ResolutionService.jpg

The following chart shows how the BCID resolution works for expeditions, datasets, and resource resolution.  All of these elements are 'BCIDs' and how they are resolved depends on whether they are expedition, dataset, or resource:

.. image:: https://raw.githubusercontent.com/biocodellc/documentation/master/docs/UpdatedIdentifierService.jpg

