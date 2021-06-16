.. Installation

Installation
============

This content is for people wishing to install GEOME on their own server.

Details
-------

GEOME consists of a core set of Java classes and REST services.  Developers have a choice of interacting with the REST services 
running _BCID, which has built in EZID minting capabilities, or running their own 
instance of _BCID and installing their own EZID instance requiring a purchase of an `EZID account`_.

.. _`EZID account`: http://ezid.cdlib.org/
.. _BCID: https://github.com/biocodellc/bcid

To run an instance of FIMS you will need the following components:

* A unix-based server
  * A java servlet container e.g. Tomcat, Glassfish, Jetty
  * Connection to a BCID service

Installation and Build
----------------------

  * Source code is available on this site via github
  * Building is done via an Gradle build file (provided as part of the distribution)
  * a properties file needs to be configured by copying biocode-fims.template to biocode-fims.props (in the root directory of the distribution) 

Optional Component
------------------
  * An ElasticSearch_ instance for indexing. See :doc:`ElasticSearch Configuration <elastic_search_config>` for configuration details.

.. _ElasticSearch: https://www.elastic.co/products/elasticsearch

Additional Installation Instructions
------------------------------------
   * The source contains a sample property file called biocode-fims.template which should be copied to biocode-fims.props  -- you will need to adjust references in this document. 
      * Note that references to URLs should begin with "www" as in www.biscicol.org instead of biscicol.org since some browsers (e.g. Firefox) automatically add the "www" and this changes the session designation and creates problems during logging in.

Notes
-----
  * It is recommended ALL service calls in the properties file begin with a "www" in the hostname.  
