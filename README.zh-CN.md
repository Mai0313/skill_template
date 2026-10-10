<div align="center" markdown="1">

# Skill Template

[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/skill_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/skill_template/pulls)

</div>

[Agent Skills](https://agentskills.io/skill-creation/quickstart) 集合的 template,格式与 runtime 无关,可以直接被 Claude Code、Cursor、OpenCode、Codex 等任何支持这个格式的 agent 加载。内附一个示例 skill `ping`,收到 ping 就回 `pong`。

> **重要**:这是一个 template 仓库,请不要直接在上面新增 skill。点 [Use this template](https://github.com/Mai0313/skill_template/generate) 建立你自己的 skill 集合。

其他语言:[English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## 仓库内容

| 路径              | 遵循的规范                                                            | 用途                                                                                 |
| ----------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `skills/`         | [Agent Skills spec](https://agentskills.io/skill-creation/quickstart) | 一个 skill 一个文件夹,内含 `SKILL.md`。这是 source of truth,格式与 runtime 无关。    |
| `.claude-plugin/` | [Claude Code plugin spec](https://code.claude.com/docs/en/plugins)    | `marketplace.json`,把上面的 skill 打包成 plugin,方便整组安装。Codex 也读取这个文件。 |
| `plugin.json`     | [Antigravity plugin spec](https://antigravity.google/docs/plugins)    | 根目录的 marker file,让整个仓库可以被 Google Antigravity 加载为 plugin。             |

## 安装

两种方式,看你用哪个 runtime。

### Option A — `npx skills`(任何 agent 都可以)

[`npx skills`](https://github.com/vercel-labs/skills) 是一个方便的 CLI,本身遵循 Agent Skills spec,负责把文件放到 Claude Code、Cursor、OpenCode、Codex 各自正确的位置。它不是另一套格式,只是同一个 spec 的安装器,用起来更顺手。

```bash
# 交互式选择要装哪些
npx skills add Mai0313/skill_template

# 先列出可用的 skill,不安装
npx skills add Mai0313/skill_template --list

# 安装指定的 skill
npx skills add Mai0313/skill_template --skill ping
```

完整 CLI 文档:<https://github.com/vercel-labs/skills>。

### Option B — Claude Code plugin marketplace

如果你用的是 Claude Code,也可以通过 [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json) 里定义的 plugin marketplace 整组安装:

```bash
# 在 Claude Code 里面
/plugin marketplace add Mai0313/skill_template
/plugin install examples@skill-template
```

template 只提供一个 bundle `examples`,里面是 `ping` 这个 skill。

## 浏览

skill 目录在 <https://mai0313.github.io/skill_template>,也可以直接看 [`skills/`](./skills/) 文件夹。

## 开发

开发环境设置、skill 编写规范与 pull request 流程请见 [CONTRIBUTING.md](./.github/CONTRIBUTING.md)。

## License

MIT — 请见 [`LICENSE`](./LICENSE)。
