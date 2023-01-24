---
creation-date: 2023-01-09
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-13 Session 7 Notes
- prev:: [[course-2023-01-06 Session 6 Notes]]
- solns:: [[course-2023-01-13 Session 7 Solutions]]
- next:: [[course-2023-01-20 Session 8 Notes]]

This week's focus is a discussion of Randomness and Primes, centered around chapters 9 and 10 in Cryptography Engineering.

## Discussion
### Chapter 9: Randomness
Note that 9.5-9.7 are information-light, and can be skimmed. How entropy is generated and used to seed a block-cipher based CSPRNG should be the central focus of this chapter. Eg. the Linux kernel uses a CSPRNG based on the ChaCha20 block-cipher.

### Chapter 10: Primes
The Extended Euclidean Algorithm and the Miller Rabin Primality test are of central focus in this chapter.
- 10.1 introduces some basic facts about the integers, and the Fundamental Theorem of Arithmetic (integers have prime factorization).
- 10.2 gives the *Sieve of Eratosthenes*
- 10.3 introduces modular arithmetic, and the terminology of groups and finite fields. Optionally, see [cryptotext_1-intro-to-math-cryptography.pdf - Google Drive](https://drive.google.com/file/d/1etl96pWvdIDfFx29eIubxvCSsbYkl-Jz/view?usp=sharing), sections 2.5 and 2.10 for a more extensive introduction to groups and fields, and their basic facts, with respect to cryptography.
- 10.3.4, 10.3.5 - The Euclidean Algorithm and Extended Euclidean Algorithm. See [this blog post](https://explained-from-first-principles.com/number-theory/#miller-rabin-primality-test) for additional resources on Miller Rabin, which probabilistically determines whether a number is prime, and is not susceptible to [Carmichael Numbers](https://en.wikipedia.org/wiki/Carmichael_number).

### Side note: Piping 1GiB of randomness to `/dev/null`
On Linux, you may use the `/dev/urandom` resource to obtain randomness from the command line:
```sh
dd if=/dev/urandom of=/dev/null bs=1M count=1024 iflag=fullblock
```

A note on `urandom` vs `random` in the Linux kernel: Since 2016, Linux 4.8, the Linux default CSPRNG has been ChaCha20-based. Historically, `/dev/random` blocked if entropy "ran out" (entropy does not run out, a system kernel may always generate further entropy from system [execution jitter](https://github.com/torvalds/linux/commit/50ee7529ec4500c88f8664560770a7a1b65db72b)). Since 2019, Linux 5.4, the kernel does exactly that, and no longer blocks. `/dev/urandom` and `/dev/random` are now essentially equivalent, though many developers still use `/dev/urandom`, which never blocked in the first place.

For more on the Linux PRNG, see [this paper](https://eprint.iacr.org/2012/251.pdf).

## Next week's reading
Read Chapters 11 and 12 on Diffie Helman and RSA.

## Exercises
### Ch 9: Randomness
- What is **entropy**? Why does a combination (eg. by XOR, or by hash-concatenation as on p145, Reseed) of two or more *independent* input-streams $\{S_1..S_n\}$ of entropy has at least $H(X)\ge \max\{S_i\}$ entropy; that is, why a combination of entropy streams is always at least as entropic as the most entropic stream.
    - Note the word *independent*: an adaptive adversary controlling stream $S_i$ may choose a function of the other streams to control the randomness.
- Give a one-sentence explanation of the difference between a **PRNG** and a **CSPRNG** (non-correlation versus unpredictability)
- Why can a CSPRNG can be constructed from a block cipher?
### Ch 10: Primes
- Compute $397^{-1} \mod 2357$ by hand. Page 18 of https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5 describes a convenient tabular method for calculating the EEA by hand.
- Recursively implement the Extended Euclidean Algorithm. Use the above exercise as a test case.
    - https://github.com/thor314/uncloak-hw/blob/main/hw7/src/lib.rs
- Implement the Miller-Rabin primality check.[^1]
    - https://github.com/thor314/uncloak-hw/blob/main/hw7/src/lib.rs

### Preview to Ch 11: Diffie Helman
Using [common.rs.html -- source](https://docs.rs/pumpkin/2.0.1/src/pumpkin/common.rs.html#106), obtain a safe prime of $n>1000$ bits.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]

## Extra
[^1]: You may refer to [this implementation of Miller Rabin](https://docs.rs/pumpkin/2.0.1/src/pumpkin/common.rs.html#213).