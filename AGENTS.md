# Project Guide

This repository is a template for an [Agent Skills](https://agentskills.io/skill-creation/quickstart) collection. The `skills/` tree feeds the spec (one `SKILL.md` per folder), the Claude Code plugin marketplace (`.claude-plugin/marketplace.json`), the Antigravity plugin (`plugin.json`), and a Zensical site. It ships one example skill, `ping`.

## Turning the template into a collection

Establish the owner, repository name, site URL, and whether the repository is public before editing. Do not treat `Mai0313`, `Wei Lee`, `mai@mai0313.com`, `skill_template`, or `skill-template` as the new project's identity.

- Apply one identity everywhere it appears: the three READMEs, `skills/index.md`, `mkdocs.yml` (`site_*`, `repo_*`, `edit_uri`, `extra.social`), `pyproject.toml` (then run `uv lock`), `.claude-plugin/marketplace.json` (`name`, `owner`, plugin names), `plugin.json`, and `.github/CODEOWNERS`.
- `ping` exists to show the layout. Remove it, its marketplace entry, and its README mentions once the first real skill lands.
- Never delete a README badge; point it at the new repository instead. Keep the three READMEs consistent in meaning.
- Modify workflows rather than deleting them. `deploy.yml` publishes the site to GitHub Pages only when the repository is public; the gate sits on the job because `actions/configure-pages` fails first when Pages is off.

## Layout

- `skills/<name>/SKILL.md` — one folder per skill, with any `references/`, `scripts/` or `assets/` next to it. `skills/index.md` is the site's home page, not a skill.
- `agents/` — Claude Code subagent definitions, one Markdown file each. Empty in the template.
- `scripts/` — maintenance scripts for the repository itself. Empty in the template.

## Plugin manifests

- **Codex** reads `.claude-plugin/marketplace.json` directly. There is no `.codex-plugin/marketplace.json`.
- **Antigravity** reads only `plugin.json` at the repository root, where `name` must match `^[a-zA-Z0-9-_]+$`. It has no marketplace concept, so it sees one plugin containing every skill.

**Do not add a plugin manifest at the repository root** (`.codex-plugin/plugin.json`, `.claude-plugin/plugin.json`, `.cursor-plugin/plugin.json`). Every marketplace entry uses `source: "./"`, so a manifest there applies to every plugin at once: Codex prefers it over the per-entry fields and loads the whole `skills/` tree into each plugin, and Claude Code entries are `strict: false`, so a root manifest declaring components makes them fail to load, and a `version` there pins them all.

## Authoring a SKILL.md

Names are kebab-case, and the folder name matches the `name:` field. Frontmatter follows the [Agent Skills spec](https://agentskills.io/specification#frontmatter): `name` (≤64 chars) and `description` (≤1024 chars) are required. Write `description` as a `>-` block: a plain scalar breaks the YAML as soon as the text contains a colon, and a skill whose frontmatter does not parse never loads.

A new folder is not enough: add `./skills/<name>` to a plugin's `skills` array in `marketplace.json`. Nothing warns about a tracked skill that belongs to no plugin.

Keep both the description and the body **short**. The model already knows standard CLI flags, shell patterns, file formats, and mainstream APIs. Write down only:

- Intent and boundaries (what the skill should and should not do)
- Defaults for omitted parameters
- Hard limits and safety rules (forbidden flags, irreversible operations)
- Output format the model cannot guess
- Gotchas not in upstream docs

Skip "When to Use" sections (the description handles triggering) and walkthroughs of standard commands.

`user-invocable: false` (only the model invokes) and `disable-model-invocation: true` (only the user invokes) are [Claude Code extensions](https://code.claude.com/docs/en/skills#control-who-invokes-a-skill), not spec fields, so other runtimes ignore them. Only the second keeps the description out of the model's context.

Reference docs (win on conflict): [Specification](https://agentskills.io/specification), [Best practices](https://agentskills.io/skill-creation/best-practices), [Optimizing descriptions](https://agentskills.io/skill-creation/optimizing-descriptions).

## Build and verify

```bash
make serve  # zensical serve on http://0.0.0.0:9987
make build  # static site into ./site
make fmt    # uvx pre-commit run -a, the same gate CI runs on every PR
```

The site is built by [zensical](https://zensical.org/) reading `mkdocs.yml`, **not** by mkdocs itself. `docs_dir` is `skills/`, so every Markdown file under it becomes a page, and `make fmt` runs mdformat over all of them, `SKILL.md` included; let it own formatting. pre-commit only sees tracked files, so `git add` a new skill folder before running it. `deploy.yml` installs with `uv sync --frozen`, so commit `uv.lock` whenever `pyproject.toml` changes.
