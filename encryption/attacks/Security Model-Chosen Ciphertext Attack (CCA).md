---
creation-date: 2022-11-26
publish: true
audience: all
completion: .2
tags: type/object/security-model, encryption/attacks,
---
# Security Model-Chosen Ciphertext Attack (CCA)
A **Chosen Ciphertext Attack Model** is a [[Security Model-Black-box Model|black-box model]] in which the adversary is given access to any plaintext-ciphertext pair of their choosing, and attempts to derive the key. The adversary may ask an [[Term-Oracle]] to encrypt any plaintext or decrypt any ciphertext. Though the CCA model is stronger than the [[Security Model-Ciphertext-Only Attack (COA)|COA]], [[Security Model-Known Plaintext Attack (KPA)|KPA]], or [[Security Model-Chosen-Plaintext Attack (CPA)|CPA]] models, an encryption scheme that is secure in the CCA model may still be insecure to [[Attack-Statistical Analysis|statistical analysis]]; the [[Encryption Scheme-AES#ECB Mode|ECB Mode of AES]] is a typical example. 

todo:
[[Property-Non-Malleability (NM)]]
[[Property-Indistinguishability (IND)]]

---
## Related Pages
- primary-topic:: [[Topic-Attacks on Encryption]]
- secondary-topic:: [[Topic-Cryptanalysis]]
- model:: [[Security Model-Black-box Model]]
- model:: [[Security Model-Ciphertext-Only Attack (COA)]]
- model:: [[Security Model-Chosen-Plaintext Attack (CPA)]]
- model:: [[Security Model-Known Plaintext Attack (KPA)]]
- property:: [[Property-Indistinguishability (IND)]]
- property:: [[Property-Non-Malleability (NM)]]

## External Resources
- Wikipedia:: [Chosen-ciphertext attack](https://en.wikipedia.org/wiki/Chosen-ciphertext_attack)

## References