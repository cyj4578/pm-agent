# pm-agent

> 通用 PM 流程编排引擎 — 一句话输入，8 模块 DAG 全流程自动执行

[![Platform](https://img.shields.io/badge/Platform-WorkBuddy%20|%20Cursor%20|%20Codex%20|%20Claude%20Code-blue)](https://github.com/cyj4578/pm-agent)
[![Version](https://img.shields.io/badge/version-v5.0-brightgreen)](https://github.com/cyj4578/pm-agent)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

## 一句话概述

输入一句需求描述，自动串联 **市场调研 → 竞品分析 → 功能清单 → PRD 文档 → TE 逻辑审查 → 系统架构 → UI 原型 → 技术实现**，生成完整的可交付产品文档包。

## DAG 工作流

```
                    ┌──────────────┐
                    │  Step 1      │
                    │  市场调研     │
                    └──────┬───────┘
                    ┌──────┴───────┐
                    │  Step 2      │
                    │  竞品分析     │
                    └──────┬───────┘
                           │
                    ┌──────┴───────┐
                    │  Step 3      │
                    │  功能清单     │
                    └──────┬───────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        Step 3-PRD   Step 3-TE    (质量关卡)
          PRD 文档   TE 逻辑审查  on_failure: ask
              │            │
              └─────┬──────┘
                    ▼
         ┌──────────────────┐
         │  Step 4          │
         │  系统架构         │
         ├──────────────────┤
         │  Step 5          │
         │  UI 原型          │
         ├──────────────────┤
         │  Step 6          │
         │  技术实现         │
         └──────────────────┘
```

## 8 大模块

| # | 模块 | 输入 | 输出 |
|---|------|------|------|
| 1 | 市场调研 | 产品方向 | 市场规模、用户画像、趋势判断 |
| 2 | 竞品分析 | 调研结论 | 竞品矩阵、差异化机会 |
| 3 | 功能清单 | 调研+竞品 | 功能列表、优先级标注 |
| 3-PRD | PRD 文档 | 功能清单 | 完整需求文档（PRD） |
| 3-TE | TE 审查 | PRD | 逻辑漏洞检测、需求一致性检验 |
| 4 | 系统架构 | 功能清单+PRD+TE | 架构图、技术选型 |
| 5 | UI 原型 | 功能清单 | 页面结构、交互流程 |
| 6 | 技术实现 | 所有上游模块 | 实现计划、任务拆分 |

## 支持的 AI 工具

| 工具 | 安装方式 |
|------|----------|
| **WorkBuddy** | `clawhub install cyj4578/pm-agent` → `@skill:pm-agent <需求>` |
| **Cursor** | 复制到 `.cursorrules` 或 `.cursor/rules/pm-agent.mdc` |
| **Codex (OpenAI)** | 粘贴到 System Prompt / Project Instructions |
| **Claude Code** | 粘贴到 `CLAUDE.md` |
| **VS Code Copilot** | 保存为 `.github/instructions.md` |
| **Cline / Continue** | 保存 `.md` 文件，在界面中加载 |
| **通用** | 复制 `SKILL.md` 全文，粘贴为初始提示词 |

## 快速开始

### WorkBuddy

```bash
clawhub install cyj4578/pm-agent
```

然后在对话中输入：

```
@skill:pm-agent 开发一个面向医疗机构的智能导诊系统
```

### Cursor / Codex / Claude Code

复制 [SKILL.md](SKILL.md) 全文，粘贴到对应工具的系统提示词区域，然后发送：

```
执行完整 DAG 流程：开发一个面向医疗机构的智能导诊系统
```

### 单独调用模块

```
执行 module:market-research（输入：在线教育 AI 辅导赛道）
执行 module:feature-checklist 和 module:prd-document（并行执行）
仅执行 module:te-review（审查已有 PRD，不生成新文档）
```

## 版本历史

| 版本 | 日期 | 变更 |
|------|------|------|
| v5.0 | 2026-06-03 | 跨平台重构：自包含万能引擎，去除平台依赖 |
| v4.0 | 2026-06-03 | Skill Package 重构：8 子模块合并为单一包 |
| v3.0 | 2026-06-03 | 集成 TE 逻辑审查，质量关卡 |
| v2.0 | 2026-06-02 | 7 Step DAG 工作流 |
| v1.0 | 2026-06-02 | 初始版本 |

## License

MIT © [cyj4578](https://github.com/cyj4578)
