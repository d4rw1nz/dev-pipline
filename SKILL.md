---
name: dev-pipline
description: 软件项目开发指南：初始化或接入已有项目，落地 docs、AGENTS.md、Make 入口和项目内 Issue 管理，接入 GitHub/Linear 等来源，按研究、需求、实现、独立测试、交叉复审、反思形成可恢复的自动开发闭环。用于功能开发、bug 修复、架构整理和长期经验沉淀；遵循第一性原理、不向后兼容、Git 历史证据与中文提交。纯问答无需完整流程。
---

# dev-pipline 开发流程

本 skill 指导目标项目建立和使用开发流程。项目自己的 CLI、Issue 数据、静态页面和门禁留在项目内，与产品运行代码隔离。指南、模板与实际可用能力要分别说明。

## 共同原则

- 创建 subagent 前必须读取并满足 [子代理规则](assets/AGENTS.md.template#子代理)，说明本次属于哪种场景、具体收益和独立交付物；不符合条件时由主 agent 完成，不为凑流程创建子代理。
- 架构、Agent 和界面规则统一维护在 [AGENTS.md 模板](assets/AGENTS.md.template)。初始化、接入项目或用户要求同步这些规则时，按 [AGENTS.md 写入规则](references/documentation.md#agentsmd-写入) 将完整原文写入目标项目的 AGENTS.md，不能只留在 skill 中或用链接代替正文。
- 正式开发完整交付已承诺范围，处理真实失败；不能用演示代码、假数据、吞错或临时拼接交差。快速开发靠聚焦范围和复用可靠能力。只有用户要求以原型为交付目标时才按原型验收；定位、研究和验证所需的隔离实验属于正常工作，不能代替正式实现。
- 从用户结果、业务规则、数据归属和实际限制推导方案。默认不向后兼容：更新受控调用方，删除旧格式、重复状态和过渡实现；查清实际用户数据与外部协议的影响，必要的数据转换一次完成，不长期维护双实现。
- 组织即架构，架构即组织：目录、模块、依赖、状态写入者和生命周期管理者表达一致职责。修 bug 必须理解相关项目架构、完整调用与状态流，再决定根因修复；不能只在报错行加条件，也不能无依据全仓重写。
- 信息不足先查证。结合相关 Git 提交图、引入、合并、回退、历史修复和当前未提交差异判断；不凭个人偏好改架构或代码风格，不把研究建议自动当成已确认需求。
- Make 是统一开发入口；已有项目逐步接入，复用可靠底层工具。长期反馈和工程经验落地并主动召回，执行状态只在项目任务记录维护。
- 按当前授权持续完成工作，不重复确认已有授权；本 skill 不自动扩大范围或授权提交、推送、发布、外部写入。

## 先判断任务和项目现状

1. 读取适用的 AGENTS.md、README、需求和模块说明，检查现有改动，召回相关任务、长期反馈、经验与历史。
2. 确定本次交付是研究、需求、文档、审查、原型还是正式代码；按 [阶段指导](references/stages.md) 选择投入，不按仓库年龄判断。
3. 需要保存任务时先读 [Issue 契约](references/issue-contract.md)：复用已有体系；尚未建立工具时由单一协调者保存最小项目记录，继续原任务。普通 bug 不顺带建设完整 CLI 和页面。`status` 保持只读，纯问答不创建任务。
4. 找到实际构建、格式化、测试入口与版本。已有 Make 直接复用；缺少 Make 时按 [Make 接入](references/make.md) 使用可靠现有入口、按范围逐步统一，不能把工具未接入当成无法修 bug。
5. 明确可观察的验收、事实与未知；能自行查证的先查，只有影响产品选择且无法推断的缺口才询问。按下表读取当前任务需要的规则。

## 操作与规则入口

使用 `$dev-pipline <操作> <目标>`，也接受中文意图；这些是 skill 识别的操作，不是多个原生斜杠命令。入口范围与示例见 [操作说明](references/commands.md)。

| 当前工作 | 读取并执行 |
| --- | --- |
| `init` / `adopt` | [文档结构](references/documentation.md)、[Make](references/make.md)、[项目门禁](references/gates.md)；已有项目另读 [现有项目分析](references/project-adoption.md)。按 [写入规则](references/documentation.md#agentsmd-写入) 落地 [AGENTS.md 模板](assets/AGENTS.md.template) 中的完整规则，并适配项目约定 |
| `research` / `require` | [文档结构](references/documentation.md)：研究与需求必须文件落地，逐轮更新同一主题；验收内容由需求文件维护 |
| `connect` | [来源接入](references/sources.md)：实际配置、验证与记录，不能用占位适配器声称已接通 |
| `run` / `loop` / `resume` | [自动闭环](references/workflow.md)：任务类型、完成条件、恢复与停止规则；[门禁](references/gates.md) 核实适用证据 |
| 界面设计、实现或 review | [AGENTS.md 模板中的界面规则](assets/AGENTS.md.template#界面)：文案、交互、排版、颜色、形状与对齐、动画 |
| bug、架构、接口、界面或外部集成 | [架构与问题修复](references/architecture.md) 及 [Git 历史与提交](references/git.md)：内含 geju 的目标判断、方案取舍与可证伪验证 |
| `test` / `review`、正式代码交付 | [验证与复审](references/quality.md)：实现与测试独立设计，单测行覆盖率以 80% 为目标；首轮验证后做 deep-review，需要独立审阅时按子代理规则安排交叉复审，修正后重验与复核 |
| 任务结束或交付内容 | 按 [闭环完成条件](references/workflow.md) 验收；执行 [quality 中的 sanitize-artifacts](references/quality.md)，保留真实限制与未执行项，清除对话和制作过程残留 |
| `learn` / `tidy`、每个需求的反思 | [知识维护](references/knowledge.md)：落实长期反馈，判断经验是否值得保存，优先修正已有知识与可执行检查，不凑总结数量 |
| `status`、提交或 PR | 状态报告区分本地验收、远端状态、提交与发布；实际提交和 PR 遵循 [中文 Git 规范](references/git.md) |

不要为凑齐流程创建空文档或执行无关检查。具体任务的结束条件统一维护在 workflow，测试与复审细则维护在 quality，其他文件引用它们。
