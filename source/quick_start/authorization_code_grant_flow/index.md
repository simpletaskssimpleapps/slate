---
title: "Authorization Code Grant Flow"

rightPanel: OFF

languageTabs: OFF

---

# Authorization Code Grant Flow

The Authorization Code Grant flow follows the next steps. See below the sequence of steps for a detailed description of each.  

1. [Retrieve an Authorization Code](#grant-1-authenticating-the-user)—Request the code on a user agent (browser). On successful authentication, the Dow Jones Identity Server redirects the user to the specified URL (parameter `redirect_uri`) and sends the authorization code. Otherwise, the server returns an error. To receive a Refresh token in the next step, request it in this step through the `scope` query parameter. See the [Query Parameters table](#query-param) of Step 1 in the detailed description.
2. [Exchange the Authorization Code for AuthN Tokens](#grant-2-exchanging-the-authorization-code-for-the-authn-token)—Send both the authorization code received and the client secret on a server-to-server call. The Authorization server sends back an AuthN Access token, an AuthN ID token, and a Refresh token if requested in the previous step. Make sure to keep the returned Refresh token safe because it can be reused multiple times for gaining access without having to re-enter your credentials.
3. [Retrieve an AuthZ Access Token](#grant-3-retrieving-the-authz-access-token)—Send the AuthN tokens received in Step 2 on a server-to-server call to get an AuthZ Access token, which is the one used to access the API resources.
4. [Use the AuthZ Access Token in API Calls](#grant-4-using-the-authz-access-token-to-make-api-calls)—In each request, include the AuthZ Access token. If the Access token is valid, the Resource server returns an API response.
5. [Refresh the AuthZ Access Token when it Expires](#grant-5-refreshing-the-access-token)—When AuthZ Access tokens expire, the Resource server returns a 401 HTTP error code. The expiration date is also given in the `expires_in` response parameter of Step 3. Use the Refresh token on a server-to-server call to renew the AuthN ID token previously received in Step 2. Re-execute Step 3 using the renewed AuthN ID token to generate a fresh AuthZ Access token.
6. [Log Out](#grant—6-logging-out)—Perform this step on a user agent (browser) to invalidate the PIB session ID contained in the AuthZ Access token and to delete the browser auto-login session established in Step 1.

<span id="grant-1-authenticating-the-user"></span>
## 1. Retrieving an Authorization Code

Use the endpoint `GET /authorize` to retrieve the authorization code.
</br>**Note**: You must perform this step on a user agent (browser).

### URL

`https://accounts.dowjones.com/oauth2/v1/authorize`

<span id="query-param"></span>
### Query Parameters

The following table lists the query parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`client_id`*|Specifies the unique Auth0-registered client identifier.|string
|`connection`|Specifies the custom name of the Auth0 connection used to identify the user. Default value: `DJPIB` (for PIB product authentication). |string
|`device`| Specifies if a Refresh token is requested. </br>When requesting a Refresh token, set its value to any string, for example, the unique mobile device identifier. This string value acts as a unique identifier under which the Refresh token is listed and could be revoked by an admin either from the Auth0 Dashboard or from the Auth0 Management API, forcing the user to re-log in. </br>When a value is not specified, the Refresh token is preserved under an `ignore` device string.| string
|`redirect_uri`\*|Specifies the URL to which, after successful authorization, the server sends the authorization code that is later exchanged. </br>**Note**: The provided value must be whitelisted in Auth0 for the `client_id` specified. |string
|`response_type`\*|Specifies the type of flow to execute: Authorization Code or Implicit. To request an Authorization Code grant, set its value to `code`. |string
|`scope`\*|Specifies the scope returned in the AuthN ID token. </br>To get only the two AuthN tokens, set its value to `openid pib`. </br>To get the two AuthN tokens plus the Refresh token, set its value to `openid pib offline_access`. |string
|`state`| Specifies the caller state that is propagated back to the `redirect_uri` on successful authentication.|string
**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
GET
https://accounts.dowjones.com/oauth2/v1/authorize?
client_id=CLIENT_ID&
redirect_uri=REDIRECT_URI&
response_type=code&
scope=openid%20pib%20offline_access&
state=abc
```

### Response

Successful response: An authorization code sent to the URL specified in the parameter `redirect_uri`.

<span id="grant-2-exchanging-the-authorization-code-for-the-authn-token"></span>
## 2. Exchanging the Authorization Code for AuthN Tokens

Use the endpoint `POST /token` to exchange the authorization code for the AuthN tokens and optionally a Refresh token.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`client_secret`\*|Specifies the unique Auth0-registered client secret for the given `client_id`.|string
|`code`*|Specifies the code returned by the `GET /authorize` request of Step 1. </br>**Note**: You can use a code only once in a call to this endpoint. Further calls using the same code fail.|string
|`grant_type`\*|Specifies the type of access grant. Set its value to `authorization_code`. |string
|`redirect_uri`\*|Specifies a URL that matches the one specified in the `redirect_uri` parameter of Step 1. |string


**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST
https://accounts.dowjones.com/oauth2/v1/token
client_id: "CLIENT_ID",
client_secret: "CLIENT_SECRET",
code: "AUTH_CODE_RECEIVED",
grant_type: "authorization_code",
redirect_uri: "REDIRECT_URI"
```

### Response Body

The following table lists the elements sent in the response. The tokens return as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`|Represents the issued AuthN Access token used to access the user profile.|string
|`expires_in`|Represents the duration of the AuthN ID token in seconds.|integer
|`id_token`|Represents the issued AuthN ID token as a signed JWT. |string
|`refresh_token`|Represents the issued Refresh token that is used to refresh the AuthN ID token when it expires. An application must securely store the Refresh token, because it enables a user to remain authenticated forever. </br>**Note**: The response returns the Refresh token only if the value of the `scope` parameter of the `GET /authorize` request of Step 1 equals `openid pib offline_access`.|string
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer.|string

### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik0wRkNRakJEUVRNeVFUTTNSREUwTWpGRE5VWkNNekE0UWpoR1JUaENOek5CTVRGRU56TkVPQSJ9.eyJwaWIiOnsic2lkIjoiNXNrZFVnUFVNeThjQUFCOTg3WHR3OU5BWVZsejN1SGCIsImlsIjoiZW4ifSwiaXNzIjoiaHR0cHM6Ly9hdRoLmludC5hY2NvdW50cy5kb3dqb25lcy5jb20vIiwic3ViIjoiYXV0aDB8Vk5KUUVQSlYzUUJEMk5QWSIsImF1ZCI6IkpiOEU0UxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4IiwiZXhwIjoxNTA5MDExMjQwLCJpYXQiOjE1MDg3NTIwNDAsIm5vbmNlIjoic29tdW5pcXVldmFsdWUxMjMifQ.IeNKj7ftoQPaMqDoX4LbpzFaL7akt3e4Y-7GMcFEaF3lFCs-O5dZdJS-OfYDGqTrnqkU9YseDD4bchgGh6PCobS8-CzT2N8dU7pwfWrggBenDg7Ko0ixEUocee4uJMpXufIrYrBKdE4oo7pTBj0ISd52R9YfaxlgDtj8bUq1xSlgOT86y8bDXC-6JA-5m8qmYcZaFcBU1CXtpiCwSeG7IPcpGV5zPjNHhHwA434ZZRcN2Qvra4K50PaIIgBxTR0M8JiDf1VcI92eI3GejP9PPQYRBF6bEPWw0g7oX_bf916IcxOmDIGK_FVjm01v6lgUI-XAr-oruvJ638K6g",
    "access_token": "mZR7bZoJbnjndxCF",
    "refresh_token": "G3W6uVBbtidMCnTaHjP7cQQOyRDLL13WQbJBnCOkqGpkt",
    "token_type": "Bearer",
    "expires_in": 86400
}
```

<span id="grant-3-retrieving-the-authz-access-token"></span>
## 3. Retrieving an AuthZ Access Token

Use the endpoint `POST /token` to exchange the AuthN tokens for the AuthZ Access token.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description |Type
| --- | ---- | ----
|`access token`\*|Specifies the AuthN Access token obtained in the `access_token` response parameter of Step 2.|string
|`assertion`\*|Specifies one of the following:</br> - The AuthN ID token obtained in the `id_token` response parameter of Step 2. </br> - The renewed AuthN ID token obtained in the `access_token` response parameter of Step 5.|string
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`grant_type`\*|Identifies the passed AuthN ID token as the grant type to get an access token. Set its value to `urn:ietf:params:oauth:grant-type:jwt-bearer`.|string
|`scope`\*|Specifies the level of access that the client requests. Set its value to `openid pib`.|string

**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST
https://accounts.dowjones.com/oauth2/v1/token
access_token: "AUTHN_ACCESS_TOKEN_RECEIVED",
assertion: "AUTHN_ID_TOKEN_RECEIVED",
client_id: "CLIENT_ID",
grant_type: "urn:ietf:params:oauth:grant-type:jwt-bearer",
scope: "openid pib"
```

### Response Body

The following table lists the elements sent in the response. A successful response returns the AuthZ Access token as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`|Represents the final AuthZ Access token issued that serves to access the resources. It is a signed JWTA, containing the claims requested in the scope parameter. For the `pib` scope, there is a `pib` object in the JWT, which contains PIB-specific user properties such as `session_id`, `ctc` (client type code), `apc` (access point code), etc.|string
|`expires_in`|Represents the duration of the AuthZ Access token in seconds.|integer
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer. |string


### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik0wRkNRakJUaENOek5CTVRGRU56TkVPQSJ9.eyJwaWIiOnsibWFzdGVyX2FwcF9pZCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4Iiwic2Vzc2lvbl9pZCI6IjI3MTQ0WHhYX2NkYzVkNzE0LWQ1MGEtNDAzMy1lOGM2LWNjMGZiNDU5Njc3NCIsImFsbG93X2F1dG9fb9naW4iOiJ0cnVlIiwiYXBjIjoiOSIsImN0YyI6IkQifSwiaXNzIjoiaHR0cHM6Ly9hdXRoLmludC5hY2vdW50cy5kb3dqb25lcy5jb20vIiwic3ViIjoiYXV0aDB8Vk5KUUVQSlYzUUJEMk5QWSIsImF1ZCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4IiiZXhwIjoxNTAzODQ2NTU3LCJpYXQiOjE1MDM1ODczNTcsImF6cCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4In0.AdGy4iNtRnB1sEUOdx8iqWaCiJS0MkGOrRCt6SsDl3HyxLa5SoNczb2rCu9x7fYbyDnjKUn0ZkLHDS_DDyio6JrJ5qXF9p07IGhKhouDW1ouX6GEZ_LyTsJ7gFK0830N_VjBMFJcDiTOQ89Pz8QwaNlrkKgjq11bEVOxSsiWFzjDAhB23fUiIN6Fn8ABezySZhDzWOM87H7fG2t8gOlC0aPRwAHGZvyrUopApyK2G7v6ODyvD6S5ghqAmqB_BsgAyr4urvGg2euH5MNCCepclK09BMgb9KqoNoFQe0Q34H9wzjFlu1FPWP-GZm3cgJZYqhx7G4ih12FVOMA",
    "token_type": "Bearer",
    "expires_in": 259200
}
```
<span id="grant-4-using-the-authz-access-token-to-make-api-calls"></span>
## 4. Using the AuthZ Access Token in API Calls

Any time the client application makes an API request to the Resource server, include the AuthZ Access token obtained from the Authorization server. If the Resource server determines that the Access token is valid, it authorizes access to the resources and returns an API response.

<span id="grant-5-refreshing-the-access-token"></span>
## 5. Refreshing the AuthZ Access Token

Use the endpoint `POST /token` to refresh the AuthN ID token previously issued. After refreshing, [retrieve a new AuthZ Access token](#grant-3-retrieving-the-authz-access-token) to continue having access to the Resource server.

In Auth0, the number of requests to this endpoint using the same Refresh token from the same IP address has a limit. When this limit is reached, all subsequent requests fail for a certain time. For this reason, obtain new tokens using the Refresh token, only if the AuthZ Access token has expired.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`grant_type`\*|Specifies the OAuth 2.0 specification value for refresh tokens. Set its value to `refresh_token`.|string
|`refresh_token`\*|Specifies the Refresh token previously returned in the `refresh_token` parameter of Step 2. </br>**Note**: Refresh tokens are returned only if the value of the `scope` parameter of the `GET /authorize` request of Step 1 equals `openid pib offline_access`|string
|`scope`\*|Specifies the level of access of the regenerated AuthN ID token. Set its value to `openid pib`.|string

**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST https://accounts.dowjones.com/oauth2/v1/token
client_id: "CLIENT_ID",
grant_type: "refresh_token",
refresh_token: "REFRESH_TOKEN_RECEIVED",
scope: "openid pib"
```

### Response Body

The following table lists the elements sent in the response. The token returns as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`|Represents the renewed AuthN ID token as a signed JWT. This new token is used to produce a new AuthZ Access token. Assign its value to the `assertion` parameter when re-executing Step 3.|string
|`expires_in`|Represents the duration of the new AuthN ID token in seconds.|integer
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer.|string

### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik0w5ViOnsic2lkIjoiNUVnTmNLYXdfWGp2ZEx0em9GLVRTOFAzT0M4cm9LMlAiLCJrbWxpIjoiMCIsImlsIjoiZW4ifSwiaXNzIjoiaHR0cHM6Ly9hdXRoLmludC5hY2NvdW50cy5kb3db25lcy5jb20vIiwic3ViIjoiYX0aDB8Vk5KUUVSlYzUUJEMk5QWSIsImF1ZCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4IiwiZXhwIjoxNTA5MDE3NDcyLCJpYXQiOjE1MDg3NTgyNzIsImF6cCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4In0.QqRSbYxlPXwICoAYLRloUakI1Wgv5Tfqxy903W_gEcMqr3LgAhL-LaBNvBtyiaaWOMNkZ1HHPyFspUO-szBBHuBi5bQ4y1YhXh9zM3S8IikDL55W6RmnLftazv3gponIsUNmZ0KIDr2QK3Fxxv8tc0yGypNko9k3gXboa7JDjsaVHdQdgDPwImFr_W0Xoip6pu9-Rhdo9gfSf811kPyeuOtzQvE-acL4TIAFIszvrtqi0hktukvgPgmfvQ3iHK4j4ZxEurWF36RsA-m0_gP13RXLp7-a2tnoGqWg-zIXR-elXtpMDFGAaIlrLq3Y22XK0PVorUHmw3txanyPgQQ",
    "token_type": "Bearer",
    "expires_in": 259200
}
```

<span id="grant—6-logging-out"></span>
## 6. Logging Out

Use the endpoint `GET /logout` or `POST /logout` to invalidate the PIB session ID contained in the AuthZ Access token and to delete the browser auto-login session established.
</br>**Note**: You must perform this step on a user agent (browser).

### URL

`https://accounts.dowjones.com/oauth2/v1/logout`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`access_token`\*|Specifies the AuthZ Access token returned in Step 3.|string
|`productname`|Specifies the PIB product. Default value: `dna`.|string
|`return_uri`|Specifies the URL where to return after logging out. If it's not provided, the user is redirected to www.dowjones.com.|string

**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
GET https://accounts.dowjones.com/oauth2/v1/logout?
access_token=AUTHZ_ACCESS_TOKEN_RECEIVED&
return_uri=RETURN_URI
```

### Response

A successful response sends an authorization code to the URL specified in the parameter `redirect_uri`.