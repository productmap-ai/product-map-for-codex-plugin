---
name: pm-connect
description: Connect the current folder to its Product Map project - from the repository's .productmap/productmap.json marker, its git remotes, or an earlier connection; otherwise let the user pick or create one. Use first in a new project, or when the user asks to connect or switch the Product Map project. Also the plugin's onboarding.
---

# Connect this folder to a Product Map project

The tools below belong to the `productmap` MCP server. If a call says the account is not connected, tell the
user to run `codex mcp login productmap` (or Authenticate in the app) and stop.

1. Gather the facts: `git rev-parse --show-toplevel` (repository root), `git remote -v` (remote URLs),
   `cat .productmap/productmap.json` (the marker, if it exists), and the folder fingerprint:
   `printf '%s:%s' "$(hostname)" "<repository root>" | shasum -a 256 | cut -d' ' -f1`.
2. Call `connect_workspace(remote_urls, marker, cwd=<repository root>, folder_fingerprint, client="codex",
   project_id=<only if the user named one>)`.
3. `status: "connected"`: the project is `project`. If `write_marker` is true, write `marker` as JSON to
   `.productmap/productmap.json` under the repository root (create the folder if needed) and tell the user
   the file can be committed so every clone resolves to this project.
4. `status: "choose"`: show the user `projects` (name, type, storage_mode) and ask which one this folder is -
   or whether to create a new project whose context is stored on Product Map
   (`create_project(name, description, project_type)`; suggest the folder name). Never pick or create without
   asking. Then call `connect_workspace` again with the chosen `project_id`.
5. Finish with one line: project name, type, storage_mode, and that the `$pm-<slug>` skills run an
   agent here (`$pm-agents` lists them). Remember `project_id` for the rest of the conversation.
