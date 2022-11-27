---
creation-date: 2022-11-03
publish: true
audience: all
completion: .4
tags: type/topic, encryption
---
# Topic-Encryption
**Encryption** and decryption are protocols for algorithmically hiding and unhiding information. Cryptography terms the original message the [[Term-Plaintext and Ciphertext|plaintext]], and the encrypted message [[Term-Plaintext and Ciphertext|ciphertext]]. Encryption is often described in a message passing context between two parties, but includes the hiding of static information, as in the case of [Disk Encryption](https://en.wikipedia.org/wiki/Disk_encryption) .

Encryption can be broadly categorized into two categories: [[Topic-Symmetric Encryption|symmetric encryption]] and [[Topic-Asymmetric Encryption, Public Key Encryption|asymmetric (public key) encryption]]. Symmetric encryption algorithms require both the encrypter and decrypter to have access to the same information, a shared key. In asymmetric key cryptography, the receiving decrypter holds a secret key (known only to the decrypter), while the encrypter uses the receiving party's public key (which may be published online, or distributed in any way).

## Alice and Bob encrypt a message, Eve listens in
Encrypted communication is assumed to be over an [[Term-Insecure Channel|insecure channel]], where an eavesdropper (typically [[Term-Alice and Bob|Eve]]) may attempt to intercept or modify messages, or impersonate parties.
```mermaid
flowchart LR
A(Alice) <-.Maybe Eve!.-> B(Bob)
```

To keep communication private, Alice *encrypts* her message $m$ with encryption key $k_E$ to ciphertext $c$, with an encryption protocol $(E,D)$ known to both parties. Bob may decrypt it with a decryption key, $k_D$.
$$
\begin{align}
\text{Alice}:&\ c:= E(k_E, m) \\
\text{Bob}:&\ m = D( k_D, c)
\end{align}
$$

In **symmetric encryption**, the encryption and decryption keys are equivalent, $k_{E}= k_D$. Alice and Bob must therefore already share a secret key to communicate via symmetric encryption.

In **asymmetric encryption**, the encryption and decryption keys differ. In the example given above, Bob may publish his *public (encryption) key*, which anyone may use to communicate securely with Bob, but must keep his *private (decryption) key* secret, or else Eve will be able to decrypt and read his mail. Unlike symmetric encryption, Alice and Bob may use asymmetric encryption, even if they have never communicated before and do not share a secret key. There is a cost however: asymmetric encryption algorithms tend to be at least 30 times less efficient than symmetric encryption ([[#Example: Timing asymmetric encryption]]).

To sidestep these costs, Alice and Bob may use [[Term-Key Encapsulation Mechanism (KEM)|Key Encapsulation]]: first using asymmetric encryption to agree on a shared symmetric encryption key for subsequent communication, then communicating via symmetric encryption.

Todo: [[Attack-Man In The Middle (MITM)]]

## History
Symmetric key encryption is at least as old as Julius Caesar, who was said to use a rotation cipher, termed the [[Algorithm-Caesar Cipher|Caesar Cipher]], to conceal his messages from enemy soldiers circa 69 BCE[^2].

todo: say something about world war two

Asymmetric Key encryption is a significantly more recent invention: it was simultaneously conceived of by [James H. Ellis](https://en.wikipedia.org/wiki/James_H._Ellis) of the British intelligence agency GCHQ between 1970-1974, and by [Whitfield Diffie](https://en.wikipedia.org/wiki/Whitfield_Diffie) and [Martin Hellman](https://en.wikipedia.org/wiki/Martin_Hellman) in their 1976 paper [New Directions in Cryptography](https://ieeexplore.ieee.org/document/1055638). The discovery by GCHQ was not disclosed until 1997[^3].

todo: something about the 90s crypto wars

---
## Related Pages
- primary-topic:: [[general cryptography/Topic-Cryptography]]

## External Resources
*The sources section is for recommending resources on other sites*.
- Wikipedia:: [Encryption](https://en.wikipedia.org/wiki/Encryption)

## Examples
### Example: Timing asymmetric encryption
```sh
cat "uncloak is cool" >> plain.txt
time openssl enc -aes-128-cbc -e -in plain.txt -out cipher.txt -k "password"
time openssl enc -aes-128-cbc -d -in cipher.txt -out plain2.txt -k "password"
gpg --generate-key
time gpg -e -r "replace with recipient public key or name" plain.txt
time gpg -d plain.txt.gpg
```

## References
[^2]: [Suetonius, Vita Divi Julii](http://thelatinlibrary.com/suetonius/suet.caesar.html#56)
[^3]: [GCHQ: James Ellis](https://www.gchq.gov.uk/person/james-ellis)