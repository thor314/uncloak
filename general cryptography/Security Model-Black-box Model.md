---
creation-date: 2022-11-26
publish: true
audience: all
completion: .2
tags: type/object/security-model,
---
# Security Model-Black-box Model
A **Black-box Model** describes what an [[Term-Adversary, Security Model|adversary]] may see as input and output to a cryptographic system. In a black-box model, the internal workings of the system lie inside the black-box: the adversary cannot see them, only test inputs to the system and observe the system's response. Black box models are used, for example, to analyze the security of encryption:
- [[Security Model-Chosen-Plaintext Attack (CPA)]] - the adversary can choose plaintexts to encrypt and observe the outputs, but not analyze the execution of the algorithm within the black-box.
- [[Security Model-Chosen Ciphertext Attack (CCA)]] - the adversary can choose plaintexts to encrypt and ciphertexts to decrypt, but not analyze the execution of the algorithm within the black-box.

Black box models are useful for analyzing the security of an algorithm in isolation, but are less realistic for real-world implementations, where attackers may be able to obtain the software or hardware implementing the algorithm. In the real world, [[Topic-Side-Channel Attacks|side-channel attacks]] may extrapolate key information from binary analysis on software implementations, and power-differential attacks on hardware implementations. [[Security Model-Grey-box Model|Grey box]] and [[Security Model-White-box Model|white box]] analysis models allow attackers to possess some or all knowledge of the internal workings of an algorithm.

---
## Related Pages
- primary-topic:: [[general cryptography/Topic-Cryptography]]
- secondary-topic:: [[Topic-Side-Channel Attacks]]
- term:: [[Security Model-Grey-box Model]]
- term:: [[Security Model-White-box Model]]

## External Resources
- Wikipedia:: [Black box](https://en.wikipedia.org/wiki/Black_box)
- Investopedia:: [Black box](https://www.investopedia.com/terms/b/blackbox.asp)