---
creation-date: 2022-11-26
publish: true
audience: all
completion: .1
tags: type/object/attack
---
# Attack-Collision Attack
**Collision attacks** (also meet-in-the-middle attack) are a superset of [[Attack-Birthday Attack|birthday attacks]], where the attacker may pre-compute a table of values, in addition to waiting for a value to repeat.

As an example, suppose a system uses 100-bit keys to encrypt messages. The attacker, Eve, is interested in some set of common messages, for example the message, $m=$"Send Bob \$5". Eve computes $E(m,k)$ for $2^{x}$ values of $k$. Now if a user of the system transmits a message in the set of values Eve computed, Eve has $2^{x-100}$ chance that she has pre-computed the message, and may recover the user's key.

todo: [[Algorithm-Shanks' Babystep-Giantstep Algorithm]]

---
## Related Pages
- primary-topic:: [[Topic-Cryptanalysis]]
- secondary-topic:: [[Topic-Hash Functions]]
- related:: [[Attack-Birthday Attack]]
- attack-on:: [[Property-Collision Resistance]]

## External Resources
- Wikipedia:: [Collision attack](https://en.wikipedia.org/wiki/Collision_attack)

## References
*This section is for citations of any claims made in the page*.