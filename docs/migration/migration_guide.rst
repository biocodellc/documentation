REST Service Migration Guide
----------------------------
This lists only the services that were changed. To get more information about the current REST services visit  http://biscicol.org/biocode-fims/rest/fims.wadl

**/id/authenticationService**
  * /loginLDAP

    * moved to nmnh-fims

  * /entrustChallenge

    * moved to nmnh-fims

  * /oauth/access_token

    * moved to "id/authenticationService/oauth/accessToken"
    * additional PostParams:

      * grant_type: optional. If grant_type = “password”, then the user will be authenticated with the provided username and password POST params. Thus skipping the need to call “/oauth/authorize” service 1st
      * username: required if grant_type = “password”
      * password: required if grant_type = “password”

  * /reset

    * moved to “biocode-fims/rest/users/resetPassword”

  * /sendResetToken

    * moved to “biocode-fims/rest/users/{username}/sendResetToken”

**/projectService**
  * /validation/{projectId}

    * removed

  * /list

    * moved to “biocode-fims/rest/projects/list”
    * now returns a JSONArray of "project" JSONObjects

      * each JSONObject contains: "projectId", "projectCode", "projectTitle", "validationXml"

  * /graphs/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/graphs"
    * now returns a JSONArray of "graph" JSONObjects

      * each JSONObject contains: "expeditionCode", "expeditionTitle", "ts", "identifier", "bcidId", "projectId", "webAddress", "graph"

  * /myGraphs

    * moved to “biocode-fims/rest/projects/myGraphs”
    * "ark" => "identifier", "expedition_code" => "expeditionCode", "project_id" => "projectId", "dataset_id" => "bcidId", "expedition_title" => "expeditionTitle"

  * /myDatasets

    * moved to “biocode-fims/rest/projects/myDatasets”
    * "ark" => "identifier", "dataset_id" => "bcidId"

  * /admin/list

    * moved to “biocode-fims/rest/projects/admin/list” 
    * now returns a JSONArray of "project" JSONObjects

      * each JSONObject contains: "projectId", "projectCode", "projectTitle", "validationXml"

  * /configAsTable/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/metadata”

  * /configEditorAsTable/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/metadataEditor”

  * /updateConfig/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/metadata/update"

  * /removeUser/{projectId}/{userId}

    * moved to “biocode-fims/rest/projects/{projectId}/admin/removeUser/{userId}"

  * /addUser

    * moved to “biocode-fims/rest/projects/{projectId}/admin/addUser”

  * /listProjectUsersAsTable/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/users”

  * /listUserProjects

    * moved to “biocode-fims/rest/projects/user/list”
    * now returns a JSONArray of "project" JSONObjects

      * each JSONObject contains: "projectId", "projectCode", "projectTitle", "validationXml"

  * /saveTemplateConfig

    * moved to “biocode-fims/rest/projects/{projectId}/saveTemplateConfig”

  * /getTemplateConfigs/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/getTemplateConfigs”

  * /getTemplateConfig/{projectId}/{configName}

     * moved to “biocode-fims/rest/projects/{projectId}/getTemplateConfig/{configName}”

  * /removeTemplateConfig/{projectId}/{configName}

    * moved to “biocode-fims/rest/projects/{projectId}/removeTemplateConfig/{configName}” 

**/expeditionService**
  * /associate

    * moved to "biocode-fims/rest/expeditions/associate"

  * /validateExpedition/{projectId}/{expeditionCode}

    * moved to "biocode-fims/rest/expeditions/validate/{projectId}/{expeditionCode}"

  * /

    * moved to “biocode-fims/rest/expeditions/”
    * now returns JSONObject of expeditionMetadata

      * "identifier", "public", "expeditionCode", "expeditionTitle", "expeditionId", "projectId"

  * /graphMetadata/{graph}

    * moved to “biocode-fims/rest/expeditions/graphMetadata/{graph}”
    * now returns JSONObject of graphMetadata

      * "graph", "projectId", "expeditionOwner", "uploader", "timestamp", "identifier", "resourceType", "finalCopy", "isPublic", "expeditionCode", "expeditionTitle"

  * /{projectId}/{expeditionCode}/{resourceAlias}

    * moved to “biocode-fims/rest/expeditions/{projectId}/{expeditionCode}/{resourceAlias}"
    * "ark" => "identifier"

  * /deepRoots/{projectId}/{expeditionCode}

    * removed

  * /list/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/expeditions"
    * now returns JSONArray of "expedition" JSONObjects
    * each "expedition" object contains:

      * "expeditionCode", "expeditionTitle", "public", "expeditionId"

  * /resourcesAsTable/{expeditionId}

    * moved to “biocode-fims/rest/expeditions/{expeditionId}/resourcesAsTable"

  * /datasetsAsTable/{expeditionId}

    * moved to “biocode-fims/rest/expeditions/{expeditionId}/datasetsAsTable"

  * /admin/listExpeditionsAsTable/{projectId}

    * moved to "biocode-fims/rest/projects/{projectId}/admin/expeditions"

  * /admin/publicExpeditions

    * moved to “biocode-fims/rest/expeditions/admin/updateStatus”

  * /publicExpedition/{projectId}/{expeditionCode}/{publicStatus}

    * moved to “biocode-fims/rest/expeditions/updateStatus/{projectId}/{expeditionCode}/{publicStatus}"

**/userService**
  * /create

    * moved to “biocode-fims/rest/users/admin/create”

  * /createFormAsTable

    * moved to “biocode-fims/rest/users/admin/createUserForm"

  * /profile/update/{username}

    * moved to “biocode-fims/rest/users/profile/update”
    * now return JSONObject with: "adminAccess", "returnTo"

  * /profile/update

    * moved to “biocode-fims/rest/users/profile/update”
    * now return JSONObject with: "adminAccess", "returnTo"

  * /profile/listEditorAsTable/{username}

    * moved to “biocode-fims/rest/users/admin/profile/listEditorAsTable/{username}"

  * /profile/listEditorAsTable

    * moved to “biocode-fims/rest/users/profile/listEditorAsTable"

  * /profile/listAsTable

    * moved to “biocode-fims/rest/users/profile/listAsTable"

  * /oauth

    * moved to “biocode-fims/rest/users/profile”
    * now return JSONObject with: "firstName", "lastName", "email", "institution", "hasSetPassword", "userId", "username", "projectAdmin"

**/elementService**
  * /select/{select}

    * moved to "biocode-fims/rest/resourceTypes" or "biocode-fims/rest/resourceTypes/minusDataset"
    * returns a JSONArray of resourceTypes. Each resourceType containing the following:
      * resourceType, uri, description, string

  * /resourceTypes

    * moved to “biocode-fims/rest/resourceTypes”
    * returns a JSONArray of resourceTypes. Each resourceType containing the following:

      * resourceType, uri, description, string

  * /creator

    * removed

**/groupService**
  * /

    * moved to “biocode-fims/rest/bcids/”
    * "prefix" => "identifier"

  * /metadata/{datasetId}

    * moved to “biocode-fims/rest/bcids/metadata/{bcidId}”
    * returns JSONObject containing "metadataElement" JSONObjects

  * /list

    * moved to “biocode-fims/rest/bcids/list”
    * returns JSONArray of "bcid" JSONObjects
    * "identifier", "bcidId"

  * /listUserBCIDsAsTable

    * removed

  * /listUserExpeditionsAsTable

    * removed

  * /dataGroupEditorAsTable

    * removed

  * /dataGroup/update

    * moved to “biocode-fims/rest/bcids/update” 

**/biocode-fims/rest/authenticationService**
  * /login

    * no longer uses oAuth to log a user in. Now accepts a username and password to login

  * /access_token

    * removed

**/mapping**
  * /filterOptions/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/filterOptions"
    * return JSONArray of JSONObjects
      * JSONObject contains "column" & "uri" attributes

**/query**
  * /json (GET)

    * moved to “biocode-fims/rest/projects/query/json" (GET)

  * / json (POST)

    * moved to “biocode-fims/rest/projects/query/json" (POST)

  * /kml (GET)

    * moved to “biocode-fims/rest/projects/query/kml" (GET)

  * /kml (POST)

    * moved to “biocode-fims/rest/projects/query/kml" (POST)

  * /cspace

    * moved to “biocode-fims/rest/projects/query/cspace"

  * /excel (GET)

    * moved to “biocode-fims/rest/projects/query/excel" (GET)

  * /excel (POST)

    * moved to “biocode-fims/rest/projects/query/excel" (POST)

  * /tab (GET)

    * moved to “biocode-fims/rest/projects/query/tab" (GET)

  * /tab (POST)

    * moved to “biocode-fims/rest/projects/query/tab" (POST)

**/templates**
  * /attributes

    * moved to “biocode-fims/rest/projects/{projectId}/attributes "

  * /getConfig/{projectId}/{configName}

    * moved to “biocode-fims/rest/projects/{projectId}/getTemplateConfig/{configName}”

  * /getConfigs/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/getTemplateConfigs”

  * /removeConfig/{projectId}/{configName}

    * moved to “biocode-fims/rest/projects/{projectId}/removeTemplateConfig/{configName}”

  * /saveConfig/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/saveTemplateConfig”

  * /abstract

    * moved to “biocode-fims/rest/projects/{projectId}/abstract”
    * returns JSONObject with "abstract"

  * /createExcel

    * moved to “biocode-fims/rest/projects/createExcel"

  * /definition

    * moved to “biocode-fims/rest/projects/{projectId}/getDefinition/{columnName}"

**/utils**
  * /refreshCache/{projectId}

    * removed

  * /expeditionCodes/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/expeditions"
    * now returns JSONArray of "expedition" JSONObjects
    * each "expedition" object contains:

      * "expeditionCode", "expeditionTitle", "public", "expeditionId"

  * /graphs/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/graphs"
    * now returns a JSONArray of "graph" JSONObjects

      * each JSONObject contains: "expeditionCode", "expeditionTitle", "ts", "identifier", "bcidId", "projectId", "webAddress", "graph"

  * /validateExpedition/{projectId}/{expeditionCode}

    * moved to "biocode-fims/rest/expeditions/validate/{projectId}/{expeditionCode}"

  * /getListFields/{listName}

    * moved to “biocode-fims/rest/project/{projectId}/getListFields/{listName}”
    * returns a jsonArray with the acceptable values for the list

  * /isNMNHProject/{projectId}

    * removed

  * /listProjects

    * moved to “biocode-fims/rest/projects/list”

  * /callBCID

    * removed

  * /getDatasetDashboard

    * removed

  * /updatePublicStatus

    * moved to “biocode-fims/rest/expeditions/updateStatus/{projectId}/{expeditionCode}/{publicStatus}"

  * /getLatLongColumns/{projectId}

    * moved to “biocode-fims/rest/projects/{projectId}/getLatLongColumns"

**/validate**

  * /continue_nmnh

    * removed

  * /continue_spreadsheet

    * removed
