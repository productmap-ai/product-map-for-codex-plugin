# Product Map for Codex

Product Map's product-management agents as skills in Codex. `$pm-product-strategy-roadmap`,
`$pm-prd-specification`, `$pm-ideal-customer-profile-icp` and the others answer with your project's knowledge
base as context, inside your normal coding session, and propose knowledge changes you review like code.

## Install

```
codex plugin marketplace add productmap-ai/product-map-for-codex-plugin
```

Then enable the plugin for a project in `.codex/config.toml`:

```toml
[plugins."product-map@productmap"]
enabled = true
```

Sign in once: `codex mcp login productmap` in the CLI, or **Authenticate** in the app.

Full documentation: [codex-plugin/README.md](codex-plugin/README.md). Website: https://www.productmap.io.
Support: hey@productmap.io.

This repository is published from the Product Map monorepo; changes land here on each plugin release.
