---
creation-date: 2023-01-17
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-13 Session 7 Solutions
- back:: [[course-2023-01-13 Session 7 Notes]]

### Ch 9: Randomness
- What is **entropy**? Why does a combination (eg. by XOR, or by hash-concatenation as on p145, Reseed) of two or more *independent* input-streams $\{S_1..S_n\}$ of entropy has at least $H(X)\ge \max\{S_i\}$ entropy; that is, why a combination of entropy streams is always at least as entropic as the most entropic stream.
    - Note the word *independent*: an adaptive adversary controlling stream $S_i$ may choose a function of the other streams to control the randomness.

Entropy is the measure of randomness in a system, measured as a random variable. For random variable $X$, the entropy is expressed[^2] :
$$H(X)=\sum\limits_{x\in X} p(x)\log p(x)=\mathbb E[-\log p(X)]$$
Conceptually, any combination of two independent streams of entropy $X=f(X_1,X_2)$ where bit $i$ of $X$ depends on one or more bits in $X_1,X_2$ will be at least as random as bit $i$ in $X_1$ or $X_2$. If, however, and adversary is allowed to choose $X_2$ as dependent on $X_1$, they may instead bias the results; for instance, if $f$ is the XOR function, and the adversary chooses the output of $X_2$ to be exactly the output of $X_1$ (note that this means $X_2$ is not even a random variable), then $f(x_1,x_1)=0$.

- Give a one-sentence explanation of the difference between a **PRNG** and a **CSPRNG** (non-correlation versus unpredictability)
    - A Cryptographically Secure PRNG is a PRNG whose outputs are not only **uncorrelated**, but also **unpredictable** to any adversary not possessing the RNG seed value.
- Why can a CSPRNG can be constructed from a block cipher?
    - A block cipher, seeded with some random value, produces an arbitrarily long pseudo-random string. If the block cipher were not pseudo-random, the adversary would gain information about the plaintext by analyzing patterns in the ciphertext.

### Ch 10: Primes
- Compute $397^{-1} \mod 2357$ by hand. Page 18 of https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5 describes a convenient tabular method for calculating the EEA by hand.
$$\begin{align}
&&\text{let } a&=2357, b=397\\
372&=2357-(5)397 &  372&=a-5b\\
25 &= 397 - (1)372 & 25&=-a+6b\\
22 &= 372 -(14)25 & 22&=15a-89b\\
3&=25-(1)22 & 3&=-16a+95b\\
1&=22-(3)3 & 1&=127a-754b\\
   \end{align}$$

   Since $127(a)\equiv 0\mod a$, we obtain $(a-754)b\equiv 1\mod a$, so $397^{-1}=1603$.

- Recursively implement the Extended Euclidean Algorithm. Use the above exercise as a test case.
    - https://github.com/thor314/uncloak-hw/blob/main/hw7/src/lib.rs
- Implement the Miller-Rabin primality check.[^1]
    - https://github.com/thor314/uncloak-hw/blob/main/hw7/src/lib.rs

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]

[^2]: [Entropy (information theory) - Wikipedia](https://en.wikipedia.org/wiki/Entropy_(information_theory))