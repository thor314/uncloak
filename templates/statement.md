---
creation-date: <% tp.file.creation_date("YYYY-MM-DD") %>
publish: true
audience: all
completion: .1
tags: type/statement, 
<% tp.file.cursor(1) %>
# Delete the degree-of-support line if the statement is (dis)proven.
provable: <% tp.file.cursor(2) %> # choices: 0 for unprovable or unproven, 1 for proven
degree-of-support: <% tp.file.cursor(3) %> # between 0.0 and 1.0
---

<% tp.file.cursor(4) %> *Prepend `statement-TITLE` to your title. Don't forget to refile this file to the correct location with Alt-R.*
*Press Enter after you are satisfied with your title to jump to the topic tag, then `Alt-'` to jump farther down the document. **Do not include an introduction**, get straight to the statement.*

## Remarks (optional)


---
## Related Pages
*The related pages section is for linking this page other the rest of the graph, press F11 for details. If applicable, replace the following dummy links.*
- primary-topic:: \[\[topic\]\]
- secondary-topic:: \[\[topic\]\]
- describes:: \[\[object\]\]
- primary-proof:: \[\[proof\]\]
- primary-data:: \[\[data\]\]

## External Resources
*The sources section is for recommending resources on other sites*.
- source:: \[source\](link)

## References
*This section is for citations of any claims made in the page*.