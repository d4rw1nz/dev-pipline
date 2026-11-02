# 操作说明

使用 `$dev-pipline <操作> <目标>`，也可以直接描述工作。根据意图选择操作，在约定范围内持续执行。

| 操作 | 工作内容 |
| --- | --- |
| init | 建立必要的 README、AGENTS.md、文档与 Make 入口，有实际任务时建立 Issue |
| adopt | 分析现有结构、调用、数据、构建和历史，按授权范围完成调整 |
| research | 查证问题，更新同主题结论；需要跟进时在 Issue 中保留下一步 |
| require | 明确目标与验收，小任务写入 Issue，长期产品说明更新需求文档 |
| connect | 使用已有工具读取外部任务，记录来源和必要结论 |
| run | 完成指定任务 |
| loop | 按依赖与优先级完成已授权的任务集合 |
| test | 验证当前实现，记录真实结果与失败事项 |
| review | 检查完整改动，按需安排独立复审；仅要求审查时交付发现与建议 |
| resume | 读取当前任务、源码和来源，核实已有结果后继续 |
| status | 只读核实进度，区分本地验收、提交、远端状态和发布 |
| learn | 将可复用经验更新到已有规则、文档或测试 |
| tidy | 原位精简重复与过时内容，压缩已结束 Issue，保留未解决问题 |

任务完成条件见 [执行流程](workflow.md)，记录格式见 [Markdown Issue](issue-contract.md)。

## 初始化与接入

检查目录、Git、已有规则和工具，按实际需要维护文档。选型尚未确定时注明未知，命令以实际可运行入口为准。

Makefile 复用现有工具，执行 help 与相关检查。按 [写入规则](documentation.md#agentsmd-写入) 将模板固定规则原文合入 AGENTS.md，并填入本项目职责、路径和命令。仅要求文档初始化时，修改限于文档范围。

## 研究与需求

研究区分事实、假设与建议，记录来源、版本、工作区情况和适用限制。未成功的实验只保留影响结论的内容。

需要保存的需求更新同一 Issue 或文档，描述用户行为、验收条件和待确认项。明确要求实现的部分直接执行，关键产品选择缺失时再确认。外部任务链接保存在 Issue 的 `source` 字段中。

## 用法示例

```text
$dev-pipline init 初始化项目开发约定
$dev-pipline adopt 分析现有结构并调整模块职责
$dev-pipline research 查清取消请求后页面仍更新的原因
$dev-pipline require 支持断网后恢复上传
$dev-pipline connect 读取指定 GitHub Issue
$dev-pipline run docs/issues/upload-resume.md
$dev-pipline loop 完成指定的两项待办任务
$dev-pipline resume docs/issues/upload-resume.md
```
