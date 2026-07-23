# catalyst-design · Skill

> A bilingual **catalyst design guidance skill** for AI agents. | 面向 AI 智能体的双语**催化剂设计指导技能**。

## 简介 | Introduction

**中文**：催化剂设计指导技能。基于分层、可追溯、可动态演进的方法论体系，为催化剂组分选择、结构设计、合成策略与性能优化提供建议。覆盖 HER / OER / ORR / PEMWE 等电催化反应；每条建议标注来源（文献已证实 / 经验推测）与置信度，并附可执行验证路径。可独立运行，也可与 [catalyst-search](https://github.com/ANDYPENG09/catalyst-search) 协作——消费其文献矩阵以增强针对性。

**English**: A catalyst design guidance skill. Built on a layered, traceable, dynamically evolving methodology system, it advises on catalyst composition, structure, synthesis strategy, and performance optimization. Covers HER / OER / ORR / PEMWE electrocatalysis; each advice item carries a source tag (literature-confirmed vs empirical) and confidence, with an actionable validation path. Runs standalone or pairs with [catalyst-search](https://github.com/ANDYPENG09/catalyst-search).

## 兼容性 | Compatibility

本技能遵循标准 [Agent Skills](https://github.com/anthropics/agent-skills)（`SKILL.md`）格式，无脚本依赖。
This skill follows the standard [Agent Skills](https://github.com/anthropics/agent-skills) (`SKILL.md`) format with no script dependencies.

| 工具 Tool | 状态 Status | 说明 Note |
|---|---|---|
| Claude Code | ✅ | 原生支持 Native；`~/.claude/skills/` |
| Cursor | ✅ | `~/.cursor/skills/` |
| WorkBuddy | ✅ | SkillHub 生态 SkillHub ecosystem |
| QClaw | ✅ | OpenClaw 框架 |
| ima | ✅ | 知识号发布 |
| Codex (OpenAI) | ⚠️ | 需经 AGENTS.md 适配 Non-native; adapt via AGENTS.md |

> ✅ catalyst-design 无工具依赖，以上工具均可用。
> ✅ catalyst-design has no tool dependencies; works in all the above.

## 安装 | Install

**SkillHub CLI**（推荐 Recommended）：
```bash
skillhub install catalyst-design
```

**手动 Manual** — 将本仓库内容复制到对应工具的 skills 目录 / copy this repo into your tool's skills directory：
- Claude Code: `~/.claude/skills/catalyst-design/`
- Cursor: `~/.cursor/skills/catalyst-design/`

## 结构 | Structure
- `SKILL.md` — skill 入口 entry point
- `references/` — 设计方法论体系 / design methodology，可追溯台账 / traceability registry，更新协议 / update protocol
- `templates/` — 设计建议书模板 / design proposal template

## 配套 | Pairs with
[catalyst-search](https://github.com/ANDYPENG09/catalyst-search) — 催化文献检索技能 / catalysis literature search skill

## License
MIT
