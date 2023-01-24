---
creation-date: 2023-01-24
audience: developer
completion: .1
tags: type/context/course
---
# course-2023-01-27 Session 9 Solutions
- TLS 1.3 deprecates **session resumption**, allowing previously connected parties to re-use a previously used shared secret key. Does the session resumption protocol obtain **forward secrecy?** (Not answered in the book, use the internet). 

Recall that **forward secrecy** implies that an adversary who obtains either an ephemeral session key, or a long-term private key, cannot obtain further information about the other key; though if an adversary obtains a private key, they will be able to decrypt future session keys until the secret key is rotated. 

**Session resumption** allows servers to re-use recent TLS sessions and keys, bypassing key-negotiation. But if users send long-term keys instead of ephemeral keys for connection, forward secrecy is not obtained.

This was the situation with TLS 1.2. Session resumption in TLS 1.2 and prior did not mandate ephemeral session keys, instead allowing users to use long-term public/private keys. TLS 1.3 (2018) mandated forward secrecy by requiring users to use ephemeral session keys.

It is not safe for a machine to store a private secret in long-term storage, so session-resumption keys typically die after 24 hours or less; Cloudflare, for instance, defaults to one hour before the session-resumption expires.

- List the checks performed in the protocol in chapter 14 on page 235. Could this protocol be vulnerable to a Man-in-the-Middle attack? 

The total protocol requires 9 checks, and is still vulnerable to Man-in-the-Middle attacks, as Alice does not have a method to authenticate her first message. In the real world, the internet has on the order of 600 Certificate Authorities (CAs). In the following protocol, every server (Bob) would additionally return the CA's signature on Bob's public key, so that Alice could verify Bob's identity.

Alice's first message does not contain any checks, only a specification for minimum $p$ size $s_a > p$ and a nonce. 
On receiving Alice's first message, Bob checks that Alices minimum size $s_a$ is not larger than his maximum $p$ size, that $s_a\le 2s_b$.

On receiving Bob's response, Alice checks that:
- Bob's authentication is valid
- Bob's choice of prime $p$ lies inside the requested range, $s_a \le \log p \le 2s_a$.
- Bob's choice of $q$ is in the correct range, $255 \le \log q \le 256$ (recall that for safe prime $p$,  $p=nq+1$, with $q\sim 2^{256}$)
- $p,q$ are prime
- Bob's session public key $X=g^x$ is not 1 (otherwise, the shared secret will be just Alice's session public key, $g^{1*y}=g^y=Y$)
- Bob's session public key $X$ lies inside the order $q$-subgroup: $X^q=1$ 

On receiving Alices response, Bob checks that:
- Alice's authentication is valid
- Alice's session public key $Y$ is not 1
- Alice's session public key $Y$ lies inside the subgroup

- Using the internet, find at least one method used for nonce-generation, besides a counter. Describe this method for nonce generation in the Discord `study-group-main-channel` chat.

A counter is a very simple method for nonce generation, and is easy to verify for multi-party protocols.  A counter is easily not vulnerable to replay attacks, as the counter monotonically increases.

The nanosecond timestamp of a message is another commonly used, monotonically increasing nonce-method. Clock-based nonce systems must still be checked for uniqueness, and provide the advantage that messages may be given a time-out deadline. For instance, a message with 15 minutes to live (called Time To Live TTL in HTTP) would not be accepted 15 minutes after created.

Any collision-resistant random number generator could be used as a nonce-system, but the algorithm would be overkill for most systems; however, Proof of Work nodes compete with one another to test nonces. If one node could predict the nonce sequence of another node, it could frontrun the other node. Proof of work nodes may be secretive about their methods to genererate nonces, but the use of a PRNG is typical.

---
## Topic
- primary-topic:: [[course-Rust Cryptography Engineering Study Group Syllabus]]