---
title: "ChaCha20"
---

ChaCha20 is a stream cipher designed by Daniel J. Bernstein.  It is a refinement of the Salsa20 algorithm, and it uses a 256-bit key.

ChaCha20 works great in general purpose CPUs and takes advantage of [[notes/crypto/Single Instruction, Multiple Data (SIMD)|Single Instruction, Multiple Data (SIMD)]] which exists on virtually all non-embedded CPUs.

ChaCha20 vs. AES
- ChaCha20 is more efficient than AES in software-only implementations
- Larger [[notes/crypto/Security Margin|security margin]] than almost all AES ciphers 

XChaCha20 is a variant of the ChaCha20 algorithm that uses a 192-bit nonce instead of a 96-bit nonce, which makes it suitable for applications where nonces are generated randomly and there is a risk of collision.

# Resources

https://datatracker.ietf.org/doc/html/rfc8439#section-2

https://www.reddit.com/r/crypto/comments/f7c2nv/chacha20_v_aes256/