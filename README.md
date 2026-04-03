# autonomous-workflow

A [Claude Code](https://code.claude.com/docs/en/overview.md) plugin: a gated, multi-agent pipeline that turns a short requirement into research, briefs, design options, contracts, a tech spec, and implementation—**with human approval at each gate**.

This repository is **plugin source** (`.claude-plugin/`, `commands/`, `agents/`). It is **not** a Node app; there is no `npm run dev`.

## Requirements

- [Claude Code](https://code.claude.com/docs/en/quickstart.md) (terminal CLI, [Desktop](https://code.claude.com/docs/en/desktop.md), or another supported surface)

## Install the plugin

### Option A — Marketplace (recommended)

From within Claude Code (terminal or Desktop, latest version):

```text
/plugin marketplace add D4rsh4k/autonomous-workflow
/plugin install autonomous-workflow@d4rsh4k-plugins
```

Then run `/reload-plugins` to activate. After that, open your **application project** in Claude Code and use the plugin commands (see [Slash commands](#slash-commands-and-namespacing) below).

### Option B — Local folder (no marketplace required)

1. Clone this repository:
   ```bash
   git clone https://github.com/D4rsh4k/autonomous-workflow.git
   ```
2. Start Claude Code from your **application project** with the plugin loaded:
   ```bash
   cd /your/app/project
   claude --plugin-dir /absolute/path/to/autonomous-workflow
   ```
3. Run `/reload-plugins` if you change plugin files mid-session.

## Slash commands and namespacing

Plugin commands are often **namespaced** with the plugin `name` from `plugin.json` (`autonomous-workflow`). After install, check **`/help`** in your session.

You may need:

- `/autonomous-workflow:build <requirement>`
- `/autonomous-workflow:decide <decision>`
- `/autonomous-workflow:status`

The markdown in `commands/` also refers to `/build`, `/decide`, and `/status`; your Claude Code version may show the prefixed form.

## If you see `Unknown skill: plugin` (especially on Desktop)

1. **Update** Claude Code (Desktop app and/or CLI) to the latest version, then fully restart.
2. Try the same flow in the **terminal** with `claude` and `claude --version` for parity.
3. See [Discover plugins — Troubleshooting](https://code.claude.com/docs/en/discover-plugins.md#plugin-command-not-recognized).

That message usually means the session did not register **`/plugin`** as a built-in command, not that `plugin.json` in this repo is invalid.

## Run the workflow in the right repo

Gates 2–4 assume a **real codebase** (frontend routes, backend, etc.). Run **`/autonomous-workflow:build`** (or the equivalent shown in `/help`) from your **product** repository, not from a copy of this plugin-only tree.

Artifacts are written under **`.build/`** in the project (see `commands/build.md`).

## Commands (overview)

| Command   | Role |
| --------- | ---- |
| `build`   | Start or resume the pipeline from a rough requirement |
| `decide`  | Human gate: approve, pick a design option, or send feedback |
| `status`  | Summarize current gate and state from `.build/current-run/state.json` |

## Further reading

- [Claude Code plugins](https://code.claude.com/docs/en/plugins.md)
- [Discover and install plugins](https://code.claude.com/docs/en/discover-plugins.md)
- [Plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces.md)
- [Plugins reference](https://code.claude.com/docs/en/plugins-reference.md)
