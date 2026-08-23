<!-- Based on README.md @ v2.0.0 -->
# AI Engineering Harness

**Sprachen:** [English](../README.md) · [Türkçe](README.tr.md) · [Español](README.es.md) · [Português (Brasil)](README.pt-BR.md) · **Deutsch** · [Français](README.fr.md) · [Русский](README.ru.md) · [简体中文](README.zh-CN.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [العربية](README.ar.md) · [हिन्दी](README.hi.md)

Eine minimale Grundlage für AI-gestützte Softwareentwicklung mit vendor-neutral (anbieterneutral) ausgerichteter Policy-/Kontextschicht und einem kleinen Satz wiederverwendbarer Verfahren. Sie ist kein agent runtime (Agenten-Laufzeitsystem), kein orchestrator (Orchestrator zur Koordination), kein installer (Installationswerkzeug) und kein Framework.

## Dateien

- `AGENTS.md` — gemeinsame, always-on (stets aktive) Engineering-Basis.
- `MODEL_ROUTING.md` — stabile Qualitäts-/Kosten- und capability tier (Fähigkeitsstufen)-Policy.
- `MODEL_CATALOG.md` — zeitabhängiger runtime (Laufzeitumgebungs)-/Modellkatalog.
- `CLAUDE.md` — schlanke Brücke von Claude Code zu `AGENTS.md`.
- `skills/` — Harness-owned (dem Harness zugehörige), canonical (aus der maßgeblichen Quelle stammende), on-demand (bei Bedarf geladene) Verfahren.
- `i18n/` — lokalisierte README-Zusammenfassungen.

## Regeln und Fähigkeiten: vier Schichten

Hier stehen rules (Regeln) für dauerhaft geltende Vorgaben und skills (Fähigkeiten) für Verfahren, die bei bestimmten Aufgaben eingesetzt werden.

| | Stets aktiv | Bei Bedarf |
| --- | --- | --- |
| **Gemeinsam** | `AGENTS.md` + `MODEL_ROUTING.md` | `skills/` |
| **Projektspezifisch** | Eigener Regel-/Policy-Mechanismus des Projekts | Eigene Fähigkeiten des Projekts |

AI Engineering Harness liefert bewusst kein separates `rules/`-Verzeichnis. Die gemeinsame always-on (stets aktive) Regelschicht hat ihre canonical source (einzige maßgebliche Quelle) bereits in `AGENTS.md`; die model routing (Modellweiterleitungs)-Policy liegt in `MODEL_ROUTING.md`. Eine zweite stets aktive Quelle würde Duplikate und Konfliktrisiken erzeugen.

Domain rules (Domänenregeln), environment/deployment topology (Umgebungs-/Deployment-Topologie), vendor/model preferences (Anbieter-/Modellpräferenzen), product behavior (Produktverhalten), business rules (Geschäftsregeln) und infrastructure paths (Infrastrukturpfade) bleiben projektspezifisch. Für neue Vorgaben verwenden Sie den safeguard (dauerhafte Schutzmaßnahme)-Ansatz aus dem Skill `continuous-improvement`.

## Gemeinsame Fähigkeiten

Skills (Fähigkeiten) sind task-specific procedures (aufgabenspezifische Verfahren), keine always-on policy (stets aktive Policy). Bei progressive disclosure (schrittweiser Offenlegung) ist normalerweise nur discovery metadata (Metadaten zur Erkennung) sichtbar; der vollständige Inhalt von `SKILL.md` wird nur geladen, wenn die Aufgabe wirklich passt.

Die canonical source (einzige maßgebliche Quelle) für Harness-owned skills (dem Harness zugehörige Fähigkeiten) ist `skills/`. Der ownership marker (Eigentumsmarker) lautet:

```yaml
metadata:
  ai-engineering-harness: "2.0.0"
```

Ein gleichnamiger skill (Fähigkeit) ohne diesen Schlüssel ist nicht Harness-owned (dem Harness zugehörig) und darf bei adoption (Installation) oder update (Aktualisierung) niemals überschrieben werden.

v2 enthält 14 Fähigkeiten:

- `backup-and-recovery-review` — Bereitschaft für Backup, Restore und Recovery.
- `interface-qa` — Prüfung von Web-, Mobile-, Desktop-, CLI- und API-Schnittstellen.
- `calculation-model-validation` — Validierung von Formeln und Entscheidungsmodellen.
- `change-review` — Review abgeschlossener Änderungen, Regressionen und Risiken.
- `compatibility-and-rollout` — compatibility (Kompatibilität), migration (Migration), rollout (schrittweise Einführung) und rollback (Rücknahme).
- `high-risk-change-review` — zusätzliche Disziplin für Änderungen mit hohem Risiko.
- `delegation-strategy` — sicherer Einsatz verifizierter delegation (Delegation) und parallelism (Parallelität).
- `dependency-change` — Bewertung von Dependency-Hinzufügung, -Entfernung und Upgrades.
- `documentation-sync` — dauerhafte Dokumentation mit der Realität synchron halten.
- `environment-release-safety` — Sicherheit von Release/Deployment und approval (Freigabe).
- `continuous-improvement` — wiederkehrende Fehler in dauerhafte safeguards (Schutzmaßnahmen) überführen.
- `root-cause-debug` — root cause (Grundursache) identifizieren und belegen.
- `secret-exposure-response` — Reaktion auf exposure (Offenlegung) von Secrets und Credentials.
- `cross-surface-consistency` — Verhaltenskonsistenz über mehrere surfaces (Oberflächen) hinweg.

Der gemeinsame Satz sollte ungefähr **20 Fähigkeiten oder weniger** umfassen; `description` sollte **höchstens 300 Zeichen** lang sein.

Priorität: **project-local rules/policy (projektspezifische Regeln/Policy) > gemeinsame `AGENTS.md`-Basis > shared skills (gemeinsame Fähigkeiten)**. Ein Skill darf approval boundaries (Freigabegrenzen), authorized scope (autorisierten Umfang), runtime capabilities (Fähigkeiten der Laufzeitumgebung) oder production/live safety (Produktions-/Live-Sicherheit) niemals abschwächen.

## Installation und Aktualisierung

Operative copy/paste prompts (Prompts zum Kopieren/Einfügen) bleiben in einer einzigen canonical source (maßgeblichen Quelle) und werden nicht übersetzt:

- [Installations-Prompt (Englisch)](../README.md#copypaste-adoption-prompt)
- [Aktualisierungs-Prompt (Englisch)](../README.md#copypaste-update-prompt)

Adoption (Installation) erkennt verwendete runtimes (Laufzeitumgebungen) aus repository evidence (Repository-Nachweisen); ein installierter CLI allein reicht nicht. Verifizierte project-level skill paths (Fähigkeitspfade auf Projektebene): `.agents/skills/` für Cursor/Antigravity/Codex und `.claude/skills/` für Claude Code; Cursor kann ebenfalls `.claude/skills/` lesen. Deckt ein verifizierter root (Wurzelpfad) alle erkannten Laufzeitumgebungen ab, wird nur eine Kopie verwendet. Ist native activation (native Aktivierung) nicht verifizierbar, wird `harness/skills/` als neutral fallback (neutrale Ausweichlösung) verwendet und keine native Aktivierung behauptet.

Vor jedem Schreiben werden alle canonical names (Namen der maßgeblichen Quelle) in allen target roots (Ziel-Wurzelpfaden) auf collision (Namenskollisionen) geprüft. Geänderte managed files (verwaltete Dateien) werden byte-for-byte (bytegenau) außerhalb des Repository gesichert. Harness-owned (dem Harness zugehörige) Kopien bleiben verbatim (wortgetreu identisch) zur canonical source (maßgeblichen Quelle). Ein update (Aktualisierung) verschiebt vorhandene Installationen nicht; ein upstream (in der übergeordneten Quelle) entfernter managed skill (verwalteter Skill) wird nicht automatisch gelöscht, sondern als orphaned (in der Quelle nicht mehr vorhanden) gemeldet.

## Entfernung und Tests

Es gibt keinen automatischen uninstaller (Deinstallationsmechanismus). Nur managed skills (verwaltete Fähigkeiten) mit dem ownership marker (Eigentumsmarker) `metadata.ai-engineering-harness` werden entfernt; project-local skills/rules (projektspezifische Fähigkeiten/Regeln) bleiben unangetastet. Siehe [Gemeinsame Fähigkeiten entfernen (Englisch)](../README.md#remove-the-shared-skills).

Kann native skill activation (native Aktivierung einer Fähigkeit) nicht verifiziert werden, darf der agent (Agent) nicht behaupten, die Fähigkeit sei active (aktiv). Bei einer unpassenden Aufgabe dürfen nicht alle skill bodies (Fähigkeitsinhalte) in den context (Kontext) geladen werden; nur discovery metadata (Erkennungsmetadaten) darf sichtbar sein. Siehe [Installation testen (Englisch)](../README.md#how-to-test-an-installation).

`SKILL.md`-Dateien werden nicht übersetzt; es bleibt eine canonical English copy (einzige maßgebliche englische Kopie). Für detaillierte maintenance (Wartung), adoption/update behavior (Installations-/Aktualisierungsverhalten) und scope boundaries (Umfangsgrenzen) gilt das [englische README](../README.md).
