---
name: dev-pipline
description: 指导软件项目初始化、接入、功能开发、bug 修复和架构调整。使用 Markdown Issue 记录任务，按需维护文档与 Make 入口，完成研究、实现、验证、复审和经验维护。遵循不向后兼容、Git 历史查证与中文提交约定。普通问答直接回答。
---

# dev-pipline 开发流程

按任务范围组织研究、实现和验证。需要持续跟进的任务使用带 YAML 头信息的 Markdown Issue，保存当前情况与下一步。

## 共同原则

- 从用户目标、业务规则、数据归属和实际环境确定方案。正式开发交付完整可用的行为，并处理相关失败情形；用户明确要求原型时按原型目标验收。
- 默认不向后兼容。更新受控调用方，删除旧格式、重复状态和过渡实现；核实实际数据与外部协议的影响，完成必要转换。
- 目录、模块、依赖和生命周期应体现清楚的职责。修 bug 前理解相关调用与数据变化，在根因所属位置修复。
- 结合当前源码、未提交改动和相关 Git 历史查证。研究结论与已确认需求分别记录。
- Make 提供统一开发入口；已有项目逐步接入，复用可靠脚本。任务进度维护在对应 Issue，长期规则维护在项目文档或测试中。
- 使用子代理前读取 [子代理规则](assets/AGENTS.md.template#子代理)，说明适用场景、具体收益与交付物；其余工作由主 agent 完成。
- 初始化、接入项目或同步规则时，按 [AGENTS.md 写入规则](references/documentation.md#agentsmd-写入) 将模板中的固定规则原文写入项目 AGENTS.md。
- 在已授权范围内持续完成工作。提交、推送、外部回写与发布分别遵守当前授权。

## 开始工作

1. 读取适用的 AGENTS.md、README、需求与模块说明，检查工作区改动，查阅相关任务和历史。
2. 明确交付类型与可观察的完成条件，按 [阶段指导](references/stages.md) 确定工作深度。
3. 需要跨轮推进或后续跟进时，按 [Issue 记录规则](references/issue-contract.md) 更新同一任务文件。普通问答和无需跟进的小改在回复中说明即可。
4. 确认实际构建、格式化和测试命令。已有 Make 入口直接使用；缺少时按 [Make 接入](references/make.md) 先使用可靠的现有入口。
5. 自行查证事实；影响产品选择且无法推断的信息向用户确认，同时继续不受影响的工作。

## 操作与规则

使用 `$dev-pipline <操作> <目标>`，也可直接描述工作。操作范围和示例见 [操作说明](references/commands.md)。

| 当前工作 | 规则 |
| --- | --- |
| `init` / `adopt` | [文档结构](references/documentation.md)、[Make 入口](references/make.md)、[交付检查](references/gates.md)；已有项目另读 [项目接入](references/project-adoption.md) |
| `research` / `require` | [文档结构](references/documentation.md)：更新同主题内容，小任务的目标与验收直接写入 Issue |
| `connect` | [任务来源](references/sources.md)：使用已有工具读取指定任务，记录来源与必要结论 |
| `run` / `loop` / `resume` | [任务执行](references/workflow.md)：完成条件、持续推进与中断恢复 |
| 界面设计、实现或审查 | [界面规则](assets/AGENTS.md.template#界面)：文案、交互、排版、颜色、对齐与动画 |
| bug、架构、接口或外部集成 | [架构与根因修复](references/architecture.md)、[Git 历史与提交](references/git.md) |
| `test` / `review`、代码交付 | [验证与复审](references/quality.md)：独立设计测试，首轮验证后深度复审，按需安排交叉复审 |
| 交付 | [完成条件](references/workflow.md)、[交付检查](references/gates.md)、[交付内容整理](references/quality.md#交付内容整理) |
| `learn` / `tidy`、需求结束 | [知识维护](references/knowledge.md)：保存可复用结论，更新已有规则或测试 |
| `status`、提交或 PR | 只读核实进度；提交与 PR 遵循 [中文 Git 规范](references/git.md) |

文件按实际用途创建。验证结果简记在 Issue 或交付回复中，临时材料按 [保存规则](references/documentation.md#验证材料的保存) 处理。
