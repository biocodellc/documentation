.. Identifers

Identifiers
=================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources (described below).  Each FIMS system installation must use its own name assigning authority number and register with California Digital Library's EZID service to mint Archival Resource Keys (ARKs).  

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

BCID Resolution System
--------------------

The BCID Resolution system resolves BCID identifiers that are passed through the Name-to-thing resolver (http://nt2.net/).  All BCID groups identifiers are registered with EZID.  EZID then uses its suffix passthrough feature to pass the suffix back to the BCID resolver.  At this point, a series of decisions are made based on the identifier syntax to determine how to display returned content.  Element-level identifiers,  with registered suffixes in the BCID system, also containing targets, can be resolved to a user-specified homepage.  Un-registered suffixes, or where there is no defined target associated with the identifier, or when machine resolution is specifically requested will return an HTML rendering of the identifier with embedded RDF/XML syntax describing the identifier.  Machine resolution can be specifically requested to any identifier by appending a "?" to the identifier.

.. image:: https://bcid.googlecode.com/svn-history/r27/trunk/web/documents/BCID_flowChart.jpg

*How does this all work in practice?*

Suppose we have group ID = ark:/21547/Et2 (resource=dwc:Event) and do not register any elements.  Now, suppose someone passes in a resolution request for ark:/21547/Et2_UUID, the system will still tell you that this is some (dwc:Event) but can't tell you anything else -- the response will be a machine readable response (RDF/XML).  The response will be rather minimal but extremely predictable- it will tell you the resourceType, date it was loaded, a title and if there is a DOI associated with it.

Now, suppose we decide to register those UUIDs associated with ark:/21547/Et2 and also provide web pages that have some HTML content to look at (targets) then we can show a nicely formatted, human readable page of the collecting event itself and some formatted human readable text (HTML).

However, what if we're a machine and we don't want to look at all the style sheets and extraneous, difficult to parse text, we just want to know when this thing was loaded and the resourceType (regardless if there is some target or not).   This is where "?" comes in... if the "?" is appended on the end of the ark like:  ark://21547/Et2_UUID? then we automatically get RDF/XML.  Minimalist but predictable.
