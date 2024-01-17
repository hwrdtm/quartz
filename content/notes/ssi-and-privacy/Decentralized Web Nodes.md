---
title: "Decentralized Web Nodes"
---
A Decentralized Web Node (DWN) is a data storage and message relay mechanism that entities can use to locate public or private permissioned data related to a given [Decentralized Identifier(DID)](https://developer.tbd.website/docs/web5/learn/decentralized-identifiers).

A DWN is a personal data store. This means you can:

- **Own your data:** You decide where to host your node. You control who has access.
- **Back up your data:** Host multiple nodes in different places, and keep them all [synced](https://developer.tbd.website/docs/web5/learn/sync) effortlessly. If one goes down, you have your backup.
- **Send and receive data:** Alice controls her DWN using her DID. Bob controls his DWN with his DID. Alice can send data to Bob just by resolving his DID.

![image](dwn.png)

# Authorization

DWNs have two mechanisms to allow others access to read, write, or delete data on your node.

- **Permissions:** Allow someone access to read, write, or delete specific data records on your node.
- **Protocols:** Install a [protocol](https://developer.tbd.website/docs/web5/learn/protocols) that lets you define data types and authorization for a decentralized web app.

The easiest way to understand this distinction is to think of permissions as active, explicit, and manual, whereas protocols are passive, syntactic, and contractual.

# Messaging

All communication is done through simple JSON objects called messages. Web5 constructs messages and helps you send them to their destination by resolving a recipient's DID and getting the address of their Decentralized Web Node. A message can install protocols, grant permissions, and read, write, update, query, or delete a record.

# Sync

Users are able to possess multiple [Decentralized Web Nodes (DWNs)](https://developer.tbd.website/docs/web5/learn/decentralized-web-nodes) and have the data across each of them synchronized. This provides end users with the ability to own their data in resilient and convenient ways.

When an application calls [Web5.connect()](https://developer.tbd.website/api/web5-js#connectoptions), by default, a DWN is created that runs in browser memory and is considered a local DWN.

To understand the magnitude of this, let’s consider how we think of sync in our apps today. Dropbox, for example, allows us to synchronize our files across devices, but is dependent on either a web browser or platform-specific app to make that happen. Additionally, end users take a hard dependency on Dropbox to actually maintain the physical infrastructure for storing the data.

A service like iCloud may allow for users’ app data to sync across devices, but that functionality is locked to Apple’s platforms and requires developer input to enable the feature.

In Web5.js, the same features that built billion dollar businesses are included, for free, and with even more functionality. Rather than every app being an island that has to figure out how to sync on its own, Web5 abstracts away sync for all of a user’s apps and data.

Sync is orchestrated by an _agent_, which is responsible for acting on a user’s behalf to invoke the sync interface between nodes since the nodes themselves don’t actually implement this interface. In the same way that your browser has a user agent, so does your Web5 environment, which enables its agent to orchestrate privileged activities of user management on your behalf.

So why do we have agents to facilitate sync? The primary reason is because Web5 is built from a number of core components and libraries that all need to be knitted together. Libraries for DWN, DID, VC, networking, and more are all required to perform fundamental operations like sync, which is why we delegate that responsibility to an agent rather than asking app developers to perform these tasks.

Imagine having to write code to open connections, sign data, and more every time you wanted to send a message to another DWN. Web5 abstracts away this complexity via agents.

# Resources

https://developer.tbd.website/docs/web5/learn/decentralized-web-nodes

https://identity.foundation/decentralized-web-node/spec/

