---
title: DWN Agents
---
An agent - in the context of Web5 - is software that acts on behalf of a user to manage identity, public or private data, and interactions with other apps in a decentralized network.

You can think of an agent as a box that contains a user's [DIDs](https://developer.tbd.website/docs/web5/learn/decentralized-identifiers/), private keys, and a [DWN](https://developer.tbd.website/docs/web5/learn/decentralized-web-nodes/) (which can also hold [VCs](https://developer.tbd.website/blog/what-is-web5#verifiable-credentials)). Agents are capable of managing multiple DIDs and are permissioned to use the private keys of DIDs to act on a user's behalf.

# Where?

A user's agent can live anywhere. It could be a headless process that runs on their computer; it could be their phone; it could be running on a machine at home.

Agents don’t necessarily have root access over the user's device or even their data, but they do have all the authority necessary to provide agency.

Web5 doesn't have remote agents today, so it simply creates an embedded agent if one doesn't already exist. When connecting to a Web5 app, if the user doesn't have an agent at all, the library will:

- create a fallback embedded agent directly in the browser
    
- bootstrap that agent with a DID and a set of necessary keys needed to sign and encrypt things

