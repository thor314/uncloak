---
creation-date: <% tp.file.creation_date("YYYY-MM-DD") %>
publish: true
audience: all
completion: .1
tags: type/context,
<% tp.file.cursor(1) %>
---

<% tp.file.cursor(2) %> *Prepend `context-TITLE` to your title. Don't forget to refile this file to the correct location with Alt-R.*
*Press Enter after you are satisfied with your title to jump to the topic tag, then `Alt-'` to jump farther down the document. Start with an introduction at the top.*
*Context pages should **only use Markdown links** ( `[markdown](links)` ) throughout the page, to avoid cluttering the graph, and to make pages easier for contributors to re-host on their own-sites. However, they should include normal internal Primary and Secondary Topic links.*

## Sections of your choosing start here


---
## Topic(s)
- primary-topic:: \[\[]]
- secondary-topic:: \[\[optional-secondary-topic\]\]

## External Resources
*The sources section is for recommending resources on other sites*.
- resource:: \[a\]\(link\)

## References
*This section is for citations of any claims made in the page*.