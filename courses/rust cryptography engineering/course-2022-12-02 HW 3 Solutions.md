---
creation-date: 2022-12-06
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-02 HW 3 Solutions
- back:: [[course-2022-12-02 Session 3 Notes]]

## ch5 exercises
See [GitHub - thor314/uncloak-hw](https://github.com/thor314/uncloak-hw) for solutions to chapter 5.
- Exercise 5.3 Consider SHA-512-$n$, a hash function that first runs SHA-512 and then outputs only the first $n$ bits of the result. Write a program that uses a birthday attack to find and output a collision on SHA-512-$n$, where $n$ is a multiple of 8 between 8 and 48. Your program may use an existing cryptography library. Time how long your program takes when $n$ is 16, averaged over five runs for each $n$. How long would you expect your program to take for SHA-512-256? For SHA-512?
- Exercise 5.4 Let SHA-512-n be as in the previous exercise. Write a program that finds a message M that hashes to the following value under SHA-512-16 (in hex):`3D 4B`.
    - How many tries would you expect the algorithm to need?
    - Running the algorithm 5 times, How many tries did it take on average?
- With command line tools or Criterion, benchmark the [blake3 hash](https://docs.rs/blake3/latest/blake3/) (default is 256 bit output), and compare it to benches of [SHA3-256](https://docs.rs/sha3/latest/sha3/) and [SHA-256](https://docs.rs/sha2/latest/sha2/) (when written without a number, SHA is assumed to be SHA2).

## ch 6 exercises
- Exercise 6.3 Suppose a and b are both one block long, and suppose the sender MACs a, b, and $a || b$ with CBC-MAC. An attacker who intercepts the MAC tags for these messages can now forge the MAC for the message $m=b || (M(b) ⊕ M(a) ⊕ b)$, which the sender never sent. The forged tag for this message is equal to $M(a || b)$, the tag for $a || b$. Justify mathematically why this is true.

Let:
$$ t_{a} = E_K(a);\quad t_{b} = E_K(b);\quad t_{a||b}=E_K(b\oplus t_{a)} $$
Then:
$$
\begin{align}
MAC(m)=& MAC(b || (M(b) \oplus M(a) \oplus b))\\
=& E_K( t_b\oplus t_{a}\oplus b \oplus t_b)\\
=& E_K( t_{a}\oplus b ) \\
=& t_{a||b}\\
\end{align}
$$
- Exercise 6.4 Suppose message $a$ is one block long. Suppose that an attacker has received the MAC $t$ for a using CBC-MAC under some random key unknown to the attacker. Explain how to forge the MAC for a two-block message of your choice. What is the two-block message that you chose? What is the tag that you chose? Why is your chosen tag a valid tag for your two-block message?
This problem outlines a length extension attack. As specified in CBC-MAC:
$$
\begin{align}
H_{0}:=& IV=0 \\
t = H_{1}:=& E_K(P_{i}\oplus H_{i-1})=E_{K}(a\oplus 0)=E_K(a) \\
\end{align}
$$
If the attacker can compute $E_k$, the attacker may choose any second block $b$, and compute MAC $t'$:
$$
\begin{align}
t' = H_{2}:=&E_{K}(b\oplus t) \\
\end{align}
$$
The attacker does not have the key. But, if the attacker has any pair $(x,y)$ satisfying: $E_K(x)=y$, then the attacker may choose $b$ such that $b\oplus t =x$ to obtain $E_K(b\oplus t) = E_K(x)=y$, where $y$ is the obtained tag.

Does the attacker have any such pair? Yes! The attacker has $(a,t)$. So the attacker chooses $b=a\oplus t$ to obtain $t'=t$, for the two-block message $(a,a\oplus t)$.

- Exercise 6.5 Using an existing cryptography library, compute the MAC of the message:
```hex
4D 41 43 73 20 61 72 65 20 76 65 72 79 20 75 73 65 66 75 6C 20 69 6E 20 63 72 79 70 74 6F 67 72 61 70 68 79 21 20 20 20 20 20 20 20 20 20 20 20
```

using CBC-MAC with AES and the 256-bit key:
```hex
80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01
```

- solution:
```sh
~ ❯ echo $msg | openssl dgst -hmac $key -hex
SHA256(stdin)= f2d6d1c954bcd62df5a3c6611cb56b21d3f96f5681abd5b13f0b398499f9894c
~ ❯ echo $key
8000000000000000000000000000000000000000000000000000000000000001
~ ❯ echo $msg
4D4143732061726520766572792075736566756C20696E2063727970746F677261706879212020202020202020202020
```

- For message authentication, when would you use TupleHash? ParallelHash? KMAC?
    - These three algorithms are specified in NIST 800-185, published after the SHA3 standards competition. [https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-185.pdf](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-185.pdf). All three are designed for use with SHA3.
    - TupleHash is takes a tuple of messages and produces a message authentication code. It's useful when you want to create a MAC on multiple messages simultaneously, for instance, on a key-value pairing.
    - ParallelHash is a multithreaded algorithm for computing the hash of a long message, instead of hashing each bite of the long message sequentially.
    - KMAC is designed for use with SHA3 (K is for Keccak), and avoids the need, as in HMAC, to hash messages twice; thus, KMAC is faster than HMAC.