---
creation-date: 2023-01-24
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-03 Session 10 Solutions
- (optional) re-calculate by EEA $397^{-1}$ in the group modulo $2357$, with the tabular method given on page 19. (Also see [[course-2023-01-13 Session 7 Solutions]])

The tabular method proceeds:
![[Pasted image 20230124122323.png]]
*Markdown tables not rendered by the site, see the footnote for source Markdown*[^1]

Eg. the third column, gives that $372=1*a-5*b$; the final column gives that $1=127*a-754*b$.

- implement the modular Fast Powering Algorithm for big ints.
```rust
fn fast_power(n: &BigUint, e: usize, modulo: &BigUint) -> BigUint {
  // handle dumb inputs
  assert!(!n.is_zero());
  assert!(!modulo.is_zero());
  if e.is_zero() {
    return BigUint::from(1u8);
  }
  let n = n % modulo;

  // obtain the (little-endian) binary representation of e
  let e_bits: Vec<bool> = format!("{e:b}").chars().map(|c| c == '1').rev().collect();
  // obtain the powers of two to multiply
  let mut state = BigUint::from(1u8);
  let mut exp_state: BigUint = n;
  for bit in e_bits {
    if bit {
      state = state * &exp_state % modulo;
      dbg!(&state, &exp_state);
    }
    exp_state = &exp_state * &exp_state % modulo;
  }

  state
}
```

- (1.11a) For positive $a,b\in \mathbb Z^+$, suppose $\exists u,v\in \mathbb Z$ satisfying $au+bv=1$. Prove $\gcd(a,b)=1$.
Let $d=\gcd(a,b)$, and suppose $d>1$. Let $a'=a/d, b'=b/d$. Then:
$$1=au+bv = d(a'u+b'v)$$
But since $d>1$, this implies $0<(a'u+b'v)<1$, violating either that $d=\gcd(a,b)$, or that all variable take on integer values, thereby proving the statement by contradiction.

- (1.18) Suppose $g^a\equiv 1\mod m, g^b\equiv 1 \mod m.$ Prove that $g^{\gcd(a,b)}\equiv 1\mod m$.
Provided there is a generator for the elements mod $m$, the problem reduces to an application of [Euler's (totient) theorem](https://explained-from-first-principles.com/number-theory/#eulers-totient-function). However, consider the integers mod 8. Any element {1,3,5,7} (the coprimes of 8) has only order 2; no generator exists.

Let $k=|g|$, that is, let $k$ be the least element such that $g^k\equiv 1\mod m$. We must show that $k$ exists and unique; then $\gcd(a,b)$ must be a multiple of $k$. Anticipating a contradiction, suppose $j$ is the *smallest* other minimal order of the element $g$, such that $g^{j}\equiv 1\mod m$, and $j$ is not a multiple of $k$ or vice versa. WLOG, let $k>j$ Then we may obtain $k-j$ as a yet-smaller order of $g$.
$$g^k=g^j=1\implies g^{k-j}=1$$
But this contradicts our premise that $j$ was the smallest other order of $g$. Therefore $j=k$. Now, any elements $a,b$ satisfying $g^a=1=g^b$ must each be multiples of $k$, guaranteeing that $\gcd(a,b)$ must also be a multiple of $k$. 

- Using a program, obtain a generator for the group of integers in $\mathbb Z / 1009 \mathbb Z$ and $\mathbb Z / 2357 \mathbb Z$. Both values are prime. What method did you use to check if the candidate was a generator?

Exploit Fermat's Little Theorem: if $g^{\frac{p-1}{2}}\equiv p-1\equiv -1\mod p$, then $g$ generates the group. Using the fast-powering algorithm allows you to calculate each check in $O(\log_2 p)$ exponentiations.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]

[^1]:
| a=2357 | b=397 | r1=372 | r2=25 | r3=22 | r4=3  | r5=1  |
| ------ | ----- | ------ | ----- | ----- | ----- | ----- |
|        |       | q1=5   | q2=1  | q3=14 | q4=1  | q5=3  |
| 0      | 1     | (5)    | 6     | (89)  | 95    | (754) |
| 1      | 0     | 1      | (1)   | 15    | (167) | 127   |