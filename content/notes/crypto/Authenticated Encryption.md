---
title: "Authenticated Encryption"
---

https://en.wikipedia.org/wiki/Authenticated_encryption

Authenticated Encryption (AE) are forms of encryption which simultaneously assure the confidentiality and authenticity of data.

## Programming Interface

A typical [programming interface](https://en.wikipedia.org/wiki/Application_programming_interface "Application programming interface") for an AE implementation provides the following functions:

- Encryption
    -   Input: _plaintext_, _key_, and optionally a _header_ in plaintext that will not be encrypted, but will be covered by authenticity protection.
    -   Output: _ciphertext_ and _authentication tag_ ([message authentication code](https://en.wikipedia.org/wiki/Message_authentication_code "Message authentication code") or MAC).
-   Decryption
    -   Input: _ciphertext_, _key_, _authentication tag_, and optionally a _header_ (if used during the encryption).
    -   Output: _plaintext_, or an error if the _authentication tag_ does not match the supplied _ciphertext_ or _header_.

The _header_ part is intended to provide authenticity and integrity protection for networking or storage metadata for which confidentiality is unnecessary, but authenticity is desired.

## Motivation

The need for authenticated encryption emerged from the observation that securely combining separate _confidentiality_ and _authentication_ block cipher operation modes could be error prone and difficult.

## Approaches

### Encrypt-then-MAC (EtM)

The plaintext is first encrypted, then a MAC is produced based on the resulting ciphertext. The ciphertext and its MAC are sent together.

Used in IPsec.

This is the only method which can reach the highest definition of security in AE, but this can only be achieved when the MAC used is "strongly unforgeable".

Note that key separation is mandatory (distinct keys must be used for encryption and for the keyed hash), otherwise it is potentially insecure depending on the specific encryption method and hash function used.

![image](ae_etm.png)

### Encrypt-and-MAC (E&M)

A MAC is produced based on the plaintext, and the plaintext is encrypted without the MAC. The plaintext's MAC and the ciphertext are sent together.

Used in, e.g., [SSH](https://en.wikipedia.org/wiki/Secure_Shell "Secure Shell").

![image](ae_e&m.png)

### MAC-then-Encrypt (MtE)

A MAC is produced based on the plaintext, then the plaintext and MAC are together encrypted to produce a ciphertext based on both. The ciphertext (containing an encrypted MAC) is sent. AEAD is used in [SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "SSL/TLS").[[16]](https://en.wikipedia.org/wiki/Authenticated_encryption#cite_note-16) Even though the MtE approach has not been proven to be strongly unforgeable in itself,[[13]](https://en.wikipedia.org/wiki/Authenticated_encryption#cite_note-BN-13) the [SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "SSL/TLS") implementation has been proven to be strongly unforgeable by Krawczyk who showed that SSL/TLS was, in fact, secure because of the encoding used alongside the MtE mechanism.

![image](ae_mte.png)



