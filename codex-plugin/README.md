# Product Map for Codex

Product Map's product-management agents as skills in Codex. `$pm-product-strategy-roadmap`, `$pm-prd-specification`,
`$pm-ideal-customer-profile-icp` and the others answer with your project's knowledge base as context, inside your
normal coding session, and propose knowledge changes you review like code. Every agent you invoke in one
conversation takes its turn in the same Product Map chat, which the website shows too.

## Install

From the Codex app's plugin directory, or from the public plugin repository:

```
codex plugin marketplace add productmap-ai/product-map-for-codex-plugin
```

Then enable the plugin for a project in `.codex/config.toml`:

```toml
[plugins."product-map@productmap"]
enabled = true
```

Sign in once: `codex mcp login productmap` in the CLI, or **Authenticate** in the app. The browser opens the
Product Map consent page; the token stays with Codex. `mcp.json` names the production connector
(`https://app.productmap.io/platform-api/mcp`).

Without the plugin, the connector alone works as an MCP server. Add it to `~/.codex/config.toml` (or a trusted
project's `.codex/config.toml`):

```toml
[mcp_servers.productmap]
url = "https://app.productmap.io/platform-api/mcp"   # local backend: http://localhost:8080/platform-api/mcp
auth = "oauth"
```

The server's instructions then carry the same flow; `list_agents` lists the agents.

## Use

| Skill | What it does |
|---|---|
| `$pm-connect` | Finds the Product Map project for this folder - from `.productmap/productmap.json`, the git remotes, or an earlier connection - or lets you pick or create one, and remembers it. Runs on first use. |
| `$pm-agents` | Lists the agents for the project with a starter request each. |
| `$pm-<agent> <request>` | Runs that agent for one request: Codex writes a short brief about the work in progress, the agent answers with your project context, Codex prints the reply and offers any proposed knowledge changes for review. |
| `$pm-context` | Reviews the open knowledge-change proposals for the project's context and applies or discards each. |

Projects whose context is stored on Product Map need no repository: proposals are applied there. Projects
synced from a git repository get accepted proposals written into `.productmap/`. Proposals are shown for
review before changing local files. Discarding a proposal only rejects it on Product Map; it leaves local
files and the Git index untouched.

## Local development

For a local checkout: `codex plugin marketplace add /path/to/product-map-for-codex-plugin` (the marketplace file
is at `.agents/plugins/marketplace.json` in the repository root).

`codex-plugin/skills/pm-<agent>/` (the `SKILL.md`, the `agents/openai.yaml` that names the skill in the
Codex app's picker, "PM: Strategy", and a copy of the icon from `codex-plugin/assets/`, which Codex
resolves relative to the skill folder) is generated from the backend's agent catalogue:

```
PYTHONPATH=backend backend/.venv/bin/python claude-plugin/scripts/generate_agent_skills.py
```

The generator lives in the Product Map monorepo, outside this repository. Keep its proposal workflow in
sync with these skills: write local files only after acceptance, and reject discarded proposals without
restoring or deleting files or changing the Git index.

Support: hey@productmap.io or https://www.productmap.io/. Privacy policy:
https://www.productmap.io/privacy-policy. Terms: https://www.productmap.io/terms-of-use.
