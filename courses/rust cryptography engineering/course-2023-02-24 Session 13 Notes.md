---
creation-date: 2023-02-14
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-02-24 Session 13 Notes
- prev:: [[course-2023-02-17 Session 12 Notes]]
- solns:: [[course-2023-02-24 Session 13 Solutions]]
- next:: [[course-2023-03-10 Session 14 Notes]]

Elliptic curve point addition may be unintuitive, but at the end of the day, everyone learns a bit about elliptic curves, slowly forgets most of it, and ends up treating elliptic curves as a black box with group structure. This is okay. But the basic facts of elliptic curves are reasonably straight-forward, which is what we will be exploring this week.

I will be away next Friday on March 3rd, so we'll be **taking a week off**. Course will resume Friday, March 10th at the usual time.

## Discussion
Many [excellent](https://explained-from-first-principles.com/number-theory/#elliptic-curves) [guides](https://andrea.corbellini.name/2015/05/17/elliptic-curve-cryptography-a-gentle-introduction/) and [resources](https://curves.xargs.org/) exist on elliptic curves. The content between them is mostly the same, with minor differences. We will cover the book, but the reader is invited to use these as supplementary resources.

Aim to develop an intuition for the geometric interpretation of elliptic curve point-addition, as the algebraic interpretation is much less elegant, and captures less of the intuition. Sections 5.1-5.5 give the basic facts of elliptic curves, section 5.8 on bilinear pairings is optional, but will be relevant when we discuss BLS signatures in week 15.

## Exercises
Migrate [this toy elliptic curve](https://github.com/cjeudy/EllipticCurves) implementation to Rust. Then review the [Rust Crypto elliptic-curves library](https://github.com/RustCrypto/elliptic-curves). What techniques could you use to improve your implementation?

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]