---
creation-date: 2022-12-15
publish: true
audience: developer
completion: 1
tags: type/context/course
---
# course-2022-12-09 HW 4 Solutions
- back:: [[course-2022-12-09 Session 4 Notes]]

- Justify or disqualify each of the following schemes, with message $m$, tag $t$, and ciphertext $c$.
    - $t=MAC(m)\quad c=E(m)$, send $(c,t)$
        - Encrypt and Authenticate $m$: SSH does this. This approach allows the computation of ciphertext and tag to performed in parallel. This approach is less secure than the following two approaches. There have also been concerns about the capacity for the tag to leak information about the plaintext. Test yourself: what would this imply about the keyed hash function used in MAC? Hash functions in practice may conceal pre-images, but any information leaked about the message may allow further avenues for decryption attacks. Standard MACs, including HMAC-SHA256, are designed not to leak information about the message, but new attacks on cryptography previously thought to be secure are not unimaginable.
    - $t = MAC(m)\quad c = E(m||t)$, send $c$
        - Authenticate then Encrypt: SSL/TLS do this. The recipient must decrypt $c$ before they can determine whether they have received corrupted packets, making the system more vulnerable to DDoS attacks, but the adversary cannot obtain the tag. If the security of the authentication protocol is questionable, this method protects the authentication key from attack, relying instead on the security of the encryption scheme. Modern authentication protocols are thought to be secure enough to render this point moot, but this was not always the case.
    - $c=E(m)\qquad t=MAC(c)$, send $(c,t)$
        - Encrypt then Authenticate: IPSec does this. This technique requires less effort on the receiving party end to verify authentication, reducing the threat of DDoS attacks. Assuming that the block cipher and authentication scheme are secure, this is the most efficient scheme of the bunch.


- You're the adversary, watching a TLS handshake. Pick three steps from [TLS Handshake - OSDev Wiki](https://wiki.osdev.org/TLS_Handshake#Handshake_Overview), and describe how the step prevents you from (pick one):
    - reading message content (confidentiality)
    - tampering with message content (integrity)
    - impersonating either party (authenticity)

Soln:
-   Reading message content (confidentiality)
    - The client sends a Encrypted Handshake Message; first ones to be sent encrypted.
        - They contain a hash of the initial handshake messages and are here to ensure these were not tampered with.
-   Tampering with message content (integrity)
    - The server sends a Server Key Exchange message, initiating the key exchange and signing it with its public key: because server signed with public key.
        - Once this step is achieved, the server and client can communicate without the attacker being able to trick either party by injecting their own messages: Change Cipher Spec message
-   Impersonating either party (authenticity)
    - The server sends its certificates. These are used by the client to verify that it is actually talking to the site it thinks it is talking to, as opposed to a malicious site.