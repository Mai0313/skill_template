---
title: Home
description: About Agent Skills
---

# Skill Template

A template for an [Agent Skills](https://github.com/vercel-labs/skills) collection for Claude Code, Cursor, OpenCode, Codex, and other agent runtimes.

## Install

Install every skill in this repo:

```bash
npx skills add Mai0313/skill_template
```

List available skills first:

```bash
npx skills add Mai0313/skill_template --list
```

Install a specific skill:

```bash
npx skills add Mai0313/skill_template --skill ping
```

See the [`skills` CLI docs](https://github.com/vercel-labs/skills) for the full flag reference (global vs project install, targeting specific agents, etc.).

## Browse

Use the navigation on the left to browse the catalogue. Each entry under `skills/` is one installable skill, with a `SKILL.md` describing what it does and when an agent should reach for it. The template ships one, `ping`, which answers `pong`.
