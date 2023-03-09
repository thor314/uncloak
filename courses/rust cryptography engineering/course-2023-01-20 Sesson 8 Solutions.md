---
creation-date: 2023-01-24
audience: developer
completion: 1
tags: type/context/course
---
# course-2023-01-20 Sesson 8 Solutions
- Suppose that $x\mod 30=2$. What is obtained about $x\mod 2$, $x\mod 3$, and $x\mod 5$? What about $x\mod 7$?
If $x\mod 30\equiv 2$, then $x=2\pm 30k$ for some integer $k$. We may also compute $x\mod d$ for any divisor of $30$. We could not, for instance, compute $x\mod 7$. For example, if $x_1=2$, $x_2=32$, we do not obtain a single possible value for $x$: $x_1\mod 7 = 2, x_2\mod 7 =4$.
- $2\pm 30k \mod 2 = 2\mod 2 = 0$
- $2\pm 30k \mod 3 = 2 \mod 3 = 2$
- $2\pm 30k \mod 5 = 2 \mod 5 = 2$

- You're Eve, intercepting a message from Alice to Bob. Alice asked Bob to choose a prime larger than 30 to construct a prime field. You choose $p=31, g=2$. How many unique choices of exponent $x$ in $g^x\equiv a\mod p$ does Alice now have? A unique choice is any uniquely obtainable values for $a$. For instance, $2^{17}\equiv 4$ and $2^{32}=4$ are not unique.
First observe that $p-1=30$. [Lagrange's Theorem]() states that the order of $g$ divides $30$. For instance, $(31-1)^{2}= (-1)^2\mod 31=1$ , so the element 29 has order 2. The element $2$ produces the cycle $2, 4, 8, 16, 32=1$, so the element 2 has order 5. There are 5 unique choices for Alice's private key. If Alice wants to prevent this attack, she must check that the generator $g$ does not lie in a small cycle.
- Bob would have chosen $p=83, g=2$. How many unique choices for $x$ does Alice have now? What if Bob chose $p=83,g=3$?
$g=2$ has order $82$, so there are $82$ unique choices for Alice's secret key. $g=3$ has only order 41. Verify this with any script, eg `python3>>> 3**41 % 83`

- 576001 is the prime with factorization $p-1=2^9*3^2*5^3$ . Find a generator $g\ne 1$ with order $|g|< 10$.

Another simple python script:
```python
p = 576001
for g in range(2,p):
    for e in range(2,10):
        if g**e % p == 1:
            print(g,e)
            break

# Equivalent 1-liner:
v = [(g,e) for g in range(2,p) for e in range(2,10) if g**e % p == 1]
for x in v: print(x)
```

639 is the smallest, with order 9. 11333 has order 3. Finally, you can always count on $p-1$ to have order 2. There are, in total, 21 choices of generator with order smaller than 10.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]