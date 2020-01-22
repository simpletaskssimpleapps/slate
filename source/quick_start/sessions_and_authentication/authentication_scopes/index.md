---
title: "Sessions and Authentication"

rightPanel: OFF

languageTabs: OFF

---

# Authentication Scopes

The Dow Jones Identity Service supports the following scopes.

|Identifier | Descriptor | Description
|--- | --- | ---
|`openid` | Access your identity in Factiva | Provides the ID token (JWT).
|`email` | View your email address | Provides the user's email included in the ID token (JWT).
|`family_name` | View your family name | Provides the user's family name included in the ID token (JWT).
|`given_name` | View your given name | Provides the user's given name included in the ID token (JWT).
|`offline_access`| | Indicates that a refresh token is returned.
