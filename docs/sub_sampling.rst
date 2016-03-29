.. sub_sampling

Samples and Sub-sampling
=================

.. _samples: http://purl.obolibrary.org/obo/OBI_0100051
.. _`specimen collection process`: http://purl.obolibrary.org/obo/OBI_0000659
.. _`Semantics in Support of Biodiversity Knowledge Discovery`: http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0089606

NOTE: this section assumes the fuseki data storage engine is used in your FIMS installation.

FIMS is primarly a system of samples_ which are the result of some `specimen collection process`_.   Each specimen collection process can be uniquely defined by the procedure used, who performed it, when it was performed and subject and target samples.  Samples can be thought of in terms of a directed graph with each sample as nodes and processes represented by edges, connecting samples with all respective sub-samples. It is important to maintain all points in the chain where significant transformation of material occurs so we can understand the significance of a distinct sample at any point in the chain.   **The FIMS configuration file defines the relationships between samples and processes that join them, mapping a single flat file to a graph-based representation (using the fuseki module)**

For more information about connecting samples and processes, read the publication `Semantics in Support of Biodiversity Knowledge Discovery`.
