<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Sprachen:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · **Deutsch** · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Eine minimale, anbieterneutrale Grundlage für KI-gestützte Softwareentwicklung: eine portable Policy-/Kontextschicht plus ein kleiner Satz wiederverwendbarer Verfahren. Kein Agent-Runtime (Ausführungsumgebung für Agenten), Orchestrator, Installer oder Framework.

## Dateien

- `AGENTS.md` — gemeinsame Engineering-Baseline, always-on (stets aktiv).
- `MODEL_ROUTING.md` — stabile Qualitäts-/Kosten- und capability-tier (Fähigkeitsstufen)-Policy.
- `MODEL_CATALOG.md` — zeitabhängiger runtime (Ausführungsumgebung)-/Modellkatalog.
- `CLAUDE.md` — dünne Claude-Code-Brücke zu `AGENTS.md`.
- `skills/` — Harness-owned (Harness-eigene), canonical (maßgebliche Quelle), on-demand (bei Bedarf) Verfahren.
- `i18n/` — lokalisierte README-Zusammenfassungen.

## Regeln und skills (Fähigkeiten): vier Schichten

| | Always-on | On-demand |
| --- | --- | --- |
| **Gemeinsam** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Projektspezifisch** | Eigener Rule-/Policy-Mechanismus des Projekts | Eigene Skills des Projekts |

Der Harness liefert bewusst kein separates `rules/`-Verzeichnis aus. Die canonical Quelle der gemeinsamen always-on Regelschicht ist bereits `AGENTS.md`; die Modellrouting-Policy liegt in `MODEL_ROUTING.md`. Eine zweite maßgebliche always-on Quelle würde Duplikate und Konfliktrisiken erzeugen.

Domainregeln, Environment-/Deployment-Topologie, Anbieter-/Modellpräferenzen, Produktverhalten, Geschäftsregeln und Infrastrukturpfade bleiben projektspezifisch. Für die Entscheidung, in welche Schicht neue Guidance gehört, verweist der Harness auf den Skill `continuous-improvement` und dessen Prinzip des kleinsten dauerhaften safeguard (Schutzmechanismus).

## Gemeinsame Skills

Skills sind aufgabenbezogene Verfahren, keine always-on Policy. Bei progressive disclosure (schrittweiser Offenlegung) sollte für Discovery normalerweise nur Metadata sichtbar sein; der vollständige `SKILL.md`-Inhalt wird erst geladen, wenn die Aufgabe tatsächlich passt.

Canonical Quelle der Harness-owned Skills ist `skills/`. Der ownership marker (Eigentumsmarker) ist:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Ein gleichnamiger Skill ohne diesen Schlüssel ist nicht Harness-owned und darf bei adoption (Übernahme) oder Update niemals überschrieben werden.

v2 enthält 14 Skills:

- `backup-and-recovery-review` — Backup-, Restore- und Recovery-Bereitschaft.
- `interface-qa` — Prüfung von Web-, Mobile-, Desktop-, CLI- und API-Interfaces.
- `calculation-model-validation` — Validierung von Formeln und Entscheidungsmodellen.
- `change-review` — Review abgeschlossener Änderungen, Regressionen und Risiken.
- `compatibility-and-rollout` — Kompatibilität, Migration, schrittweise Einführung und Rücknahme.
- `high-risk-change-review` — zusätzliche Disziplin für Änderungen mit hohem Risiko.
- `delegation-strategy` — sicherer Einsatz verifizierter Delegation und Parallelisierung.
- `dependency-change` — Bewertung von Dependency-Hinzufügung, -Entfernung und Upgrades.
- `documentation-sync` — dauerhafte Dokumentation mit der Realität synchron halten.
- `environment-release-safety` — Release-/Deployment-Sicherheit und Approval-Grenzen.
- `continuous-improvement` — wiederkehrende Fehler in dauerhafte Schutzmechanismen überführen.
- `root-cause-debug` — Root Cause identifizieren und belegen.
- `secret-exposure-response` — Reaktion auf Secret-/Credential-Exposition.
- `cross-surface-consistency` — Verhaltenskonsistenz über mehrere Oberflächen hinweg.

Der gemeinsame Satz sollte ungefähr **20 Skills oder weniger** umfassen; `description` sollte **höchstens 300 Zeichen** lang sein.

Priorität: **projektspezifische Regeln/Policy > gemeinsame `AGENTS.md`-Baseline > gemeinsame Skills**. Ein Skill darf Approval-Grenzen, autorisierten Scope, Runtime-Capabilities oder Production/Live-Sicherheit niemals abschwächen.

## Adoption und Update

Operative Copy/Paste-Prompts bleiben in einer einzigen canonical Quelle und werden nicht übersetzt:

- [Canonical adoption prompt](../README.md#copypaste-adoption-prompt)
- [Canonical update prompt](../README.md#copypaste-update-prompt)

Adoption erkennt verwendete Runtimes aus Repository-Evidenz; ein installierter CLI allein reicht nicht. Verifizierte Projekt-Skill-Pfade: `.agents/skills/` für Cursor, Antigravity und Codex; `.claude/skills/` für Claude Code. Cursor kann ebenfalls `.claude/skills/` lesen. Deckt ein verifizierter Root alle erkannten Runtimes ab, wird nur eine Kopie verwendet. Ist native activation (native Aktivierung) nicht verifizierbar, wird `harness/skills/` als neutral fallback (neutrale Ausweichoption) verwendet und keine native Aktivierung behauptet.

Vor jedem Skill-Write werden alle canonical Namen in allen Ziel-Roots auf collisions (Kollisionen) geprüft. Geänderte managed (verwaltete) Dateien werden bytegenau außerhalb des Repositories gesichert. Harness-owned Kopien bleiben verbatim (wortgetreu) zur canonical Quelle. Updates verschieben vorhandene Skill-Installationen nicht; upstream entfernte managed Skills werden nicht automatisch gelöscht, sondern als orphaned (ohne Upstream-Gegenstück) gemeldet.

## Entfernung und Tests

Es gibt keinen automatischen Uninstaller. Nur Skills mit `metadata.ai-engineering-harness` werden als Harness-owned entfernt; projektspezifische Regeln und Skills bleiben unangetastet. Siehe [Remove the shared skills](../README.md#remove-the-shared-skills).

Kann native Skill-Aktivierung nicht verifiziert werden, darf der Agent nicht behaupten, der Skill sei aktiv. Bei einer nicht passenden Aufgabe dürfen nicht alle Skill-Bodies in den Kontext geladen werden; nur Discovery-Metadata darf sichtbar sein. Siehe [How to test an installation](../README.md#how-to-test-an-installation).

`SKILL.md`-Dateien werden nicht übersetzt; es bleibt eine canonical englische Kopie. Für detaillierte Wartung, Adoption/Update und Scope-Grenzen gilt das [englische README](../README.md).
