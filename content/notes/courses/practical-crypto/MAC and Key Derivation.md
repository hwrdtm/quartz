---
title: "MAC and Key Derivation"
---

**Message authentication codes** (**MAC**), **HMAC** (hash-based message authentication code) and **KDF** (key derivation functions) play important role in cryptography.

MACs behave similar to a hash function. MAC algorithms are also known as "**keyed hash functions**", because they behave like a hash function with a key.

```
auth_code = MAC(key, msg)
```

For example

```
HMAC-SHA256('key', 'some msg') = 32885b49c8a1009e6d66662f8462e7dd5df769a7b725d1d546574e6d5d6e76ad
```

The MAC code is **digital authenticity code**, like a **digital signature**, but with **pre-shared key**. We shall learn more about digital signing and digital signatures later.

## MAC Algorithms

Many **algorithms** for calculating message authentication codes (MAC) exist in modern cryptography. The most popular are based on **hashing** algorithms, like [**HMAC**](https://en.wikipedia.org/wiki/HMAC) (Hash-based MAC, e.g. HMAC-SHA256) and [**KMAC**](https://www.cryptosys.net/manapi/api_kmac.html) (Keccak-based MAC). Others are based on **symmetric ciphers**, like [**CMAC**](https://en.wikipedia.org/wiki/One-key_MAC) (Cipher-based MAC), [**GMAC**](https://en.wikipedia.org/wiki/Galois/Counter_Mode) (Galois MAC) and [**Poly1305**](https://en.wikipedia.org/wiki/Poly1305) (Bernstein's one-time authenticator). Other MAC algorithms include [**UMAC**](https://en.wikipedia.org/wiki/UMAC) (based on universal hashing), [**VMAC**](https://en.wikipedia.org/wiki/VMAC) (high-performance block cipher-based MAC) and [**SipHash**](https://en.wikipedia.org/wiki/SipHash) (simple, fast, secure MAC).

## When Do We Need MAC Codes

A sample scenario for using MAC codes is like this:

- Two parties exchange somehow a certain secret **MAC key** (pre-shared **key**).
- We receive a **msg** + **auth_code** from somewhere (e.g. from Internet, from the blockchain, or from email message).
- We want to be sure that the **msg** is **not tampered**, which means that both the **key** and **msg** are correct and match the MAC code.
- In case of **tampered message**, the MAC code will be incorrect.

## Authenticated Encryption: Encrypt / Decrypt Using MAC

Another scenario to use **MAC codes** is for [[notes/learning/crypto/Authenticated Encryption|authenticated encryption]] when we **encrypt a message** and we want to be sure the **decryption password is correct** and the decrypted message is the same like the original message before encryption.

-   First, we **derive a key** from the password. We can use this key for the MAC calculation algorithm (directly or hashed for better security).
-   Next, we **encrypt the message** using the derived key and store the ciphertext in the output.
-   Finally, we calculate the **MAC code** using the derived key and the original message and we append it to the output.

When we **decrypt the encrypted message** (ciphertext + MAC), we proceed as follows:

-   First, we **derive a key** from the password, entered by the user. It might be the correct password or wrong. We shall find out later.
-   Next, we **decrypt the message** using the derived key. It might be the original message or incorrect message (depends on the password entered).
-   Finally, we calculate a **MAC code** using the derived key + the decrypted message.
    -   If the calculated MAC code matches the MAC code in the encrypted message, the **password is correct**.
    -   Otherwise, it will be proven that the decrypted message is not the original message and this means that the **password is incorrect**

Some **authenticated encryption algorithms** (such as **AES-GCM** and **ChaCha20-Poly1305**) integrate the MAC calculation into the encryption algorithm and the MAC verification into the decryption algorithm.

The MAC is stored along with the ciphertext and it **does not reveal** the password or the original message. Storing the MAC code, visible to anyone is safe, and after decryption, we know whether the message is the original one or not (wrong password).

## MAC-Based Pseudo-Random Generator

Another application of MAC codes is for **pseudo-random generator** functions. We can start from certain **salt** (constant number or the current date and time or some other randomness) and some **seed** number (last random number generated, e.g. **0**). We can calculate the **next_seed** as follows:

```
next_seed = MAC(salt, seed)
```

This **next pseudo-random number** is "randomly changed" after each calculation of the above formula and we can use it to generate the next random number in certain range.

## HMAC and Key Derivation

Simply calculating `hash_func(key + msg)` to obtain a MAC (message authentication code) is considered **insecure** (see the [details](https://en.wikipedia.org/wiki/HMAC#Design_principles)). It is recommended to use the **HMAC algorithm instead**, e.g. `HMAC-SHA256` or `HMAC-SHA3-512` or other secure MAC algorithm.

The `hash_func` can be any cryptographic hash function like `SHA-256`, `SHA-512`, `RIPEMD-160`, `SHA3-256` or `BLAKE2s`.

**HMAC** is used for message **authenticity**, message **integrity** and sometimes for **key derivation**.

### Key Derivation Functions

**Key derivation function** (KDF) is a function which transforms a variable-length password to fixed-length key (sequence of bits):

```
function(password) -> key
```

As **very simple KDF function**, we can use SHA256: just hash the password. Don't do this, because it is **insecure**. Simple hashes are vulnerable to **dictionary attacks**.

As more complicated KDF function, you can derive a password by calculating **HMAC(salt, msg, SHA256)** using some random value called "**salt**", which is stored along with the derived key and used later to derive the same key again from the password.

Using **HKDF (HMAC-based key derivation)** for key derivation is **less secure** than modern KDFs, so experts recommend using stronger key derivation functions like [PBKDF2](https://en.wikipedia.org/wiki/PBKDF2), [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt), [Scrypt](https://en.wikipedia.org/wiki/Scrypt) and [Argon2](https://en.wikipedia.org/wiki/Argon2). We shall discuss all these KDF functions later.

## KDF - Deriving Keys from Passwords

In cryptography we often use **passwords** instead of **binary keys**, because passwords are easier to remember, to write down and can be shorter.

When a certain algorithm needs a **key** (e.g. for encryption or for digital signing) a **key derivation function** (password -> key) is needed.

We already noted that using `SHA-256(password)` as key-derivation is insecure! It is vulnerable to many attacks: **brute-forcing**, **dictionary attacks**, **rainbow attacks** and others, which may reverse the hash in practice and attacker can obtain the password.

[PBKDF2](https://en.wikipedia.org/wiki/PBKDF2), [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt), [Scrypt](https://en.wikipedia.org/wiki/Scrypt) and [Argon2](https://en.wikipedia.org/wiki/Argon2) are significantly stronger key derivation functions and are designed to survive password guessing (brute force) attacks.

By design **secure key derivation functions** use **salt** (random number, which is different for each key derivation) + **many iterations** (to speed-down eventual password guessing process). This is a process, known as [**key stretching**](https://en.wikipedia.org/wiki/Key_stretching).

## PBKDF2

**PBKDF2** is a simple cryptographic key derivation function, which is resistant to [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack) and [rainbow table attacks](https://en.wikipedia.org/wiki/Rainbow_table). It is based on iteratively deriving **HMAC** many times with some padding. The **PBKDF2** algorithm is described in the Internet standard [RFC 2898 (PKCS #5)](http://ietf.org/rfc/rfc2898.txt).

**PBKDF2** takes several **input parameters** and produces the derived **key** as output:

```
key = pbkdf2(password, salt, iterations-count, hash-function, derived-key-len)
```


Technically, the **input data** for **PBKDF2** consists of:

-   `password` – array of bytes / string, e.g. "_p@$Sw0rD~3_" (8-10 chars minimal length is recommended)
-   `salt` – securely-generated random bytes, e.g. "_df1f2d3f4d77ac66e9c5a6c3d8f921b6_" (minimum 64 bits, 128 bits is recommended)
-   `iterations-count`, e.g. 1024 iterations
-   `hash-function` for calculating **HMAC**, e.g. `SHA256`
-   `derived-key-len` for the output, e.g. 32 bytes (256 bits)

Today **PBKDF2** is considered old-fashioned and less secure than modern KDF functions, so it is recommended to use **Bcrypt**, **Scrypt** or **Argon2** instead. 

## Modern Key Derivation Functions

**PBKDF2** has a major weakness: it is **not GPU-resistant** and **not ASIC-resistant**, because it uses relatively small amount of RAM and can be efficiently implemented on GPU (graphics cards) or **ASIC** (specialized hardware).

Modern key-derivation functions (KDF) like [**Scrypt**](https://en.wikipedia.org/wiki/Scrypt) and [**Argon2**](https://en.wikipedia.org/wiki/Argon2) are designed to be **resistant** to **dictionary attacks**, **GPU attacks** and **ASIC attacks**. These functions derive a key (of fixed length) from a password (text) and need a lot memory (RAM), which does not allow fast parallel computations on GPU or ASIC hardware.

Algorithms like **Bcrypt**, **Scrypt** and **Argon2** are considered more **secure** KDF functions. They use **salt** + many **iterations** + a lot of **CPU** + a lot of **RAM** memory and this makes very hard to design a custom hardware to significantly speed up password cracking.

It takes a lot of **CPU time** to derive the key (e.g. 0.2 sec) + a lot of **RAM memory** (e.g. 1GB). The calculation process is memory-dependent, so **the memory access is the bottleneck** of the calculations. Faster RAM access will speed-up the calculations.

## Scrypt

The **memory** in Scrypt is accessed in strongly **dependent order** at each step, so the memory access speed is the algorithm's bottleneck. The **memory required** to compute Scrypt key derivation is calculated as follows:

```
Memory required = 128 * N * r * p bytes
```

Example: e.g. 128 * N * r * p = 128 * 16384 * 8 * 1 = 16 MB (or 128 * N * r * p = 128 * 2048 * 8 * 1 = 2 MB)

In many applications, frameworks and tools, **Scrypt encrypted passwords are stored together with the algorithm settings and salt**, into a single string (in certain format), consisting of several parts, separated by `$` character. For example, the password `p@ss~123` can be stored in the Scrypt standard format like this (several examples are given, to make the pattern apparent):


```
16384$8$1$kytG1MHY1KU=$afc338d494dc89be40e317788e3cd9166d066709db0e6481f0801bd918710f46

16384$8$1$5gFGlElztY0=$560f6229356c281a525fad4e2fc4c209bb55c21dec789381335a32bb84888a5a

32768$8$4$VGhlIHF1aWo=$54d657cec8b3aaca675b407e790bccf1dddb0a23665cd5f994820a736d4b58ba
```

## Bcrypt

[**Bcrypt**](https://en.wikipedia.org/wiki/Bcrypt) is another cryptographic KDF function, **older than Scrypt**, and is **less resistant** to ASIC and GPU attacks. It provides configurable iterations count, but uses constant memory, so it is easier to build hardware-accelerated password crackers.

In many applications, frameworks and tools (e.g. in the database of WordPress sites), **Bcrypt encrypted passwords are stored together with the algorithm settings and salt**, into a single string (in certain format), consisting of several parts, separated by `$` character. For example, the password `p@ss~123` can be stored in the Bcrypt encrypted format like this (several examples are given, to make the pattern apparent):

```
$2a$07$wHirdrK4OLB0vk9r3fiseeYjQaCZ0bIeKY9qLsNep/I2nZAXbOb7m

$2a$12$UqBxs0PN/u106Fio1.FnDOhSRJztLz364AwpGemp1jt8OnJYNsr.e

$2a$12$8Ov4lfmZZbv8O5YKrXXCu.mdH9Dq9r72C5GnhVZbGNsIzTr8dSUfm
```

## Argon2

[**Argon2**](https://en.wikipedia.org/wiki/Argon2) is modern **ASIC-resistant** and **GPU-resistant** secure key derivation function. It has better password cracking resistance (when configured correctly) than **PBKDF2**, **Bcrypt** and **Scrypt** (for similar configuration parameters for CPU and RAM usage).

## Secure Password Storage

### Salted Hashed Passwords - Secure, but Not Enough

-   The idea is to keep different random **salt**, along with different **password hash**, changed every time, when the password is written in the database. Thus the same password is encrypted every time as different ciphertext { **salt** + **hash** }.
-   To **check the password**, developers **calculate the hash**(password for checking) using the **salt** from the database and compare the **calculated hash** with the **hash from the database**.
-   This method works well to prevent dictionary attacks, but does not prevent **GPU**-based and **ASIC**-based brute force password cracking attacks.
-   It has also the same **security problems** like using hash(key + msg) instead of HMAC(key, msg), e.g. [length-extension attack](https://en.wikipedia.org/wiki/Length_extension_attack).
-   Basically keeping **salted hashed passwords** is more secure than the previous methods, but still **avoid it**.
    -   Use more attack-resistant password hashing function (which is unlikely to be brute-forced) instead of simple hash, e.g. Argon2 or Scrypt.

### Secure KDF-Based Password Hashing - Recommended

The most complicated and **most secure** method for secure password storage and password-based authentication is to use **secure KDF-based password hash**, written in the database as pair { **salt** + **KDF(password, salt)** }. The **key-derivation function** (KDF) should be strong and secure, e.g. **Scrypt** or **Argon2** with carefully selected parameters.

-   The idea is to keep different random **salt** for each encrypted password, along with the **key** derived by a secure KDF-function, such as **Scrypt** or **Argon2** (with reasonable number of iterations and RAM consumption settings).
-   To **check the password**, take the **salt** from the database and **derive a key** from the password for checking, using the same KDF function and KDF parameters like when the password was stored in the database. Compare the **derived key** with the **key from the database**.
-   This method is **resistant to most attacks** and is considered as standard in the software industry.
    -   It is as **secure** as the KDF function with the selected KDF parameters. For example, **Argon2** taking 128 MB RAM, 4 threads and 200 ms computing time) may be appropriate for the average case.
    -   Crackers cannot perform **brute force attacks**, because the password guessing will be too slow, even on a modern computer with good CPU and GPU or even using a specialized ASIC hardware.

## Password-Based Authentication Attacks

- Password guessing
	- Using a [**CAPTCHA**](https://en.wikipedia.org/wiki/CAPTCHA) after a 2-3 unsuccessful login attempts provides quite good protection.
- **Denial of service attack**: attacker may attempt to login too many times to overload the system or can try to lock some user account with too many invalid login attempts for the same user.
	- The **protection** from this attack is similar to the previous attack: use a **CAPTCHA** and **delay the login** process for certain IP address after each login attempt.
- **Intercept and replay attack**: attacker may intercept the authentication communication (to sniff the login / password / auth ticket / other credentials) and use the intercepted credentials to login later.
	- Most systems solve this problem by using [**TLS**](https://en.wikipedia.org/wiki/Transport_Layer_Security) (encrypted connection) to securely send the authentication credentials (password / authentication ticket) to the server.
	-   Other solutions include [challenge-response](https://en.wikipedia.org/wiki/Challenge%E2%80%93response_authentication) based **cryptographic authentication scheme**, such as the scheme used in the [Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol)) protocol.
-   **Man-in-the-middle attack**: attacker can intercept and modify the intercepted traffic between the server and the client to trick the user to reveal its login credentials.
    -   This is solved by using a [**TLS**](https://en.wikipedia.org/wiki/Transport_Layer_Security) secure connection with server certificate, which **authenticates the server**.
    -   In some scenarios (e.g. online banking) **clients are also authenticated** by a digital certificate or OTP (one-time password).
-   **Compromised server attack**: if the authentication server and its database is compromised (hacked) and all its authentication data is leaked, the attacker should be unable to reveal user's plaintext passwords.
    -   First, it should be clear that if the authentication server is compromised, in all cases the **attackers will get unauthorised access**, because they will be able to intercept user's legitimate sessions (their login and communication after successful login) and use them to impersonate the user.
    -   Using a strongly **secure password storage** mechanism mitigates the risk for users' passwords to be revealed as plaintext. Still, attackers who gain access to the authentication server may inject password interception [backdoor](https://en.wikipedia.org/wiki/Backdoor_(computing)) and steal each user's plaintext credentials (username + password) during the login.
    -   The **backdoored server attack** can be stopped like this: the client generates a random number **r** and sends as authentication **HMAC(password, r)**; the server compares the HMAC with its stored password. This process may be combined with **client-side Scrypt or Argon2** computation and securely stored password at the server side (Scrypt or Argon2 hashed). In this scenario, unless the client software is not compromised, attackers who gained access to the authentication server will not obtain user's passwords in plaintext.
    -   In Web applications, if the server is compromised it can **inject JavaScript code** to compromise the client itself. In desktop and mobiles apps, the client is more safe in case of compromised server.