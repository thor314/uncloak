---
creation-date: 2022-12-29
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-01-06 Session 6 Notes
This week's focus: is a review of techniques from session 5, with a focus on techniques to obtain compile-time guarantees with Rust.
- [Why does cryptographic software fail?](https://people.csail.mit.edu/nickolai/papers/lazar-cryptobugs.pdf)  - In this short paper from 2014, the authors explore common vulnerabilities in cryptography implementations and APIs. The four main categories of vulnerabilities discussed are:
    - Plaintext disclosure - revealing plaintext in logging, storage, or directly sending the plaintext over the wire. The crates [secrecy](https://docs.rs/secrecy/latest/secrecy/) and [zeroize](https://docs.rs/zeroize/latest/zeroize/index.html), introduced last week, prevent the cryptography implementer from accidentally disclosing or insecurely storing secrets.
    - Man in the Middle Attacks - proper authentication techniques prevent MITM attacks. Using Authenticated Encryption protocols such as ChaCha20-Poly1305 or AES-GCM, (in combination with a [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority)) avoid allowing an adversary to perform MITM attacks.
    - Brute Force attacks - A kludge of implementation errors for divergence from standard cryptographic tools, or else, implementations diverging from protocols.
    - Side channel attacks - the most common of these being timing attacks, discussed last week in the context of the [subtle](https://people.csail.mit.edu/nickolai/papers/lazar-cryptobugs.pdf) crate. More on timing attacks in the recent paper, [They're not that hard to mitigate](https://eprint.iacr.org/2021/1650.pdf). Not advocating for this, but [some developers](https://research.nccgroup.com/2022/04/26/real-world-cryptography-conference-2022/#timing) take the extreme approach of examining all assembly; this should not be necessary.
    - Compile-time guarantees:
        - The [Generic Array](https://docs.rs/generic-array/latest/generic_array/) crate gives tools for implementing generically sized arrays, determined at compile time. With [const-generics](https://without.boats/blog/shipping-const-generics/) on Rust Stable, Generic Array is less generally useful than it was when it was introduced int 2015, but remains a standard crate untli [generic_cost_exprs](https://github.com/fizyk20/generic-array/issues/115) is stabilized. Generic arrays must be used with generic integer type values, typically provided by the [typenum](https://docs.rs/typenum/latest/typenum/) crate. See the prior links for usage information, and the following links for several examples in the wind:
            - [generic array dependents crates.io](https://crates.io/crates/generic-array/reverse_dependencies)
            - [typenum dependents crates.io](https://crates.io/crates/typenum/reverse_dependencies); See esp. [filecoin merkle tree](https://github.com/filecoin-project/rust-fil-proofs/blob/128f7209ec583e023f04630102ef1dd17fbe2370/storage-proofs-core/src/merkle/mod.rs#L43), [libsecp256k1](https://github.com/paritytech/libsecp256k1/blob/70795ba9b86866233ada643a62b3dd58645cb540/src/lib.rs#L823).
        - See also [this example at dotnetperls](https://www.dotnetperls.com/const-generic-rust) on const generics.
    - Traits: There are often standard APIs and marker traits (eg. `CryptoRng` ([here](https://rust-random.github.io/book/update-0.5.html?highlight=cryptorng#cryptographic-rngs)) for any CSPRNG). Use the [GitHub - RustCrypto/traits: Collection of cryptography-related traits](https://github.com/RustCrypto/traits) and [Awesome Rust Cryptography](https://cryptography.rs/#traits-for-cryptographic-primitives) to look for traits when implementing standard cryptographic APIs.
- Extra reading for this week:
    - A recent development in secure cryptographic implementation is the development of auditing and secure design tools, including Jasmine, Vale, Z3, and others. See [this paper](https://hal.inria.fr/hal-03046757/file/BarbosaetalOakland21.pdf) for an overview.
    - A fun read: [The Grug Brained Developer](https://grugbrain.dev/)

## Exercises
-

---
## Topic(s)
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus