<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**语言：** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · **简体中文** · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

这是一个面向 AI 辅助软件开发的最小化基线，采用 vendor-neutral（供应商中立）方式：由可移植的策略/上下文层和一小组可复用流程组成。它不是 agent runtime（智能体运行环境）、orchestrator（编排器）、installer（安装器）或 framework（软件框架）。

## 文件

- `AGENTS.md` — 共享、always-on（始终生效）的工程基线。
- `MODEL_ROUTING.md` — 稳定的质量/成本与 capability tier（能力层级）策略。
- `MODEL_CATALOG.md` — 随时间变化的 runtime（运行环境）/模型目录。
- `CLAUDE.md` — Claude Code 指向 `AGENTS.md` 的轻量桥接。
- `skills/` — Harness-owned（归 Harness 所有）、canonical（来自唯一权威来源）、on-demand（按需加载）的流程。
- `i18n/` — README 的本地化摘要。

## 规则与技能：四层结构

这里的 rules（规则）表示持续生效的指导，skills（技能）表示用于特定任务的流程。

| | 始终生效 | 按需 |
| --- | --- | --- |
| **共享** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **项目专属** | 项目自己的规则/策略机制 | 项目自己的技能 |

AI Engineering Harness 不提供单独的 `rules/` 目录。共享的 always-on（始终生效）规则层已经以 `AGENTS.md` 作为 canonical source（唯一权威来源），model routing（模型路由）策略位于 `MODEL_ROUTING.md`。再增加第二个始终生效的来源只会带来重复和冲突风险。

Domain rules（领域规则）、environment/deployment topology（环境/部署拓扑）、vendor/model preferences（供应商/模型偏好）、product behavior（产品行为）、business rules（业务规则）和 infrastructure paths（基础设施路径）都保留在项目内。判断新指导应放在哪一层时，应使用 `continuous-improvement` 技能中的 safeguard（持久防护措施）选择方法。

## 共享技能

Skills（技能）是 task-specific procedures（面向特定任务的流程），不是 always-on policy（始终生效的策略）。采用 progressive disclosure（渐进式展示）时，通常只显示 discovery metadata（发现元数据）；完整的 `SKILL.md` 内容只有在当前任务确实匹配时才加载。

Harness-owned skills（归 Harness 所有的技能）的 canonical source（唯一权威来源）是 `skills/`。Ownership marker（所有权标记）如下：

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

同名 skill（技能）如果没有这个键，就不是 Harness-owned（归 Harness 所有）的内容，在 adoption（安装）或 update（更新）期间绝不能覆盖。

v2 包含 14 个技能：

- `backup-and-recovery-review` — backup（备份）、restore（还原）与 recovery（恢复）准备。
- `interface-qa` — web、mobile、desktop、CLI 与 API 界面验证。
- `calculation-model-validation` — 公式与决策模型验证。
- `change-review` — 已完成变更的 review（审查）、回归与风险检查。
- `compatibility-and-rollout` — compatibility（兼容性）、migration（迁移）、rollout（分阶段发布）与 rollback（回退）。
- `high-risk-change-review` — 高影响变更的额外工程约束。
- `delegation-strategy` — 安全使用已验证的 delegation（任务委派）与 parallelism（并行执行）。
- `dependency-change` — dependency（依赖项）的添加、删除与 upgrade（版本升级）评估。
- `documentation-sync` — 让长期文档与实际系统保持一致。
- `environment-release-safety` — release（发布）/deployment（部署）影响与 approval（审批）安全。
- `continuous-improvement` — 将重复失败转化为持久 safeguards（防护措施）。
- `root-cause-debug` — 找到并证明 root cause（根本原因）。
- `secret-exposure-response` — 响应 secret（机密）与 credential（凭据）的 exposure（暴露）。
- `cross-surface-consistency` — 保持多个 surface（交互面）之间的行为一致。

共享集合应保持在约 **20 个技能或更少**；每个 `description` 应为 **300 个字符以内**。

优先级：**project-local rules/policy（项目本地规则/策略） > 共享 `AGENTS.md` 基线 > shared skills（共享技能）**。任何技能都不能放宽 approval boundary（审批边界）、authorized scope（授权范围）、runtime capability（运行环境能力）或 production/live safety（生产/在线安全）。

## 安装与更新

可复制/粘贴的操作 prompts（提示词）只保留一个 canonical source（权威来源），并且不翻译其正文：

- [安装提示词（英文）](../README.md#copypaste-adoption-prompt)
- [更新提示词（英文）](../README.md#copypaste-update-prompt)

Adoption（安装）根据 repository evidence（代码库证据）判断实际使用的 runtimes（运行环境）；机器上安装了 CLI 并不能单独作为证据。已验证的 project-level skill paths（项目级技能路径）：Cursor/Antigravity/Codex 使用 `.agents/skills/`，Claude Code 使用 `.claude/skills/`；Cursor 也能读取 `.claude/skills/`。如果一个已验证的 root（根目录）覆盖所有检测到的运行环境，只保存一份。无法验证 native activation（原生活化）时，使用 `harness/skills/` 作为 neutral fallback（中立备用方案），并且不能宣称已经原生活化。

写入任何技能之前，必须在所有 target roots（目标根目录）中检查全部 canonical names（权威来源名称）的 collision（名称冲突）。任何要修改的 managed files（受管理文件）都必须在 repository（代码库）外进行 byte-for-byte（逐字节）备份。Harness-owned（归 Harness 所有）的副本必须与 canonical source（权威来源）保持 verbatim（逐字一致）。Update（更新）不会迁移现有安装位置；upstream（上游来源）已删除的 managed skill（受管理技能）也不会自动删除，而是报告为 orphaned（上游已不存在）。

## 删除与测试

没有自动 uninstaller（卸载器）。只有带有 ownership marker（所有权标记）`metadata.ai-engineering-harness` 的 managed skills（受管理技能）才会被删除；project-local skills/rules（项目本地技能/规则）保持不变。参见 [删除共享技能（英文）](../README.md#remove-the-shared-skills)。

如果无法验证 native skill activation（技能原生活化），agent（智能体）不应声称该技能 active（已激活）。处理无关任务时，不应把全部 skill bodies（技能正文）加载进 context（上下文）；只允许 discovery metadata（发现元数据）可见。参见 [测试安装（英文）](../README.md#how-to-test-an-installation)。

`SKILL.md` 文件不翻译；只保留一份 canonical English copy（唯一权威英文副本）。详细 maintenance（维护）、adoption/update behavior（安装/更新行为）和 scope boundaries（范围边界）请以 [英文 README](../README.md) 为准。
