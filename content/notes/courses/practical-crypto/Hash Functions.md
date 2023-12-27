---
title: "Hash Functions"
---

# Overview

**Cryptographic hash** functions transform text or binary data to fixed-length **hash value** and are known to be **collision-resistant** and **irreversible**.

Hash functions are **irreversible by design**, which means that there is no fast algorithm to restore the input message from its hash value.

A **naive hash function** is just to sum the bytes of the input data / text. It causes a lot of collisions, e.g. `hello` and `ehllo` will have the same hash code. **Better hash functions** may use the [Merkle–Damgård construction](https://en.wikipedia.org/wiki/Merkle%E2%80%93Damg%C3%A5rd_construction) scheme, which takes the first byte as **state**, then **transforms the state** (e.g. multiplies it by a prime number like 31), then **adds the next byte** to the state, then again transforms the state and adds the next byte, etc. This significantly reduces the rate of collisions and produces better distribution.

The **ideal cryptographic hash function** should have the following properties:
- **Deterministic**: the same input message should always result in the same hash value.
- **Quick**: it should be fast to compute the hash value for any given message.
- **Hard to analyze**: a small change to the input message should totally change the output hash value.
- **Irreversible**: generating a valid input message from its hash value should be **infeasible**. This means that there should be no significantly better way than brute force (try all possible input messages).
- **No collisions**: it should be extremely hard (or practically impossible) to find two different messages with the same hash.

# Applications of hash functions

- Document integrity (sha256 checksum)
- Storing passwords
	- Storing **passwords** and verification of passwords. Instead of keeping a plain-text password in the database, developers usually keep **password hashes** or more complex values derived from the password (e.g. **Scrypt**-derived value).
- Pseudorandom number generation
	- **Pseudorandom generation** and key derivation. Hash values can serve as random numbers. A simple way to generate a random sequence is like this: start from a **random seed** (entropy collected from random events, such like keyboard clicks or mouse moves). Append "**1**" and calculate the hash to obtain the first random number, then append "**2**" and calculate the hash to obtain the second random number, etc.
- PoW algorithms
	- Most proof-of-work algorithms calculate a hash value which is bigger than certain value (known as mining difficulty). To find this hash value, miners calculate billions of different hashes and take the biggest of them, because hash numbers are unpredictable. For example, the proof of work problem might be defined as follows: find a number `p`, such that `hash(x + p)` holds 10 zero bits at its beginning.


# Secure Hash Algorithms


- **Modern cryptographic hash algorithms** (like **SHA-3** and **BLAKE2**) are considered **secure** enough for most applications.
- [**SHA-2**](https://en.wikipedia.org/wiki/SHA-2) is a family of strong cryptographic hash functions: **SHA-256** (256 bits hash), **SHA-384** (384 bits hash), **SHA-512** (512 bits hash), etc. It is based on the cryptographic concept "[**Merkle–Damgård construction**](https://en.wikipedia.org/wiki/Merkle%E2%80%93Damg%C3%A5rd_construction)" and is considered **highly secure**. SHA-2 is published as official crypto standard in the United States.
- More hash bits == more collision resistance

## SHA-3

[**SHA-3**](https://en.wikipedia.org/wiki/SHA-3) (and its variants SHA3-224, SHA3-256, SHA3-384, SHA3-512), is considered **more secure than SHA-2** (SHA-224, SHA-256, SHA-384, SHA-512) for the same hash length. For example, SHA3-256 provides **more cryptographic strength than SHA-256** for the same hash length (256 bits).

The **SHA-3** family of functions are representatives of the "**Keccak**" hashes family, which are based on the cryptographic concept "[**sponge construction**](https://en.wikipedia.org/wiki/Sponge_function)". Keccak is the winner of the [SHA-3 NIST competition](https://en.wikipedia.org/wiki/NIST_hash_function_competition#Finalists).

Unlike **SHA-2**, the **SHA-3** family of cryptographic hash functions are not vulnerable to the "[**length extension attack**](https://en.wikipedia.org/wiki/Length_extension_attack)".

The hash function **Keccak-256**, which is used in the **Ethereum** blockchain, is a variant of SHA3-256 with some constants changed in the code.

The hash functions **SHAKE128(msg, length)** and **SHAKE256(msg, length)** are variants of the **SHA3-256** and **SHA3-512** algorithms, where the output message length can vary.

## Blake2

[**BLAKE**](https://en.wikipedia.org/wiki/BLAKE_%28hash_function) / **BLAKE2** / **BLAKE2s** / **BLAKE2b** is a family of fast, highly secure cryptographic hash functions, providing calculation of 160-bit, 224-bit, 256-bit, 384-bit and 512-bit digest sizes, widely used in modern cryptography. BLAKE is one of the finalists at the [SHA-3 NIST competition](https://en.wikipedia.org/wiki/NIST_hash_function_competition#Finalists).

The **BLAKE2** function is an improved version of **BLAKE**.

**BLAKE2s** (typically **256-bit**) is BLAKE2 implementation, performance-optimized for 32-bit microprocessors.

**BLAKE2b** (typically **512-bit**) is BLAKE2 implementation, performance-optimized for 64-bit microprocessors.

## RIPEMD-160

[**RIPEMD-160**](https://en.wikipedia.org/wiki/RIPEMD) is a secure hash function, widely used in cryptography, e.g. in PGP and Bitcoin.

The **160-bit** variant of **RIPEMD** is widely used in practice, while the other variations like RIPEMD-128, RIPEMD-256 and RIPEMD-320 are not popular and have disputable security strengths.

As recommendation, **prefer using SHA-2 and SHA-3** instead of RIPEMD, because they are more stronger than RIPEMD, due to higher bit length and less chance for collisions.

## Insecure Hash Functions

Avoid using of the following hash algorithms, which are considered **insecure** or have disputable security: [**MD2**](https://en.wikipedia.org/wiki/MD2_(hash_function), [**MD4**](https://en.wikipedia.org/wiki/MD4), [**MD5**](https://en.wikipedia.org/wiki/MD5), [**SHA-0**](https://en.wikipedia.org/wiki/SHA-1#SHA-0), [**SHA-1**](https://en.wikipedia.org/wiki/SHA-1), [**Panama**](https://en.wikipedia.org/wiki/Panama_(cryptography), [**HAVAL**](https://en.wikipedia.org/wiki/HAVAL) (disputable security, collisions found for HAVAL-128), [**Tiger**](https://en.wikipedia.org/wiki/Tiger_(hash_function) (disputable, weaknesses found), [**SipHash**](https://en.wikipedia.org/wiki/SipHash) (it is not a cryptographic hash function).

## PoW Hash Functions

Learn more about **ETHash** at: [https://github.com/ethereum/wiki/wiki/Ethash](https://github.com/ethereum/wiki/wiki/Ethash), [https://github.com/lukovkin/ethash](https://github.com/lukovkin/ethash).

Learn more about **Equihash** at: [https://www.cryptolux.org/images/b/b9/Equihash.pdf](https://www.cryptolux.org/images/b/b9/Equihash.pdf), [https://github.com/tromp/equihash](https://github.com/tromp/equihash).

Lear more about the **ASIC-resistant hash functions** at: [https://github.com/ifdefelse/ProgPOW](https://github.com/ifdefelse/ProgPOW).