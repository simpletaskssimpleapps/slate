---
title: "Sessions and Authentication"

rightPanel: OFF

languageTabs: OFF

---

# Relationship to Other Standards

OAuth 2.0 does not exist in isolation from existing identity and security standards. On its own, OAuth 2.0 does not provide an identifier for the user. The access token is not an identifier, but rather a means to obtain such information subsequently. An identity layer such as [OpenID Connect](http://openid.net) can be added on top of the OAUth 2.0 protocol. This identity layer specifies how to add to the existing OAuth 2.0 messages the necessary identifiers to make Single Sign On (SSO) possible. Rather than having a distinct SSO protocol for sharing identifiers and a separate protocol for sharing access tokens, OAuth 2.0 and OpenID Connect can be combined.

OpenID is an open standard and decentralized protocol provided by the OpenID Foundation that allows users to be authenticated by cooperating sites, known as Relying Parties (RP), using a third-party service. 	 	
