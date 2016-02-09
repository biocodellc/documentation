.. Identifers

Identifiers
=================

FIMS uses a centralized minting service to assign identifiers for three types of identifiers: 
expeditions, datasets, and resources (described below).  "Shoulders" (borrowed from the EZID terminology)
are minted and encoded/decoded to correspond to Integer values in the "bcids" table in mysql.  All Shoulders
end with the integer "2" and use the following character based codes for translation:

`ABCDEFGHIJKLMNPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz`

Expedition identifiers
--------------------
 * Mutable
 * Metadata:

Dataset identifiers
--------------------
 * Immutable
 * Belongs to a specific expedition
 * Metadata:

Resource identifiers
--------------------
 * Belongs to an expedition
 * Implements suffix-passthrough feature to identify individual resources within each dataset
 * For example, a single "Material Sample" identifier is created for each expedition.  If the expedition has 1000 rows representing physical samples, 1000 identifiers can be resolved by appending a locally unique suffix on to the Resource Identifier root.
