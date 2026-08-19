# AI Engineering Harness

**Sprachen:** [English](README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · **Deutsch** · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

<!-- Based on README.md @ 088ed75fe790d2b1626ab1c222b2623246966c9b -->

Eine minimale, anbieterneutrale Grundlage für KI-gestützte Softwareentwicklung.

Beim Wechsel zwischen KI-Coding-Tools oder Modellen geht häufig der Engineering-Kontext eines Projekts verloren und muss erneut erklärt werden. AI Engineering Harness ist eine kleine, portable Policy- und Kontextschicht, die genau das verhindert. Es ist weder Agent-Runtime noch Orchestrator; Cursor, Claude Code, Codex und Antigravity bringen ihre eigenen Ausführungs- und Orchestrierungsfunktionen mit.

## Was es löst

1. Projektkontext und Engineering-Disziplin über Tool- und Modellwechsel hinweg erhalten.
2. Qualität und Kosten ausbalancieren, indem stärkeres Reasoning nur bei entsprechender Komplexität oder Risiko eingesetzt wird.
3. Modell-/Runtime-Entscheidungen aktuell halten, ohne kurzlebige Modellnamen in stabile Policies einzubrennen.

## Dateien

- `AGENTS.md` — gemeinsame Engineering-Baseline für kompatible Coding Agents.
- `MODEL_ROUTING.md` — stabile FAST / STANDARD / REASONING / FRONTIER-Policy.
- `MODEL_CATALOG.md` — zeitabhängiger Modell-/Runtime-Katalog mit aktuellen Empfehlungen.
- `CLAUDE.md` — minimaler Adapter, damit Claude Code `AGENTS.md` einbindet.
- `README.md` — zentrale Anleitung für Adoption, Updates, Tests und Wartung.

## Was es ist — und was nicht

Der eigentliche Wert liegt in den Policies: repository-first Kontext, Routing-Tiers, fail-closed Prüfung von Runtime-Capabilities, menschliche Freigabe nach Wirkung, Scope-Disziplin, dauerhafter Handoff und sichere Adoption/Updates.

Es ist kein Workflow-Engine, Multi-Agent-Framework, Runtime, Regel-Synchronisierer oder Ersatz für tool-native Rules/Skills.

## Kompatibilität

`AGENTS.md` ist eine externe, toolübergreifende Konvention. Runtimes, die sie direkt lesen, benötigen keinen Harness-spezifischen Adapter. Claude Code nutzt `CLAUDE.md`; deshalb enthält dieses Repository nur die minimale Brücke `@AGENTS.md`. Antigravity-spezifische Mechanismen wie `.agents/skills/` und `.agents/workflows/` bleiben projektlokal.

## Adoption in einem bestehenden Projekt

1. Im aktuellen Repository und Branch bleiben.
2. Vor Änderungen Regeln, Docs, Git-Status, Deployment-Topologie und Validierungsbefehle durch einen geeigneten Agent untersuchen lassen.
3. Vor jeder Änderung an einer bestehenden Datei ein bytegenaues Backup außerhalb des Repositories erstellen.
4. Projektspezifische Inhalte vollständig bewahren und nur Shared-Harness-Inhalte ergänzen.
5. Keine Branches, Worktrees, Installer, Manifeste, Adapter oder Sync-Mechanismen nur für die Adoption erzeugen.
6. Ohne ausdrückliche Freigabe kein Commit, Push, Deploy oder Publish.

**Vollständiger Adoption-Prompt:** [Englisches README](README.md#copypaste-adoption-prompt)

## Update

Ein Update erneuert nur Harness-eigene Shared-Inhalte. `AGENTS.md`, `MODEL_ROUTING.md`, `MODEL_CATALOG.md` und der Shared-Teil von `CLAUDE.md` werden aus Upstream aktualisiert, während projektspezifische Regeln, Modelle, Skills, Docs, Code und uncommittete Arbeit erhalten bleiben.

**Vollständiger Update-Prompt:** [Englisches README](README.md#copypaste-update-prompt)

## Zentrale Prinzipien

- Repository-Wahrheit muss Modell- und Agent-Wechsel überleben.
- Ergänzen statt ersetzen: tool-native Regeln bleiben an ihrem Ort.
- `MODEL_ROUTING.md` ist stabil; `MODEL_CATALOG.md` ist bewusst zeitabhängig.
- Die aktive Runtime ist maßgeblich dafür, welche Modelle/Agents tatsächlich aufrufbar sind.
- Das Entdecken eines Problems ist keine Autorisierung für eine Änderung außerhalb des angeforderten Scopes.
- High-impact Aktionen benötigen menschliche Freigabe aufgrund ihrer Wirkung, nicht aufgrund von Tool- oder Umgebungsnamen.
- Tests, Linters, Typen, CI und andere deterministische Kontrollen sind wiederholtem Modellurteil vorzuziehen, wenn sie dieselbe Regel zuverlässig durchsetzen können.

## Installation testen

In frischen Sessions testen: structural smoke test, real-task behavior test, approval-boundary test und cross-tool runtime-capability test. Der Agent muss Kontext korrekt entdecken und darf niemals Capabilities behaupten, die die aktive Runtime nicht verifizieren kann.

Exakte Prompts: [How to test an installation](README.md#how-to-test-an-installation)

## Lizenz

Open Source unter **Apache License 2.0**.