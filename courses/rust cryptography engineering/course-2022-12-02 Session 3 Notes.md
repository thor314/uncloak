---
creation-date: 2022-12-02
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-02 Session 3 Notes
- prev:: [[course-2022-11-25 Session 2 Notes]]
- solns:: [[course-2022-12-02 HW 3 Solutions]]
- next:: [[course-2022-12-09 Session 4 Notes]]

## Notes
- Review of Chapter 3 and 4
- Review of Exercises from Chapter 3 and 4 (we may have gone a bit overboard)
- Notes on Block Ciphers
    - Block Ciphers operate on, naturally enough, blocks (128 bits for AES, 64 bits for DES).
    - the *Ideal Block Cipher* is difficult to formally define, but we want some properties:
        - Indistinguishable: the block ciphertext should be indistinguishable from randomness; that is, there should not exist a generic *distinguishing attack* for the block cipher, reducing the block cipher's security to (much) less than 128 bits. Generic in this instance refers to the fact that, by block cipher construction, several useless attacks (eg. non-odd permutations) apply to all existing block-ciphers.
            - On distinguishing attacks: a distinguishing attack is useful for identifying *which cipher is used*, though a strong adversary is already assumed to know which cipher is used. The existence of a distinguishing attack does not imply that the adversary can decrypt, but that an adversary may be able to decrypt certainly implies a distinguishing attack.
            - AES128 for instance has a distinguishing attack running in 126 operations; this is technically a distinguishing attack, but not one we care much about in practice
        - Fast: the cipher should be efficient to compute.
    - The authors express great skepticism for AES. At time of publishing (2010), several theoretical attacks on AES were recently uncovered. These attacks have hardly improved. AES-CBC and AES-CTR are still widely used. At the same time, stream ciphers have improved, and are quite efficient. The faster ChaCha20-poly1305 stream cipher is a [standardized](https://datatracker.ietf.org/doc/rfc7905/) cipher for TLS.
- Notes on Block Cipher Modes
    - Since a block cipher is typically used to encrypt more than one block (64 or 128 bits), block cipher modes are used to encrypt longer messages.
    - Padding schemes: If the block length is $n$, and the message is $kn-d$, where $d\in [1,n-1]$, the message should be padded to a multiple of $n$ with a padding scheme. Several padding schemes are standard, optionally see the Wikipedia articles on [PKCS - Wikipedia](https://en.wikipedia.org/wiki/PKCS) and [Padding oracle attack - Wikipedia](https://en.wikipedia.org/wiki/Padding_oracle_attack) for more details.
        - On padding attacks on CBC mode, in a variation of the CCA model: If the attacker has access to an oracle who will attempt to decrypt ciphertexts, and inform the attacker whether the padding on the decrypted plaintext is valid, (eg. some server to decrypt messages), the attacker can obtain messages with a padding oracle attack! See the above Wikipedia article for details. These attacks can be avoided by denying the attacker access to whether the ciphertext decrypted successfully, or more simply, avoiding CBC mode.
    - Behold the ECB Penguin [Exploring an Encrypted Penguin with AES-ECB](https://tonybox.net/posts/ecb-penguin/)
    - "What modes should I use?" Unless you are implementing a cipher yourself, You will rarely use a block cipher mode directly. You will more likely use an Authenticated Encryption with Associated Data (AEAD) cipher, to authenticate yourself to the corresponding party and vice versa. This week's reading covers several Message Authentication Code techniques, used in conjunction with a block cipher to construct a *secure channel* (an encrypted and authenticated chanel). See: [AEADs/aes-gcm at master · RustCrypto/AEADs · GitHub](https://github.com/RustCrypto/AEADs/tree/master/aes-gcm), though any TLS library should also include AEADs.
    - "When should I use the standard?" Very hard to answer! Often when you would like to use a standardized algorithm, there are new and vastly improved performance constructions! Sometimes there isn't a standard at all, and sometimes the standard is crap or out of date. NIST has been reasonably swift about keeping standards for the last several decades, but no standards body will ever be able to meet the needs of developers rapidly changing environments. If it's not obvious, ask around. If you need non-standard cryptography, the authors of that cryptography may have input on whether it is production-ready. It may also be the case that standard cryptography can be used in ways you didn't expect. Cryptographers tend to be open to receiving (well-posed, grammatically correct) questions about their work.

## Extra reading for this week
The reading is somewhat outdated this week. Several additional reading assignments to cover bases on hash functions:
- On the history of hash function attacks: we're pretty good at pre-image resistance! Collision resistance too lately. [Lessons From The History Of Attacks On Secure Hash Functions - Electric Coin Company](https://web.archive.org/web/20220708064142/https://electriccoin.co/blog/lessons-from-the-history-of-attacks-on-secure-hash-functions/)
- SHA2 and SHA3 are quite slow for hash functions. Blake3 is a 2-year-old, extremely fast hash function, based on the ChaCha stream cipher. [BLAKE (hash function) - Wikipedia](https://en.wikipedia.org/wiki/BLAKE_(hash_function)#BLAKE3).
- optional additional reading on analysis of collision resistance: [Analyzing the MD5 collision in Flame | Trail of Bits Blog](https://blog.trailofbits.com/2012/06/11/analyzing-the-md5-collision-in-flame/)
- additional optional reading on Keccak/SHA-3 (standardized 2016), to understand the Sponge construction for hashes.
    - By the Keccak authors: [Keccak Sponge](https://keccak.team/sponge_duplex.html)
    - If you'd like to read more, see: [https://www.crypto-textbook.com/download/Understanding-Cryptography-Keccak.pdf](https://www.crypto-textbook.com/download/Understanding-Cryptography-Keccak.pdf)
    - NIST on SHA3 standards [Hash Functions | CSRC](https://csrc.nist.gov/projects/hash-functions/sha-3-project)
- optional: Keccak-derived authentication functions: [SHA-3 Derived Functions: cSHAKE, KMAC, TupleHash and ParallelHash | NIST](https://www.nist.gov/publications/sha-3-derived-functions-cshake-kmac-tuplehash-and-parallelhash)

## ch5 exercises
- Exercise 5.3 Consider SHA-512-n, a hash function that first runs SHA-512 and then outputs only the first $n$ bits of the result. Write a program that uses a birthday attack to find and output a collision on SHA-512-n, where n is a multiple of 8 between 8 and 48. Your program may use an existing cryptography library. Time how long your program takes when n is 16, averaged over five runs for each $n.$ How long would you expect your program to take for SHA-512-256? For SHA-512?
- Exercise 5.4 Let SHA-512-n be as in the previous exercise. Write a program that finds a message M that hashes to the following value under SHA-512-16 (in hex):  `3D 4B`. How many tries would you expect the algorithm to need? Running the algorithm 5 times, How many tries did it take on average?
- With command line tools or Criterion, benchmark the [blake3 hash](https://docs.rs/blake3/latest/blake3/) (default is 256 bit output), and compare it to benches of [SHA3-256](https://docs.rs/sha3/latest/sha3/) and [SHA-256](https://docs.rs/sha2/latest/sha2/) (when written without a number, SHA is assumed to be SHA2).

## ch 6 exercises
- Exercise 6.3 Suppose a and b are both one block long, and suppose the sender MACs a, b, and $a || b$ with CBC-MAC. An attacker who intercepts the MAC tags for these messages can now forge the MAC for the message $m=b || (M(b) ⊕ M(a) ⊕ b)$, which the sender never sent. The forged tag for this message is equal to $M(a || b)$, the tag for $a || b$. Justify mathematically why this is true.
- Exercise 6.4 Suppose message $a$ is one block long. Suppose that an attacker has received the MAC $t$ for a using CBC-MAC under some random key unknown to the attacker. Explain how to forge the MAC for a two-block message of your choice. What is the two-block message that you chose? What is the tag that you chose? Why is your chosen tag a valid tag for your two-block message?
- Exercise 6.5 Using an existing cryptography library, compute the MAC of the message:
```hex
4D 41 43 73 20 61 72 65 20 76 65 72 79 20 75 73 65 66 75 6C 20 69 6E 20 63 72 79 70 74 6F 67 72 61 70 68 79 21 20 20 20 20 20 20 20 20 20 20 20
```

using CBC-MAC with AES and the 256-bit key:
```hex
80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```

- For message authentication, when would you use TupleHash? ParallelHash? KMAC?