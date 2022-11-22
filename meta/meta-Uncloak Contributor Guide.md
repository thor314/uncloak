---
creation-date: 2022-11-16
tags: type/meta
completion: .7
---

# meta-Uncloak Contributor Guide
This document is intended to help contributors get up to speed on where and how to contribute. If using the Obsidian Vault, press `F12` at any time to open this page.

## Getting started
Clone or [fork](https://github.com/thor314/uncloak/fork) the [repo](https://github.com/thor314/uncloak) and edit in a Markdown editor of your choosing. Obsidian is the recommended choice for extensive editing. Open a pull request when your contribution is ready for review, and is easy to start with.

**Contributions of all sizes are welcome**. Easy areas for first contributions include suggesting resource links, citations, and fixing typos. Many pages are empty stubs with a link to another resource, often Wikipedia. Suggesting content for stub pages is a great way to help out. We don't currently have the resources to check your suggestion for plagiarism, but **please don't copy-paste from another site**.

If you'd like to make a larger contribution to an area of site content that doesn't yet exist, you **might consider opening an issue first** to describe the contribution you intend to make so that we can discuss how we can structure your contribution into the graph.[^1] If you intend to propose **more than one new node addition** to the graph, we prefer that you structure your contribution into several pull requests:
- PR $N=1$: propose new stub nodes (**stub** means with little or no content), and their connections to one another. Opening an issue to discuss this structure before the first PR helps us avoid wasting your time.
- PRs $N>1$: Add content updates to your stub nodes. It's alright if your subsequent PRs continue to introduce new nodes and edges that you hadn't yet considered, but we continue to recommend first proposing stub nodes for discussion in PR $N=n-1$ before fleshing out contributions in PRs $N\ge n$.

You are free to use whatever Markdown editor you would like. The Obsidian application comes with convenient tools for creating new pages from templates, linking pages together, and generally working with Markdown documents. We include a short guide on using Obsidian with Uncloak at the bottom of this document. A more extensive guide on Obsidian for personal use can be found [here](https://github.com/thor314/obsidian-setup).

## On Node Types
Uncloak's primary difference from other wikis and knowledge vectors is the emphasis on **communicating the dependency structure of knowledge** via the graph. To achieve this, we have developed a categorization typology for nodes and edges. Each node type has a [template](https://github.com/thor314/uncloak/tree/main/templates), specifying what to include in each type of node. Our node typology attempts to cover all concepts that may arise in the study of cryptography. We have attempted to allow our system to be flexible enough to be encompassing, while remaining legibly obvious to a casual user.

### Basic node types
Cryptography descends from Computer Science and Mathematics; our typology attempts to be generally flexible, but would not serve all scientific disciplines equally well!

These are several primary node types in our graph:
- **Topics** group together other pages (including other topics). Topics are non-exclusive: a page may belong to more than one topic, but each page identifies a **primary topic**. Each topic gets its own subdirectory. Each page lives in the subdirectory of its primary topic. Topics may have many links, but a topic with more than 50 links may be worth separating into further sub-topics. Unfortunately because of the Obsidian graph limitations, nodes with many links quickly become visually messy.
- **Object** nodes are the "main characters" of the graph.
    - **Mathematical** objects are concepts that a mathematician might work with. They tend to be Platonic in the sense that they are "discovered" as much as they are "invented". There is a growing list of math node subtypes: functions, algorithms, sets, algebraic structures, and complexity classes, for a start.
    - **Software** objects describe code and techniques used in software. Software nodes give descriptions of existing libraries, binaries, tools, data structures, DSLs, etc.
    - **Physical** objects are physically occurring stuff. This includes man-made objects (hardware, physical tools) and naturally occurring physical objects, though cryptography generally has less to say on the latter.
    - **Phenomena** objects are a catch-all category for interesting stuff that happens. It's not yet well considered how phenomena objects will be used, but it seems important to include them as a possibility.
- **Statements** nodes make claims about objects. Statements are *complex*: there are many kinds of statements we might like to make.
    - **Provable** statements have proofs (or disproofs). Theorems, propositions, lemmas, and conjectures are common characters in mathematical cryptography. Conjectures in this system are treated as empirical statements. Also see **proof** in the next section.
    - **Empirical** statements have some degree of supporting or rejecting evidence. They may also be lacking evidence in any direction. Also see **data** in the next section.
    - A **Model** groups together a *set of statement nodes* (typically empirical statements) into a coherent structure. Security models and simulations are examples of models.
    - **Proverbial** statements are commonly known truisms or advice, e.g. "don't roll your own crypto" and Kerckhoffs's Principle.
    - **Property** statements describe significant features of some object, e.g. the divisibility of the integers.
    - You might observe that we make statements all the time, on all types of nodes! Not every statement deserves its own node, though our bar for what deserves a statement node is not high. Much of mathematics is constructed from a towering architecture of relatively trivial statements, stacking on top of one another. That it is not already common practice to represent this structure with a graph is a colossally wasted opportunity!

Starting with just these basic node types, we might begin to imagine a graph looking something like this:
```mermaid
flowchart TB
T1(Topic, eg Encryption)
T2(Another Topic, eg Hash Functions)
T1 --- a1[Math m1]
T1 --- a2[Math m2]
a2 --- a2w1(Software w2)
T2 --- a2
a1 --- a1s1(Statement s1)
a1 --- a1s2(Statement s2)
a1 --- a1s3(Software w1)
```

With just a basic language for organizing the structure of knowledge, we can already begin to organize the relations between concepts in non-linear ways. The structure demonstrates that we may organize concepts into fields of study, which contain principal objects, about which we observe statements and properties. But we haven't yet discussed node type for describing whether a statement might be true!

### Statements have Truthiness
As described in the section on Statements, there are two epistemic ways that we might show something is true or false: by **proof**, or by accumulation of **data**.
- **Proofs** are propositional sequences of logic, potentially drawing on other statements in the graph. If the proof of a statement is simple and draws on little, then there is little extra cost in including the proof on the statement itself. But if the proof is complex, it may draw on many other statements; separating the proof from the statement then clarifies the total relation. Further, there may be multiple proofs for any given statement. By separating proofs from statements, we enable a proof to more clearly demonstrate its network of linkages to other statements, while allowing statements to possess a multitude of proofs.
- **Data** is supporting, rejecting, or otherwise relevant evidence in connection to some statement. In cryptography, there are fewer examples of "data" than in other scientific disciplines, but we often analyze protocols under security assumptions and security models that are only conjectured to be secure. A piece of *data* supporting these assumptions might be the number of years that the assumption has held.

With just these node types, we have all we need to start building our knowledge graph. But we aren't quite done. There's one final node category worth discussing, and that's context.

### Context, the Knowledge Envelope
Even with a graph, the context of a node can be difficult to parse. Context is the envelope around nodes that helps clarify relationships, highlight paths through the graph, and consider human effort in the process. The umbrella of context includes definitions of **terms**, **comparisons** between tools and other objects, **pedagogical** content, as well as human efforts like **projects**, **companies**, and **schools**.

Context pages are important, but pretty straight-forward. They don't require much explaining, so we refer you to the [[meta-Node Type List|full list of node types]], while we move onto the next section.

But a quick note before we move on: nodes on **People and Locations are explicitly excluded** from the graph, at least while the project focuses on more pressing pages. Links to people pages on other sites is allowed, but nodes on people and locations [distract from the site purpose and invite vandalism](https://en.wikipedia.org/wiki/Wikipedia#Vandalism).

### How node type is indicated
Each page has a YAML front-matter metadata area at the top of the page. We use **tags** to indicate both node type, and node topic. Eg for a page on a zk-circuit compiler:
```
---
creation-date: 2022-10-22 14:45
tags: type/object/software/programming-language/compiler, topic/zero-knowledge/circuit-compiler
---
Page starts here.
For contextual clarity, an indicator of node type is the first word of the title.

# compiler-Title
```

Tags can also be included with a hashtag \#like/this, but we will prefer to keep tags in the format demonstrated above. Don't include spaces in tags, use dashes instead, as demonstrated above.

## On Edge Types
Edge types are much simpler than node types. Links within a page imply an undirected relationship between nodes.
- Link to nodes within the graph with double square brackets: \[\[A link to a node with this name\]\]. This is particularly useful when linking to terms--pages giving concise definitions--thereby allowing the user to **hover over the link to get a preview of the page** without clicking away.
- Change the description of a link with a pipe: \[\[name-of-node|display-this-text\]\]. Prefer to avoid renaming nodes links, but you have it as an option.
- Link to external pages with normal Markdown links: \[some human descriptor\]\(some link\)

Links are assumed to be undirected edges. Obsidian does not yet provide flexible tools for manipulating link directions. On the local Obsidian client, link direction is recognized by the graph; but on the website, all links in the graph are undirected edges.

The Related Pages section at the bottom of each page is where we explicitly label and categorize edge types. The Obsidian Publish site does not currently have a way to reflect this information in the graph, but we may implement more flexible graph features in the future.

See [[meta-Related Pages Edge Types List]] for a working list of all edge-types.

## On addressing different audiences with different needs
TODO, document the audience metadata tag

## On Using Obsidian
This will be a short guide on using Obsidian. The `.obsidian` directory in the Uncloak repo contains a default setup that you may use. If you would like to customize the

Todo. Just kidding on short, see the long version until I get around to it. [thor314/obsidian-setup: A template repo, with instructions for getting started with Obsidian](https://github.com/thor314/obsidian-setup) until I get around to writing it.
Also todo: [[meta-Obsidian Setup Choices]].


### Plugins

[^1]: We care a lot about the structure of connections between the atoms of knowledge! We've chosen to use Obsidian Publish for our site to demonstrate the dependency graph of concepts, as we believe that communicating structure is as important for a wiki as the individual node content.

## Related Pages
- primary-topic:: [[topic-Meta]]
- related:: [[meta-Node Type List]]
- related:: [[meta-Related Pages Edge Types List]]
- related:: [[meta-Obsidian Setup Choices]]