---
title: DWN Agents
---
An agent - in the context of Web5 - is software that acts on behalf of a user to manage identity, public or private data, and interactions with other apps in a decentralized network.

You can think of an agent as a box that contains a user's [DIDs](https://developer.tbd.website/docs/web5/learn/decentralized-identifiers/), private keys, and a [DWN](https://developer.tbd.website/docs/web5/learn/decentralized-web-nodes/) (which can also hold [VCs](https://developer.tbd.website/blog/what-is-web5#verifiable-credentials)). Agents are capable of managing multiple DIDs and are permissioned to use the private keys of DIDs to act on a user's behalf.

# Where Does It Live?

A user's agent can live anywhere. It could be a headless process that runs on their computer; it could be their phone; it could be running on a machine at home.

Agents don’t necessarily have root access over the user's device or even their data, but they do have all the authority necessary to provide agency.

Web5 doesn't have remote agents today, so it simply creates an embedded agent if one doesn't already exist. When connecting to a Web5 app, if the user doesn't have an agent at all, the library will:

- create a fallback embedded agent directly in the browser
    
- bootstrap that agent with a DID and a set of necessary keys needed to sign and encrypt things

# Data Store

Today, there are 2 main types of data stores available to a DWN agent, all of which support the generic key value store interface:
1. In memory store (ie. `Map`), or
2. [[notes/databases/LevelDB|LevelDB]]

In the browser context, embedded agents would interact with the LevelDB via IndexedDB. In other contexts, agents would interact with the LevelDB via the filesystem.