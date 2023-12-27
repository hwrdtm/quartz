---
title: "Storage Peers"
---

Source: https://www.inkandswitch.com/pushpin/#storage-peers

A limitation of any peer-to-peer system is that two peers can only communicate while they are both online. However, mobile devices are often offline, potentially making it difficult to find an opportunity to exchange updates. For example, if your colleague has shared the URL of a PushPin board with you, it would be annoying if you could not access that board because the only copy of the board resides on your colleague’s closed laptop.

We can overcome this limitation by introducing _storage peers_, which replicate all the data belonging to a particular user or set of users. A storage peer runs the same replication code as PushPin, recursively following any Hypermerge URLs, but it runs as a simple Unix daemon without any visual user interface. The storage peer can be deployed on a server or other computer that is always online, allowing other devices to sync with the storage peer at any time. Storage peers also provide a form of backup.

Unlike a traditional server, a storage peer can be reached through NAT traversal, so it does not need a public IP address: for example, it could be a device on the user’s home internet connection. Since it only stores the data for a small number of users, it does not need to be a powerful machine. We have experimented with using a Raspberry Pi as storage peer, writing data to an SD card, and also running storage peers on virtual server instances in public cloud providers.

