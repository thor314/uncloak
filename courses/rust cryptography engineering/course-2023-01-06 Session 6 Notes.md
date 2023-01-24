---
creation-date: 2022-12-29
audience: developer
completion: 1
tags: type/context/course
---
# course-2023-01-06 Session 6 Notes
- prev:: [[course-2022-12-16 Session 5 Notes]]
- solns:: [[course-2023-01-06 Session 6 Solutions]]
- next:: [[course-2023-01-13 Session 7 Notes]]

This week's focus: is a review of techniques from session 5, with a focus on techniques to obtain compile-time guarantees with Rust. Next week we will be returning to the book, chapter 9 and 10, to discuss randomness and primes. We may take 2 weeks to cover chapter 10 on primes, depending on group sentiment.

More implementation techniques:
- [Why does cryptographic software fail?](https://people.csail.mit.edu/nickolai/papers/lazar-cryptobugs.pdf)  - In this short paper from 2014, the authors explore common vulnerabilities in cryptography implementations and APIs. The four main categories of vulnerabilities discussed are:
    - Plaintext disclosure - revealing plaintext in logging, storage, or directly sending the plaintext over the wire. The crates [secrecy](https://docs.rs/secrecy/latest/secrecy/) and [zeroize](https://docs.rs/zeroize/latest/zeroize/index.html), introduced last week, prevent the cryptography implementer from accidentally disclosing or insecurely storing secrets.
    - Man in the Middle Attacks - proper authentication techniques prevent MITM attacks. Using Authenticated Encryption protocols such as ChaCha20-Poly1305 or AES-GCM, (in combination with a [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority)) avoid allowing an adversary to perform MITM attacks.
    - Brute Force attacks - A kludge of implementation errors for divergence from standard cryptographic tools, or else, implementations diverging from protocols.
    - Side channel attacks - the most common of these being timing attacks, discussed last week in the context of the [subtle](https://docs.rs/subtle/latest/subtle/) crate. More on timing attacks in the recent paper, [They're not that hard to mitigate](https://eprint.iacr.org/2021/1650.pdf). Not advocating for this, but [some developers](https://research.nccgroup.com/2022/04/26/real-world-cryptography-conference-2022/#timing) take the extreme approach of examining all assembly; this should not be necessary.
- Compile-time guarantees:
    - The [Generic Array](https://docs.rs/generic-array/latest/generic_array/) crate gives tools for implementing generically sized arrays, determined at compile time. With [const-generics](https://without.boats/blog/shipping-const-generics/) on Rust Stable, Generic Array is less generally useful than it was when it was introduced int 2015, but remains a standard crate untli [generic_cost_exprs](https://github.com/fizyk20/generic-array/issues/115) is stabilized. Generic arrays must be used with generic integer type values, typically provided by the [typenum](https://docs.rs/typenum/latest/typenum/) crate. See the prior links for usage information, and the following links for several examples in the wild:
        - [generic array dependents crates.io](https://crates.io/crates/generic-array/reverse_dependencies)
        - [typenum dependents crates.io](https://crates.io/crates/typenum/reverse_dependencies); See especially;
            - [filecoin merkle tree](https://github.com/filecoin-project/rust-fil-proofs/blob/128f7209ec583e023f04630102ef1dd17fbe2370/storage-proofs-core/src/merkle/mod.rs#L43), where typenum generics are used to fully specify merkle tree size at compile-time;
            - [libsecp256k1](https://github.com/paritytech/libsecp256k1/blob/70795ba9b86866233ada643a62b3dd58645cb540/src/lib.rs#L823), [HMAC-DRBG](https://docs.rs/hmac-drbg/0.3.0/src/hmac_drbg/lib.rs.html#7-16) - where typenum generics are used to specify a compile-time customizable-sized Deterministic Random Bit Generator (DRBG).
    - See also [this example at dotnetperls](https://www.dotnetperls.com/const-generic-rust) on const generics.
- Traits: There are often standard APIs and marker traits (eg. `CryptoRng` ([here](https://rust-random.github.io/book/update-0.5.html?highlight=cryptorng#cryptographic-rngs)) for any CSPRNG). Use the [GitHub - RustCrypto/traits: Collection of cryptography-related traits](https://github.com/RustCrypto/traits) and [Awesome Rust Cryptography](https://cryptography.rs/#traits-for-cryptographic-primitives) to look for traits when implementing standard cryptographic APIs.
- Extra reading for this week:
    - A recent development in secure cryptographic implementation is the development of auditing and secure design tools, including Jasmine, Vale, Z3, and others. See [this paper](https://hal.inria.fr/hal-03046757/file/BarbosaetalOakland21.pdf) for an overview.
    - A fun read: [The Grug Brained Developer](https://grugbrain.dev/)

Notes for Chapter 9:
- Be familiar with the difference between a PRNG and a [CSPRNG](https://en.wikipedia.org/wiki/Cryptographically_secure_pseudorandom_number_generator), and how the latter can be generated from any secure block cipher. Aim to understand the Fortuna construction, now standard in Apple devices. A Rust implementation can be found here: [crypto::fortuna - Rust](https://nicolasdp.github.io/git/crypto/fortuna/) , also see [wikipedia](https://en.wikipedia.org/wiki/Fortuna_(PRNG)). Note that 9.5-9.7 are information-light, and can be skimmed.
Notes for Chapter 10:
- Be familiar with the definition of a [Sophie Germain Prime](https://en.wikipedia.org/wiki/Safe_and_Sophie_Germain_primes#Sophie_Germain_prime), and [Schnorr](https://en.wikipedia.org/wiki/Schnorr_group) group. We may take 2 weeks to cover chapter 10 on primes, depending on group sentiment. As an extra resource, also see [this](https://medium.com/snips-ai/prime-number-generation-2a02f28508ff) blog post.

## Exercises
Shorter exercises this week, as I was late to posting them. Exercises focus on using typenum, generating primes and randomness.
- Using the `generic_array`, modify the following struct to wrap a generically sized array. Implement a `new`, `len`, and `get_index` method for the array. Instantiate your array in a test with the `typenum` crate. Repeat the exercise with const generics (without `generic_array` or `typenum`).
```rust
struct GenArrayWrapper<T>{
    inner: Vec<T>
}
```
- Pick one implementer of `CryptoRng`, and explain how the Rng generates values. See [CryptoRng in rand - Rust](https://rust-random.github.io/rand/rand/trait.CryptoRng.html) for a list.
- The Extended Euclidean Algorithm "means" that obtaining inverses is not "hard". Explain what hardness means in this context, and why the EEA obtains this result.

---
## Topic(s)
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]