---
creation-date: 2023-02-09
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-10 Session 11 Solutions
- back:: [[course-2023-02-10 Session 11 Notes]]

## Exercises
- Compute with pen and paper, the Elgamal algorithm for Alice sending Bob a message. Use parameters: p=19, g=2, a=3, b=5, m=12. You may choose any k. If an adversary obtained the computed ciphertext $(c_1,c_2)$, and obtained access to $k$, how could they decrypt the ciphertext?
With these parameters, Alice chooses nonce $k$ computes:
$$(c_1,c_2)=(g^k,mB^k) \mod p$$
Let $k=4$. Then:
$$(c_1,c_2)=(2^4,12*(2^5)^4) \mod 19=(16,10)$$
Bob computes, by EEA $c_1^{-1}=16^{-1}$:
$$\begin{align}
3 = 19 - (1)16 \\
1 = 16 - (5)3
 \end{align}$$
 Therefore $1=g^k-5(p-g^k)=-5p+6g^k\mod p$, so $g^{-k}=6$. We verify this: $6*16=96=5(19)+1=1\mod 19$.

 Bob then computes $B^{-k}=(g^{-k})^b=6^{5}=5\mod 19$
 $$c_2*B^{-k}=10*5=50=12\mod 19$$
Bob successfully recovers $m=12$.  Now, if an adversary obtained $k$, they could compute $B^k$, without knowledge of Bob's private key $b$. They could subsequently compute $B^{-k}$, allowing them to strip $c_2$ of the hiding, and obtain $m$ as above.

- Compute with Shank's algorithm, on pen and paper, the discrete log of $2^x=33 \mod 83$. Note that $2$ is a generator, which you may check by verifying $2^{41}=82 \mod 83$ (check that you understand why this works).
We obtain the first $\lceil\sqrt{83}\rceil=10$ powers of $g=2$ and $g^{-10}=2^{-10}=42^{10}=3\mod 83$.[^1]
```
2^0=1,	33*3^(-10*0)=33
2^1=2,	33*3^(-10*1)=16
2^2=4,	33*3^(-10*2)=48
2^3=8,	33*3^(-10*3)=61
2^4=16,	33*3^(-10*4)=17
2^5=32,	33*3^(-10*5)=51
2^6=64,	33*3^(-10*6)=70 <- 2^6
2^7=45,	33*3^(-10*7)=44
2^8=7,	33*3^(-10*8)=49
2^9=14,	33*3^(-10*9)=64 <- h*2^(-10)^9
2^10=28,33*3^(-10*10)=26
```

We thereby obtain $2^6=33*2^(-90)$, so $2^{96}=2^{14}=33\mod 83$. Note that modular the reduction of 96 to 14 is a modular reduction of 82, not 83, as it occurs in the exponent (check your knowledge: why is this valid?)[^2]

- Optional: Implement one or both of Elgamal encryption and/or Shank's algorithm.
Consult [rust-elgamal/src at main · eleanor-em/rust-elgamal · GitHub](https://github.com/eleanor-em/rust-elgamal/tree/main/src) for an elgamal implementation.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]

[^1]: python:
```python
>>> for i in range(11):
...     print("2^%s=%s,\t33*3^(-10)^%s=%s" % (i, 2**i % 83, i, 33*(3**i) % 83 ))
```

[^2]: Fermat's Little Theorem provides the result that $g^{p-1}\mod p=1$, so we may perform modular reductions, modulo $p-1$ in the exponent for any group element $g$.