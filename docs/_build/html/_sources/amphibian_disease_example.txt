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
First determine your projectID::

     http://www.biscicol.org/biocode-fims/rest/projects/list

Mint Bcid
----------------------

**Login by sending POST request to**::
    
    http://www.biscicol.org/biocode-fims/rest/authenticationService/login 

    POST Parameters:
        username=AmphibianDisease
        password={yourPassword}

Be sure to save the cookies that are returned.  How you do this depends on your application (see some curl examples of how to do this here:
http://fims.readthedocs.org/en/latest/curl_examples.html)

**Mint Bcid by send POST request to**::

     http://www.biscicol.org/biocode-fims/rest/bcids with the following data:
 
     POST Parameters:
        webAddress={dataset_webAddress}
        title={dataset_title}
        resourceType="http://purl.org/dc/dcmitype/Dataset

    Cookies with login data (For all requests requiring authentication, be sure to send cookies with the request.  How you do this depends on your application (see some curl examples of how to do this here: http://fims.readthedocs.org/en/latest/curl_examples.html)

Note the identifier returned  that was returned and use it in the following request.

Associate Bcid with Expedition by sending POST request::
 
    http://www.biscicol.org/biocode-fims/rest/expeditions/associate 

    POST Parameters:
        expeditionCode={dataset_expeditionCode}
        bcid={identifier returned in step 2}
        projectId={your_projectId}

    Cookies with login data

Validate Dataset
------------------

To validate your dataset, send a POST request to:: 

    http://www.biscicol.org/biocode-fims/rest/validate 

    Send request as type 'multipart/form-data'

    POST Parameters:
        projectId={your_projectId}
        expeditionCode={your_expeditionCode}
        dataset={your_dataset}

    Cookies with login data

The response is returned as JSON, which will look something like::

    {"done": [{
        "Samples": {
            "errors": [],
            "warnings": [{
                "Missing column(s)": [
                    "yearCollected has a missing cell value", 
                    "permitInformation has a missing cell value", 
                    "locality has a missing cell value"
                ]
            }]
        }
    }]}

Create new Expedition
--------------------

Mint Expedition by sending the following POST request::

    http://www.biscicol.org/biocode-fims/rest/expeditions 

    POST Parameters:
        expeditionCode={new_expeditionCode}
        expeditionTitle={new_expeditionTitle}
        projectId={your_projectId}
        public={public_expedition}
        webaddress={target URL for expedition, forwarded when the expedition ID resolved}


    Cookies with login data
