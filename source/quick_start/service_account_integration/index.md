---
title: "Service Account Integration"

rightPanel: OFF

languageTabs: OFF

---

<span id="#service-account"></span>
# Service Account Integration

The Service Account Integration follows the next steps. See below the sequence of steps for a detailed description of each.  

1. [Retrieve AuthN Tokens](#service-1-retrieving-the-authn-tokens)—Request the tokens on a server-to-server call providing the account username and password. On successful authentication, the Dow Jones Identity Server generates an AuthN Access token, an AuthN ID token, and optionally a Refresh token. Otherwise, it returns an error.

</br>**Note**: In Service Account Integration, the AuthN Access token is generated, but it is not used in the flow.

2. [Retrieve an AuthZ Access Token](#service-2-retrieving-the-authz-access-token)—Send the AuthN tokens received in Step 1 on a server-to-server call to get an AuthZ Access token, which is the one used to access the resources.

3. [Use the AuthZ Access Token in API Calls](#service-3-using-the-authz-access-token-to-make-api-calls)—In each request, include the AuthZ Access token. If the Access token is valid, the Resource server returns an API response.

4. [Refresh the AuthZ Access Token when it Expires](#service-4-refreshing-the-access-token)—When AuthZ Access tokens expire, the Resource server returns a 401 HTTP error code. The expiration date is also given in the `expires_in` response parameter of Step 2. Use the Refresh token on a server-to-server call to renew the AuthN ID token previously received in Step 1. Re-execute Step 2 using the renewed AuthN ID token to generate a fresh AuthZ Access token.

<span id="service-1-retrieving-the-authn-tokens"></span>
## 1. Retrieving AuthN Tokens

Use the endpoint `POST /token` to request the AuthN tokens and optionally a Refresh token.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`connection`\*|Specifies the custom name of the Auth0 connection  configured for the service account users. Set its value to `service-account`.|string
|`device`\* </br> (when `scope` specifies `offline_access`)| Specifies if a Refresh token is requested. In Service Account Integration, this parameter is mandatory when requesting a Refresh token, `scope=openid service_account_id offline_access`. In such case, set its value to any string, for example, the unique mobile device identifier. This string value acts as a unique identifier under which the Refresh token is listed and could be revoked by an admin either from the Auth0 Dashboard or from the Auth0 Management API, forcing the user to re-login. |string
|`grant_type`\*|Specifies the type of access grant. Set its value to `password`. |string
|`password`\*|Specifies the service account password provided. |string
|`scope`\*|Specifies the scope returned in the AuthN ID token. </br>To get only the two AuthN tokens, set its value to `openid service_account_id`. </br>To get the two AuthN tokens plus the Refresh token, set its value to `openid service_account_id offline_access`. |string
|`username`\*| Specifies the service account username or email provided. |string


**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST
https://accounts.dowjones.com/oauth2/v1/token
client_id: "CLIENT_ID",
connection: "service-account",
device: "orion-tablet",
grant_type: "password",
password: "PASSWORD",
scope: "openid service_account_id offline_access",
username: "user-serviceaccount@dowjones.com"
```

### Response Body

The following table lists the elements sent in the response. The token returns as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`|Represents the issued AuthN Access token used to access the user profile. This token is not used in the flow.|string
|`id_token`|Represents the issued AuthN ID token as a signed JWT. |string
|`refresh_token`|Represents the issued Refresh token, which is used to refresh the AuthN ID token when it expires. An application must securely store the Refresh token, because it enables a user to remain authenticated forever. </br>**Note**: The response returns the Refresh token only if the value of the `scope` parameter in the POST /token request equals `openid service_account_id offline_access`.|string
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer.|string


### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImoR1JUaENOek5CTVRGRU56TkVPQSJ9.eyJzZXJ2aWNlX2FjY291bnRfaWQiOiI5UFJPMDAwMjAwIiwiaXNzIjoiaHR0cHM6Ly9hdXRoLmludC5hY2NvdW50cy5kb3dqb25lcy5jb20vIiwic3iIjoiYXV0aDB8NTlkYRjMjExZDhkNDExNGYwNDcyMWE0IiwiYXVkIjoiSmI4RTRQbGJoZEIyYU5ZRFEwQTg0VXJBVDROZGpGMDgiLCJleHAiOjE1MDgwNTcxMzksImhdCI6MTUwNzc5NzkzOX0.meO4n-2zGPw1Pzco7p2VcDEVnMvugte5QduztTu4jSSwmHYw1mNLkeWpoAjP_ID020DRdDuQ7Am6JbRvDduCzNVDHnmjR365QOh4Audh8AoiMREYfiZJk6UbWmFST909QvJaTe78kTrF7LyTVCU0ZkoecHrVazg454Sq38fyIJ8TKO-ncVUv9Lr1hPlxmmOd8fLzXzeGzrvDigXYmIN9Zq9wY3k8zsrecMR0Q4GRuGMBwxht9b6pcOhoxaSKkLkjKbv6nGEoICD4ImiPxhBKghkD27VIDtppDaVRcyC5QHxg7VYtxg0bLjlYLZF78_sp2vEnMhb-08mKAs8brF6A",
    "access_token": "KMSm3v6ZKGCysDv2",
    "refresh_token": "fOQRVhisivQbQgXWvzKtVkkz4XwKzmTHwmqhMU8Swx2P4",
    "token_type": "bearer"
}
```

<span id="service-2-retrieving-the-authz-access-token"></span>
## 2. Retrieving an AuthZ Access Token

Use the endpoint `POST /token` to exchange the AuthN ID token for the AuthZ access token.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`assertion`\*|Specifies one of the following:</br> - The AuthN ID token obtained in the `id_token` response parameter of Step 1. </br> - The renewed AuthN ID token obtained in the `access_token` response parameter of Step 4.|string
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`grant_type`\*|Identifies the passed AuthN ID token as the grant type to get an access token. Set its value to `urn:ietf:params:oauth:grant-type:jwt-bearer`.|string
|`scope`\*|Specifies the level of access that the client requests. Set its value to `openid pib`.|string

**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST
https://accounts.dowjones.com/oauth2/v1/token
assertion: "AUTHN_ID_TOKEN_RECEIVED",
client_id: "CLIENT_ID",
grant_type: "urn:ietf:params:oauth:grant-type:jwt-bearer",
scope: "openid pib"
```

### Response Body

The following table lists the elements sent in the response. A successful response returns the AuthZ Access token as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`| Represents the final AuthZ Access token issued that serves to access the resources. It is a signed JWT, containing the claims requested in the scope parameter. For the `pib` scope, there is a `pib` object in the JWT, which contains PIB-specific user properties such as `encrypted_token`, `service_account_id`, etc.|string
|`expires_in`|Represents the duration of the AuthZ Access token in seconds.|integer
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer. |string


### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
     "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik0wRkNRakJEUV6TkVPQSJ9.eyJwaWIiOnsibWFzdGVyX2FwcF9pZCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4IiwiZW5jcnlwdGVkX3Rva2VuIjoiSTAwX0pVWVRLTUJYRzQ0VElOQllHVVhXVVNCUEY1WVdZMkxJTzU1RUVXQ0dHWTRHWVUyQkhGUVdHTUxYTVo1RkM0M1lPNVpET01LTtCU0hRM0NFT05CRlVXU1lNUlhFS1JTSE1OSERTUUpMS05UU1dMM1NPRlhWUzVURkdBMlhHUUtZTlZMSFVWUlJPRVpHV09LUEpCQ0RTSzNJT1JXSE81Q0hOUkZYS00yVktWUlhNVUxTSzVZVEVUQlBHRkhVWVdKNUk0Iiwic2VydmljZV9hY2NvdW50X2lkIjoiOVBSTzAwMDIwMCJ9LCJpc3MiOiJodHRwczovL2F1dGguaW50LmFjY291bnzLmRvd2pvbmVzLmNvbS8iLCJzdWIiOiJhdXRoMHw1OWRiNGMyMTFkOGQ0MTE0ZjA0NzIxYTQiLCJhdWQiOiJKYjhNFBsYmhkQjJhTllEUTBBODRVckFUNE5kakYwOCIsImV4cCI6MTUwODA1ODM3MCwiaWF0IjoxNTA3Nzk5MTcwLCJhenAiOiJKYjhFNFBsYmhkQjJhTllEUTBBODRVckFUNE5kakYwOCJ9.PPqOloY1AjKgdabnQBXQ9bx5JZQoti8G5BriQfMqJvhOvJA05fGZUyvUXSyLqEdinb8T5fWUtOiEZW0d8S_cjaNUPn0K99IXBOHmWexUw82idqRk3tDQeOe1Ob9VcFQ3ypoSyCZsZ9QszGagitYGBHZpwh64tdzO79LgK_dc_QO9xnsqN3fCQSvWP5XSTE1jcF2V7dEhLmlgsNs968ndJFLj9mwmP7wwVRj_uismmOZQ_IyqZJUqPG55oPxrLFigQhlZILmSF75AQLNPpAhsl3mr1cAmv6PJAka7hMqudu_Y1JoBtZ0dv9RsirtAnbooa4BZPK2NoASHbd6UA",
     "token_type": "Bearer",
     "expires_in": 259200
}
```

<span id="service-3-using-the-authz-access-token-to-make-api-calls"></span>
## 3. Using the AuthZ Access Token to Make API Calls

Anytime the client application makes an API request to the Resource server, include the AuthZ access token obtained from the Authorization server. If the Resource server determines that the access token is valid, it authorizes access to the resources and returns an API response.

<span id="service-4-refreshing-the-access-token"></span>
## 4. Refreshing the AuthZ Access Token

Use the endpoint `POST /token` to refresh the AuthN ID token previously issued. After refreshing, [retrieve a new AuthZ Access token](#service-2-retrieving-the-authz-access-token) to continue having access to the Resource server.

In Auth0, the number of requests to this endpoint using the same Refresh token from the same IP address has a limit. When this limit is reached, all subsequent requests fail for a certain time. For this reason, obtain new tokens using the Refresh token, only if the AuthZ Access token has expired.

### URL

`https://accounts.dowjones.com/oauth2/v1/token`

### Parameters

The following table lists the parameters that configure the request.

|Parameter|Description|Type
| --- | --- | ---
|`client_id`\*|Specifies the unique Auth0-registered client identifier.|string
|`grant_type`\*|Specifies the OAuth 2.0 specification value for refresh tokens. Set its value to `refresh_token`.|string
|`refresh_token`\*|Specifies the Refresh token returned in the `refresh_token` parameter of Step 1. </br>**Note**: Refresh tokens are returned only if the value of the `scope` parameter of the `POST /token` request of Step 1 equals `openid service_account_id offline_access`|string
|`scope`\*|Specifies the level of access of the regenerated AuthN ID token. Set its value to `openid service_account_id`.|string

**Note**: The asterisk indicates a required parameter.

### Sample HTTP Request

```
POST https://accounts.dowjones.com/oauth2/v1/token
client_id: "CLIENT_ID",
grant_type: "refresh_token",
refresh_token: "REFRESH_TOKEN_RECEIVED",
scope: "openid service_account_id"
```

### Response Body

The following table lists the elements sent in the response. The token returns as a JSON object with status = 200. If any error occurs, status ≠ 200.

|Element|Description|Type
| --- | --- | ---
|`access_token`|Represents the renewed AuthN ID token as a signed JWT. This new token is used to produce a new AuthZ Access token. Assign its value to the `assertion` parameter when re-executing Step 2.|string
|`expires_in`|Represents the duration of the new AuthN ID token in seconds.|integer
|`token_type`|Represents the token type. Generally, access tokens are of type Bearer.|string

### Sample Response

The following is an example of a typical successful response showing all the elements of the token object.

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1N0UWpoR1JUaENOek5CTVRGRU56TkVPQSJ9.eyJwaWIiOnsic2lkIjoiNUVnTmNLYXdfWGp2ZEx0em9GLVRTOFAzT0M4cm9LMlAiLCJrbWxpIjoiMCIsImlsIjoiZW4ifSwiaXNzIjoiaHR0cHM6Ly9hdXRoLmludC5hY2NvdW50cy5kb3db25lcy5jb20vIiwic3ViIjoiYX0aDB8Vk5KUUVSlYzUUJEMk5QWSIsImF1ZCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4IiwiZXhwIjoxNTA5MDE3NDcyLCJpYXQiOjE1MDg3NTgyNzIsImF6cCI6IkpiOEU0UGxiaGRCMmFOWURRMEE4NFVyQVQ0TmRqRjA4In0.QqRSbYxlPXwICoAYLRloUakI1Wgv5Tfqxy903W_gEcMqr3LgAhL-LaBNvBtyiaaWOMNkZ1HHPyFspUO-szBBHuBi5bQ4y1YhXh9zM3S8IikDL55W6RmnLftazv3gponIsUNmZ0KIDr2QK3Fxxv8tc0yGypNko9k3gXboa7JDjsaVHdQdgDPwImFr_W0Xoip6pu9-Rhdo9gfSf811kPyeuOtzQvE-acL4TIAFIszvrtqi0hktukvgPgmfvQ3iHK4j4ZxEurWF36RsA-m0_gP13RXLp7-a2tnoGqWg-zIXR-elXtpMDFGAaIlrLq3Y22XK0PVorUHmw3txanyPgQQ",
    "token_type": "Bearer",
    "expires_in": 259200
}
```
