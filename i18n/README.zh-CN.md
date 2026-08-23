<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**语言：** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · **简体中文** · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

这是一个面向 AI 辅助软件开发的最小化、供应商中立基线：便携的策略/上下文层，加上一小组可复用的工程流程。它不是 agent runtime（智能体运行环境）、orchestrator、installer 或 framework。

## 文件

- `AGENTS.md` — 共享的 always-on（始终生效）工程基线。
- `MODEL_ROUTING.md` — 稳定的质量/成本与 capability-tier（能力层级）策略。
- `MODEL_CATALOG.md` — 随时间变化的 runtime（运行环境）/model 目录。
- `CLAUDE.md` — Claude Code 指向 `AGENTS.md` 的轻量桥接。
- `skills/` — Harness-owned（归 Harness 所有）、canonical（权威来源）、on-demand（按需加载）的流程。
- `i18n/` — README 的本地化摘要。

## Rules（规则）与 skills（技能）：四层结构

| | Always-on | On-demand |
| --- | --- | --- |
| **共享** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **项目专属** | 项目自己的 rules/policy 机制 | 项目自己的 skills |

Harness 不提供单独的 `rules/` 目录。共享 always-on 规则的 canonical 来源已经是 `AGENTS.md`，模型路由策略位于 `MODEL_ROUTING.md`。再创建第二个权威的 always-on 来源只会带来重复和冲突风险。

领域规则、环境与部署拓扑、供应商/模型偏好、产品行为、业务规则和基础设施路径都应保留在项目本地。判断新的 guidance 应放在哪一层时，使用 `continuous-improvement` skill 中“选择最小、可长期维护 safeguard（保护机制）”的方法。

## 共享 skills

Skills 是面向具体任务的流程，不是 always-on policy。采用 progressive disclosure（渐进展示）时，通常 discovery 只暴露 metadata；完整 `SKILL.md` 内容仅在当前任务真正匹配时加载。

Harness-owned skills 的 canonical 来源是 `skills/`。Ownership marker（所有权标记）：

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

同名 skill 如果没有这个 key，就不属于 Harness，adoption（接入）或 update 时绝不能覆盖。

v2 包含 14 个 skills：

- `backup-and-recovery-review` — backup、restore 与 recovery 准备度。
- `interface-qa` — web、mobile、desktop、CLI 与 API 界面验证。
- `calculation-model-validation` — 公式与决策模型验证。
- `change-review` — 完成变更的回归与风险 review。
- `compatibility-and-rollout` — 兼容性、迁移、分阶段发布与回退。
- `high-risk-change-review` — 高风险变更的额外工程约束。
- `delegation-strategy` — 安全使用已验证的任务委派与并行处理。
- `dependency-change` — dependency 添加、删除与升级评估。
- `documentation-sync` — 让长期文档与实际系统保持一致。
- `environment-release-safety` — release/deployment 与审批边界安全。
- `continuous-improvement` — 将重复失败转化为持久保护机制。
- `root-cause-debug` — 找到并证明 root cause。
- `secret-exposure-response` — secret/credential exposure 响应。
- `cross-surface-consistency` — 多个 surface/channel 之间的行为一致性。

共享集合应保持在约 **20 个 skills 或更少**；每个 `description` 应为 **300 个字符以内**。

优先级：**project-local rules/policy > 共享 `AGENTS.md` baseline > shared skills**。任何 skill 都不能放宽 approval boundary、授权 scope、runtime capability 或 production/live safety。

## Adoption 与 update

可复制的操作 prompt 只保留一个 canonical 来源，不做翻译：

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption 根据 repository evidence 判断项目实际使用的 runtimes；机器上安装了 CLI 并不能单独作为证据。当前已验证的项目级 skill 路径：Cursor、Antigravity、Codex 使用 `.agents/skills/`；Claude Code 使用 `.claude/skills/`；Cursor 也能读取 `.claude/skills/`。如果一个已验证 root 能覆盖所有已检测 runtimes，只保存一份。无法验证 native activation（原生激活）时，使用 `harness/skills/` 作为 neutral fallback（中立备用方案），并且不能宣称 native activation 已生效。

写入任何 skill 之前，必须对所有 canonical skill 名称在所有目标 roots 做 collision（命名冲突）扫描。任何要修改的 managed（受管理）文件都必须在 repository 外进行 byte-for-byte backup。Harness-owned 副本必须与 canonical 来源保持 verbatim（逐字一致）。Update 永不迁移现有 skill 安装位置；upstream 已删除的 managed skill 也不会自动删除，而是报告为 orphaned（上游已不存在）。

## 删除与测试

没有自动 uninstaller。只有包含 `metadata.ai-engineering-harness` 的 skills 才能作为 Harness-owned 内容删除；project-local rules/skills 保持不变。参见 [Remove the shared skills](../README.md#remove-the-shared-skills)。

如果 native skill activation 无法验证，agent 不应声称 skill 已激活。与任务无关时，不应把所有 skill body 加入 context；只允许 discovery metadata 可见。参见 [How to test an installation](../README.md#how-to-test-an-installation)。

`SKILL.md` 文件不翻译；只保留一份 canonical English 版本。详细 maintenance、adoption/update 和 scope boundaries 请以 [English README](../README.md) 为准。
