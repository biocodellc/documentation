.. Amphibian Disease REST Example

Amphibian Disease REST Example
========================

* With all of the following data parameters, you must replace the {....} with values of your choosing. 
* Unless otherwise noted, the params must be sent with the type 'application/x-www-form-urlencoded'.


Determine your projectID:
----------------------
First determine your projectID http://www.biscicol.org/biocode-fims/rest/projects/list

Mint Bcid
----------------------

1. Login:

  * send POST request to http://www.biscicol.org/biocode-fims/rest/authenticationService/login with the following data:

    * `username=AmphibianDisease`
    * `password={yourPassword}`

2. Mint Bcid:

  * send POST request to http://www.biscicol.org/biocode-fims/rest/bcids with the following data:
 
    * `webAddress={dataset_webAddress}`
    * `title={dataset_title}`
    * `graph={dataset_graph}`
    * `resourceType="http://purl.org/dc/dcmitype/Dataset"` 


3. Note the identifier returned in the previous step

4. Associate Bcid with Expedition:
 
  * send POST request to http://www.biscicol.org/biocode-fims/rest/expeditions/associate with the following data:

    * `expeditionCode={dataset_expeditionCode}`
    * `bcid={identifier returned in step 2}`
    * `projectId={your_projectId}`

Validate Dataset
------------------

**POST params must be sent with type 'multipart/form-data'**

1. Send POST request to http://www.biscicol.org/biocode-fims/rest/validate with the following data:

  * `projectId={your_projectId}`
  * `expeditionCode={your_expeditionCode}`
  * `dataset={your_dataset}`


Create new Expedition
--------------------

1. Login:

  * send POST request to www.biscicol.org/biocode-fims/rest/authenticationService/login with the following data:
    * `username=AmphibianDisease`
    * `password={yourPassword}`

2. Mint Expedition:

  * send POST request to http://www.biscicol.org/biocode-fims/rest/expeditions with the following data:
    * `expeditionCode={new_expeditionCode}`
    * `expeditionTitle={new_expeditionTitle}`
    * `projectId={your_projectId}`
    * `public={public_expedition}`

