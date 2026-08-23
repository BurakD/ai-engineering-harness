<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**言語:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · **日本語** · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI 支援ソフトウェア開発のための、最小かつベンダー中立な基盤です。ポータブルな policy/context 層と、小さな再利用可能な engineering procedures で構成されます。Agent runtime、orchestrator、installer、framework ではありません。

## ファイル

- `AGENTS.md` — 共有 always-on engineering baseline。
- `MODEL_ROUTING.md` — 安定した品質/コストと capability-tier policy。
- `MODEL_CATALOG.md` — 時間とともに更新される runtime/model catalog。
- `CLAUDE.md` — Claude Code から `AGENTS.md` への薄い bridge。
- `skills/` — Harness-owned の canonical on-demand procedures。
- `i18n/` — README のローカライズ要約。

## Rules と skills：4 つの層

| | Always-on | On-demand |
| --- | --- | --- |
| **Shared** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Project-specific** | プロジェクト独自の rule/policy mechanism | プロジェクト独自の skills |

Harness は別の `rules/` ディレクトリを配布しません。共有 always-on rules の canonical source はすでに `AGENTS.md` にあり、model routing policy は `MODEL_ROUTING.md` にあります。2 つ目の canonical always-on source を作ると、重複と矛盾の原因になります。

Domain rules、environment/deployment topology、vendor/model preferences、product behavior、business rules、infrastructure paths は project-local のままにします。新しい guidance をどの層に置くかは、`continuous-improvement` skill の「最小の durable safeguard を選ぶ」考え方を使って判断します。

## Shared skills

Skills は task-specific procedures であり、always-on policy ではありません。通常、discovery では metadata のみを表示し、完全な `SKILL.md` body は現在のタスクに本当に適合した場合だけ読み込みます。

Harness-owned skills の canonical source は `skills/` です。Ownership marker：

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

同名 skill にこの key がなければ Harness-owned ではなく、adoption/update で上書きしてはいけません。

v2 は 14 skills を含みます：

- `backup-and-recovery-review` — backup/restore/recovery readiness。
- `interface-qa` — web、mobile、desktop、CLI、API interface validation。
- `calculation-model-validation` — formula と decision-model validation。
- `change-review` — 完了した変更の regression/risk review。
- `compatibility-and-rollout` — compatibility、migration、rollout、rollback。
- `high-risk-change-review` — 高リスク変更への追加 discipline。
- `delegation-strategy` — 検証済み delegation/parallelism の安全な利用。
- `dependency-change` — dependency の追加・削除・upgrade 評価。
- `documentation-sync` — durable documentation を実態と同期。
- `environment-release-safety` — release/deployment と approval boundary の安全性。
- `continuous-improvement` — 繰り返す failure を durable safeguard に変換。
- `root-cause-debug` — root cause を特定し証明。
- `secret-exposure-response` — secret/credential exposure 対応。
- `cross-surface-consistency` — 複数 surface/channel の挙動整合性。

Shared set はおおむね **20 skills 以下**に保ち、各 `description` は **300 文字以下**にします。

優先順位：**project-local rules/policy > shared `AGENTS.md` baseline > shared skills**。Skill は approval boundary、authorized scope、runtime capability、production/live safety を弱めてはいけません。

## Adoption と update

運用用 copy/paste prompt は 1 つの canonical source に保ち、翻訳しません：

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption は repository evidence から実際に使われる runtimes を検出します。マシンに CLI がインストールされているだけでは証拠になりません。検証済み project-level skill paths は、Cursor/Antigravity/Codex が `.agents/skills/`、Claude Code が `.claude/skills/` です。Cursor は `.claude/skills/` も読めます。1 つの検証済み root で全 runtimes をカバーできるなら 1 コピーだけ使用します。Native activation を検証できない場合は neutral `harness/skills/` を使い、native activation 済みとは主張しません。

Skill を 1 つでも書き込む前に、すべての canonical skill names をすべての target roots で collision scan します。変更する managed file は repository 外に byte-for-byte backup を作成します。Update は既存の skill placement を移動しません。Upstream から削除された managed skill も自動削除せず、orphaned として報告します。

## 削除とテスト

自動 uninstaller はありません。`metadata.ai-engineering-harness` を持つ skills だけが Harness-owned として削除対象になり、project-local rules/skills は変更しません。詳細は [Remove the shared skills](../README.md#remove-the-shared-skills)。

Native activation が検証できない runtime では、agent は skill が active だと主張してはいけません。無関係なタスクで全 skill body を context にロードしてはいけず、discovery metadata のみが見える状態を期待します。詳細は [How to test an installation](../README.md#how-to-test-an-installation)。

`SKILL.md` は翻訳せず、canonical English copy を 1 つだけ維持します。詳細な maintenance、adoption/update、scope boundaries は [English README](../README.md) を参照してください。
