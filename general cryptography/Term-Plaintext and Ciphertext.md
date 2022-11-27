---
creation-date: 2022-11-23
publish: true
audience: all
completion: .5
tags: type/context/term,
---
# Term-Plaintext and Ciphertext
Plaintext is unencrypted data. Plaintext historically describes human-readable text data, but is inclusive of other machine-readable data types: audio, video, program binaries, etc.

Ciphertext is encrypted data. If the encryption system is [[Term-Cryptographically Secure|secure]], the adversary should find that:
- [[Property-Indistinguishability (IND)|Indistinguishable (IND)]] - the ciphertext is indistinguishable from randomness
- [[Property-Non-Malleability (NM) |Non-malleable (NM)]] - the adversary gains no information about other ciphertext-plaintext pairs.

Plaintext is typically one of two or more inputs to an encryption algorithm

---
## Related Pages
- primary-topic:: [[general cryptography/Topic-Cryptography]]

## External Resources
- Wikipedia:: [Plaintext](https://en.wikipedia.org/wiki/Plaintext)
- Wikipedia:: [Ciphertext](https://en.wikipedia.org/wiki/Ciphertext)