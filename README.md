# pm-agent

> 通用 PM 流程编排引擎 — 一句话输入，8 模块 DAG 全流程自动执行
>
> Universal PM workflow orchestration engine — one-line input, 8-module DAG pipeline auto-execution

[![Platform](https://img.shields.io/badge/Platform-WorkBuddy%20|%20Cursor%20|%20Codex%20|%20Claude%20Code-blue)](https://github.com/cyj4578/pm-agent)
[![Version](https://img.shields.io/badge/version-v5.0-brightgreen)](https://github.com/cyj4578/pm-agent)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## 一句话概述 / Overview

输入一句需求描述，自动串联 **市场调研 → 竞品分析 → 功能清单 → PRD 文档 → TE 逻辑审查 → 系统架构 → UI 原型 → 技术实现**，生成完整的可交付产品文档包。

Input a single requirement description. Automatically chains **Market Research → Competitive Analysis → Feature Checklist → PRD Document → TE Logic Review → System Architecture → UI Prototype → Technical Implementation**, producing a complete deliverable product documentation package.

---

## DAG 工作流 / DAG Workflow

```
                    ┌──────────────┐
                    │  Step 1      │
                    │  市场调研     │
                    │  Mkt Research│
                    └──────┬───────┘
                    ┌──────┴───────┐
                    │  Step 2      │
                    │  竞品分析     │
                    │  Comp. Allys │
                    └──────┬───────┘
                           │
                    ┌──────┴───────┐
                    │  Step 3      │
                    │  功能清单     │
                    │  Features    │
                    └──────┬───────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        Step 3-PRD   Step 3-TE    (质量关卡)
         PRD 文档    TE 逻辑审查  Quality Gate
              │            │    on_failure: ask
              └─────┬──────┘
                    ▼
         ┌──────────────────┐
         │  Step 4          │
         │  系统架构         │
         │  Architecture    │
         ├──────────────────┤
         │  Step 5          │
         │  UI 原型          │
         │  UI Prototype    │
         ├──────────────────┤
         │  Step 6          │
         │  技术实现         │
         │  Tech Impl       │
         └──────────────────┘
```

---

## 8 大模块 / 8 Modules

| # | 模块 / Module | 输入 / Input | 输出 / Output |
|---|--------------|-------------|---------------|
| 1 | 市场调研 / Market Research | 产品方向 / Product direction | 市场规模、用户画像、趋势判断 / Market size, user personas, trends |
| 2 | 竞品分析 / Competitive Analysis | 调研结论 / Research findings | 竞品矩阵、差异化机会 / Competitor matrix, differentiation |
| 3 | 功能清单 / Feature Checklist | 调研+竞品 / Research + competitors | 功能列表、优先级标注 / Feature list with priorities |
| 3-PRD | PRD 文档 / PRD Document | 功能清单 / Feature checklist | 完整需求文档 / Complete requirements doc |
| 3-TE | TE 审查 / TE Review | PRD | 逻辑漏洞检测、需求一致性检验 / Logic flaw detection, consistency check |
| 4 | 系统架构 / System Architecture | 功能清单+PRD+TE / Features + PRD + TE | 架构图、技术选型 / Architecture diagram, tech stack |
| 5 | UI 原型 / UI Prototype | 功能清单 / Feature checklist | 页面结构、交互流程 / Page structure, interaction flow |
| 6 | 技术实现 / Tech Implementation | 所有上游模块 / All upstream modules | 实现计划、任务拆分 / Implementation plan, task breakdown |

---

## 支持的 AI 工具 / Supported AI Tools

| 工具 / Tool | 安装方式 / Installation |
|-------------|------------------------|
| **WorkBuddy** | `clawhub install cyj4578/pm-agent` → `@skill:pm-agent <需求>` |
| **Cursor** | 复制到 `.cursorrules` 或 `.cursor/rules/pm-agent.mdc` / Copy to `.cursorrules` or `.cursor/rules/pm-agent.mdc` |
| **Codex (OpenAI)** | 粘贴到 System Prompt / Project Instructions / Paste into System Prompt or Project Instructions |
| **Claude Code** | 粘贴到 `CLAUDE.md` / Paste into `CLAUDE.md` |
| **VS Code Copilot** | 保存为 `.github/instructions.md` / Save as `.github/instructions.md` |
| **Cline / Continue** | 保存 `.md` 文件，在界面中加载 / Save as `.md` and load in UI |
| **通用 / Generic** | 复制 `SKILL.md` 全文，粘贴为初始提示词 / Copy full `SKILL.md` as initial prompt |

---

## 快速开始 / Quick Start

### WorkBuddy

```bash
clawhub install cyj4578/pm-agent
```

然后在对话中输入 / Then in conversation:

```
@skill:pm-agent 开发一个面向医疗机构的智能导诊系统
```

### Cursor / Codex / Claude Code

复制 [SKILL.md](SKILL.md) 全文，粘贴到对应工具的系统提示词区域，然后发送 / Copy [SKILL.md](SKILL.md) and paste as system prompt, then send:

```
执行完整 DAG 流程：开发一个面向医疗机构的智能导诊系统
```

### 单独调用模块 / Call Individual Modules

```
执行 module:market-research（输入：在线教育 AI 辅导赛道）
执行 module:feature-checklist 和 module:prd-document（并行执行）
仅执行 module:te-review（审查已有 PRD，不生成新文档）
```

---

## 版本历史 / Version History

| 版本 / Version | 日期 / Date | 变更 / Changes |
|---------------|-------------|----------------|
| v5.0 | 2026-06-03 | 跨平台重构：自包含万能引擎，去除平台依赖 / Cross-platform refactor: self-contained engine, platform-independent |
| v4.0 | 2026-06-03 | Skill Package 重构：8 子模块合并为单一包 / Package refactor: 8 sub-modules merged into single package |
| v3.0 | 2026-06-03 | 集成 TE 逻辑审查，质量关卡 / Integrated TE logic review, quality gate |
| v2.0 | 2026-06-02 | 7 Step DAG 工作流 / 7-step DAG workflow |
| v1.0 | 2026-06-02 | 初始版本 / Initial release |

---

## License

MIT © [cyj4578](https://github.com/cyj4578)
