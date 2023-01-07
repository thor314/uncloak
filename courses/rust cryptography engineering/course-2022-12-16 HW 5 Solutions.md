---
creation-date: 2022-12-29
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-16 HW 5 Solutions
- back:: [[course-2022-12-16 Session 5 Notes]]

- Write an Error type with `anyhow` and `thiserror`.
    - See https://github.com/thor314/uncloak-hw/tree/main/hw5/src `error.rs` and `lib.rs` for examples.
- Implement a type-level program using `PhantomData` to parameterize the state of a struct.
    - See https://github.com/thor314/uncloak-hw/tree/main/hw5/src/lib.rs for examples.
- Put CI on a project. Deny lints, failing tests, and failing formatting.
    - See https://github.com/thor314/uncloak-hw/tree/main/hw5/.github for examples.
- Compile your codebase with a malicious feature. Test against it in a unit or integration test.
    - See https://github.com/thor314/uncloak-hw/tree/main/hw5/src/lib.rs for examples.
- implement a program that loops 1000 times, repeatedly branching on secret data (say, equality to number 123456789012345678), taking the left path in execution A and the right path in execution B. Benchmark your program. Determine if your benchmarks are statistically different. Try this first with a single u64, then repeat the experiment making your secret data a vector of length 100 u64's.
    - See https://github.com/thor314/uncloak-hw/tree/main/hw5/src/lib.rs and benches for examples.
- Perform the test demonstrated in the zeroize blog post. For bonus credit, use a debugger [lldb](https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb) for instance, to insert break points into your code. See if you can determine where the secret value remains within memory, either with `lldb`, or even with `dd`. See [this](https://rustc-dev-guide.rust-lang.org/debugging-support-in-rustc.html) documentation page for the state of debugger support in Rust.
    - Solutions already contained in the blog post, not replicated.

---
## Topic(s)
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]