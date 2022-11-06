---
publish: true
---
# Uncloak: A Community Maintained Cryptography Resource
Welcome to Uncloak, a community-maintained knowledge wiki experiment, aiming to increase the accessibility of cryptography for developers, researchers, and everyone else. 

Our approach to knowledge organization attempts to incorporate basic ideas about how knowledge is constructed by representing links between concepts as connections between nodes in a graph. We believe this approach may help to clarify how to approach cryptography as a field for readers of all levels, while aiming to maintain a high standard for what information is relevant for different audiences.

The site will initially focus on generating content directed at cryptography learners and developers in cryptography engineering and zero knowledge, as we see these fields as most lacking in resources. Where there are already decent existing resources (wikipedia pages, blog posts, etc.), the site will aim to link to them, while we expand content in target areas where the need is greater. These stubs are great candidates for first-time-contributions.

Work on site content began in November 2022; the site graph is sparse at the moment, but growing. If you see an area you might like to improve, we appreciate contributions to the site. Currently the best way to do so is by opening an issue or pull request on our [Github](https://github.com/thor314/uncloak).  If you're reading this from Github, the site is hosted at https://uncloak.org. Though the site is hosted via [Obsidian Publish](https://obsidian.md/publish), you don't need to use [Obsidian](https://obsidian.md/) to contribute to the site; all files are pure Markdown. We're currently working on resources for site contributors. 

Our [Discord](https://discord.gg/TYwr4pMS2h) is a good place to ask questions and connect with other contributors. We also have a [Twitter](https://twitter.com/uncloakcrypto) account for site-related announcements. Questions for the site maintainer should be directed at thorck a-squiggle pm dot me.

The Obsidian-Publish mobile site is unfortunately unable to display the desktop-only interactive graph.

[[Topic-Cryptography|Click here, or on the graph, to continue to the site root node on cryptography]].

## Tips for making best use of the site
If you've ever rabbit-holed on Wikipedia and thought, "oh that went pretty well, but the relationship between those concepts is still a little unclear" then you basically already know what the site is about. This site aims to address the complaint that it can be difficult to know where a particular concept or tool fits in context. Hyperlinks between typical wiki pages demonstrate connections between concepts, but without much context. The graph is an attempt at generating that context.

To see this in action, take a look at the path from [[Topic-Number Theory]] to the [[Algorithm-Extended Euclidean Algorithm]]. If you're viewing this from the website, you can see the path traverses [[Set-Integers]] and [[Algorithm-Euclidean Algorithm]]. The path between nodes and the system of node categorization is how the site attempts to put these concepts in context. 

*Nit-pickers: yes, the extended euclidean algorithm can be applied to objects other than integers, and no, the structure of the graph is not final. Open a PR to propose updates to nodes and alternative organizing structures. Pedantry and nitpicking are welcome, we would appreciate your help.*

Each page includes **forward-links** and **backlinks** (you can find backlinks at the bottom of the page in the section titled "Links to this page"). The prior paragraph contains 5 forward links; no other page in the wiki links to the README, so there are no backlinks for this page, but *every other node* in the wiki is linked to by at least one other node. 

**A rule of thumb:** To navigate the graph structure, traveling *forward* links, especially those at the bottom of a page, generally direct the reader *toward the edges of the graph*, where knowledge may be more specific and technical. Traveling *backlinks* returns the reader toward the *central root*, and higher-level topic discussion.

The site graph can sometimes be a bit messy; pages are also organized by folders, representing what primary topics the page falls under. Folders can be navigated in the left sidebar. The sidebar also contains a search bar, for readers who already have some idea of what information they're trying to find.

Similar to Wikipedia, hovering over any site-internal link will produce a modal pop-up with the contents of that resource. This works recursively; you can produce nested pop-ups by hovering over links in the pop-up.

The *global graph* feature on the website is buggier than the desktop *global graph*, sometimes refusing to render. If you clone the [Github](https://github.com/thor314/uncloak) and open the graph as an Obsidian vault (requires downloading Obsidian, which is free), you can even see the entire graph structure by calling the function `Graph view: Open Graph View`. 

Optionally, for more on using Obsidian, consult the Uncloak Obsidian Usage guide (todo).

## Contributor Guide
For more on contributing, see [[Topic-Meta]].

## How to give
The site would not be possible without the support of grants and donations. The site maintainer works full time on improving site content, alongside volunteer contributors.

If you would like to support the continued growth of the site, consider donating. Some addresses are managed through Kraken, which may include a minimum deposit. 

We also participate in [Gitcoin Grants](https://gitcoin.co/grants/9478/uncloak-cryptography) rounds. The next round is anticipated to start in late November; we will make an announcement on the [Uncloak Twitter](https://twitter.com/uncloakcrypto) when the round is beginning.
- [Patreon](https://www.patreon.com/uncloak/membership)
- Paypal: @thorck (may be challenged for last 4 cell digits: 7582)
- Venmo: @cryptograthor
- Eth/Polygon/Optimism/Arbitrum/zkSync: 0xaE72f891Fc9914b13a90cbED799ee73359077bee
- Bitcoin: 3JyCwpwpUkXRiiQQqQ2fq3omvLZF1Jtz4N (min deposit: 0.0001 BTC)
- Cosmos: cosmos15lescyy00y6v8nz5ujxn4ry3wpltxklr30pd22 (min deposit: 1 ATOM)
- Polkadot: 13Mpe6FR2Tm968QpH62WMTaafwpqePaJXpxwvXbitBu7xwyx (min deposit: 1 DOT)
- Solana: 6SBQGqhfnazaEQQycvk2MSbNtgjwhTK8TgrujNxBgsW (min deposit: 0.01 SOL)
- Monero: 8ARaWkq7BBm3EMoRxg635qA3V1VZLzwbaWGqNvCxyDf28SFpgH3prxUduhtSaKFFsDg69HFqNMGxxJJZJ5Zk4G7NVmuvePC (min deposit: 0.1 XMR)
- Zcash: t1bMzCnGkCz5SYGmnpAnTn6SRECvuwdiv5X (min deposit: 0.00500 ZEC)