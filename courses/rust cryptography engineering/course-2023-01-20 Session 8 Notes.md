---
creation-date: 2023-01-18
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-20 Session 8 Notes
- prev:: [[course-2023-01-13 Session 7 Notes]]
- solns:: [[course-2023-01-20 Sesson 8 Solutions]]
- next:: [[course-2023-01-27 Session 9 Notes]]

This week's focus is Diffie Hellman key exchange and RSA, chapters 12 and 13. A brief announcement: This is the second-last session that will cover the book Cryptography Engineering. Next week's reading is posted in [[course-2023-01-27 Session 9 Notes]]. For sessions 10-13, we will be switching gears and covering several sections from [An introduction to mathematical cryptography](https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5) (henceforth, ItMC).  The course will finish with a set of special topic lectures on Zero Knowledge Proofs, Threshold Schemes, and if there is time, Fully Homomorphic Encryption.

Bonus reading for this week: [Don't use RSA.](https://github.com/trailofbits/publications/blob/master/papers/rsagtfo.pdf)

## Discussion
### An aside on groups
Chapter 12 presents Diffie Hellman (DH), which relies on the difficulty of Discrete Log, that given $g,a,p$, it is difficult to obtain $x$ such that (in multiplicative notation):
$$g^x \equiv a\mod p$$
Difficult, in this case, means that no algorithm obtains $x$ in sub-polynomial time.

Multiplicative notation is commonly used when the field $\mathbb F_p$ is a prime-order field. That is, any set $S=\{1,2,...,p-1\}$, where $p$ is prime, defines a multiplicative group. The set $S+\{0\}$ defines a group under addition.

A quick backgrounds on groups: Groups are algebraic structures representing a set of objects with some operation on pairs of elements in the set. They are representative of each kind of symmetry in mathematical objects. Groups are typically written $(S,*)$, for some set of elements $S$ and some operation $*$.

A group is an algebraic structure composed of:
- A nonempty set of elements
- A binary operation (for example, $+$, $*$), defined over elements in the group $G$, that satisfies several axioms:
    - **associativity**: $\forall a,b,c\in G, (a*b)*c=a*(b*c)$
    - **identity**: One element, $e\in G$ satisfies the following property: $\forall a\in G, a*e = e*a = a$. In additive groups, $e$ is typically $0$, in multiplicative groups, $e$ is often $1$. Note that this axiom guarantees that the set is non-empty. The identity is often written $1$ in multiplicative groups and $0$ in additive groups. Multiplicative and additive are loosely defined adjectives in this case, and may describe multiplication-like and addition-like binary operations.
    - **inverses**: For each $a\in G,$ there is some inverse element, $b\in G$ satisfying $a*b=e$. An inverse of $a$ is typically written $a^{-1}$, regardless of the binary operation used.
    - **closure**: the operation applied to any two elements in $G$ produces only other elements in $G$: $\forall a,b\in G, a*b\in G$.
- A group is said to be **abelian** (commutative) if it obeys the additional rule that $a*b=b*a,\ \forall a,b\in G$.

An element $g\in G$ such that the powers of $g$ entirely generate the set $G$ is called a **generator**. For example, $3$ is a generator of $\mathbb Z_7$.

Most cryptographic operations are defined over some group. [Elliptic curve](https://curves.xargs.org/) (also an [excellent introduction](https://research.nccgroup.com/2021/11/18/an-illustrated-guide-to-elliptic-curve-cryptography-validation/)) groups are commonly used in preference over prime fields, due to the existence of linear algebraic attacks on prime fields, known as index calculus methods (see ItMC 3.8, though the section is mathematically involved, and may not be easy to follow, out of context). The interested reader is invited to peruse sections 2.5 and 2.10 from [ItMC](https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5) for a background on groups, rings, and fields.

Operations defined over elliptic curve groups often use a different notation, the additive group notation. Where before, $g,a$ were any elements of the group $\mathbb Z_p$ , the additive notation typically uses capital letters to express group elements. The following express the discrete log problem in multiplicative and additive notation:
$$
\begin{align}
&g^x \equiv a\mod p &\text{multiplicative notation}\\
&xG = A &\text{additive notation}
\end{align}
$$

### Chapter 11: Diffie Hellman
Chapter 11 presents an introduction to the DH protocol in the context of a multiplicative group. The chapter is somewhat dense, especially for the mathematically rusty, refer to 11.8 for the larger picture of the chapter.

Otherwise, the reading for this section is straight forward; groups, DH, Man in the Middle attacks, and safe primes are fundamental objects in asymmetric cryptography. The explanation of using safe subgroups in section 11.6 is a bit evasive. The main take-away is that subgroups are used for efficiency reasons, as efficient attacks exist on prime-field cryptography, requiring $p$ to be thousands of bits, but using a *large-enough* (256-bit) prime-order subgroup of $\mathbb Z_p$ reduces operation overhead. This point is rendered somewhat irrelevant by elliptic curve cryptography.


### Chapter 12: RSA
Chapter 12 introduces several results, before presenting RSA encryption.

The Chinese Remainder Theorem (CRT), is an algorithm to obtain $x$, given $a,b,p,q$ such that:
$$\begin{align}
x \equiv a \mod p\\
x \equiv b \mod q
\end{align}$$
The exercises this week are especially recommended to gain an understanding of the CRT.

The authors introduce the totient function, but give reasonably sparse background. The following aims to supplement that:
The Euler $\varphi$-function is defined: for $n\in \mathbb Z^+$, $\varphi(n)$ is the number of positive integers $a\le n$ relatively prime to $n$: that $\gcd(a,n)=1$. For example:
- $6$: only $1,5$ are coprime to $6$, so $\varphi(6)=2$
- $7$: $7$ is prime, so $1..6$ are each coprime, therefore $\varphi(7)=6$. This is generalizable: for any prime $p$, $\varphi(p)=p-1$.
- 8: $8=2^3$, and each of $2,4,6,8$ divide 8, thus $\varphi(8)=4$. This is also generalizable: for prime powers, $p^e$, $\varphi(p^e)= (p^{e-1})(p-1)$. For example, $27=3^3$, and we would expect 27 to have $27/3$ divisors. Thus $\varphi(27)= 3^3-3^2=3^2(3-1)=18$ .

The $\varphi$ function is **multiplicative** in the sense that for coprime $a,b: \gcd(a,b)=1$, $\varphi(ab)=\varphi(a)\varphi(b)$. With this fact and the Fundamental Theorem of Arithmetic, we may derive the closed formula for $\varphi$.  If $n=\prod_i p_i^{e_i}$:
$$\large{
\begin{align}
\varphi(n) &= \varphi(\prod_i p_i^{e_i}) \\
&= \prod_i \varphi(p_i^{e_i}) \quad \text{by $\varphi$ multiplicative} \\
&= \prod_i p_i^{e_i -1}(p_i -1) \quad\text{by the third example above}
\end{align}
}$$
$(e*d) = 1 \mod \varphi(pq)$
$(e*d) = 1 \mod \varphi(n)$
Encrypt: $(a^e) = a \mod pq$
decrypt: $(a^e)^d = a \mod pq$
Sign: $(a^d) = a \mod pq$
verify: $(a^d)^e = a \mod pq$
d is private
e is public

## Exercises
- Suppose that $x\mod 30=2$. What is obtained about $x\mod 2$, $x\mod 3$, and $x\mod 5$? What about $x\mod 7$?
- You're Eve, intercepting a message from Alice to Bob. Alice asked Bob to choose a prime larger than 30 to construct a prime field. You choose $p=31, g=2$. How many unique choices of exponent $x$ in $g^x\equiv a\mod p$ does Alice now have? A unique choice is any uniquely obtainable values for $a$. For instance, $2^{17}\equiv 4$ and $2^{32}=4$ are not unique.
- Bob would have chosen $p=83, g=2$. How many unique choices for $x$ does Alice have now? What if Bob chose $p=83,g=3$?
- 576001 is the prime with factorization $p-1=2^9*3^2*5^3$ . Find a generator $g\ne 1$ with order $|g|< 10$.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]