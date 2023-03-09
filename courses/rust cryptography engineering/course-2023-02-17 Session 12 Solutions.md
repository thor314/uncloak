---
creation-date: 2023-02-14
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-17 Session 12 Solutions
- back:: [[course-2023-02-17 Session 12 Notes]]

## Exercises
- What kind of security would you expect an encryption scheme to obtain?
First, any secure encryption scheme would at least need to target computational security: there must not exist a polynomial time algorithm breaking the encryption scheme. Now, if an adversary could distinguish the ciphertext of an algorithm from randomness with greater than negligible probability, they would be able to obtain at least some information about the plaintext. Encryption algorithms often have trivial distinguishers--recall even permutations and the DES complementation property from Cryptography Engineering Chapter 3. We may restrict our definition of statistical security to non-generic methods, discounting even-permutations; but the DES complementation property is plainly non-generic. So at best, DES could only obtain computational security (despite exceptionally weak security parameters), though modern encryption schemes obtain statistical security in practice.

- Win the [Kelly Criterion Game](https://explore.paulbutler.org/bet/). Then read the article and re-derive the Kelly criterion equation with probability of winning $p$, bet size $l$. Now suppose your bet pays out with some ratio $r$; e.g. set $r=1$ for the prior game, but if $r=2$, a bet size of $l$ pays back out $(r+1)l=3l$ for victory, and nothing for a loss. Adjust your derivation to account for $r$.
We want to optimize for bet size. It usually helps to first define a value function. Let our initial value be $V_0$, our probability of winning be $p$, and our proportional bet size be $l$. We have:
$$V = \begin{cases}
V_0(1+l) & \text{win} \\
V_0(1-l) & \text{lose}
\end{cases}
$$
For simplicity, we set $V_0=1$. Now we may define an expected value. We expect to win with probability $p$, so we obtain:
$$E[V]=(1+l)^p(1-l)^{1-p}$$
We would like to optimize the expected value function for our bet size $l$. We have a convenient trick: since the slope of $\log(f)$ is identical to the slope of $f$ for any function $f$, we may compute $\frac d{dl} \log E[V], instead of $\frac d{dl} E[V]$. $\log E[V]= p\log(1+l)+(1-p)\log(1-l)$, so we have:
$$\begin{align}
\frac{d}{dl}E[V] &= \frac p{1+l}- \frac{1-p}{1-l} = 0\\
&p(1-l)-(1-p)(1+l) = 0\\
&l=2p-1
 \end{align}$$
We now adjust for $r$. The value equation becomes:
$$V = \begin{cases}
V_0(1+rl) & \text{win} \\
V_0(1-l) & \text{lose}
\end{cases}
$$
And the logarithmic expected value becomes:
$$\log E[V]= p\log(1+rl)+(1-p)\log(1-l)$$
Finally:
$$\begin{align}
\frac{d}{dl}E[V] &= \frac {pr}{1+rl}- \frac{1-p}{1-l} = 0\\
&pr(1-l)-(1-p)(1+rl) = 0\\
&pr-prl-(1 + rl - p - prl) = 0\\
&pr - 1 - rl + p = 0\\
&l = \frac{pr+p-1}{r}\\
 \end{align}$$
 The reader may verify that, by setting $r=1$, the new optimized formula for $l$ remains $2p-1$ as before.


- Spend 30 minutes reading the RustCrypto [Schnorr](https://github.com/RustCrypto/elliptic-curves/blob/master/k256/src/schnorr.rs) implementation over k256. You may see words you do not recognize, like `affine` and `projective` points. Post a comment in the discord about any new words you learned to discuss with the group.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]