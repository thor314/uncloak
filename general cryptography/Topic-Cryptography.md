---
creation-date: 2022-11-03
publish: true
audience: all
completion: .3
tags: type/topic,
---
# Topic-Cryptography
**Cryptography** (also cryptology) is the practice and study of [[Term-Cryptographically Secure|secure]] techniques for communication, [[Term-Authentication|authentication]], and computation in the presence of a malicious or interfering [[Term-Adversary, Security Model|adversary]]. [[Term-Cryptographer|Cryptographers]] and [[Term-Cryptography Engineer|cryptography engineers]] draw on techniques from a wide range of fields (mathematics, information theory, computer science, computer security, electrical engineering, distributed systems, physics, and beyond) to construct protocols.

Cryptographic protocols are designed in mathematical [[Term-Adversary, Security Model|security models]] based on [[Term-Computational Hardness Assumptions|computational hardness assumptions]]. In order to "break" a cryptographic scheme, an adversary must be able to either:
- break the computational hardness assumption by performing computation thought to be effectively impossible
- exploit a flaw in the security proof, if one exists

Adversaries are more commonly able to attack non-cryptographic parts of a system, including:
- cryptographic implementations, which may have greater [[Term-Attack Surface|attack surfaces]] than cryptographic protocols
- insecure elements of the software system beyond the cryptography
- individuals themselves, who may (unintentionally or by force) release secure information

## Reducing Trust Assumptions
Cryptography can be seen as a general tool for reducing the necessary trust assumptions in a system. Taking [[Topic-Encryption|encryption]] as an example, suppose [[Term-Alice and Bob|Alice and Bob]] would like to privately exchange messages in the over an [[Term-Insecure Channel|insecure channel]]. Without encryption, Alice and Bob have few options. They may trust a third party to securely deliver messages between them, but the third party may inspect the contents of their private conversations.

If the they have access to [[Topic-Symmetric Encryption|symmetric encryption]], they have the capacity to communicate privately, but only if they each possess a shared secret key for encryption and decryption. It's possible the couple are previously acquainted and have already exchanged secret keys, but if they are unfamiliar with one another, they're back to square one, needing to exchange secret keys over the insecure channel. Limiting ourselves to symmetric encryption, Alice and Bob might request keys from a symmetric-key management intermediary, but this scenario is identical to the prior section: the key intermediary would also have access to the secret key, and by extension, the ability read the private communication.

Symmetric encryption in the prior scenario represents a significant reduction in the necessary amount of trust: if Alice and Bob already know and trust one another, there is no need for an intermediary at all. But [[Topic-Asymmetric Encryption, Public Key Encryption|asymmetric encryption]] allows Alice and Bob to communicate without a trusted intermediary, whether or not they have previously communicated. With an asymmetric encryption, Alice and Bob may privately communicate without trusting any other party.

## Recommended Paths through this topic

## Applications

## History
The word cryptography comes from the Greek root words *kryptos*, meaning hidden, and *graphikos*, meaning writing. Prior to 1976, cryptography was limited to the study of [[Topic-Encryption|encryption]] techniques: techniques for encrypting from [[Term-Plaintext and Ciphertext|unhidden plaintext to inscrutible ciphertext]], and decrypting ciphertext to plaintext. In 1976, cryptographers Whitfield Diffie and Martin Hellman introduced the [[Security Assumption-Diffie Helman Assumption|Diffie Helman Assumption]], along with a new set of asymmetric primitives to the field of cryptography in their appropriately named paper, New Directions in Cryptography[^1].

---
## External Resources
- Wikipedia:: [Cryptography](https://en.wikipedia.org/wiki/Cryptography)

## References
*This section is for citations of any claims made in the page*.

[^1]: https://ee.stanford.edu/~hellman/publications/24.pdf