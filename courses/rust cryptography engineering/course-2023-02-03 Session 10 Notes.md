---
creation-date: 2023-01-24
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-03 Session 10 Notes
- prev:: [[course-2023-01-27 Session 9 Notes]]
- solns:: [[course-2023-02-03 Session 10 Solutions]]

This week we'll be shifting to a more mathematical coverage of cryptography. For the next 4 weeks, we'll be covering from sections from [An Introduction to Mathematical Cryptography](https://drive.google.com/drive/u/0/folders/1ILBHUZrDZDku3HfK1yyp6AbBD_F3nRm5). This week's coverage is a partial review of chapters 12 and 13 of Cryptography Engineering, with a closer eye to detail.

If you are inexperienced at reading mathematical texts, some advice. Of greatest importance are definitions. A thorough student will copy each definition into their notes. All the theorems and results follow directly from the definitions! Much of the difficulty with mathematical development is simply obtaining the correct definitions. 

Second, try to understand the crux of each algorithm, theorem, lemma, and proposition, and summarizing in a sentence for your reference. For instance, the Fundamental Theorem of Arithmetic (1.21, p 27) states that if $n>1 \in \mathbb Z$, then $n$ may be factored into the product of primes. That is, for all $n>1\in \mathbb Z$, there exists a unique factorization $\{p_i\}, \{e_i\}$ such that: 
$$n = \prod_i p_i^{e_i}$$
The greatest common denominator of $a,b\in \mathbb{Z} - \{0\}$, may be thus restated:
$$\large{
\gcd(a,b) = \prod_i p_i^{\min(e_{i,a}, e_{i,b})}
}$$
But an easy-to remember, one-sentence summary should help recall the theorem, for instance: *"Every positive integer has a unique prime factorization"*, is much easier to remember!

Finally, try to understand the proofs, but don't fret if they don't come naturally to you. Proofs often reveal not only the reasoning behind the theorem, but even motivation to further theorems and corollaries. However, proofs are often the "hardest" part of reading a mathematical text; only spend as much time as is necessary learning proofs: you decide what necessary means.

## Discussion
The goal of this week is to give a more complete introduction to mathematical tools used in public key cryptography. Pay most attention to sections 1.2-1.5, to develop intuition for properties and algorithms on the modular integers. 

We start in section 1.2 on divisibility, which should remind the reader about basic facts of divisibility, GCD, the Division Algorithm, the Euclidean Algorithm (covered in CE ch 10). Section 1.2 is an opportunity to review in detail, coverage of the Extended Euclidean Algorithm, which guarantees that we can easily obtain modular inverses. The EEA is an incredibly useful algorithm; the tabular method given on page 19 may be of help in calculating it by hand.

Section 1.3 formally introduces some common notation in modular arithmetic. Pay special attention to Euler's totient function and the Fast Powering Algorithm.

Prime Fields are the central focus of Section 1.4. Make sure you understand Proposition 1.22. You may need to revisit the Extended Euclidean Algorithm if it is unclear.

Section 1.5 is the first non-review section. Take care to understand Fermat's Little Theorem, and the Primitive Root Theorem, which guarantees the existence of a generator. If you are familiar with Sylow's First Theorem, the Primitive Root Theorem becomes trivial to prove.

1.6 is optional, historical notes on the significance of cryptography (but comes well recommended). 

1.7 is also optional, formalizing the mathematical notions of asymmetric and symmetric encryption, and introducing the premise of (binary) encoding schemes.

## Exercises
- (optional) re-calculate by EEA $397^{-1}$ in the group modulo $2357$, with the tabular method given on page 19.
- implement the modular Fast Powering Algorithm for big ints.
- (1.11a) For positive $a,b\in \mathbb Z$, suppose $\exists u,v$ satisfying $au+bv=1$. Prove $\gcd(a,b)=1$. 
- (1.18) Suppose $g^a\equiv 1\mod m, g^b\equiv 1 \mod m.$ Prove that $g^{\gcd(a,b)}\equiv 1\mod m$.  
- Using a program, obtain a generator for the group of integers in $\mathbb Z / 1009 \mathbb Z$ and $\mathbb Z / 2357 \mathbb Z$. Both values are prime. What method did you use to check if the candidate was a generator?


---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]
