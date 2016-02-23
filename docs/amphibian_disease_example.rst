.. Amphibian Disease REST Example

Creating Expeditions and Validation with REST ONLY
========================

A frequent use case is a user only wants to use the FIMS validation and expedition creation services.  This
is possible by calling FIMS services and using the JSON responses in the context of another website.  Of course, there
are many DIFFERENT permutations that are possible here, such as only creating expedition identifiers, only validating data, 
only  creating spreadsheet templates or any combination of steps.  The example presented below was created for the
Amphibian Disease Portal, which wanted expedition identifiers and data validation for datasets loaded into their portal.

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

Be sure to save cookies the cookies that are returned.  How you do this depends on your application (see some curl examples of how to do this here:
http://fims.readthedocs.org/en/latest/curl_examples.html)

2. Mint Bcid:

  * send POST request to http://www.biscicol.org/biocode-fims/rest/bcids with the following data:
 
    * `webAddress={dataset_webAddress}`
    * `title={dataset_title}`
    * `resourceType="http://purl.org/dc/dcmitype/Dataset"` 

Be sure to send cookies with the request.  How you do this depends on your application (see some curl examples of how to do this here:
http://fims.readthedocs.org/en/latest/curl_examples.html)

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

