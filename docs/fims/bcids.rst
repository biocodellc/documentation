.. bcids

NOTE: This page needs Updating!

Introduction to BCIDs
=====================

BCIDs addresses offer a robust, easy to use service, extending the [http://n2t.net/ezid California Digital Library EZID] solution for the biological collections community.  EZIDs offer  ease of use, scalability, long-term persistence, resolvability, and a consistent metadata format.  BCIDs extend this by offering an easy mechanism to assign billions of identifiers right now for data elements (individual samples or processes acting on those samples).  BCIDs allow any local ID/UUID to resolve to a group level identifier.  Organizations have the option of later purchasing their own EZID subscription for more control over their identifiers.  All of the representations that are referred to by BCIDs fall under the [http://creativecommons.org/licenses/by/3.0/ Creative Commons Attribution 3.0 License], enabling others to reference your identifiers and the objects that they refer to as long as they attribute them.  Since BCIDs are self-describing in HTML and RDF/XML, downstream users need only maintain the original identifier 

Discussion
----------

BCIDs are hierarchical identifiers, allowing a single "group" to represent and resolve many sub-identifiers.  A group is associated with a column of local identifiers, such as a set of specimens, sharing a single common concept.  These concepts are, for now, a [http://biscicol.org/bcid/concepts.jsp constrained list] defined by the  biodiversity informatics communities and assembled by the [http://biscicol.org BiSciCol project].  Elements are references to individual instances, such as an individual specimen.  

A data group may have the following form:

  * ark:/21547/R2

A data element within the group may extend this in the following manner:

  * ark:/21547/R2MBIO56

The structure above defines the following segments:

||description||value||notes||
||scheme||ark:||all BCIDs are ARKs||
||NAAN (Name Assigning Authority Number)||21547||all BCIDs use this NAAN||
||data group||R2||The data group identifier must be assigned by BCID||
||data element||MBIO56||The user can supply a local ID, Darwin Core Triplet, or UUID||

Data elements share a root structure with a data group. The delimiter between the scheme, NAAN, and data group is a forward slash.  Data group identifiers always end with the first number and data elements immediately follow this number.
 
Data groups are technically not datasets.  This is because a data group must be defined by a single conceptual entity, and stands for that conceptual entity for all child elements.  For instance, we can define a data group of "Sound".  Any unregistered element that appears following the data group designation will technically be a type of "Sound".  This is useful, for instance, if we have scores of objects or processes that have no web-resolution but we still want to be able to refer to them uniquely and know they are an instance of "Sound".  

We can also attribute a dataset to one or more data groups.  The dataset can be an ARK or a DOI (issued separately). 

Resolution w/ Suffixes 
----------------------
N2T resolver = {{{http://n2t.net/{ARK}}}}  (e.g. http://n2t.net/ark:/21547/R2)

N2T metadata = {{{http://n2t.net/ezid/id/{ARK}}}}  (e.g. http://n2t.net/ezid/id/ark:/21547/R2)

BCID resolver = {{{http://biscicol.org/id/{ARK}}}}  (e.g. http://biscicol.org/id/ark:/21547/R2)

BCID Metadata = {{{http://biscicol.org/id/metadata/{ARK}}}}  (e.g. http://biscicol.org/id/metadata/ark:/21547/R2)

BCID Suffix resolver = {{{http://biscicol.org/id/{ARK}_{Suffix}}}}  (e.g. http://biscicol.org/id/ark:/21547/R2MBIO56)

BCID Suffix Metadata = {{{http://biscicol.org/id/metadata/{ARK}_{Suffix}}}}  (e.g. http://biscicol.org/id/metadata/ark:/21547/R2MBIO56)

Data groups can be assigned a target URL which indicates where to resolve this group.    If the "Maintain local ID's" box is checked on data group creation then that indicates suffixes will be passed through to the resolution target.  The following table illustrates how identifiers resolve. Note that the N2T resolver does not handle suffix-passthrough *yet* so in the short term, N2T will only resolve data groups without suffixes.  

||BCID||Maintain Local ID's||Target URL (group or element)||Ultimate Resolution Target||
||http://n2t.net/ark:/21547/R2||true||NULL||(BCID metadata)||
||http://n2t.net/ark:/21547/R2||false||NULL||(BCID metadata)||
||http://n2t.net/ark:/21547/R2||true||http://biocode.berkeley.edu/specimens/||(BCID metadata)||
||http://n2t.net/ark:/21547/R2||false||http://biocode.berkeley.edu/specimens/||http://biocode.berkeley.edu/specimens/||
||http://n2t.net/ark:/21547/R2MBIO56||true||http://biocode.berkeley.edu/specimens/||http://biocode.berkeley.edu/specimens/MBIO56||
||http://n2t.net/ark:/21547/R2MBIO56||false||http://biocode.berkeley.edu/specimens/||http://biocode.berkeley.edu/specimens/||

Relationship with EZIDs 
-----------------------

All group level identifiers are registered as EZIDs.  It is possible to also register element level identifiers as EZIDs.  Please talk to us if you would like to do this.

RDF/XML Accept Headers 
----------------------

Calling the Metadata or Resolution targets using the BCID resolver will return RDF/XML.  To enable this, you must pass in the "application/rdf+xml" accept header.  To do this in curl, try:

{{{curl -H "Accept: application/rdf+xml" http://biscicol.org/id/metadata/ark:/21547/R2MBIO56}}}

You can also try it out using [http://linkeddata.informatik.hu-berlin.de/uridbg/index.php?url=http%3A%2F%2Fbiscicol.org%2Fbcid%2Fid%2Fark%3A%2F21547%2FR2&useragentheader=&acceptheader=application%2Frdf%2Bxml an online tool using and the "ark:/21547/R2" BCID]. 

Developer Information
---------------------
  * View the list of [http://biscicol.org/id/bcid.wadl BCID REST services]
  * [http://biscicol.org/bcid/javadoc/index.html JavaDocs] are available
  * This is an open source project, please contact the owner to contribute!
