---
creation-date: 2022-11-17
tags: type/meta
completion: .9
---
# meta-Node Type List
This is the growing list of node types with short descriptions, and their subtypes. The list anticipates node types that may be useful in the future but do not yet exist. Those that do not yet have templates are marked todo. Press `F10` at any time to open this page while within Obsidian.

Note that this ontology is growing and changing. I find the current separation and term selection for "mathematical objects" and "software objects" to be particularly inelegant. The system has no natural place for certain types of objects like networks, and underrepresents the application space. But it seems worthwhile to begin, even with an imperfect system.

##  Topic: a container of nodes

## Object: a concept or idea about which we may make statements
- Mathematical: 
    - Function
        - Cryptographic Hash Function
        - Elliptic Curve
    - Algorithm
        - Attack - an algorithm to attack another algorithm or structure.
        - Encryption Scheme
        - Signature Scheme (todo)
        - Commitment Scheme (todo)
        - Zero Knowledge Protocol (todo)
    - Set
    - Algebraic Structure (todo)
    - Complexity Class (todo)
- Abstraction - an abstract, platonic ideal of an existing object
- Software: written by monkeys like you, me, and GPT-3
    - Library (todo)
    - Binary (todo)
    - Operating System (todo)
    - Virtual Machine (todo)
    - Data Structures (todo)
    - Programming Language (todo)
        - Compiler (todo)
        - DSL (todo)
- Physical - stuff that physically exists 
    - Hardware - computing infrastructure 
    - Natural - something a physicist might study. Is this even needed for cryptography? (todo)
- Phenomena: stuff that happens 
- Other Objects
    - Methodology: nodes describing methods (todo)

## Statement: a statement about an object
- Proven: a statement with a (dis)proof
    - Theorem: (subjectively-defined) an important propositional result
    - Lemma: (subjectively-defined) a small propositional result used in a larger result
    - Proposition: similar to Lemma, without implied use in a theorem
- Empirical: a falsifiable statement with some degree of evidence
    - Security Assumption: an assumption on which the security of algorithms depend
- Aphorism: a commonly repeated idea or piece of advice
- Model: a grouping of statements
    - Security Model: a model that protocols may be proven secure in (todo)
    - Simulation: a model implemented in software, often for empirical test results (todo)
- Property: a worthy-of-note feature of some node
    - Conjectured Property: a property that may or may not hold (todo)

## Evidence
- Proof: a proof or disproof of a statement
    - Disproof (todo)
- Data: supporting or rejecting evidence of a statement

## Context: putting the graph and its contents in clearer light
- Term: a short (<300 word) page giving just the definition of a term; todo: this is a main node type, promote this
- Comparison (todo)
    - Table (todo)
    - List (todo)
- Pedagogical (todo)
    - Flowchart: a guide on how to make a certain decision (todo)
    - Tutorial: a guide of how to do something (todo)
    - Trail Guide: a guide through a path on the graph (todo)
        - Book: A set of trail guides (todo)
- Efforts (todo)
    - Organizations (todo)
        - Non-Profit (todo)
        - Company (todo)
        - DAO (todo)
        - School (todo)
    - Project (todo)
    - Event (todo)
        - Conference (todo)
- Meta: pages about the site (todo)
- Maybe in the future:
    - Source material: pages on particularly relevant source material, though it may be easier to automate this and import the entire IACR graph than manage sources by hand
- Explicitly not included as node types:
    - People: annoying to manage, doesn't much to the project of clarifying technical knowledge, to be left out of the graph initially.
    - Locations: doesn't add to the project of clarifying technical knowledge

## Related pages
- primary-topic:: [[topic-Meta]]
- related:: [[meta-Uncloak Contributor Guide]]
- related:: [[meta-Related Pages Edge Types List]]
