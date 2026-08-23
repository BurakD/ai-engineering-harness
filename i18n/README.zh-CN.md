<!-- Based on README.md @ v2.0.3 -->
# AI Engineering Harness

语言：[English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · 简体中文 · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

面向 AI 辅助软件开发的最小化、供应商中立（vendor-neutral）策略/上下文层，并配有一小组可复用流程。它不是 agent runtime（智能体运行环境）、orchestrator（编排系统）、installer（安装工具）或 framework（软件框架）。

## 你会得到什么

- 跨工具的一套 engineering baseline（工程基线）。Cursor、Claude Code、Codex 和 Antigravity 读取相同的 project context（项目上下文）与 constraints（约束），因此切换工具不意味着重新解释项目。
- 模型选择由风险决定，而不是由习惯决定。工作会被划分到 capability tiers（能力层级），并从最低的足够层级开始。这是 policy（策略），不是 enforcement（强制执行）：实际能节省多少取决于 active runtime（当前运行环境）和你的套餐。
- 为出错代价高的工作准备好流程。Secret exposure（机密泄露）、releases（发布）、dependency changes（依赖变更）、high-risk changes（高风险变更）和 recovery（恢复）各有共享流程，而且任何流程都不能放宽 approval boundary（审批边界）。
- Discovery（发现）不等于 authorization（授权）。Agent（智能体）发现任务范围外的问题时，会先报告并等待决定，而不是自行修复。
- 对 capabilities（能力）采取 fail closed（无法验证时按不可用处理）。Agent 不得声称 active runtime 实际无法提供的 model（模型）、subagent（子智能体）或 skill activation（技能激活）能力。
- Context（上下文）保持精简。共享流程只在任务匹配时加载，而不是填满每个 session（会话）。
- Low lock-in（低锁定）。内容就是 repository（代码库）里的 Markdown，没有 installer、runtime 或 service（服务）。Adoption（安装）和 removal（移除）都是有文档的流程，而不是单向门。

## 文件

- `AGENTS.md` — 共享的 always-on（始终生效）工程基线。
- `MODEL_ROUTING.md` — 稳定的质量/成本与 capability tier（能力层级）策略。
- `MODEL_CATALOG.md` — 随时间变化的 runtime（运行环境）和模型目录。
- `CLAUDE.md` — Claude Code 指向 `AGENTS.md` 的轻量桥接。
- `skills/` — 来自 Harness-owned（归 Harness 所有）、canonical（唯一权威）来源并按 on-demand（按需加载）方式使用的流程。
- `i18n/` — `README.md` 的本地化摘要。

## Rules（规则）与 skills（技能）：四层结构

Rules 是持续生效的指导；skills 是在特定任务中启用的流程。

| | Always-on（始终生效） | On-demand（按需） |
| --- | --- | --- |
| 共享 | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| 项目专属 | 项目自己的 rules/policy 机制 | 项目自己的 skills |

Harness 不提供单独的 `rules/` 目录：共享 always-on 规则层的 canonical source（唯一权威来源）已经是 `AGENTS.md`，模型路由策略位于 `MODEL_ROUTING.md`。第二个 always-on 来源只会带来重复和冲突风险。

领域规则、环境与 deployment（部署）拓扑、供应商/模型偏好、产品行为、业务规则和基础设施路径都保持项目专属。判断新指导应放在哪一层时，使用 `continuous-improvement` skill 中选择最小持久 safeguard（防护措施）的方法。

## 共享 skills（技能）

Skills 是面向具体任务的流程，不是 always-on policy。采用 progressive disclosure（渐进式展示）时，通常只显示 discovery metadata（发现元数据）；完整 `SKILL.md` 内容仅在任务真正匹配时加载。

Harness-owned skills 的 canonical source 是 `skills/`，ownership marker（所有权标记）如下：

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

同名 skill 如果没有这个键，就不是 Harness-owned；在 adoption（安装）或 update（更新）期间不会被覆盖。

v2 包含 14 个 skills：

- `backup-and-recovery-review` — 检查 backup（备份）、restore（还原）与 recovery（恢复）的准备情况。
- `interface-qa` — 验证 web、mobile、desktop、CLI 与 API 界面。
- `calculation-model-validation` — 验证公式与决策模型。
- `change-review` — 检查已完成变更的回归与风险。
- `compatibility-and-rollout` — 兼容性、migration（数据/模式迁移）、rollout（分阶段发布）与 rollback（回退）。
- `high-risk-change-review` — 对高影响变更施加额外纪律。
- `delegation-strategy` — 使用已验证的 delegation（任务委派）与并行工作。
- `dependency-change` — 检查 dependency（依赖项）的添加、删除与版本升级。
- `documentation-sync` — 让长期文档与实际情况保持同步。
- `environment-release-safety` — release（发布）和 deployment（部署）的影响及审批安全。
- `continuous-improvement` — 将重复错误转化为持久 safeguards（防护措施）。
- `root-cause-debug` — 查找并证明根本原因，而不是只处理症状。
- `secret-exposure-response` — 响应 secret（机密）与 credential（凭据）泄露。
- `cross-surface-consistency` — 保持多个界面之间的行为一致性。

共享集合应保持在约 20 个 skills 或更少；`description` 字段应为 300 个字符或更短。

优先级顺序：项目专属 rules/policy > 共享 `AGENTS.md` 基线 > 共享 skills。任何 skill 都不能放宽 approval boundary（审批边界）、authorized scope（授权范围）、runtime capability（运行环境能力）或 production/live safety（生产/在线安全）规则。

## Adoption（安装）与 update（更新）

复制/粘贴 prompts 只保留在一个 canonical source 中，并且不翻译：

- [安装 prompt（英文）](../README.md#copypaste-adoption-prompt)
- [更新 prompt（英文）](../README.md#copypaste-update-prompt)

Adoption 根据 repository evidence（代码库中的证据）判断实际使用的 runtimes；机器上安装了 CLI 并不能单独作为依据。已验证的项目级 skill 路径如下：Cursor、Antigravity 和 Codex 使用 `.agents/skills/`；Claude Code 使用 `.claude/skills/`。Cursor 也可以读取 `.claude/skills/`。如果一个已验证的 root（根目录）覆盖所有正在使用的 runtimes，只保存一份副本。无法验证 native activation（原生激活）时，使用 `harness/skills/` 作为 neutral fallback（中立备用方案），并且不能声称 native activation 已完成。

写入任何 skill 之前，必须在所有目标 roots 中检查全部 canonical 名称是否发生 collision（名称冲突）。如果要修改 managed（受管理）skill，则在 repository 外创建 byte-for-byte（逐字节一致）备份。Harness-owned 副本与 canonical 来源保持 verbatim（逐字一致）。Update 不会迁移现有 skill 位置；upstream（上游来源）已删除的 managed skill 也不会自动删除，而是报告为 orphaned（上游已不存在）。

## 删除与测试

没有自动 uninstaller（卸载工具）。只有带有所有权标记 `metadata.ai-engineering-harness` 的 managed skills 才会被删除；项目专属 skills 和 rules 不会被修改。参见 [删除共享 skills（英文）](../README.md#remove-the-shared-skills)。

如果安装测试中无法验证 native activation，agent 不应声称 skill 已激活。处理无关任务时，skill 正文不应加载进 context（上下文）；只应显示 discovery metadata。参见 [测试安装（英文）](../README.md#how-to-test-an-installation)。

`SKILL.md` 文件不翻译；只保留一份 canonical 英文副本。详细维护、adoption/update 行为和范围边界以 [英文 `README.md`](../README.md) 为准。
