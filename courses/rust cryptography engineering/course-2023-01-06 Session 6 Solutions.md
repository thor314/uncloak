---
creation-date: 2023-01-09
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-06 Session 6 Solutions
- back:: [[course-2022-01-06 Session 6 Notes]]

## Exercises
- Using the typenum crate, modify the following struct to wrap a generically sized array. Implement a `new`, `len`, and `get_index` method for the array.
```rust
struct GenArrayWrapper<T>{
    inner: Vec<T>
}
```
See [uncloak-hw/hw6 at main · thor314/uncloak-hw · GitHub](https://github.com/thor314/uncloak-hw/tree/main/hw6).

---

- Pick one implementer of `CryptoRng`, and explain how the Rng generates values. See [CryptoRng in rand - Rust](https://rust-random.github.io/rand/rand/trait.CryptoRng.html) for a list.
*A note to the ambitious reader: RNGs typically rely on bit-manipulations, which often require unsafe APIs.*
The Rust Rand library includes 6 CSPRNGs, 3 of which are ChaCha-based, and the 2 Isaac RNGs exist only for historical-compatibility: [Our RNGs - The Rust Rand Book](https://rust-random.github.io/book/guide-rngs.html#cryptographically-secure-pseudo-random-number-generators-csprngs).

The standard rust CSPRNG is a wrapper around 12-round ChaCha ([std.rs - source](https://rust-random.github.io/rand/src/rand/rngs/std.rs.html#34)), implementing three traits. Two base functionality traits:
- `RngCore` - the core functionality for an RNG requires a basic iterator capable of filling a buffer and generating u32s and u64s.
- `SeedableRng`, for generating a new Rng from seeded entropy.
And finally, the thin marker trait `CryptoRng` is an empty trait for signaling to library consumers that the RNG is cryptographically secure.

The implementation of Chacha12 can be found here: [chacha.rs - source](https://docs.rs/rand_chacha/0.3.1/src/rand_chacha/chacha.rs.html#70). The `generate` function relies on [refill4](https://github.com/rust-random/rand/blob/master/rand_chacha/src/guts.rs#L78), which executes the [linked closure](https://docs.rs/rand_chacha/0.3.1/src/rand_chacha/chacha.rs.html#91).

The implementation of the eSTREAM competition winner can be found [here](https://docs.rs/rand_hc/latest/src/rand_hc/hc128.rs.html#122), and is somewhat easier to read, though slightly less documented. The `generate` function assigns a random bit sequence by a series of modular operations and rotations, see [here](https://docs.rs/rand_hc/latest/src/rand_hc/hc128.rs.html#138).

---

- The Extended Euclidean Algorithm "means" that obtaining inverses is not "hard". Explain what hardness means in this context, and why the EEA obtains this result.
Cryptographic algorithms may be "hard" in two ways:
1. The algorithm relies on a "security reduction" to a difficult problem $\mathcal L$ in complexity theory, where difficult typically means NP-complete: $\mathcal L\in \mathsf {NP}$. A security reduction implies that, if an adversary were able to efficiently (in **polynomial time**) obtain a solution to algorithm, the adversary would also be able to efficiently solve the NP-complete problem, proving the underlying difficult problem has a polynomial solution: $\mathcal L\in \mathsf P$, thereby proving $\mathsf P=\mathsf {NP}$.
2. The algorithm relies on layered non-linear operations (ie. substitution-permutation networks), forcing any cryptanalysis of the algorithm to solve complex systems of non-linear equations. This type of "hard" is theoretically unclean, in that there is often no "security reduction" to a known difficult problem in complexity theory, yet many hash functions and block ciphers rely on them.

Over a field of order $n$, the EEA obtains an inverse for element $a$ in $\log n$ steps, where each step requires one execution of the Division Algorithm (AKA long division). The DA computes $r_i \equiv q_i \mod n$ in $O(\log q_i)$ multiplication operations. Naive multiplication requires $O(n^2)$ bit operations (non-naive multiplication, eg. Karatsuba or FFT multiplication is faster, $O(n^{1.6})$ or less, for large $n$). Step $i$ therefore requires $O(n^2\log q_i)$ bit operations. The total runtime of the EEA is $O(n^2\log n)$ bit operations, so the EEA runs in a polynomial number of bit-operations. Per definition 1 above, the EEA is in the complexity class $\mathsf P$.

---
## Topic(s)
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]