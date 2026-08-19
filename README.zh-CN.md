# AI Engineering Harness

**语言：** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · **简体中文** · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

一个用于 AI 辅助软件开发的最小化、厂商中立基础层。

在不同 AI 编程工具或模型之间切换，往往会丢失项目的工程上下文并需要重新解释。AI Engineering Harness 是一个小型、可移植的策略与上下文层，用来避免这种情况。它不是 Agent Runtime，也不是编排器；Cursor、Claude Code、Codex 和 Antigravity 各自提供执行与编排能力。

## 它解决什么问题

1. 在切换工具或模型时保持项目上下文与工程纪律。
2. 只在复杂度或风险值得时使用更强推理，从而平衡质量与成本。
3. 在不把短生命周期模型名称写死进稳定策略的前提下，让模型/runtime 选择保持更新。

## 文件

- `AGENTS.md` — 供兼容 coding agent 使用的共享工程基线。
- `MODEL_ROUTING.md` — 稳定的 FAST / STANDARD / REASONING / FRONTIER 策略。
- `MODEL_CATALOG.md` — 随时间变化的模型/runtime 目录和当前建议。
- `CLAUDE.md` — 让 Claude Code 导入 `AGENTS.md` 的最小适配器。
- `README.md` — adoption、更新、测试和维护的主要说明。

## 它是什么，也不是什么

核心价值在策略内容：repository-first 上下文、routing tiers、runtime capability 的 fail-closed 验证、按影响定义的人类审批、scope 纪律、可持续 handoff 与安全更新。

它不是 workflow engine、multi-agent framework、runtime、规则同步生成器，也不会取代各工具自己的 rules/skills。

## 兼容性

`AGENTS.md` 是外部的 cross-tool 约定。能直接读取它的 runtime 不需要 Harness 专用适配器。Claude Code 使用 `CLAUDE.md`，因此本仓库只包含最小的 `@AGENTS.md` 桥接。Antigravity 特有的 `.agents/skills/`、`.agents/workflows/` 等机制仍保持为 project-local。

## 接入现有项目

1. 保持在当前 repository 和 branch。
2. 修改前让合适的 agent 检查规则、docs、Git 状态、deployment 拓扑与 validation 命令。
3. 修改任何现有文件前，在 repository 外创建 byte-for-byte backup。
4. 保留所有 project-specific 内容，只添加 Harness 的 shared 内容。
5. 不要仅为了采用 Harness 创建 branch、worktree、installer、manifest、adapter 或 sync 机制。
6. 未经明确批准，不要 commit、push、deploy 或 publish。

**完整 adoption prompt：** [英文 README](README.md#copypaste-adoption-prompt)

## 更新

更新只刷新 Harness-owned shared 内容。`AGENTS.md`、`MODEL_ROUTING.md`、`MODEL_CATALOG.md` 和 `CLAUDE.md` 的 shared 部分从 upstream 更新，同时保留项目本地 rules、models、skills、docs、code 和未提交工作。

**完整 update prompt：** [英文 README](README.md#copypaste-update-prompt)

## 关键原则

- Repository 中的事实应当跨模型和 agent 切换持续存在。
- 只添加，不替换：tool-native 规则留在原处。
- `MODEL_ROUTING.md` 稳定；`MODEL_CATALOG.md` 明确是时间敏感的。
- 当前 runtime 对实际可调用的模型/agent 拥有最终权威。
- 发现问题不等于获得修复超出 scope 问题的授权。
- 高影响操作是否需要人工批准，按实际效果判断，而不是按工具或环境名称判断。
- 如果 tests、linters、types、CI 等确定性机制能可靠执行同一规则，应优先于重复依赖模型判断。

## 测试安装

请在新的 session 中执行：structural smoke test、real-task behavior test、approval-boundary test 和 cross-tool runtime-capability test。Agent 应正确发现上下文，并且绝不能声称当前 runtime 无法验证的能力。

精确 prompts： [How to test an installation](README.md#how-to-test-an-installation)

## 许可证

基于 **Apache License 2.0** 开源。