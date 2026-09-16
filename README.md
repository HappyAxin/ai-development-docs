# AI Development Docs

> 为 AI 辅助开发保留可维护、可追溯、可验证的过程文档。

`ai-development-docs` 是一个可同时用于 Codex 和 Claude 的 Agent Skill。它会根据开发任务的规模与风险，指导 AI 创建或维护需求分析、技术方案、开发里程碑、AI 开发记录、验证证据和交付总结，避免代码完成后无人知道“为什么这样改、AI 做了什么、如何验证”。

## 适用场景

- 新增用户功能或业务能力
- 修复非简单缺陷或线上问题
- 重构核心模块
- 调整接口、数据结构或服务边界
- 进行架构迁移、兼容改造或分阶段发布
- 审查代码变更是否缺少配套过程文档

这个 Skill 不要求为每个小改动创建一套大而全的文档。它会按风险分级，小任务可以把必要信息合并在一个文件中。

## 核心能力

- 检查并延续项目已有的 `docs/` 目录和命名规范
- 根据任务风险选择最小但完整的文档集合
- 区分计划、实际完成、未验证和遗留事项
- 记录 AI 参与范围及人工审阅结果
- 要求测试、构建和人工验证具有真实证据
- 记录需求、设计与最终实现之间的偏差
- 在涉及架构变化时补充 ADR、迁移、兼容、观测和回滚信息
- 避免保存内部思维链、完整聊天记录和敏感数据

## 文档分级

| 任务级别 | 典型情况 | 最小文档集合 |
|---|---|---|
| 小型修改 | 局部、低风险、无契约或数据变化 | 一份 AI 开发记录，包含范围、变更、验证和风险 |
| 标准功能 | 新增用户可见能力或跨多个文件、模块 | 需求分析、AI 开发记录、验证记录 |
| 重大功能 | 核心业务、高风险、跨系统或分阶段交付 | 需求分析、技术方案、里程碑、开发记录、验证记录、交付总结 |
| 架构变更 | 服务边界、公共接口、数据归属或部署拓扑变化 | 重大功能文档，加 ADR、迁移、兼容、观测和回滚说明 |

若项目已有明确规范，Skill 会优先遵守项目规范，不会擅自重组整个 `docs/` 目录。

## 仓库结构

```text
ai-development-docs/
├─ SKILL.md
├─ agents/
│  └─ openai.yaml
├─ references/
│  └─ document-standard.md
└─ assets/
   └─ templates/
      ├─ 需求分析模板.md
      ├─ 技术方案模板.md
      ├─ AI开发记录模板.md
      ├─ 测试验证模板.md
      └─ 功能交付总结模板.md
```

- `SKILL.md`：触发条件、执行流程、任务分级和证据要求。
- `references/document-standard.md`：完整的 AI 辅助开发过程文档规范。
- `assets/templates/`：可直接复制或由 AI 按任务调整的 Markdown 模板。
- `agents/openai.yaml`：Codex 的显示与默认提示配置；Claude 会忽略该文件。

## 安装

### Codex

安装为个人 Skill：

```bash
git clone https://github.com/HappyAxin/ai-development-docs.git ~/.codex/skills/ai-development-docs
```

Windows PowerShell：

```powershell
git clone https://github.com/HappyAxin/ai-development-docs.git "$env:USERPROFILE\.codex\skills\ai-development-docs"
```

安装后可以显式调用：

```text
使用 $ai-development-docs 为这个新增功能创建并持续维护过程文档。
```

也可以直接描述新增功能、复杂缺陷、核心重构或架构变更，Codex 会根据 Skill 的描述自动判断是否使用。

### Claude Code

安装为个人 Skill：

```bash
git clone https://github.com/HappyAxin/ai-development-docs.git ~/.claude/skills/ai-development-docs
```

仅在一个项目中使用时，也可以放到项目根目录：

```text
.claude/skills/ai-development-docs/
```

Claude Code 会发现其中的 `SKILL.md`，并在任务匹配时按需加载。

### Claude.ai

1. 在 GitHub 仓库中选择 **Code → Download ZIP**。
2. 在 Claude.ai 的自定义 Skills 设置中上传 ZIP。
3. 确认自定义 Skill 已启用。

自定义 Skills 的可用范围取决于 Claude.ai 当前套餐和代码执行设置。

### Claude API

可以把本仓库打包成 ZIP，通过 Anthropic Skills API 上传到工作区，然后在请求的 `container.skills` 中引用对应 Skill。通过 API 使用 Agent Skills 时，需要同时启用代码执行工具。

官方文档：

- [Agent Skills 概览](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)
- [使用 Skills API](https://platform.claude.com/docs/en/build-with-claude/skills-guide)

## 快速使用

### 新增功能

```text
使用 ai-development-docs 为“批量导出订单”建立过程文档。
先完成需求分析和技术方案，再制定开发里程碑；开发过程中持续更新 AI 开发记录，完成后补充验证和交付总结。
```

### 小型修改

```text
使用 ai-development-docs 记录“用户列表增加状态筛选”这个改动。
这是小型任务，尽量合并为一个文件，但必须包含范围、实际变更、验证证据和残余风险。
```

### 架构变更

```text
使用 ai-development-docs 为“通知模块拆分为独立服务”建立完整文档。
需要包括 ADR、迁移步骤、兼容策略、可观测性、回滚方案和分阶段里程碑。
```

### 检查已有变更

```text
使用 ai-development-docs 检查当前代码变更缺少哪些需求、设计、验证或交付记录，并补齐必要文档。
```

## 推荐输出结构

没有现有项目规范时，可以采用：

```text
docs/
├─ README.md
├─ EVOLUTION.md
├─ 01-总体规划/
├─ 02-需求管理/
├─ 03-架构设计/
├─ 04-详细设计/
├─ 05-开发规范/
├─ 06-测试与质量/
├─ 07-部署运维/
├─ 08-会议与讨论/
├─ 09-亮点总结/
└─ ai-process/
   └─ REQ-001-功能名称/
      ├─ 00-任务说明.md
      ├─ 01-实施计划.md
      ├─ 02-开发日志.md
      ├─ 03-验证记录.md
      └─ 04-交付总结.md
```

目录只是默认建议。已有项目应延续现有结构，避免为了套模板进行无关整理。

## 模板说明

| 模板 | 用途 |
|---|---|
| `需求分析模板.md` | 记录背景、目标、范围、业务规则、验收标准和待确认事项 |
| `技术方案模板.md` | 记录现状、总体设计、详细设计、方案权衡、风险、里程碑和验证方案 |
| `AI开发记录模板.md` | 记录 AI 参与、实际文件变更、关键决策、计划偏差和当前交付状态 |
| `测试验证模板.md` | 记录验收验证、自动化命令、人工验证、失败或未执行项目 |
| `功能交付总结模板.md` | 汇总已交付内容、验证结论、部署回滚、残余风险和维护入口 |

## 文档原则

### 应该记录

- 需求背景、范围和可检查的验收标准
- 关键方案、取舍以及重要决策的原因
- 实际修改的文件和影响范围
- AI 参与了哪些工作，哪些内容经过人工调整或拒绝
- 实际执行的测试命令、环境、结果和证据
- 已知问题、残余风险、回滚方式和后续负责人

### 不应该记录

- AI 的内部思维链
- 未经整理的完整聊天记录
- 密码、Token、连接串和生产环境凭证
- 未脱敏的生产数据或日志
- 没有实际执行却被写成“已经通过”的测试
- 为了满足目录形式而创建的空文档

## 完成标准

只有满足以下条件，任务文档才能标记为“已完成”：

- 验收标准逐项有结论
- 实际变更可以追溯到文件、提交或 PR
- 所声称的测试和验证具有真实证据
- 需求、设计和实现之间的偏差已经说明
- 遗留问题与残余风险具有明确状态
- 需要跟进的事项有负责人
- 文档与代码在同一任务、提交或 PR 中同步更新

存在关键未验证项时，应标记为“待验证”或“部分完成”，不能提前宣称完成。

## 更新

如果通过 Git 克隆安装，可以这样更新：

```bash
git -C ~/.codex/skills/ai-development-docs pull
```

Claude Code 用户将路径替换为：

```bash
git -C ~/.claude/skills/ai-development-docs pull
```

## 贡献

欢迎通过 Issue 或 Pull Request 提交：

- 更清晰的触发条件和任务分级建议
- 新的通用过程文档模板
- 针对真实项目验证过的改进
- Codex、Claude Code 或 Claude API 的兼容性修正

提交改动时，请说明适用场景、预期行为和验证方式，避免加入只适用于单个项目的强制规则。
