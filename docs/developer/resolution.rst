.. Resolution

Resolution System
=================

The following illustration shows how BCIDs work with local identifiers, the world wide web, and EZID's name-to-thing resolution service.  A field researcher uses their own numbering system (e.g. 'MBIO56'), and uploads their data to FIMS, which assigns it to a resource category (e.g. 'R2').  The FIMS system itself is registered under the ark: scheme, and has a name assigning authority number (NAAN) of 21547.  Resolution requests coming through name-to-thing are re-directed to the BCID resolution service.

.. image:: /images/resolution.png

The following chart shows how BCID resolution works for expeditions, datasets, and resources in the FIMS system with actions falling under forwarding, or metadata display.  Forwarding behaviour is determined by either the specification of a target webaddress in the database, or absent that, a specification in the project's configuration file.

.. image:: /images/resolverBehaviour.png

