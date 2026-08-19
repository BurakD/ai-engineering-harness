# AI Engineering Harness

**言語:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · [Deutsch](README.de.md) · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · **日本語** · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

AI支援ソフトウェア開発のための、最小構成でベンダー中立な基盤です。

AIコーディングツールやモデルを切り替えると、プロジェクトのエンジニアリング文脈が失われ、同じ説明をやり直すことがよくあります。AI Engineering Harness はそれを防ぐための、小さく移植可能なポリシー／コンテキスト層です。Agent Runtime やオーケストレータではありません。Cursor、Claude Code、Codex、Antigravity はそれぞれ独自の実行・オーケストレーション機能を提供します。

## 解決する課題

1. ツールやモデルを切り替えても、プロジェクト文脈とエンジニアリング規律を維持する。
2. 複雑さやリスクが正当化する場合にだけ強い reasoning を使い、品質とコストを両立する。
3. 短命なモデル名を安定ポリシーへ固定せず、モデル/runtime 選択を最新に保つ。

## ファイル

- `AGENTS.md` — 互換 coding agent 向けの共有エンジニアリング基盤。
- `MODEL_ROUTING.md` — 安定した FAST / STANDARD / REASONING / FRONTIER ポリシー。
- `MODEL_CATALOG.md` — 時間依存のモデル/runtime カタログと現在の推奨。
- `CLAUDE.md` — Claude Code が `AGENTS.md` を読み込むための最小アダプタ。
- `README.md` — adoption、更新、テスト、保守の主要ガイド。

## これは何か／何ではないか

中心的な価値はポリシー内容です。repository-first の文脈、routing tier、runtime capability の fail-closed 検証、影響ベースの人間承認、scope 規律、持続可能な handoff、安全な adoption/update を提供します。

workflow engine、multi-agent framework、runtime、ルール同期ジェネレータではなく、各ツール固有の rules/skills を置き換えるものでもありません。

## 互換性

`AGENTS.md` はこの repository 独自の形式ではなく、外部の cross-tool convention です。直接読み込める runtime には Harness 固有アダプタは不要です。Claude Code は `CLAUDE.md` を使うため、最小の `@AGENTS.md` ブリッジだけを含めています。Antigravity 固有の `.agents/skills/` や `.agents/workflows/` は project-local のままです。

## 既存プロジェクトへの導入

1. 現在の repository と branch のまま作業する。
2. 変更前に、適切な agent に rules、docs、Git 状態、deployment topology、validation コマンドを調査させる。
3. 既存ファイルを変更する前に、repository 外へ byte-for-byte backup を作る。
4. project-specific な内容をすべて保持し、Harness の shared content だけを追加する。
5. Harness 導入だけを理由に branch、worktree、installer、manifest、adapter、sync 機構を作らない。
6. 明示的な承認なしに commit、push、deploy、publish しない。

**完全な adoption prompt:** [英語 README](README.md#copypaste-adoption-prompt)

## 更新

更新対象は Harness-owned shared content のみです。`AGENTS.md`、`MODEL_ROUTING.md`、`MODEL_CATALOG.md`、`CLAUDE.md` の shared 部分を upstream から更新し、project-local rules、models、skills、docs、code、未コミット作業を保持します。

**完全な update prompt:** [英語 README](README.md#copypaste-update-prompt)

## 主要原則

- Repository の真実はモデルや agent の切り替えを越えて残るべきです。
- 置換ではなく追加。tool-native rules は元の場所に残します。
- `MODEL_ROUTING.md` は安定、`MODEL_CATALOG.md` は意図的に時間依存です。
- 実際に呼び出せるモデル/agent については active runtime が最終的な権威です。
- 問題を発見したことは、依頼 scope 外の修正権限を意味しません。
- High-impact 操作はツール名や環境名ではなく、その影響に基づいて人間承認を必要とします。
- tests、linters、types、CI などの deterministic safeguard が同じルールを確実に enforce できるなら、繰り返しの model judgment より優先します。

## インストールのテスト

新しい session で structural smoke test、real-task behavior test、approval-boundary test、cross-tool runtime-capability test を行います。Agent は文脈を正しく発見し、active runtime が検証できない capability を決して主張してはいけません。

正確な prompts: [How to test an installation](README.md#how-to-test-an-installation)

## ライセンス

**Apache License 2.0** の下でオープンソース公開されています。