---
creation-date: 2022-11-23
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-Rust Cryptography Engineering Study Group Syllabus
## What
A 4-month, open to the public, Rust Cryptography Engineering weekly study group, covering topics in [*Cryptography Engineering: Design Principles and Practical Applications*](https://drive.google.com/drive/folders/1506sz7G5o6ATeGObP1AEwMV4msaLK3HD?usp=sharing), and other materials as necessary. The group will have optional weekly programming assignments for practice. We will meet in the [Uncloak Discord](https://discord.gg/TYwr4pMS2h) and record lectures weekly on [Youtube](https://www.youtube.com/@uncloakcrypto).

[Practical Cryptography for Developers](https://cryptobook.nakov.com/) and [Number Theory Explained From First Principles](https://explained-from-first-principles.com/number-theory/), and [Cryptography in Rust for Hackers](https://cryptographyinrustforhackers.com/index.html) are recommended as supplemental resources.

## Why
Learning materials on cryptography engineering are scattered, out of date, or generally inaccessible for most developers. Rust has taken the cryptography world by storm, but resources on Rust-based cryptography engineering are few and far between. Training in cryptography does not belong behind closed doors. Learn cryptography with a community of enthusiasts and practitioners. Experience with Rust will be helpful but not required. See the [Uncloak Discord Rust Channel](https://discord.gg/TYwr4pMS2h) for some recommended starting resources on Rust.
Shared notes for the study group will live on the [Uncloak Graph](https://uncloak.org).

## Why not
**You: I want to use cryptography tools, especially ZK stuff, but I don't actually want to do Crypto Engineering**
That's cool too. We're working on resources in that direction as well, but we're pretty early, and things aren't quite ready yet. In the meanwhile, we recommend checking out these resources:
- [0xPARC learning](https://learn.0xparc.org/)
- [Halo 2 Book](https://zcash.github.io/halo2/concepts.html)
- [ZK Whiteboard sessions](https://zkhack.dev/whiteboard/module-one/)
- [Moon Math Manual](https://raw.githubusercontent.com/LeastAuthority/moonmath-manual/main/main-moonmath.pdf)([youtube lectures by Ingonyama](https://www.youtube.com/watch?v=diDyZh2elcY))

## When
The study group will begin on November 18, 2022, running until roughly mid-March. We will meet Fridays at 17:45 UTC (9:45am pacific, 18:45 CET) to accommodate as many time zones as possible.

## Syllabus
We will approximately follow the structure laid out in the text. We have a lot of ground to cover, and this is our first time running the course, so regard this syllabus as approximate, while we gather feedback. We will aim for roughly 2 hours of weekly reading, with optional programming exercises for members who would like to get hands on practice.

Sessions will be recorded and posted to [youtube](https://www.youtube.com/@uncloakcrypto).

- W1
  - Discussion: course structure, and cryptography engineering at a high level, as presented in chapters 1 and 2. Optional pre-study group reading: Chapter 1
  - Reading (assigned reading for before week 2's meeting on 2022-11-25): Chapter 2, bird's eye view of Cryptography, and chapter 23: Involving experts
  - Notes: [[course-2022-11-18 Session 1 Notes]]
- W2
  - Reading: Ch 3-4 on block ciphers
  - Exercises: TBA
- W3
  - Reading: Ch 5-6: Hash Functions and MACs
  - Exercises: TBA
- W4:
  - Reading: Ch 7 Secure Channels
  - Exercises: TBA
- W5:
  - Discussion: scheduled Code Review
  - Reading: Ch 8 Implementation Issues
  - Exercises: TBA
- W6
  - Reading: Chapter 9-10 Randomness and Primes
  - Exercises: TBA
- W7
  - Reading: Ch 11 Diffie Helman
  - Exercises: TBA
- W8
  - Reading: Ch 12 RSA
  - Exercises: TBA
- W9
  - Reading: Ch 13-14 Cryptographic Protocols and Key Negotiation
  - Exercises: TBA
- W10
  - Discussion: scheduled Code Review
  - Reading: Ch 15 Implementation Issues II
  - Exercises: TBA
- W11
  - Reading: ch 16-17, 21 Clocks, Key Servers, and Secret Sharing
  - Exercises: TBA
- W12
  - Reading: Miscellaneous Topics (Zero Knowledge)
  - Exercises: TBA
- W13
  - Reading: Miscellaneous Topics (Multi Party Computation)
  - Exercises: TBA
- W14
  - Reading: Miscellaneous Topics: (Fully Homomorphic Encryption)
  - Exercises: TBA
- W15
  - scheduled Code Review
  - Reading: Miscellaneous Topics
  - Exercises: TBA
- W16
  - Course Review


## FAQ
### How do I sign up?
Show up for sessions, no sign up. See the Discord Event schedule. https://discord.gg/TYwr4pMS2h

### Will sessions be recorded? Can I take the course at my own pace?
Yes and Yes. Sessions will be recorded, and notes will be published. The advantage of keeping up with the group is a deeper liquidity pool of people who are simultaneously thinking and learning about the same things as you, but you're welcome to keep your own pace. [Recordings Link](https://drive.google.com/drive/folders/1506sz7G5o6ATeGObP1AEwMV4msaLK3HD?usp=share_link).

### What time commitment?
See above, you may pace yourself if the pacing doesn't suit you, but we will aim to assign 1-2 hours of reading per week, with an optional pool of development homework. The time taken to complete "development homework" is highly varying on skill level, but we will attempt to target 4-5 hours per week.

### Can I join in the middle?
Yes. The book isn't too heavy, so you may be able to quickly read and catch up, though the exercises are important for comprehension.

### How much Rust do I need to know?
The course will assume some level of rust knowledge, but most content should be accessible for participants with only a basic understanding. If you have a working understanding of another programming language, you should be fine. This blogger has a good series of introductory posts:
https://fasterthanli.me/articles/a-half-hour-to-learn-rust
https://fasterthanli.me/articles/frustrated-its-not-you-its-rust
https://fasterthanli.me/articles/aiming-for-correctness-with-types
https://fasterthanli.me/articles/whats-in-the-box

The rustlings course has some exercises you might try:
https://github.com/rust-lang/rustlings

Two useful cheatsheets:
https://cheats.rs/
https://danielkeep.github.io/itercheat_baked.html

### How much math do I need to know?
Wouldn't hurt to have an understanding of abstract algebra and number theory, but these aren't necessary. So, not much. The course will emphasize engineering skills over mathematical details.

However, if you want to continue in cryptography engineering, you will have to learn enough mathematics to follow along with papers.
I recommend the following post on number theory:
https://explained-from-first-principles.com/number-theory/#outline

And I'm still looking for approachable resources on abstract algebra for developers, but in the context of Cryptography, I would recommend the first two chapters of A Mathematical Introduction to Cryptography.
https://drive.google.com/file/d/1etl96pWvdIDfFx29eIubxvCSsbYkl-Jz/view?usp=sharing

### Will there be certificate/token/NFT rewards for coming?
No. This is unlikely to change. I don't intend to grade group members or take attendance. Your github history is a more applicable certificate.

### How employable will I be after 4 months (and who is the group for?)
4 months isn't really enough time to train up at cryptography engineering, especially if you aren't already reasonably familiar with mathematics and Rust programming...But at least half the people with cryptography jobs in cryptocurrency world are self taught, myself included, setting aside a mathematics bachelor degree and an undergrad course (source on at least half: just a guess https://twitter.com/badcryptobitch/status/1591129635974443014)

Our goal here isn't really to be a substitute for training entirely, but to make discovery and conversation more accessible for a somewhat wide range of participants. Most cryptography conversation is kindof an inside game, you either get everything already because you spent months/years at uni or self-studying; this **kindof sucks**. Learning outside of university is inevitably mostly solitary, kindof lonely, and sometimes even crazy-making when you don't know whether you have something correct, or where to ask questions. Our goal here is to **structure an approach to learning, and create a community of people who might like to learn with you and talk through stuff, allowing that people may want to learn differently, with different levels of time commitment.**

Some participants will want to get a high-level sense of cryptography, and will read/skim the book, but won't much care about the programming exercises. They may ask the occasional question in chat or during group sesh's. Questions, even most **"dumb-but-honest questions" are not extractive**. If something is confusing on a skim, it's likely-by-heuristic to be confusing to others, and helps facilitate discussion (which we want!). I predict minimum effort (but honest) participants should make up at least half of the group, especially early on, and this is good.

Some participants will want to go a little deeper, dip toes with APIs, better understand primitives and how they tie together, but not deep dive on implementations of say, SHA256 or RSA or whatever. This is also good. I wouldn't predict that most group members will go on to look for jobs in cryptography, but they may use cryptography, and **having a better understanding of the primitives, and a place to ask questions** seems good.

Some participants will want to do cryptography engineering. This is nominally the target audience of the group, though we want to be non-exclusive of the first two groups. The **weekly programming exercises and code review** are for this group. Folks who want to understand how cryptography works in the context of the rust programming language over 4 months should be **learn how cryptography engineers think**, and whether the field is something they would like to continue in. If continuing seems like an attractive option, consider committing more time to the group. **Creating resources for others is a great way to learn, help others, and demonstrate your abilities**. Employers around cryptocurrency tend to care more about demonstrated interest than anything else. No promises on your employment prospects, but this course is a great way to train, and build your github with artifacts of that demonstrated interest.

### Who are Thor and Chloe, the hosts of the group?
Thor: [I am](https://twitter.com/cryptograthor) a cryptography engineer and educator. For the last year, I've run the [*Proofs, Arguments, and Zero Knowledge Study Group*](https://gitcoin.co/grants/6020/the-proofs-arguments-and-zero-knowledge-study-gro) with Dr. Justin Thaler, centered around his [pre-print book](https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf) on Zero Knowledge Cryptography. At the same time, I've been building [Entropy](https://entropy.xyz/), the decentralized asset custodian, building on recent work in ECDSA threshold signature schemes. Under a grant from the Ethereum Foundation, I wrote [learning-grade implementations](https://github.com/thor314/pazk) of early protocols in the book, in Python and Rust. I've worked with cryptography for several years; I am **by no means an all-knowing cryptography guru**. Building better foundations for cryptography communication and education is my passion. I think cryptography is beautiful but generally inscrutible for most audiences. Uncloak is my vision for how we can make cryptography community, discussion, and education more accessible for all.

Chloe:
I generally spend most of my time educating communities about various Web3 topics, supporting creators with onboarding into the Web3 space, and developing ways to provide more support with fewer resources. I am passionate about learning, teaching, and giving back to the communities that I find myself a part of. My main research interests are pedagogy and decision neuroscience. Previous to being full-time in crypto, I received my Master’s in Sport Psychology after a decade-long career in Coaching.

In 2020, I dropped out of the Computer Science program at the University of Windsor to pursue a Research Intern position at HashCloak.

In 2021, I worked with the NEAR Foundation to help build functionality for DAOs within the NEAR ecosystem. This led to the creation of the Marma J DAO which seeks to spread love and positivity within the Web3 ecosystem.

Currently, I strive to observe a balance between self-study and community support. Through Uncloak, I hope that this balance can be more efficiently obtained by others as well as myself.