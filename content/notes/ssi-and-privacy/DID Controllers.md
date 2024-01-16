---
title: "DID Controllers"
---
An entity that has the capability to make changes to a [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). A [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) might have more than one DID controller. The DID controller(s) can be denoted by the optional `controller` property at the top level of the [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). Note that a DID controller might be the [DID subject](https://www.w3.org/TR/did-core/#dfn-did-subjects).

The easiest way to describe the controller-subject relationship is by coming back to Alice and Bob for an analogy.

Alice and Bob (controller group) have a baby. They decide to get their baby a DID. The baby is the _subject_ of the DID, but may not be ready for the responsibility of managing the DID yet. Alice and Bob can use their own DID's verification methods to control their baby's DID on behalf of their baby.

# Resources

https://developer.tbd.website/docs/web5/learn/decentralized-identifiers