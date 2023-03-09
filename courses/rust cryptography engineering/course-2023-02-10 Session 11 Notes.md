---
creation-date: 2023-02-09
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-10 Session 11 Notes
- prev:: [[course-2023-02-03 Session 10 Notes]]
- solns:: [[course-2023-02-10 Session 11 Solutions]]
- next:: [[course-2023-02-17 Session 12 Notes]]

The reading for this week is [An Introduction to Mathematical Cryptography](https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5) Chapter 2.1-2.4, 2.6, 2.7 A mathematical review of Discrete Log. This chapter provides background on the ubiquitous discrete log problem.

What we are covering: Discrete log and the Diffie Helman problem, The ElGamal cryptosystem, and briefly, Shank's Collision algorithm for Discrete Log.

What we will not cover, but is recommended for the industrious reader: Sections 2.5 and 2.10 on basic abstract algebra are fundamental for understanding the objects research operates over. You already have seen the Chinese Remainder Theorem, section 2.8 gives further background necessary to understand the Polig-Hellman algorithm. PH in combination with the Index Calculus methods (sections 3.6-3.8) are why we use elliptic curves instead of Finite Fields, be warned, but they are not simple, and the book demands a higher level of mathematical attention, if you would like to understand these topics.
Finally, we will be skipping all of chapter 3 on RSA and primality. The first 5 sections of Chapter 3 are very accessible, the latter half is more challenging. Chapter 4 is a survey of a range of fields employed by cryptography; we will only cover probability (next week), but all of chapter 4 is worth reading.

## Exercises
- Compute with pen and paper, the Elgamal algorithm for Alice sending Bob a message. Use parameters: p=19, g=2, a=3, b=5, m=12. You may choose any k. If an adversary obtained the computed ciphertext $(c_1,c_2)$, and obtained access to $k$, how could they decrypt the ciphertext?
- Compute with Shank's algorithm, on pen and paper, the discrete log of $2^x=33 \mod 83$. Note that $2$ is a generator, which you may check by verifying $2^{41}=82 \mod 83$ (check that you understand why this works).
- Optional: Implement one or both of Elgamal encryption and/or Shank's algorithm.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]