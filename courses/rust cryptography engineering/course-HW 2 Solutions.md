---
creation-date: 2022-12-01
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-HW 2 Solutions
- back:: [[course-2022-11-25 Session 2 Notes]]

## Chapter 3 (p. 61)
1; How much space would be required to store a table for an entire idealized block cipher that operates on 64-bit blocks and has 80-bit keys?
- How many possible keys are there? $2^{80}$.
- How many possible blocks are there? $2^{64}$
- There will be $2^{144}=2^{64}*2^{80}$ entries, with 64 bits per block, so $2^{150}=2^{144}*2^6$ bits total, or $2^{147}$ bytes.

6; Consider a new block cipher, *DES2*, that consists only of two rounds of the *DES* block cipher. *DES2* has the same block and key size as *DES*. For this question you should consider the *DES* $F$ function as a black box that takes two inputs, a 32-bit data segment and a 48-bit round key, and that produces a 32-bit output. Suppose you have a large number of plaintext-ciphertext pairs for *DES2* under a single, unknown key. Give an algorithm for recovering the 48-bit round key for round 1 and the 48-bit round key for round 2. Your algorithm should require fewer operations than an exhaustive search for an entire 56-bit *DES* key. Can your algorithm be converted into a distinguishable attack against *DES2*?

- This is the "fun problem of the set". The problem challenges us to break the keys in the KPA attack model. Let $L$ and $R$ be indexed by round: $L_0$ is for instance, the initial value, and $L_2$ the output. For convenience, let $f_i(R)=F(R, k_i)$. Then:
    - $R_1=F(R_0,k_0) \oplus L_0=f_0(R_0) \oplus L_0$
    - $L_1=R_0$
    - $R_2=F(R_1,k_1) \oplus L_1= f_1(R_1) \oplus L_1$
    - $L_2=R_1$

We start with some simple observations:
- 1.  Given $\{L_0,L_2,R_0,R_2\}$ (known-pairs), we can clearly obtain $L_1,R_1$.

The hard way would be to actually recover the key, as the problem suggests. If we have $2^{48}$ unique pairs, we can completely determine $f_0,f_1$ in $2^{48}$ steps, thereby retrieving the key. Now we arrive at the fun part. Some further observations:

- We can obtain an evaluation of $f_1,f_2$ for each given pair: $f_i(R_i) = R_{i+1}\oplus L_i$
- Given $f_i: 2^{32} \rightarrow 2^{32}$ ; we would need, on average, $\Theta(2^{16})$ pairs before obtaining any collision. The problem suggests that we have an ambiguous, *large* set of pairs. This should be more specific, **bonk** the authors!
- Can we directly detect collisions in $f$ for unknown ciphertexts with a collected table of known plaintexts? That is, if we know $L_i,R_i$, and are given $l_2,r_2$ for an encrypted message, can we break it? We have:
$$r_2= f_1(r_1) \oplus l_1$$
$$l_2=r_1=f_0(r_0)\oplus l_0$$

Since $l_2$ gives us a value for $r_1$, we may already have the evaluation $f_1(r_1)$ in storage. If we do, we may obtain half the plaintext, $r_0$:
$$r_0=l_1= r_2 \oplus f_1(r_1)$$

Further, if we can obtain $r_0$, and we have the evaluation $f_0(r_0)$ in storage, we likewise may obtain $l_0$.

Given a large enough set of pairs, this attack against *DES2* is quite efficient! If the attacker is able to *choose* messages, they can obtain a full plaintext-ciphertext table for this attack in $O(2^{32})$ pairs.

However, an even more efficient probabilistic attack exists. Though the ciphertext space for $l_2$ may be $2^{32}$, the common plaintext space for the first 4 bytes is much smaller, perhaps on the order of $2^10$. Suppose $l_0=L_0$. Then:
$$l_2\oplus L_2\oplus f_0(R_0)=(f_0(r_0)\oplus l_0) \oplus  L_0=f_0(r_0)$$

And we may check: $f_0(r_0)=_?l_2\oplus l_1$; if the equality is satisfied, then $l_0=L_0$. By a similar argument, we may check if $r_1=R_1$.


8; Using an existing cryptographic library, decrypt the following ciphertext (in hex)
```hex
	53 9B 33 3B 39 70 6D 14 90 28 CF E1 D9 D4 A4 07
```

with the following 256-bit key (also in hex)

```hex
	80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
	00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```

using *AES*.
- bash:
```bash
$ echo "539B333B39706D149028CFE1D9D4A407" | xxd -r -p | openssl enc -aes-256-ecb -d -nopad -K "8000000000000000000000000000000000000000000000000000000000000001" | xxd
```
- rust:
    - https://github.com/thor314/uncloak-hw/tree/main/hw2

## Chapter 4 (p. 107)
1; Let $P$ be a plaintext and let $\ell(P)$ be the length of $P$ in bytes. Let $b$ be the block size of the block cipher in bytes. Explain why the following is not a good padding scheme:

Determine the minimum number of padding bytes necessary in order to pad the plaintext to a block boundary. This is a number n which satisfies $0 ≤ n ≤ b − 1$ and $n +l (P)$ is a multiple of $b$. Pad the plaintext by appending $n$ bytes, each with value $n$.
- The above is not a good padding scheme because it allows for the padding to be 0 bytes long ($n = 0$). If $n=0$, and the plaintext $P$ is exactly the same length as the block ($b$), the block cipher will not know how much padding to remove and might remove some of the message. Generally $n$ should be $>0$ so that the block cipher knows how to deal with $P$. If $P$ is exactly the same length as the $b$, then an additional block of padding can be added ($\ell(P) = \ell(b)$).

3; Suppose you, as an attacker, observe a pair of  32-byte ciphertexts $C, C'$, and you know these ciphertexts were generated using CTR mode with the same nonce. By chance, you obtain $P$ corresponding to $C$. What information, if any, can you infer about the plaintext $P'$ corresponding to $C'$?

- Since we know $P$, $C$, & $C'$, we obtain $P'$:
    - $P' = P \oplus C \oplus C'$

If $C$ & $C'$ used a different nonce, this equality would not hold.

4; The ciphertext (in hex)

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
- bash:
```bash
$ echo "7C3D26F77377635A5E43E9B5CC5D05926E26FFC5220DC7D405F1708670E6E017" | xxd -r -p | openssl enc -aes-256-cbc -d -K "8000000000000000000000000000000000000000000000000000000000000001" -iv 87F348FF79B811AF3857D6718E5F0F91 -nopad | xxd
```
- Since The IV is included at the beginning of the ciphertext we know that "87F348FF79B811AF3857D6718E5F0F91" is the IV and can decrypt the ciphertext using the 256-bit AES key and this IV.


6; Let $P_1$, $P_2$ be a message that is two blocks long, and let $P'_1$ be a message that is one block long. Let $C_0, C_1, C_2$ be the encryption of $P_1, P_2$ using CBC mode with a random IV and a random key, and let $C'_0, C'_1$ be the encryption of $P'_1$ using CBC mode with a random IV and the same key. Suppose an attacker knows $P_1, P_2$ and suppose the attacker intercepted and thus knows $C_0, C_1, C_2$ and $C_0', C_1'$. Further suppose that, by random chance, $C_1' = C_2$. Show that the attacker can compute $P'_1$.
- Given that $C_i=E(K,P_i\oplus C_{i-1})$, we have:
$$C_2=E(K,P_2\oplus C_{1})=C'_1=E(K,P'_1\oplus C'_0)$$
it's extremely likely that $P'_1 = P_2\oplus C_1\oplus C'_0$.



# Extended Exercises
## Chapter 3
5; Suppose you have a processor that can perform a single $DES$ encryption or decryption operation in $2^{-26}$  seconds. Suppose you also have a large number of plaintext-ciphertext pairs for $DES$ under a single unknown key. How many hours would it take, on average, to find that $DES$ key, using an exhaustive search approach and a single processor? How many hours would it take, with a collection of $2^{14}$ processors?
- note: "a large number" is weird, they should have just given a number. But w/e, *ahem* I mean, I assigned this for an opportunity to practice symbolic reasoning.
- Let:
    -  the number of owned plaintext-ciphertext pairs be $n$
    -  the time per (en|de)cryption be $t$ seconds
    -  the total number of possible DES keys be $N$
    -  the number of parallel processors be $d$
    -  the number of attempts to be $a$
- For any independent attempt[^1], the probability of key-discovery can be expressed: $P[\text{key discovery}]=n/N$. We make the assumption attempts approximately independent, and solve $na/N=.5$:
$$0.5 = na/N = \frac{na}{2^{56}}$$
$$a=2^{55}/n$$
and the time to obtain a collision can be expressed:
$$T := \frac{at}{d} = \frac{2^{55}2^{-26}}{n*2^{14}}$$
$$=2^{15}/n \text{ seconds}$$

9; Using an existing cryptography library, encrypt the following plaintext (in hex)

```hex
	29 6C 93 FD F4 99 AA EB 41 94 BA BC 2E 63 56 1D
```

with the following 256-bit key (also in hex)

```hex
	80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
	00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```
using *AES*.
- rust: https://github.com/thor314/uncloak-hw/tree/main/hw2
- bash:
```bash
$ echo "296C93FDF499AAEB4194BABC2E63561D" | xxd -r -p | openssl enc -aes256 -e -K "8000000000000000000000000000000000000000000000000000000000000001" -iv 0 -nopad | xxd
```
10; Write a program that experimentally demonstrates the complementation property for *DES*. This program should take as input a key $K$ and a plaintext $P$ and demonstrate that the $DES$ complementation property holds for this key and plaintext. You may use an existing cryptography library for this exercise.
- https://github.com/thor314/uncloak-hw/tree/main/hw2

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
- bash:
```bash
echo "626C6F636B2063697068657273202020686173682066756E6374696F6E732078626C6F636B2063697068657273202020" | xxd -r -p | openssl enc -aes-256-ecb -e -K "8000000000000000000000000000000000000000000000000000000000000001" -nopad | xxd
```
- Implement a pair of functions: A [PKCS 7](https://en.wikipedia.org/wiki/PKCS_7) message padding function, and a padding validation function that takes a message and validates whether it has a correct padding.
    - https://github.com/thor314/uncloak-hw/tree/main/hw2


----

[^1]: per question 3.6; these attempts aren't precisely independent, but we can model them as such for simplicity, though in reality the attacker would be slightly more powerful. The actual probability for attempt $m$ to obtain the key would be $P[E_m] = \frac{n}{N-m}$, and the probability that the key is discovered on or before attempt $m$ would be:
$$P[\bigcup_i E_i=1]= P[E_1=1 \lor (E_1=0 \land \bigcup_i=E_i=1)] |$$
We can recursively repeat the above move, and separate the probabilities by mutual independence:
$$=P[E_1=1]+ P[E_1=0 \land E_2=1]+...$$
$$= \frac{n}{N} + \frac{N-n}{N}\frac{n}{N-1}+...+(\prod_{i=0}^{m-1} \frac{N-i-n}{N-i})\frac n {N-m}$$
This expression can be simplified further, but is left as an exercise for the reader.
