---
creation-date: 2022-12-09
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-09 Session 4 Notes
- prev:: [[course-2022-12-02 Session 3 Notes]]
- solns:: [[course-2022-12-09 HW 4 Solutions]]
- next:: [[course-2022-12-16 Session 5 Notes]]

## Notes
- Review of chapter 5-6 and exercise solutions
- Chapter 7 is heavily obsolete. This weeks reading will focus on Authenticated Encryption, the TLS Handshake, AEADs, GCM, and ChaCha20-Poly1305. Reading this week will be external to the book.
- External Reading:
- [Authenticated encryption - Wikipedia](https://en.wikipedia.org/wiki/Authenticated_encryption)
- skim the following Wikipedia articles on the two most commonly used AEADs:
    - [Galois/Counter Mode - Wikipedia](https://en.wikipedia.org/wiki/Galois/Counter_Mode#cite_note-1) - GCM is older than the next entry, generally regarded secure, but less secure and slower than ChaCha-Poly. Some machines have special instruction sets for computing AES which makes GCM faster. AES-GCM can only be securely implemented at the *hardware-level*, if timing side channel attacks are to be avoided. There are also concerns about the 128-bit AES block size, reducing security against collision resistance.
    - [ChaCha20-Poly1305 - Wikipedia](https://en.wikipedia.org/wiki/ChaCha20-Poly1305#XChaCha20-Poly1305_%E2%80%93_extended_nonce_variant) - is a faster, more secure AEAD, standardized in 2015. Both algorithms are standardized for use in TLS/SSL, and widely used. The algorithm takes a 256-bit-key, and software implementations are less vulnerable to timing attacks.
    - [It takes two to ChaCha (Poly)](https://blog.cloudflare.com/it-takes-two-to-chacha-poly/) - Cloudflare ChaCha20-Poly and AE explainer.
-  TLS - familiarize yourself with TLS handshakes, and the Rustls library. You are welcome to continue to use OpenSSL, though all future examples will be given with Rustls and exclusively Rust-based implementations, where possible.
    - [What happens in a TLS handshake? | SSL handshake | Cloudflare](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/)
    - [How does SSL work? | SSL certificates and TLS | Cloudflare](https://www.cloudflare.com/learning/ssl/how-does-ssl-work/)
    - [Transport Layer Security - Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security#TLS_1.0)
    - Recommended libraries for this week:
        - [ChaCha20Poly1305 — Rust crypto library // Lib.rs](https://lib.rs/crates/chacha20poly1305)
        - [AES-GCM — Rust crypto library // Lib.rs](https://lib.rs/crates/aes-gcm)
        - [AEAD — Rust crypto library // Lib.rs](https://lib.rs/crates/aead)
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