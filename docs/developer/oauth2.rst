.. oauth2

oauth2
=============
All developers need to register their app. Please contact the system admin to register. You will be issued a client_id and client_secret. The client_secret should be kept private.

Authorization
-------------

Client app will make a GET request to /id/authenticationService/oauth/authorize. This request will contain the following query parameters:
    * client_id (Required) - The client_id your app was issued during when registered.
    * redirect_uri (Required) - The absolute URI you would like the response directed to.
    * state (Optional) - Will be returned, unmodified, in the response. 

The response will contain the following query parameters:
    * code - The random 20 character string used to exchange for an access_token. This code expires in 10 mins and can only be used 1 time.
    * state - Only if this parameter was included in the request.

Access Token
-------------

Client app will make a POST request to /id/authenticationService/oauth/access_token. This request will contain the following parameters in the request body:
    * client_id (Required) - The client_id your app was issued during when registered.
    * client_secret (Required) - The client_secret your app was issued during when registered.
    * code (Required) - The authorization code received in the authorization request.
    * redirect_uri (Required) - The absolute URI you would like the response directed to. Must be identical to the redirect_uri provided in the authorization request.
    * state (Optional) - Will be returned, unmodified, in the response.
    * grant_type (Optional) - If grant_type is "password", and a username and password is provided, the username and password will be used for authentication. If authentication is successful, an access_token and refresh_token will be returned
    * password (Optional) - Required if grant_type is "password".
    * username (Optional) - Required if grant_type is "password".

The JSON response will contain the following parameters:
    * access_token - The random 20 character string used to access a user's profile.
    * refresh_token - The random 20 character string used to obtain a new access_token. This expires after 24 hrs.
    * token_type - currently we only issue bearer tokens.
    * expires_in - the number of seconds the token is good for.
    * state - Only if this parameter was included in the request.

Refresh Token
-------------

Client app will make a POST request to /id/authenticationService/oauth/refresh. This request will contain the following parameters in the request body:
    * client_id (Required) - The client_id your app was issued during when registered.
    * client_secret (Required) - The client_secret your app was issued during when registered.
    * refresh_token (Required) - The refresh_token you were issued with you access token.

The server will validate the refresh token and if the refresh token is less then 24 hrs old, a new access token will be issued. The current refresh token will be expired and a new one will be issued.

The JSON response will contain the following parameters:
    * access_token - The random 20 character string used to access a user's profile.
    * refresh_token - The random 20 character string used to obtain a new access_token. This expires after 24 hrs.
    * token_type - currently we only issue bearer tokens.
    * expires_in - the number of seconds the token is good for.

API Access
-------------

In order to obtain a user's profile information, make a GET request to /id/userService/profile with the access_token as a query parameter.

If the token is still valid, you will receive a JSON response with the following user information:
    * firstName
    * lastName
    * email
    * institution
    * userId
    * username
    * projectAdmin
    * hasSetPassword

We also support access to any rest services on behalf of the user. Just append "?access_token=your_access_token" to the url in order to access the service.
