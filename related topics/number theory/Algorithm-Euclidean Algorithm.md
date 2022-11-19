---
creation-date: 2022-11-04
publish: true
audience: all
completion: .1
tags: type/object/math/algorithm, related/number-theory
date-origin: 
date-broken: 
---
*last-modified (only renders within Obsidian with Dataview installed): `$= dv.current().file.mtime`*
# Algorithm-Euclidean Algorithm
## Intro
The **Euclidean Algorithm** obtains the [[Property-Greatest Common Divisor|greatest common divisor]] of a pair of integers, $a,b$. 

## Definition
For $a,b\in \mathbb Z^+$, arbitrarily letting $a\ge b$, we may compute $\gcd(a,b)$:
1. Let $r_0=a, r_1=b$ . Let $i=1$.
2. Let $q_i$ be the largest integer such that: $r_{i-1}=r_i\cdot q_i+r_{i+1}\quad \text{with} \quad 0\le r_{i+1}<r_i$
3. If $r_{i+1}=0$, then $r_i=\gcd(a,b)$, terminate. Otherwise, increment $i$ and repeat step 2.

The algorithm runs in $2\log_{2}b+1$ steps.
## Reasoning
Let $a,b$ be positive integers: $a,b\in \mathbb Z^+$. Then $a/b$ has **quotient** $q_0$ and **remainder** $r_0$:
$$a=b\cdot q_0+r_0\quad \text{with } 0\le r_0<b$$
If $b\mid a$, then $r_0=0$, but we can say more than that. By [[Proposition-Natural Properties of Divisibility]], if $d$ is any common divisor of $a,b$, then $d$ must also divide $r_0$: $d\mid a \land d\mid b\implies d\mid r_0$.  That is, the common divisors of $(a,b)$ and $(b,r_0)$ are the same. We may repeat the above step:
$$b=r_0\cdot q_1+r_1\quad \text{with } 0\le r_1<r_0$$
It continues to be true that, for non-zero $r_0,r_1$, the common divisors of $(a,b),(b,r_0),\text{ and } (r_0,r_1)$ are the same. This is equivalent to the statement:
$$\gcd(a,b)=\gcd(b,r_0)=\gcd(r_0,r_1)$$
Continuing this process, the remainders decrease in size until finally becoming zero, giving $\gcd(a,b)=\gcd(r_n,0)=r_n$.

## Relation to Similar Algorithms

## Attacks

## Runtime proof
todo

---
## Related Pages
*The related pages section is for linking this page other the rest of the graph, press F11 for details. If applicable, replace the following dummy links.*
- primary-topic:: [[Topic-Number Theory]]
- [[Algorithm-Extended Euclidean Algorithm]]

## External Resources
*The sources section is for recommending resources on other sites*.
- Wikipedia:: [Euclidean Algorithm](https://en.wikipedia.org/wiki/Euclidean_algorithm)

## References
*This section is for citations of any claims made in the page*.