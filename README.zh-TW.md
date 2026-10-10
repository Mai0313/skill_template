<div align="center" markdown="1">

# Skill Template

[![license](https://img.shields.io/badge/License-MIT-green.svg?labelColor=gray)](https://github.com/Mai0313/skill_template/tree/main?tab=License-1-ov-file)
[![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Mai0313/skill_template/pulls)

</div>

[Agent Skills](https://agentskills.io/skill-creation/quickstart) 集合的 template,格式是 runtime 無關的,可以直接被 Claude Code、Cursor、OpenCode、Codex 等任何吃這個格式的 agent 載入。內附一個範例 skill `ping`,收到 ping 就回 `pong`。

> **重要**:這是一個 template repo,請不要直接在上面新增 skill。點 [Use this template](https://github.com/Mai0313/skill_template/generate) 建立你自己的 skill 集合。

其他語言:[English](README.md) | [繁體中文](README.zh-TW.md) | [简体中文](README.zh-CN.md)

## Repo 內容

| 路徑              | 遵循的規範                                                            | 用途                                                                               |
| ----------------- | --------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `skills/`         | [Agent Skills spec](https://agentskills.io/skill-creation/quickstart) | 一個 skill 一個資料夾,內含 `SKILL.md`。這是 source of truth,格式跟 runtime 無關。  |
| `.claude-plugin/` | [Claude Code plugin spec](https://code.claude.com/docs/en/plugins)    | `marketplace.json`,把上面的 skill 打包成 plugin,方便整組安裝。Codex 也讀這個檔案。 |
| `plugin.json`     | [Antigravity plugin spec](https://antigravity.google/docs/plugins)    | 根目錄的 marker file,讓整個 repo 可以被 Google Antigravity 載入成 plugin。         |

## 安裝

兩種方式,看你用哪個 runtime。

### Option A — `npx skills`(任何 agent 都可以)

[`npx skills`](https://github.com/vercel-labs/skills) 是一個方便的 CLI,本身就是遵循 Agent Skills spec,負責把檔案放到 Claude Code、Cursor、OpenCode、Codex 各自正確的位置。它不是另一套格式,只是同一個 spec 的安裝器,用起來比較順。

```bash
# 互動式挑要裝哪些
npx skills add Mai0313/skill_template

# 先列出可用的 skill,不安裝
npx skills add Mai0313/skill_template --list

# 裝指定的 skill
npx skills add Mai0313/skill_template --skill ping
```

完整 CLI 文件:<https://github.com/vercel-labs/skills>。

### Option B — Claude Code plugin marketplace

如果你是用 Claude Code,也可以走 [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json) 裡定義的 plugin marketplace 整組安裝:

```bash
# 在 Claude Code 裡面
/plugin marketplace add Mai0313/skill_template
/plugin install examples@skill-template
```

template 只提供一個 bundle `examples`,裡面是 `ping` 這個 skill。

## 瀏覽

skill 目錄在 <https://mai0313.github.io/skill_template>,也可以直接看 [`skills/`](./skills/) 資料夾。

## 開發

開發環境設定、skill 撰寫慣例與 pull request 流程請見 [CONTRIBUTING.md](./.github/CONTRIBUTING.md)。

## License

MIT — 請見 [`LICENSE`](./LICENSE)。
