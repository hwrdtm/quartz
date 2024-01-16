---
title: "Decentralized Identifiers"
tags:
- learning/did
---

A [DID](https://www.w3.org/TR/did-core/) is an address representing who you are on the decentralized web. It can point to a person, organization, thing, data model, or abstract entity. It's through your DID that others can send messages and data, and be granted access to information you wish to share.

A DID is a "type of identifier that enables verifiable, decentralized digital identity" ([DID Core Spec](https://www.w3.org/TR/did-core/)). It is created and managed independently of any centralized authority or organization. The basic idea behind a DID is to give individuals and organizations control over their own identity information and to allow them to share that information selectively and securely with others as needed. This means that they can choose when and how to share their identity information, and with whom.

DIDs are typically represented as a unique resource identifier (URI) and are designed to be used for identity verification, authentication, and authorization.

The key difference between a traditional centralized identifier, such as a username or email address, and a decentralized identifier is that **the latter is not tied to a specific service provider or organization**. An example of a centralized identifier you might have would be your Twitter handle or Google email address, where Twitter or Google are the centralized authority.
# Key Management

Your DIDs are secured with public-private key pairs. You should not let anyone have your private key, because the key material used to secure your DID is how you prove ownership of your DID. You should find a secure way to store your private key, such as through a secured keystore.

# Resources

https://developer.tbd.website/docs/web5/learn/decentralized-identifiers