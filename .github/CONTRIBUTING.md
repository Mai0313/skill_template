# Contributing Guide

Thank you for your interest in contributing to this skills collection. This document describes how to set up the local environment, the conventions for authoring skills, and the workflow expected for issues and pull requests.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Ways to Contribute](#ways-to-contribute)
- [Reporting Issues](#reporting-issues)
- [Development Setup](#development-setup)
- [Local Workflow](#local-workflow)
- [Authoring a Skill](#authoring-a-skill)
- [Branching Model](#branching-model)
- [Commit Convention](#commit-convention)
- [Pull Request Process](#pull-request-process)
- [Code Review](#code-review)
- [Coding Standards](#coding-standards)
- [Security Reports](#security-reports)
- [Licensing](#licensing)

## Code of Conduct

All contributors are expected to behave professionally and respectfully. Personal attacks, harassment, and discriminatory language are not tolerated. By participating, you agree to uphold a welcoming environment for everyone.

## Ways to Contribute

- Authoring new skills with clear scope and triggering rules
- Improving existing skills (clarity, accuracy, examples, prompts)
- Fixing bugs in skill scripts and tooling
- Improving documentation, examples, and tutorials
- Reviewing pull requests and providing constructive feedback

## Reporting Issues

Before opening a new issue:

1. Search existing issues to avoid duplicates.
2. Reproduce the problem on the latest `main`.

Please include:

- The skill name and version
- Steps to reproduce, including the prompt that triggered the skill
- Expected vs. actual behavior
- Relevant logs, transcripts, or screenshots
- Environment information (Claude Code / SDK version, OS)

## Development Setup

This project uses [`uv`](https://docs.astral.sh/uv/) for Python and dependency management, and **Zensical** to render the skills site.

```bash
# Install uv (one-time setup)
make uv-install

# Clone your fork
git clone https://github.com/<your-username>/<repo>.git
cd <repo>

# Install dependencies
uv sync

# Install pre-commit hooks
uv run pre-commit install
```

## Local Workflow

Common tasks are exposed via the `Makefile`. Run `make help` to list all targets. Frequently used ones:

```bash
make fmt       # Run pre-commit hooks (mdformat, codespell, ...)
make serve     # Serve the skills site locally at http://0.0.0.0:9987
make build     # Build the static site into ./site
make clean     # Remove caches and build artifacts
```

Always run `make fmt` before opening a pull request.

## Authoring a Skill

Each skill lives under `skills/<skill-name>/` and follows the [Agent Skills spec](https://agentskills.io/specification):

- `SKILL.md` — the entry document describing what the skill does, when to trigger it, and when to skip it
- Supporting scripts and resources next to `SKILL.md`

Guidelines for high-quality skills:

- **Scope**: a skill should solve one well-defined problem. Split broad scopes into multiple skills.
- **Triggering rules**: state explicitly when the skill *should* and *should not* be invoked. Ambiguous triggers cause regressions across other skills.
- **Outcomes over steps**: state what a correct result looks like and the limits that must hold. Prescribe an order or bundle a script only where the agent would otherwise get it wrong.
- **Examples**: include concrete examples of inputs and expected outputs.
- **Side effects**: clearly document any external systems the skill touches and the permissions required.
- **Idempotency**: when feasible, design steps so that re-running the skill is safe.

When adding a new skill, also add `./skills/<skill-name>` to a plugin's `skills` array in `.claude-plugin/marketplace.json`, or the plugin marketplace will not install it. `skills/ping` is the smallest working example. `git add` the new folder before running `make fmt`; pre-commit skips untracked files.

## Branching Model

- `main` is the default branch and is deployed automatically.
- Skill branches: `feat/<skill-name>`
- Bug fix branches: `fix/<short-description>`
- Documentation branches: `docs/<short-description>`

## Commit Convention

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/) and **must be written in English**.

Format:

```
<type>(<optional scope>): <short summary>

<optional body>

<optional footer>
```

Allowed types:

| Type       | Purpose                                 |
| ---------- | --------------------------------------- |
| `feat`     | A new skill or skill capability         |
| `fix`      | A bug fix in a skill or tooling         |
| `refactor` | Restructuring without changing behavior |
| `docs`     | Documentation-only changes              |
| `perf`     | Performance improvement                 |
| `style`    | Formatting or stylistic changes         |
| `test`     | Adding or correcting tests              |
| `build`    | Build system changes                    |
| `chore`    | Build, tooling, or auxiliary changes    |
| `ci`       | Continuous integration changes          |
| `revert`   | Reverting a previous commit             |

Use the skill name as the commit scope when applicable, e.g. `fix(ping): reply with pong only`. Reference issues with `Closes #123` or `Refs #123`.

## Pull Request Process

1. Ensure your branch is up to date with the target branch.
2. Run `make fmt` locally and verify the site builds with `make build`.
3. Ensure CI checks pass on the pull request.
4. Use a descriptive title following the commit convention; it is validated by **semantic-pull-request**.
5. Fill out the pull request template, including motivation, summary, and example transcripts when relevant.
6. Link related issues and design documents.
7. Mark the PR as **draft** while still in progress.
8. Request review only after self-review and a green CI.

Pull requests are typically merged via **squash merge** to keep history linear.

## Code Review

- Address all review comments or explain why a change is not needed.
- Keep discussions technical, focused, and respectful.
- Resolve conversations only after the concern has been addressed.

## Coding Standards

- Skill prompts and Markdown files are formatted by `mdformat` and checked by `codespell`.
- Python helpers follow `ruff` formatting and linting; new code should be type-annotated.
- Avoid hard-coding personal paths, credentials, or environment-specific values.
- Document the trigger conditions of each skill explicitly to prevent unintended invocation.

## Security Reports

Please **do not** report security vulnerabilities through public issues. Refer to the [security policy](https://github.com/Mai0313/skill_template/security/policy) for the responsible disclosure process.

## Licensing

By contributing, you agree that your contributions will be licensed under the project's license (see [`LICENSE`](../LICENSE)). Ensure that you have the right to submit any code, content, or assets you contribute.
