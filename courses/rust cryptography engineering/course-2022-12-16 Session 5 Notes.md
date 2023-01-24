---
creation-date: 2022-12-09
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-16 Session 5 Notes
- prev:: [[course-2022-12-09 Session 4 Notes]]
- solns:: [[course-2022-12-16 HW 5 Solutions]]
- next:: [[course-2023-01-06 Session 6 Notes]]

## Ch 8 notes
This weeks notes are longer than usual. We will be taking December 23 and Dec 30 off. This week's exercises target practical techniques and libraries you may use in cryptographic codebases.

- Chapter 8 discusses implementation practices at a high level. These notes aim to extend the coverage with extra details pertaining to current.
- The introduction discusses what is know referred to by "cryptographic agility" - ability to quickly adapt to discovered insecurities protocols. [SGX.Fail](http://sgx.fail/) demonstrates what may be at stake for a security product that fails to quickly adapt to announced security vulnerabilities. Andrew Miller, one of the authors of sgx.fail expands on what went wrong in [this blog post](https://medium.com/initc3org/tee-based-smart-contracts-and-sealing-pitfalls-eccd5d751329).
- "we don't know how to write a correct program" - Hello, Rust! This is much less true today than it was in 2010. Rust's compiler enforces, by default, correctness in many ways. [NSA urges orgs to use memory-safe programming languages](https://www.theregister.com/2022/11/11/nsa_urges_orgs_to_use/).
- Type level programming techniques can be applied to further prevent common correctness issues at compile-time, but is a bit beyond the scope of this lecture, see [Type-level Programming in Rust | Will Crichton](https://willcrichton.net/notes/type-level-programming/) for an introduction. Spoiler, Rust's type system is Turing-complete: traits can be seen as compile-time analogues of runtime functions, operating over types, as opposed to data. This is under rapid development now that Generic Associated Types have landed in Rust's nightly toolchain.
    -  TLDR, Traits at Compile time are type-level operators (like functions on types instead of data):
        - Inputs: Generic Types; eg `MyTrait<I1,I2>`
        - Outputs: Associated Types; eg `impl MyTrait ... { type O1; type O2; ...}`
- 8.1 provides an overview of how to spec a codebase before implementation. But as any developer knows, spec's always evolve in parallel with the development of a program, as areas of uncertainty are fleshed out. The authors give three types of spec's. See the recently announced [Ethereum Foundation KZG spec](https://github.com/ethereum/kzg-ceremony-specs/) for an example of a well developed spec.
- Section 8.3 can largely be replaced in context by [this blog post on the Zeroize library](https://benma.github.io/2020/10/16/rust-zeroize-move.html). Familiarize yourself with the [Zeroize](https://docs.rs/zeroize/latest/zeroize/index.html) and [Secrecy](https://docs.rs/secrecy/latest/secrecy/) libraries for handling secret information.
- Section 8.4 should be a familiar review of high level best development practices.
    - Leaving assertions is considered poor practice in production Rust codebases; assertions are best left to tests.
    - Error handling: A well designed Rust code base often includes at least one Enum outlining the potential error types that may occur, and what went wrong. The [anyhow - Rust](https://docs.rs/anyhow/latest/anyhow/)  and [thiserror - Rust](https://docs.rs/thiserror/1.0.37/thiserror/) libraries are your friends when writing ergonomic error handling.
    - Buffer overflows are irrelevant for safe Rust implementations, testing remains relevant as ever.
    - Make use `clippy` to lint your code for obvious improvements, consider setting your rust analyzer to run `clippy` instead of check to see inline lints in your codebase.
    - [Rust for Rustaceans #6: Testing](https://www.blog.khrynczenko.com/posts/post-2022-09-22-rust-testing/) is a decent introduction to testing in Rust. Use the `#[should_panic("expected message stub")] #[test]` macro to assert test failure with expected results. These can be aligned with your chosen `thiserror` messages.
    - Notable here is that you can use `#[cfg(TEST_OR_SOME_FEATURE)]` to run integration tests in your code against malicious behavior. This is particularly useful in distributed systems, threshold cryptography, and MPC, where protocol participants themselves may be malicious (Test your knowledge: why would this technique be more relevant for protocols with $n>2$ participants?)
        - The Axelar tofn library demonstrates the malicious feature pattern well, adding variables to functions to communicate ways an adversary may behave.
            - Malicious behavior convenience macro: [tofn/mod.rs at main · axelarnetwork/tofn · GitHub](https://github.com/axelarnetwork/tofn/blob/main/src/gg20/mod.rs)
            - Compliing the codebase with a malicious flag: [tofn/r1.rs at 5b1d0b04d7faaab0146485cf4308a0cff0e56fdb · axelarnetwork/tofn · GitHub](https://github.com/axelarnetwork/tofn/blob/5b1d0b04d7faaab0146485cf4308a0cff0e56fdb/src/gg20/sign/r1.rs#L37)
            - Corrupting behavior if the malicious flag matches:  [tofn/happy.rs at 5b1d0b04d7faaab0146485cf4308a0cff0e56fdb · axelarnetwork/tofn · GitHub](https://github.com/axelarnetwork/tofn/blob/5b1d0b04d7faaab0146485cf4308a0cff0e56fdb/src/gg20/sign/r3/happy.rs#L194)
- Continuous Integration is not mentioned in the above section. Good CI may cost several hours to set up the first time, but may prevent you or your team from firing footguns. CI should deny changes to your codebase that fail tests, linting, and typically formatting as well. Linting builds your software, you don't need to build twice. Github actions and CircleCI are two common choices:
    - [Continuous integration for Rust applications | CircleCI](https://circleci.com/blog/rust-ci/)
    - [Rust CI with GitHub Actions - DEV Community 👩‍💻👨‍💻](https://dev.to/bampeers/rust-ci-with-github-actions-1ne9)
    - Some examples in practice:
        - [tmpl/base/.github/workflows at main · thor314/tmpl · GitHub](https://github.com/thor314/tmpl/tree/43724bedbec3b8fe6a0e4915e607fc3190907475/base/.github/workflows)
        - [tofn/.github/workflows at main · axelarnetwork/tofn · GitHub](https://github.com/axelarnetwork/tofn/tree/main/.github/workflows)
- Side channel attacks - There's a lot to say here. There are many ways in which your implementation can be vulnerable to side channel attacks. Not all of them are relevant for your implementation, many of them are. A well written codebase should detail, in depth, how it avoids side channel attacks, and few do. The most relevant (exploitable) class of side channel attacks allow an attacker to extract private information from timing attacks. There are several tricks at your disposal. [This list by cryptographer JP Aumasson](https://github.com/veorq/cryptocoding) describes several common failures. Familiarize yourself with the [subtle - Rust](https://docs.rs/subtle/latest/subtle/) library for tools on inserting optimization barriers against the compiler. Also note the stable implementation of `black_box` as of Rust 1.66.0, which denies compiler optimizations [Announcing Rust 1.66.0 | Rust Blog](https://blog.rust-lang.org/2022/12/15/Rust-1.66.0.html). This may complement or supecede `subtle`, but I haven't yet used `black_box` myself.
- Designing hardware to prevent power analysis, RF attacks, Van Eck phreaking, etc. are hard-to-impossible to mitigate entirely at the software level, and a discussion of hardware is well outside my expertise. Ask your auditors whether they are capable of auditing hardware attacks against your implementations.
- This section would well be expanded by a section on when and how to audit code. Any production cryptography codebase without an audit from a credible auditing firm (in some cases, several firms) can be assumed to insecure. Auditors may use closed-source tools developed to discover vulnerabilities in your codebase that may have yet to even become publicly disclosed. The NCC group and Trail of Bits are two reputable cryptography auditing firms in the space. Pick an audit report from each list and reflect on whether you would have considered their findings.
    - [https://www.nccgroup.com/sg/assessment-advisory/cryptography/](https://www.nccgroup.com/sg/assessment-advisory/cryptography/)
    - [GitHub - trailofbits/publications: Publications from Trail of Bits](https://github.com/trailofbits/publications#security-reviews)
- Before you pay to audit your code, check it out with common open source analysis tools.
    - https://security.googleblog.com/2022/12/announcing-osv-scanner-vulnerability.html
    - https://github.com/ossf/scorecard/blob/main/docs/checks.md#vulnerabilities
- Knowledge check: What's a Box? A couple links on the Rust memory model.
    - https://doc.rust-lang.org/book/ch15-01-box.html
    - https://fasterthanli.me/articles/whats-in-the-box
    - https://youtu.be/m76sRj2VgGo

## Exercises
This week introduced many tools, and we're heading into the holidays. Get your hands dirty with them.
- Write an Error type with `anyhow` and `thiserror`.
- Implement a type-level program using `PhantomData` to parameterize the state of a struct.
- Put CI on a project. Deny lints, failing tests, and failing formatting.
- Compile your codebase with a malicious feature. Test against it in a unit or integration test.
- implement a program that loops 1000 times, repeatedly branching on secret data (say, equality to number 123456789012345678), taking the left path in execution A and the right path in execution B. Benchmark your program. Determine if your benchmarks are statistically different. Try this first with a single u64, then repeat the experiment making your secret data a vector of length 100 u64's.
- Perform the test demonstrated in the zeroize blog post. For bonus credit, use a debugger [lldb](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) for instance, to insert break points into your code. See if you can determine where the secret value remains within memory, either with `lldb`, or even with `dd`. See [this](https://rustc-dev-guide.rust-lang.org/debugging-support-in-rustc.html) documentation page for the state of debugger support in Rust.
