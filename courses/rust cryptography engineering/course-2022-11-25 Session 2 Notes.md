---
creation-date: 2022-11-24
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-11-25 Session 2 Notes
- prev:: [[course-2022-11-18 Session 1 Notes]]
- next:: [[course-2022-12-02 Session 3 Notes]]
- solns:: [[course-HW 2 Solutions]]

## Notes
- Covering chapter 2. Assigned reading for next week: chapters 3 and 4, and familiarize yourself with NIST's standard: [Block Cipher Techniques | CSRC](https://csrc.nist.gov/Projects/block-cipher-techniques/BCM/current-modes)
- Note the week 2 poll [Discord](https://discord.com/channels/1031896857074475059/1045759265689849917)
- On lectures: lectures aren't the best learning vector for anyone, but with a little effort we can make them worse. A couple great ways to reduce the effectiveness of lectures:
    - Woody Allen said ninety percent of life is just showing up, so come to every lecture, but don't interact with the lecture at all. Don't ask questions during the lecture. Certainly don't come to the lecture with prepared thoughts and questions from the reading. Multitask, but let the lecture occasionally puncture the wall of your attention, distracting you *just long enough* to break your focus on from your other tasks.
    - If you did prepare for the lecture by reading or doing the exercises, wait until the lecture to ask any and all questions. Don't talk to your study group about them, questions have **secret mystical alpha** that can only be released on Fridays.
    - 80:20 your learning by reading the book during the lecture. Maximize your sensory inputs with cryptography-related content in the weekly hour-long burst, like a HIIT exercise session.
    - And under no circumstances should you go out of your way to answer others' questions in the Discord, much less make an effort to build a well-maintained exercise repo, or write short blog posts about problems you found interesting or challenging, and how you solved them. Peers and potential employers are known to hate reading.
- Review of [[course-HW 1 Solutions]]
- Rust
    - Reminder: every 5 weeks is scheduled code review week, where every student who wants to can submit a piece of code. I'll be reviewing alongside some other cryptography engineers who have volunteered to help with that. This is week 2. Your first of three opportunities for code review will be in 3 weeks.

## Extra Reading:
Concurrently to *New Directions in Cryptography*, IBM published what would become the Data Encryption Standard in 1975, which would become standardized three years later in 1978. IBM originally targeted 64 bits of security, but the NSA offered to disclose vulnerabilities in the algorithm to IBM, in exchange for a lower bit security, 48 bits, so that the NSA would have an easier time breaking encryption by brute force. IBM and the NSA agreed on a midway, 56 bit security, and the NSA patched vulnerabilities in the DES algorithm. The precise contributions of the NSA were kept private, in part to maintain the secrecy of differential cryptanalysis techniques. However, the existence of the collaboration was publicly known and heavily scrutinized by cryptographers, including Whitfield Diffie and Martin Hellman, who argued for the necessity of a 128-bit key.
- Copy A: https://web.archive.org/web/20140226205104/http://origin-www.computer.org/csdl/mags/co/1977/06/01646525.pdf
- Copy B: https://ee.stanford.edu/~hellman/publications/27.pdf

# Exercises
This week's has a base set of exercises, and an extended exercise set for those who would like more practice.

## Chapter 3 (p. 61)
1; How much space would be required to store a table for an entire idealized block cipher that operates on 64-bit blocks and has 80-bit keys?

6; Consider a new block cipher, *DES2*, that consists only of two rounds of the *DES* block cipher. *DES2* has the same block and key size as *DES*. For this question you should consider the *DES* $F$ function as a black box that takes two inputs, a 32-bit data segment and a 48-bit round key, and that produces a 32-bit output. Suppose you have a large number of plaintext-ciphertext pairs for *DES2* under a single, unknown key. Give an algorithm for recovering the 48-bit round key for round 1 and the 48-bit round key for round 2. Your algorithm should require fewer operations than an exhaustive search for an entire 56-bit *DES* key. Can your algorithm be converted into a distinguishable attack against *DES2*?

8; Using an existing cryptographic library, decrypt the following ciphertext (in hex)
```hex
	53 9B 33 3B 39 70 6D 14 90 28 CF E1 D9 D4 A4 07
```
with the following 256-bit key (also in hex):
```hex
	80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
	00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```
using *AES*.

## Chapter 4 (p. 107)
1; Let $P$ be a plaintext and let $\ell(P)$ be the length of $P$ in bytes. Let $b$ be the block size of the block cipher in bytes. Explain why the following is not a good padding scheme:

Determine the minimum number of padding bytes necessary in order to pad the plaintext to a block boundary. This is a number $n$ which satisfies $0 ≤ n ≤ b − 1$ and $n + l(P)$ is a multiple of $b$. Pad the plaintext by appending $n$ bytes, each with value $n$.

3; Suppose you, as an attacker, observe a pair of  32-byte ciphertexts $C, C'$, and you know these ciphertexts were generated using CTR mode with the same nonce. By chance, you obtain $P$ corresponding to $C$. What information, if any, can you infer about the plaintext $P'$ corresponding to $C'$?

4; The ciphertext (in hex):
```hex
87 F3 48 FF 79 B8 11 AF 38 57 D6 71 8E 5F 0F 91
7C 3D 26 F7 73 77 63 5A 5E 43 E9 B5 CC 5D 05 92
6E 26 FF C5 22 0D C7 D4 05 F1 70 86 70 E6 E0 17
```
was generated with the 256-bit AES key (also in hex)
```hex
80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```
using CBC mode with a random IV. The IV is included at the beginning of the ciphertext. Decrypt this ciphertext. You may use an existing cryptography library for this exercise.

6; Let $P_1$, $P_2$ be a message that is two blocks long, and let $P'_1$ be a message that is one block long. Let $C_0, C_1, C_2$ be the encryption of $P_1, P_2$ using CBC mode with a random IV and a random key, and let $C'_0, C'_1$ be the encryption of $P'_1$ using CBC mode with a random IV and the same key. Suppose an attacker knows $P_1, P_2$ and suppose the attacker intercepted and thus knows $C_0, C_1, C_2$ and $C'_0, C'_1$. Further suppose that, by random chance, $C'_1 = C_2$. Show that the attacker can compute $P'_1$.


# Extended Exercises
## Chapter 3
5; Suppose you have a processor that can perform a single DES encryption or decryption operation in $2^{-26}$ seconds. Suppose you also have a large number of plaintext-ciphertext pairs for $DES$ under a single unknown key. How many hours would it take, on average, to find that $DES$ key, using an exhaustive search approach and a single processor? How many hours would it take, with a collection of $2^{14}$ processors?

9; Using an existing cryptography library, encrypt the following plaintext (in hex)
```ex
	29 6C 93 FD F4 99 AA EB 41 94 BA BC 2E 63 56 1D
```
with the following 256-bit key from problem 8, using *AES*. Then re-encrypt and decrypt it using a 3072-bit RSA key with GnuPG, or your choice of asymmetric crypto CLI.

10; Write a program that experimentally demonstrates the complementation property for DES. This program should take as input a key $K$ and a plaintext $P$ and demonstrate that the DES complementation property holds for this key and plaintext. You may use an existing cryptography library for this exercise.

## Chapter 4
5; Encrypt the plaintext
```hex
62 6C 6F 63 6B 20 63 69 70 68 65 72 73 20 20 20
68 61 73 68 20 66 75 6E 63 74 69 6F 6E 73 20 78
62 6C 6F 63 6B 20 63 69 70 68 65 72 73 20 20 20
```
using AES in ECB mode and the key
```hex
80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01.
```
You may use an existing cryptography library for this exercise.

- Implement a pair of functions: A [PKCS 7](https://en.wikipedia.org/wiki/PKCS_7) message padding function, and a padding validation function that takes a message and validates whether it has a correct padding.