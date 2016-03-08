.. Amphibian Disease REST Example

Minting IDs, Creating Expeditions, and Validating Data using REST calls
========================

The examples presented here demonstrate possible methods for interacting with the FIMS REST services for 
creating identifiers, expeditions, and validating datasets.  The full set of REST service calls are at
http://biscicol.org/biocode-fims/rest/biocode-fims.wadl

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

    Send request as type 'multipart/form-data' (in Curl, use -F for form data vs -d)

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
