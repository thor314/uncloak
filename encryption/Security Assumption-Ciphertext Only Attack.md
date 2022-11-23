---
creation-date: 2022-11-23
publish: true
audience: all
completion: .1
tags: type/statement/empirical/security-assumption, encryption, 
---

# Security Assumption-Ciphertext Only Attack
A weak encryption security model where the adversary may have the ability to intercept [[Term-Plaintext and Ciphertext|ciphertext]] in-transit ([[Security Assumption-Ciphertext Only Attack|ciphertext only attack]]), but a strong adversary may be able to ask a [[Term-Oracle|black-box oracle]] to decrypt any ciphertext or encrypt any plaintext [[Security Model-Chosen Ciphertext Attack|Chosen Ciphertext Attack]]. The latter model may seem paradoxical--the adversary can already decrypt any ciphertext--but if the adversary still cannot retrieve the secret key given these advantages, then the encryption system is demonstrably [[Term-Cryptographically Secure|secure]].

---
## Related Pages
- primary-topic:: [[Topic-Encryption]]

## External Resources
- Wikipedia:: [Ciphertext-only attack](https://en.wikipedia.org/wiki/Ciphertext-only_attack)

## References
*This section is for citations of any claims made in the page*.