<div align="center" markdown="1">

# Skill Template

[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/skill_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/skill_template/pulls)

</div>

A template for an [Agent Skills](https://agentskills.io/skill-creation/quickstart) collection, packaged so it drops straight into Claude Code, Cursor, OpenCode, Codex, and any other runtime that understands the format. It ships one example skill, `ping`, which answers `pong`.

> **Important**: This is a template repository. Do not add skills to it directly. Click [Use this template](https://github.com/Mai0313/skill_template/generate) to start your own collection.

Other Languages: [English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## What's in this repo

| Path              | Follows                                                               | Purpose                                                                                                                   |
| ----------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `skills/`         | [Agent Skills spec](https://agentskills.io/skill-creation/quickstart) | One folder per skill, each with a `SKILL.md`. This is the source of truth — the format is runtime-agnostic.               |
| `.claude-plugin/` | [Claude Code plugin spec](https://code.claude.com/docs/en/plugins)    | A `marketplace.json` that bundles the skills into plugins so they can be installed as a group. Codex reads this file too. |
| `plugin.json`     | [Antigravity plugin spec](https://antigravity.google/docs/plugins)    | Root marker file that makes the repo loadable as a Google Antigravity plugin.                                             |

## Install

Two ways to pull these into your agent, depending on which runtime you use.

### Option A — `npx skills` (any agent)

[`npx skills`](https://github.com/vercel-labs/skills) is a convenience CLI that knows how to read the Agent Skills format and drop the files into the right place for Claude Code, Cursor, OpenCode, Codex, etc. It's not a different format — it's just a more pleasant installer for the same spec.

```bash
# Interactive: pick what to install
npx skills add Mai0313/skill_template

# List what's available without installing
npx skills add Mai0313/skill_template --list

# Install a single skill
npx skills add Mai0313/skill_template --skill ping
```

Common flags:

| Flag                 | What it does                                                   |
| -------------------- | -------------------------------------------------------------- |
| `-g, --global`       | Install to `~/.<agent>/skills/` instead of the current project |
| `-a, --agent <name>` | Target a specific agent (e.g. `-a claude-code`)                |
| `-s, --skill <name>` | Install a specific skill (`'*'` for all)                       |
| `--all`              | Install all skills to all agents, no prompts                   |
| `-y, --yes`          | Skip confirmation prompts                                      |

Full CLI reference: <https://github.com/vercel-labs/skills>.

### Option B — Claude Code plugin marketplace

If you're on Claude Code, you can also install bundles via the plugin marketplace defined in [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json):

```bash
# Inside Claude Code
/plugin marketplace add Mai0313/skill_template
/plugin install examples@skill-template
```

The template publishes one bundle, `examples`, holding the `ping` skill.

## Browse

The catalogue is rendered at <https://mai0313.github.io/skill_template>. You can also browse the [`skills/`](./skills/) directory directly.

## Adding a skill

1. Create `skills/<name>/SKILL.md`, following the [Agent Skills spec](https://agentskills.io/specification). `skills/ping` is the smallest working example.
2. Add `./skills/<name>` to a plugin's `skills` array in `.claude-plugin/marketplace.json`.
3. `git add` the new folder, then run `make fmt`.

## License

MIT — see [`LICENSE`](./LICENSE).
