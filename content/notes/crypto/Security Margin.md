---
title: security-margin
---
Security margin is the difference between the number of rounds in the complete implementation of the cipher and the maximum number of rounds that are known to be breakable using the best-known real-world attack.

For instance, currently the best-known faster-than-brute-force attacks against AES-256 can break up to 9 rounds out of the total 14 rounds in the full cipher when used in the standard mode known as _Electronic Codebook_ (ECB) mode. Therefore, currently the security margin of AES-256 is 5 rounds.

Ciphers are usually implemented using multiple rounds so the concept of security margin usually applies to cryptographic ciphers.

# Resources

https://learning.quantum.ibm.com/course/practical-introduction-to-quantum-safe-cryptography/symmetric-key-cryptography
