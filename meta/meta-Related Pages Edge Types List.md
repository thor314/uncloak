---
creation-date: 2022-11-17
tags: type/meta
completion: .9
---
# meta-Related Pages Edge Types List
The following is a list of all currently accepted edge types between nodes. If you think a new edge type should be proposed, open a PR. The double-colon syntax is a feature of the [dataview](https://github.com/blacksmithgu/obsidian-dataview) Obsidian plugin to declare inline metadata. Press `F11` to open this page while within Obsidian.

## Topics
Each node **must** have a single primary topic and **may** include additional secondary topics:
- primary-topic:: \[\[topic\]\]
- secondary-topic:: \[\[topic\]\]
- secondary-topic:: \[\[topic\]\]

If there are relevant context or pedagogical pages for a topic, the topic **should** link to them:
- context:: \[\[context\]\]
- comparison:: \[\[comparison\]\]
- pedagogical:: \[\[pedagogical\]\]

## Objects
An object **may** extend other objects, **may** live within a larger set of objects, and **may** have predecessor or replacement objects:
- extends:: \[\[object\]\]
- member-of:: \[\[set-object\]\]
- predecessor:: \[\[object\]\]
- descendant:: \[\[object\]\]
- replaces:: \[\[object\]\]
- replaced-by:: \[\[object\]\]

Algorithms that rely on security assumptions/models **must** point to them:
- secure-in:: \[\[security-assumption or security-model\]\]

Software **may** implement an object, and **may** point back to an originating organization or project:
- implements:: \[\[object\]\]
- developed-by:: \[\[organization or project\]\] 

## Statements
A Statement **must** point at the object it describes:
- describes:: \[\[object\]\]

If a particular proof or piece of evidence is particularly relevant, statements **should** link to it:
- primary-proof:: \[\[proof\]\]
- primary-data:: \[\[data\]\]

Aphorism statements generally point at topics, though may also point at objects. 

A model **must** link to the statements that compose it. The statements **should not** link to one another, or the model:
- contains:: \[\[statement\]\]
- contains:: \[\[another-statement\]\]

## Evidence
Proofs and data **must** indicate their relationship to the statements they indicate the truth of. Data may also be related but ambiguous in its degree of support:
- proves:: \[\[statement\]\]
- disproves:: \[\[statement\]\]
- supports:: \[\[statement\]\]
- rejects:: \[\[statement\]\]
- ambiguous-support:: \[\[statement\]\]

## Context
Terms should link to the Primary Topic. Terms should be concise and self-contained.

Comparisons, Pedagogical pages, and Efforts should **only use Markdown links** ( `[markdown](links)` ) throughout the page, to avoid cluttering the graph, and to make pages easier for contributors to re-host on their own-sites. However, they should include normal internal Primary and Secondary Topic links.

Todo: list types of external context links, eg recommended resources for different audiences, sources, etc.


## Other
If it seems there should be a link, but none of the above types match the connection, use the generic "related". We may develop further edge types from these unspecified relations:
- related:: \[\[node\]\]

## Related Pages
- primary-topic:: [[topic-Meta]]
- related:: [[meta-Uncloak Contributor Guide]]
- related:: [[meta-Node Type List]]
