---
name: pm-agents
description: List the Product Map agents available for this folder's project, with what each one is for and a starter request, so the user can pick a $pm-<slug> skill. Use when the user asks which Product Map agents exist.
---

# Product Map agents for this project

- Find the project id: the one you know from this conversation, else the `.productmap/productmap.json`
  marker, else run `$pm-connect`.
- Call `list_agents(project_id)` on the `productmap` MCP server.
- Show a table: skill (`$pm-<slug>`, from the row's `slug`), name, summary, and the first starter's title.
- End with one line: `$pm-<slug> <request>` runs one of them; the agents take turns in the same
  Product Map chat for this conversation.
- Do not run an agent here.
