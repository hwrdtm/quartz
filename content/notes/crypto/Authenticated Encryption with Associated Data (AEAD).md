---
title: "Authenticated Encryption with Associated Data"
---

AEAD is a variant of AE that allows a recipient to check the integrity of both the encrypted and unencrypted information in a message. AEAD binds associated data (AD) to the ciphertext and to the context where it is supposed to appear so that attempts to "cut-and-paste" a valid ciphertext into a different context are detected and rejected.

It is required, for example, by network packets or frames where the header needs visibility, the payload needs [confidentiality](https://en.wikipedia.org/wiki/Confidentiality "Confidentiality"), and both need [integrity](https://en.wikipedia.org/wiki/Data_integrity "Data integrity") and [authenticity](https://en.wikipedia.org/wiki/Message_authentication "Message authentication").