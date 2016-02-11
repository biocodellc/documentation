.. sub_sampling

.. _samples: http://purl.obolibrary.org/obo/OBI_0100051
.. _`specimen collection process`: http://purl.obolibrary.org/obo/OBI_0000659

Working with samples and sub-samples
=====================

NOTE: this section assumes the fuseki data storage engine is used in your FIMS installation.

FIMS is a system of samples_ which are the result of some `specimen collection process`_.   Each specimen collection process can be uniquely defined by the procedure used, who performed it, when it was performed and subject and target samples.  Samples can be thought of in terms of a directed graph with each sample as nodes and processes represented by edges, connecting samples with all respective sub-samples. It is important to maintain all points in the chain where significant transformation of material occurs so we can understand the significance of a distinct sample at any point in the chain.   **The FIMS configuration file defines the relationships between samples and processes that join them, mapping a single flat file to a graph-based representation (using the fuseki module)**

The following are use cases describing the generation of target samples (e.g., specimens, sub-samples, tissues, extract).  

*Tissue Sub-sample from Organism:*
Remove representative tissue from a specimen where specimen is an individual or organism. Tissue is typically specified by some anatomical part (e.g. blood, heart, liver, leaf, root).  Multiple tissues from the same organism are all distinct tissues even if they are all just categorized as "muscle".

*Tissue sub-sample from Tissue:*
Derive a sub-sample from an existing tissue (aliquot).  Each aliquot is a new tissue with time it was sub-divided, how it was divided (e.g. knife), and who divided it.

*Environmental Sample (initial collection):*
Refers to the initial sample as extracted from nature (e.g. jar of seawater, core of soil).  This is characterized by isolation from environment at a particular depth, time, and location.

*Environmental sub-sample:*
The environmental sample may be sub-sampled directly after initial collection, for example, passing a liter of sea-water over a filter disc.  This is a distinct sample from the initial environmental sub-sample and is represented by the filter disc and any biological residue that did not pass through the disk.   The process of sub-sampling here is defined by time after initial collection, who performed the task, the size of the membrane on the filter.

*DNA extract:*
DNA extract is technically a sub-sample from tissue, which is in turn derived from some tissue or some environmental sub-sample.  
