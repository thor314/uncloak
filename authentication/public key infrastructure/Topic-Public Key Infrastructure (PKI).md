---
creation-date: 2022-11-24
publish: true
audience: all
completion: .3
tags: type/topic, authentication/pki,
---
# Topic-Public Key Infrastructure (PKI)
PKI is a system for managing certificates of public-key authentication, preventing [[Attack-Man In The Middle (MITM)|Man in the Middle]] attacks. In a PKI system, each user registers their public-key with a centrally trusted [[Term-Certificate Authority (CA)|Certificate Cuthority (CA)]]: the user must prove ownership of their public-key, which they may do by [[Topic-Signatures|signing]] a message. The CA returns a certificate, the CA's own signature of the user's public key. The user may then demonstrate ownership of their public-key by showing the certificate to other users.

## Alice and Bob prevent a man-in-the-middle attack
Without the CA, Alice might intend to talk to Bob, but her messages may be intercepted and/or modified by Eve in a man-in-the-middle attack.
```mermaid
flowchart LR
A(Alice) -.Hey Bob, establish secret?.-> E(Eve)
E -.Hey Bob, establish secret? <3 Alice.-> B(Bob)
B -.Sure Alice. .-> E
E -.Sure Alice. <3 Bob.-> A
```

Without an initial authentication mechanism, Alice has no guarantee that the party she initiates is actually Bob. Alice may first authenticate Bob by asking for Bob's certificate that he is actually Bob. Alice may verify Bob's certificate with her stored copy of the CA's public key.

## Recommended Paths through this topic

## Applications

## History

---
## Related Pages
- primary-topic:: [[Topic-Authentication]]
- secondary-topic:: [[Topic-Asymmetric Encryption, Public Key Encryption]]

## External Resources
- Wikipedia:: [Public key infrastructure](https://en.wikipedia.org/wiki/Public_key_infrastructure)

## References
*This section is for citations of any claims made in the page*.