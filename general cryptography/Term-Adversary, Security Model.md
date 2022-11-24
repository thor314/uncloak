---
creation-date: 2022-11-23
publish: true
audience: all
completion: .1
tags: type/context/term,
---
# Term-Adversary, Security Model
In cryptography, an adversary is an abstract malicious entity with some set of capabilities that may be employed toward interfering with a cryptographic system. The term adversary is typically interchangeable with the term security model. The strength of the security model defines the provable security of the system; [[Term-Cryptographer|cryptographers]] therefore attempt to prove system security with the strongest possible adversaries.

As an example, a typical encryption adversary may want to recover the cipher key, though the adversary may possess other goals as well. A weak adversary may have the ability to intercept [[Term-Plaintext and Ciphertext|ciphertext]] in-transit ([[Security Assumption-Ciphertext Only Attack|ciphertext only attack]]), but a strong adversary may be able to ask a [[Term-Oracle|black-box oracle]] to decrypt any ciphertext or encrypt any plaintext [[Security-Model|Chosen Ciphertext Attack]]. The latter model may seem paradoxical--the adversary can already decrypt any ciphertext--but if the adversary still cannot retrieve the key given these advantages, then the encryption system is demonstrably [[Term-Cryptographically Secure|secure]].

---
## Related Pages
- primary-topic:: [[Topic-Cryptography]]
- secondary-topic:: [[Topic-Cryptanalysis]]
- term:: [[Term-Cryptographically Secure]]

## External Resources
- Wikipedia:: [Provable security](https://en.wikipedia.org/wiki/Provable_security)
- Wikipedia:: [Adversary](https://en.wikipedia.org/wiki/Adversary_(cryptography))

Todo: promote security model into an object?