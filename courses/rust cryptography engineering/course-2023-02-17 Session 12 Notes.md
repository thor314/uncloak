---
creation-date: 2023-02-13
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-17 Session 12 Notes
- prev:: [[course-2023-02-10 Session 11 Notes]]
- solns:: [[course-2023-02-17 Session 12 Solutions]]
- next:: [[course-2023-02-24 Session 13 Notes]]

The reading for this week is [An Introduction to Mathematical Cryptography](https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5) Chapter 4.3 on Probability Theory, and 7.1-3 on digital signatures. Chapter 4 gives a survey of a wide range of cryptography-related concepts, and is recommended to the interested reader. The main two signature techniques in practice are those of Schnorr (aka EdDSA, used for instance), and ECDSA, with the industry largely moving away from [RSA](https://blog.trailofbits.com/2019/07/08/fuck-rsa/). We will not discuss BLS signatures in this lecture, but we may return to them in week 15.

**Next week's session will begin 75 minutes early at 8:30 PST, 16:30 UTC. (2032-02-24)**. We will discuss sections 5.1-5 and 5.8 on elliptic curves.

## Discussion
Before we discuss the material from this section, a prelude on several types of probabilistic security may be of service.

Most cryptographic schemes are not *perfectly secure*, but either *statistically* secure: an adversary cannot distinguish hidden information from randomness with a polynomial time algorithm; or the slightly weaker computationally secure: an adversary cannot obtain the hidden information in polynomial time. Some examples:
- [Shamir's Secret Sharing](https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing) is perfectly secure. In SSS, a private key $x$ is split into $n$ shares, of which any $t\le n$ may be used to re-construct $x$. It can be proven that the adversary with fewer than $t$ shares obtains 0 bits of information about secret $x$. It is *unusual* that a cryptographic scheme with perfect security is also an efficient system, but SSS is both. We will revisit this in the special topic week on multi-party computation.
- [One time pads](https://en.wikipedia.org/wiki/One_time_pad) are a perfectly secure symmetric encryption scheme, and are terribly inefficient. An adversary who obtains a ciphertext produced by a one-time pad obtains 0 bits of information about the plaintext or key. However, efficient systems expect to re-use keys, where the re-use of a one-time pad is terribly insecure.
- [Pedersen Vector Commitments](https://en.wikipedia.org/wiki/Commitment_scheme) allow party A to commit to some vector $v$, *computationally* binding A to the vector. That is, A could not obtain any vector $v'$ satisfying $\mathsf{COM}(v)=\mathsf{COM}(v')$ in polynomial time, so binding obtains computational security--to the careful reader, this should smell like collision resistance. Further, the hiding of $v$ is statistically secure: if $c=\sf{COM}(v)$, then an adversary would be unable to distinguish $c$ from randomness--what other cryptographic scheme looks to obtain pre-image resistance? Finally, while party A could trivially reveal the vector $v$ for others verify the commitment, Pedersen Commitments allow A to instead construct a (zero knowledge) proof that A has knowledge of $v$, *without revealing $v$*. Proofs may be {perfect, statistically, computationally} secure, but are typically computationally secure.
- Commitment schemes can be seen as a special kind of hash. Hashes do reveal information about the plaintext, namely, what the plaintext hashes to, though this information is typically less than 1 bit of information. Secure hashes therefore aim to have at least *computational security* in collision-resistance: it should be computationally infeasible to compute a collision; and potentially *statistical security* in pre-image resistance: that an adversary cannot distinguish the output of a hash from randomness.

For more on statistical versus computational security, consult [Boaz Barak's Notes](https://www.cs.princeton.edu/courses/archive/fall07/cos433/lec3.pdf).

Section 4.3 is a crash course on probability theory. The authors compress a lot of probability theory into a relatively small space; even the careful reader may need further examples (which we will give in lecture) to gain familiarity, but all readers will hopefully benefit from exposure.

Signatures are, on an intuitive level, the "inverse" of encryption. Instead of encrypting with a public key, and decrypting with a private key, one signs with a private key, which others may verify with a public key. The book covers RSA and DSA signatures, as well as a lattice-based technique (the authors are lattice-specialists, though lattice-based techniques remain unlikely to become relevant for decades). Concurrent to the book's publishing in 2008, the [patent on Schnorr/EdDSA signatures](https://en.wikipedia.org/wiki/Schnorr_signature) expired; Schnorr based signature schemes are more efficient than DSA based signatures and have grown in popularity. Schnorr signatures are flexible, and have been adapted for other contexts like [adaptor](https://bitcoinops.org/en/topics/adaptor-signatures/) and [threshold](https://docs.chainflip.io/concepts/components/frost-signature-scheme) signatures. Note that the only difference between Schnorr and EdDSA are the group over which signatures are constructed. The same holds for the DSA and ECDSA algorithm. [^1]

### ECDSA signing[^2]
With public parameters primes $q$ and $p=Nq+1$ (some safe prime), generator $g$ for the group $\mathbb Z_p$, some hash function $H$, and private key $x$:
- Signer chooses ephemeral nonce $k\gets \{2..=q-2\}$
- Signer computes:
$$\begin{align}
r&= (g^k\mod p)&&\mod q \qquad  \text{r is a blind for the secret key}\\
s&= k^{-1}(H(m)+xr)&&\mod q  \qquad   \text{(r,s) is the signature}
 \end{align}$$
The $k^{-1}$ step makes ECDSA inflexible to many desirable adjustments in the algorithm.

### ECDSA verification:
The verifier computes, with knowledge of public key $X=g^x$, message $m$, and signature $(r,s)$:
$$\begin{align}
w &=s^{-1}= k(H(m)+xr)^{-1}&\mod q\\
u_1 &= w\cdot H(m) &\mod q\\
u_2 &= r\cdot w  & \mod q \\
r (=g^k)&=?\ (g^{u_1}X^{u_2} \mod p)\mod q= (g^{wH(m)}g^{wrx}\mod p) &\mod q\\
&= g^{w(H(m)+rx)} \mod p & \mod q\\
&= g^{k} \mod p & \mod q


 \end{align}$$

By contrast, the Schnorr scheme is simpler and more efficient.

### Schnorr signing
With public parameters prime $q$, generator $g$, hash function $H$, and private key $x$:
- Signer chooses ephemeral nonce $k\gets \{2..=q-2\}$
- Signer computes:
$$\begin{align}
r&=g^k&&\mod q\\
e&=H(r||M) &&\mod q \quad \text{|| denotes bit-string concatenation}\\
s&=k-xe && \mod q \quad \text{(e,s) is the signature}
 \end{align}$$ Note that $s$ is linear in $x$. This is what makes Schnorr flexible to algebraic adjustments.

### Schnorr verification
With knowledge of public key $X$ and signature $(e,s)$, the verifier computes:
$$\begin{align}
e (=H(g^k||M)) &=?\ H(g^sX^e||M) \\
&= H(g^{s+xe}||M)\\
&= H(g^{k}||M)\\


 \end{align}$$

## Exercises
- What kind of security would you expect an encryption scheme to obtain?
- Win the [Kelly Criterion Game](https://explore.paulbutler.org/bet/). Then read the article and re-derive the Kelly criterion equation with probability of winning $p$, bet size $l$. Now suppose your bet pays out with some ratio $r$; e.g. set $r=1$ for the prior game, but if $r=2$, a bet size of $l$ pays back out $(r+1)l=3l$ for victory, and nothing for a loss. Adjust your derivation to account for $r$.
- Spend 30 minutes reading the RustCrypto [Schnorr](https://github.com/RustCrypto/elliptic-curves/blob/master/k256/src/schnorr.rs) implementation over k256. You may see words you do not recognize, like `affine` and `projective` points. Post a comment in the discord about any new words you learned to discuss with the group.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]

[^1]:  While multiplicative notation is typically used over finite fields (and is used here), operations over elliptic curve groups are often expressed in additive notation.
[^2]: checks are elided for simplicity, obviously don't use this as a spec