---
creation-date: 2023-01-17
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-20 Session 8 Notes
- prev:: [[course-2023-01-13 Session 7 Notes]]

## Discussion
Most of chapter 13 may be skipped, though 13.5.6 on replay attacks is worth covering.
Chapter 14 on key negotiation explores a protocol to obtain a secret **session key** from an existing secret shared key, for [forward secrecy.](https://en.wikipedia.org/wiki/Forward_secrecy) Challenge yourself before reading this section: explicitly outline an algorithm for Alice and Bob to generate
- 13.5.6 on Replay attacks are a common oversight in cryptographic messaging schemes, and worth reading.
    - In a replay attack, the adversary may re-submit a previously observed message. For example, if the adversary observed that Bob sent an encrypted message $c$ suspected to be the plaintext "yes", the adversary may attempt to send Alice the same message $c$ at a later time. Alice must be able to detect that $c$ is a repeated message, or is otherwise invalid. Replay attacks are commonly prevented in cryptographic protocols by enforcing that each message should be time-stamped as a nonce, preventing the adversary from replaying old messages as new. Further, the adversary may delay or selectively intercept and delete messages, despite not being able to decrypt them. A protocol may implement a message counter to guarantee that messages are not interpreted out of order, and that Alice may re-request missing messages from Bob.
- 14-14.8 Cryptographic Protocols and Key Negotiation - Chapter 14 is a short chapter on the process of developing a secure protocol. It raises several common issues in protocol development, including **parameter negotiation**, avoiding **replay attacks** with a nonce, when to authenticate intermediate values, and using hash functions to eliminate algebraic structure and guarantee predictable-length outputs.
    - The authors raise the concern that the MAC (hash function) may leak information about the internal fields. This concern is no longer significant in protocols relying on authentication.
    - 14.9-10 is highly specific to RSA, and can be skipped. 14.11-12 contain a few short notes on the section, read if you like.
- Sections in Chapter 15 are highly specific, not particularly relevant, and can be skipped.
- 16.1-3 give a high level overview on several false assumptions about using a clock for nonce generation, and may be worth a light skim.

Chapter 13: Cryptographic Protocols
-


## Exercises

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]