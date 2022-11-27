---
creation-date: 2022-11-23
publish: true
audience: all
completion: .6
tags: type/context/term, related/security
---
# Term-Defense in Depth
In security, a system with defense is a system that requires an attacker to break through several layers of security measures before the system is compromised. Examples include doubly-encrypting messages in different cryptosystems, routing packages through many [[Term-Onion Layer|onion layers]] in a mixnet, or using [[Hardware-Secure Enclave, Software Guard Extensions (SGX)|secure enclaves]] to perform private computation on a machine with other security  security measures.

```mermaid
flowchart LR
A(security layer A) --> B
B(security layer B) --> C
C(security layer C) --> D(assets)
```
*an attacker must break components A, B, and C to compromise the system. This is defense in depth.*

```mermaid
flowchart TD
A(security layer A) -.secures.-> D(assets)
B(security layer B) -.secures.-> D
C(security layer C) -.secures.-> D
```
*An attacker may break any component, A, B, or C to compromise the system. This is the opposite of defense in depth.*

---
## Related Pages
- primary-topic:: [[Topic-Computer Security]]

## External Resources
- Wikipedia:: [Defence in depth](https://en.wikipedia.org/wiki/Defence_in_depth)