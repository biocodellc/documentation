.. Amphibian Disease REST Example
.. curl examples

Minting IDs, Creating Expeditions, and Validating Data using REST calls
========================

The examples presented here demonstrate possible methods for interacting with the FIMS REST services for 
creating identifiers, expeditions, and validating datasets.  The full set of REST service calls are at
http://biscicol.org/biocode-fims/rest/fims.wadl .  Unless otherwise noted, the parameters in the following 
examples must be sent with the type 'application/x-www-form-urlencoded'.

Logging in
----------------------

All BCID minting functions require you to first login.  You can login by sending a POST request to::
    
    http://www.biscicol.org/biocode-fims/rest/authenticationService/login 

    POST Parameters:
        username={yourUsername}
        password={yourPassword}

Be sure to save the cookies that are returned.  How you do this depends on your application (see some curl examples of how to do this here:
http://fims.readthedocs.org/en/latest/curl_examples.html)

Mint Bcid
----------------------

Mint a Bcid by sending at minimum a title, webAddress, and resourceType.   Send a POST request to::

     http://www.biscicol.org/biocode-fims/rest/bcids 
 
     POST Parameters:
        webAddress={dataset_webAddress}
        title={dataset_title}
        resourceType={resourceType}  (e.g. "http://purl.org/dc/dcmitype/Dataset")
        *doi={doi} 
        *graph={graph} (A sparql endpoint or other location to be included in sparql queries)
        *suffixPassThrough={true|pase} (whether this supports suffixPassthrough}
        *finalCopy={true|false} (if this is a final copy)

    * Optional parameters
    Send cookies with your request (e.g. curl examples here: http://fims.readthedocs.org/en/latest/curl_examples.html)

Determine your projectID
----------------------
First determine your projectID::

     http://www.biscicol.org/biocode-fims/rest/projects/list

Create new Expedition
--------------------

Mint  an Expedition by sending the following POST request.  Expeditions are used in the FIMS system for organizing content that is related to versions of and resources  related to, a spreadsheet.::

    http://www.biscicol.org/biocode-fims/rest/expeditions 

    POST Parameters:
        expeditionCode={new_expeditionCode}
        expeditionTitle={new_expeditionTitle}
        projectId={your_projectId}
        public={public_expedition}
        webaddress={target URL for expedition, forwarded when the expedition ID resolved}


    Cookies with login data

Associate Bcid with Expedition by sending POST request::
-----------------------

Associate a BCID with an expedition::  
 
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

