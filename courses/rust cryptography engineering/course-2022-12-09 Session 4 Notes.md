---
creation-date: 2022-12-09
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-09 Session 4 Notes
## Notes
- Review of chapter 5-6 and exercise solutions
- Chapter 7 is obsoleted. This weeks reading will focus on Authenticated Encryption, the TLS Handshake, AEADs, GCM, and ChaCha20-Poly1305. Reading this week will be external to the book.
- External Reading:
    - Authenticated Encryption
    - AEAD
        - GCM
        - ChaCha20-Poly1305
    - Key Encapsulation
    - TLS - The TLS Handshake is a protocol for establishing a secure channel. For more: [What happens in a TLS handshake? | SSL handshake | Cloudflare](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/)
    - Recommended libraries
        - Chacha20-Poly1305 - [ChaCha20Poly1305 — Rust crypto library // Lib.rs](https://lib.rs/crates/chacha20poly1305)
        - AES-GCM - [AES-GCM — Rust crypto library // Lib.rs](https://lib.rs/crates/aes-gcm)
        - AEAD traits - [AEAD — Rust crypto library // Lib.rs](https://lib.rs/crates/aead)
- Optional Extra reading, 2007 paper introducing authenticated encryption as a primitive: https://eprint.iacr.org/2000/025.pdf

## Exercises
- Justify or disqualify each of the following schemes, with message $m$, tag $t$, and ciphertext $c$.
    - $t=MAC(m)\quad c=E(m)$, send $(c,t)$
    - $t = MAC(m)\quad c = E(m||t)$, send $c$
    - $c=E(m)\qquad t=MAC(c)$, send $(c,t)$
- You're the adversary, watching a TLS handshake. Pick three steps from [TLS Handshake - OSDev Wiki](https://wiki.osdev.org/TLS_Handshake#Handshake_Overview), and describe how the step prevents you from (pick one):
    - reading message content (confidentiality)
    - tampering with message content (integrity)
    - impersonating either party (authenticity)