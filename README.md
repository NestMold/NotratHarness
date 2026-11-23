# Notrat · Agent Harness

[Notrat](https://notrat.cn) is a local-first desktop AI workbench. This repository is about the
**harness** — the runtime around the model: which tools exist, which calls get blocked, what the
agent remembers between sessions, and how its own prompts get better. Documentation is in Chinese;
[here is the docs site](https://nestmold.github.io/NotratDoc/).

## What the harness does

| Mechanism | What it actually does |
|---|---|
| **Agent loop & experts** | Three built-in experts — planner / researcher / summarizer — split a multi-step job. A custom expert binds a role, a system prompt and its own tool set. |
| **Plan mode** | The model writes an execution plan first, then dispatches the steps to experts. The plan and its progress stay in the transcript, and you can interrupt at any point. |
| **Tool hooks** | Plugins declare `pre` / `post` hooks over prefix-matched tool names. A `pre` hook whose reply contains `deny` / `block` stops that call before it runs; `post` hooks receive the result. |
| **Prompt self-evolution** | A generational genetic algorithm over the user's prompt variants: per-generation fitness / diversity / convergence, variant lineage, Thompson sampling — the winner is re-injected. Behind an approval gate. |
| **Workspace graph** | Every document in the workspace is indexed by its links, down to block-level nodes. The agent can query neighbourhoods and backlinks, and it persists across sessions. |
| **Extension surfaces** | Panels, commands, editors, tools, MCP servers, skills and experts are declared in a manifest rather than hard-coded — a plugin's declarations and UI carry over to HarmonyOS unchanged; only the execution layer differs. |

## What is *not* the harness

The editor shell is the client. Word / Excel / PPT editing, the file tree, panels, themes and the
Markdown renderer are UI — they render state the harness produces. Whenever a behaviour depends on
what the model may touch, that decision belongs to the harness, not to the shell.

## Docs and install

- **Documentation** — <https://nestmold.github.io/NotratDoc/>: getting started, editor, chat,
  experts, plugins, MCP, changelog.
- **Installers** — the download area on **<https://notrat.cn>** detects your OS: Windows 10+,
  macOS 11+, Linux (AppImage / deb / rpm), HarmonyOS NEXT (`.hap`). Builds are published there,
  not in this repository's Releases.

## Status

This repository is being set up as the public landing point for the harness. It holds no source
code and no build artifacts: the product ships as a desktop build from the site above, and the
harness's public extension surfaces are specified in NotratDoc. Issues about the harness, the docs,
or the *best of Agent Harnesses* listing are welcome here.

## License

Notrat is a commercial product (free tier plus a one-time licence). This repository grants no
source licence; the documentation is published separately under its own terms.
