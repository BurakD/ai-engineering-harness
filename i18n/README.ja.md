<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**言語:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · **日本語** · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

AI 支援ソフトウェア開発向けの最小構成で、vendor-neutral（ベンダー非依存）な基盤です。持ち運べるポリシー/コンテキスト層と、小さな再利用可能な手順群で構成されます。agent runtime（エージェント実行環境）、orchestrator（オーケストレーター）、installer（インストール機構）、framework（ソフトウェア基盤）ではありません。

## ファイル

- `AGENTS.md` — 共有の always-on（常時有効）エンジニアリング基盤。
- `MODEL_ROUTING.md` — 安定した品質/コストと capability tier（能力レベル）のポリシー。
- `MODEL_CATALOG.md` — 時間とともに更新される runtime（実行環境）/モデルカタログ。
- `CLAUDE.md` — Claude Code から `AGENTS.md` への軽量な橋渡し。
- `skills/` — Harness-owned（Harness 所有）、canonical（唯一の正本由来）、on-demand（必要時に読み込む）の手順。
- `i18n/` — README のローカライズ要約。

## ルールとスキル：4つの層

ここで rules（ルール）は常時適用される指針を、skills（スキル）は特定のタスクで使う手順を表します。

| | 常時有効 | 必要時 |
| --- | --- | --- |
| **共有** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **プロジェクト固有** | プロジェクト独自のルール/ポリシー機構 | プロジェクト独自のスキル |

AI Engineering Harness は別の `rules/` ディレクトリを配布しません。共有の always-on（常時有効）ルール層の canonical source（唯一の正本）はすでに `AGENTS.md` にあり、model routing（モデルルーティング）ポリシーは `MODEL_ROUTING.md` にあります。常時有効な正本をもう一つ作ると、重複と矛盾の原因になります。

Domain rules（ドメインルール）、environment/deployment topology（環境/デプロイ構成）、vendor/model preferences（ベンダー/モデル設定）、product behavior（製品動作）、business rules（ビジネスルール）、infrastructure paths（インフラパス）はプロジェクト固有のままにします。新しい指針をどの層に置くかは、`continuous-improvement` スキルの safeguard（恒久的な保護策）選択の考え方で判断します。

## 共有スキル

Skills（スキル）は task-specific procedures（タスク固有の手順）であり、always-on policy（常時有効ポリシー）ではありません。progressive disclosure（段階的表示）では、通常は discovery metadata（検出用メタデータ）のみを表示し、完全な `SKILL.md` 本文は現在のタスクに本当に適合した場合だけ読み込みます。

Harness-owned skills（Harness 所有スキル）の canonical source（唯一の正本）は `skills/` です。ownership marker（所有者マーカー）は次のとおりです。

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

同名の skill（スキル）にこのキーがなければ Harness-owned（Harness 所有）ではなく、adoption（導入）や update（更新）で上書きしてはいけません。

v2 は 14 個のスキルを含みます。

- `backup-and-recovery-review` — backup（バックアップ）、restore（復元）、recovery（復旧）の準備。
- `interface-qa` — web、mobile、desktop、CLI、API インターフェースの検証。
- `calculation-model-validation` — 数式と意思決定モデルの検証。
- `change-review` — 完了した変更の review（レビュー）、回帰、リスク確認。
- `compatibility-and-rollout` — compatibility（互換性）、migration（移行）、rollout（段階的リリース）、rollback（ロールバック）。
- `high-risk-change-review` — 高影響変更に対する追加の規律。
- `delegation-strategy` — 検証済みの delegation（委任）と parallelism（並列実行）の安全な利用。
- `dependency-change` — dependency（依存関係）の追加・削除・upgrade（バージョン更新）評価。
- `documentation-sync` — 長期的な文書を実態と同期。
- `environment-release-safety` — release（リリース）/deployment（デプロイ）の影響と approval（承認）の安全性。
- `continuous-improvement` — 繰り返す失敗を恒久的な safeguards（保護策）に変換。
- `root-cause-debug` — root cause（根本原因）を特定して証明。
- `secret-exposure-response` — secret（シークレット）と credential（認証情報）の exposure（露出）への対応。
- `cross-surface-consistency` — 複数の surface（操作面）にまたがる動作の一貫性。

共有セットはおおむね **20 個のスキル以下**に保ち、各 `description` は **300 文字以下**にします。

優先順位：**project-local rules/policy（プロジェクト固有のルール/ポリシー） > 共有 `AGENTS.md` 基盤 > shared skills（共有スキル）**。スキルは approval boundary（承認境界）、authorized scope（許可された範囲）、runtime capability（実行環境の能力）、production/live safety（本番/稼働中環境の安全性）を弱めてはいけません。

## 導入と更新

運用用の copy/paste prompts（コピー/貼り付け用プロンプト）は一つの canonical source（正本）に保ち、本文は翻訳しません。

- [導入プロンプト（英語）](../README.md#copypaste-adoption-prompt)
- [更新プロンプト（英語）](../README.md#copypaste-update-prompt)

Adoption（導入）は repository evidence（リポジトリ内の証拠）から使用中の runtimes（実行環境）を判定します。マシンに CLI が入っているだけでは証拠になりません。検証済みの project-level skill paths（プロジェクト単位のスキルパス）は、Cursor/Antigravity/Codex が `.agents/skills/`、Claude Code が `.claude/skills/` です。Cursor は `.claude/skills/` も読めます。一つの検証済み root（ルートディレクトリ）で全実行環境をカバーできるなら、一つのコピーだけを使用します。native activation（ネイティブ有効化）を検証できない場合は `harness/skills/` を neutral fallback（中立的な代替先）として使い、ネイティブ有効化済みとは主張しません。

スキルを書き込む前に、すべての canonical names（正本側の名前）をすべての target roots（対象ルートディレクトリ）で collision（名前衝突）確認します。変更する managed files（管理対象ファイル）は repository（リポジトリ）外に byte-for-byte（バイト単位で完全一致）のバックアップを作ります。Harness-owned（Harness 所有）のコピーは canonical source（正本）と verbatim（完全一致）に保ちます。update（更新）は既存の配置を移動しません。upstream（上流ソース）から削除された managed skill（管理対象スキル）も自動削除せず、orphaned（上流に存在しない状態）として報告します。

## 削除とテスト

自動 uninstaller（アンインストール機構）はありません。ownership marker（所有者マーカー）`metadata.ai-engineering-harness` を持つ managed skills（管理対象スキル）だけを削除対象とし、project-local skills/rules（プロジェクト固有のスキル/ルール）は変更しません。詳しくは [共有スキルの削除（英語）](../README.md#remove-the-shared-skills) を参照してください。

native skill activation（スキルのネイティブ有効化）を検証できない場合、agent（エージェント）はそのスキルが active（有効）だと主張してはいけません。無関係なタスクでは、すべての skill bodies（スキル本文）を context（コンテキスト）へ読み込まず、discovery metadata（検出用メタデータ）だけが見える状態にします。詳しくは [導入のテスト（英語）](../README.md#how-to-test-an-installation) を参照してください。

`SKILL.md` は翻訳せず、canonical English copy（唯一の正本となる英語コピー）を一つだけ維持します。詳細な maintenance（保守）、adoption/update behavior（導入/更新の動作）、scope boundaries（範囲境界）は [英語 README](../README.md) を参照してください。
