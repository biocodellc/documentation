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

Installation and Build -- Migrating an existing installation
----------------------

  * Source code is available on this site via github
  * Building is done via an Gradle build file (provided as part of the distribution)
  * a properties file needs to be configured by copying biocode-fims.template to biocode-fims.props (in the root directory of the distribution) 

Install the following software
  * postgres
  * jetty9
  * java8
  * bcid and geome-db repositories (from github)
  
Properties file
   * update properties files in `src/main/environment/production`

gradle war
deploy build/libs/geome-db.war
(do the above for both bcid and geome-db)

generate openapi document using `gradle resolve`





