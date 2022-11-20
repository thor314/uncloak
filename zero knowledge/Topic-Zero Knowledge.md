---
creation-date: 2022-11-03
publish: true
audience: all
completion: .2
tags: type/topic, related/zero-knowledge
---
# Topic-Zero Knowledge

## Sections of your choosing start here

## Related Pages
*The related pages section is for linking this page other the rest of the graph, press F11 for details. If applicable, replace the following dummy links.*
- primary-topic:: [[Topic-Cryptography]]
- context:: \[\[context\]\]

## ZK Origins (The First Paper)
Zero Knowledge Proofs are a relatively new phenomenon. They were first introduced in 1989 with a paper written by Shafi Goldwasser, Silvio Micali, and Charles Rackoff called "The Knowledge Complexity of Interactive Proof Systems". If this title seems daunting, you are not alone. Leading cryptographers at the time were also stumped by this paper and rejected the authors’ initial publishing attempts. Eventually, they caught on, and in 2012, Goldwasser and Micali were named Turing Award winners for their contributions in revolutionizing the science of cryptography.

The paper presented an initial, interactive protocol for proving whether a number is a quadratic residue within a certain finite field without revealing the prover’s method of calculating.

### Definitions

**Finite Field**: $\mathbb{F}_n := \{0,1, ..., n-1\}$

**Quadratic Residue**: $y$ is a *quadratic residue* mod $x$ if $y=z^2$ mod $x$ for some $z$. Otherwise, we say $y$ is a *quadratic nonresidue* mod $x$.

**gcd(x,y):** Function to find the greatest common denominator between $x$ and $y$.

$QR = \{(x,y)|y \text{ is a quadratic residue mod }x\}$

$QNR = \{(x,y)|y\text{ is a quadratic nonresidue mod }x\}$

### The Protocol
Let there be a prover $P$ and a verifier $V$ that can send and receive messages. $V$ wants to know if $y$ is an element of $QR$ but doesn’t have the knowledge of how to determine this. $P$ claims to know how to do this but does not want to reveal their knowledge. 

1) $V$ randomly generates two numbers: $b\overset{R}{\in}\{0,1\}$, $z\overset{R}{\in}\mathbb{F}_x$ such that $gcd(x,z)=1$

2) $V$ sends $w \leftarrow (z^2y^{b}) \mod x$ to $P$

3) $P$ responds with $c = \left\{        \begin{array}{ll}
            1, & (x,w) \in QNR \\
            0, & (x,w) \in QR
        \end{array}
    \right.$

4) Repeat process until $V$ is satisfied ($n$ times)

### Results
If $(x,y)$ is an element of $QR$ then $(x,w)$ is also an element of $QR$ since $(x,z^2)$ is in $QR$ by definition of quadratic residue, and similarly $(x,z^2y)$ is also in $QR$. When $(x,y)\in QNR$, then $(x,w) \in QNR$ only when $b=1$. Thus, if for all $n$ rounds of the protocol the prover sends $c=0$, then the verifier can be certain with probability $1-2^{-n}$ that $y$ is an element of $QR$. If for all $n$ rounds the prover sends $c=b$, then the verifier can be certain with probability $1-2^{-n}$ that $y$ is an element of $QNR$. Otherwise, the verifier is not convinced that the prover knows how to determine whether $(x,y)\in QR$.

Notice that no knowledge of how to find this result is ever shared, thus making this a Zero Knowledge Proof. We can further specify that this is a Zero Knowledge Interactive Proof because the verifier needs to directly interact with the prover throughout multiple rounds of the protocol. Later on, you will see how proofs can become non-interactive such as zkSNARKs (Zero Knowledge Succinct Non-interactive ARgument of Knowledge).

## External Resources
*The sources section is for recommending resources on other sites*.
- Wikipedia:: [Zero Knowledge Proof](https://en.wikipedia.org/wiki/Zero-knowledge_proof)
- explainer-developer:: [The Moon Math Manual to zk-snarks by Anna Kaplan](https://raw.githubusercontent.com/LeastAuthority/moonmath-manual/main/main-moonmath.pdf)
- explainer-mathematician:: [Proofs, Arguments, and Zero-Knowledge, by Justin Thaler](https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf)
- knowledge-base:: [Delendum ZKP Knowledge Base](https://kb.delendum.xyz/zk-knowledge#foundations-of-zksnarks)
- developer:: [ZK SNARKS: The Low level working, by Rabia Fatima](https://xord.com/research/the-low-level-working-of-zk-snarks/)

## References
- [The Knowledge Complexity of Interactive Proof Systems](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Proof%20Systems/The_Knowledge_Complexity_Of_Interactive_Proof_Systems.pdf)
