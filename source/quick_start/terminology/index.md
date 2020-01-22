---
title: "Terminology"

rightPanel: OFF

languageTabs: OFF

---

# Terminology

| Term | Definition
--- | ---
|AuthZ Access token| A self-contained <a href="https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32" target="_blank">JSON Web Token</a> (JWT) by which a client accesses the API resources. This token is a Bearer credential and is sent in an HTTP Authorization header to the API. This token has an expiration date.
|AuthN Access token| An opaque short string that together with the AuthN ID token serves to obtain the AuthZ Access token. This access token does not expire.
|AuthN ID token| A JWT that contains only the user's identifying information. Together with the AuthN Access token, it serves to obtain the AuthZ Access token. This token has an expiration date.
|Authentication|Process that validates the user credentials and establishes the identity of the user.
|Authorization|Process that establishes the access restrictions (for example, the user is allowed to access X resource).
|Authorization server|Server that verifies the identity and provides authorization services to the user. It issues access tokens and refresh tokens to clients on behalf of resource servers. The access is limited to the scope of the authorization granted.
|Client|Application that requests access to the resources protected by a Resource server. It interacts with an Authorization server to obtain tokens to access the resources. For example, any web or mobile application relying on Dow Jones identity.
|Refresh token|A long-life token that enables clients to generate a fresh AuthN ID token that can then be exchanged by a new AuthZ Access token.  </br>**Note**:  Refresh tokens must be stored securely by an application, because they allow a user to remain authenticated essentially forever.
|Resource server|Server that hosts and protects the resources. It makes the resources available to properly authenticated and authorized clients.
