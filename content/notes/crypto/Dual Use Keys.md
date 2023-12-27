---
title: "Dual Use Keys"
---

Examples:
- RSA key pairs can be used for signing or encryption.
- EC key pairs can be used for signing or key agreement.
- EC key pairs can used for encryption using the EC Integrated Encryption Scheme. In this case, the EC key pair is being used for key agreement as part of the algorithm.
- Symmetric keys can be used for encryption and authentication.

Do:
- A key should only be used for one type of operation.

Don't:
- Don’t use the same key for different types of data / different security domains.
- The same key should not be used with different parameters. For example, an RSA key should not be used to create RSA/SHA256 and RSA/SHA512 signatures.

Reasons:
1. Key cycling time frames may differ for different types of keys.
2. Revocation: It may be desirable to be able to revoke the signing key pair or encryption key pair, without affecting the other key pair.
3. Non-repudiation and Key Escrow: Only the owner of a signing private key should be able to access a signing private key. However, it may be desirable to escrow encryption private keys.
4. Algorithm Compromise: In the unlikely event that one algorithm or implementation becomes compromised, using a single key pair for two usages would compromise both usages.
5. Lack of Security Proofs: Individual algorithms have security proofs written for them to show that they are secure. However, generally, two separate algorithms do not have a joint security proof showing that using the same key for two algorithms at the same time is secure.
6. Known issues: RSA

# Resources

- https://www.youtube.com/watch?v=VB3IWrgx1Bk