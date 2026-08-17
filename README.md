# AI Engineering Harness

A minimal, vendor-neutral baseline for AI-assisted software development.

The harness is designed to solve two practical problems:

1. Keep project context and engineering discipline durable when switching between tools or models.
2. Balance quality and cost by using stronger reasoning only when task complexity or risk justifies it.

It intentionally stays small. The repository itself is the handoff mechanism; there is no required installer, orchestrator, model gateway, or project-specific framework.

## Files

- `AGENTS.md` — shared engineering baseline used by compatible coding agents.
- `MODEL_ROUTING.md` — FAST / STANDARD / REASONING / FRONTIER quality-cost routing policy.
- `CLAUDE.md` — thin Claude Code adapter that points to `AGENTS.md`.
- `README.md` — adoption and maintenance guidance.
- `LICENSE` — Apache License 2.0.
- `CONTRIBUTING.md` — contribution guidance.

## License

This project is open source under the **Apache License 2.0**.

You may use, modify, redistribute, and use the project commercially under the license terms. Copyright, license, patent, trademark, and attribution obligations remain governed by `LICENSE`.

Contributions are welcome and are submitted under the Apache License 2.0 unless explicitly stated otherwise, as described in `CONTRIBUTING.md`.

## Core principles

### Repository truth survives model switches

A new model or agent should be able to reconstruct the current state from the repository rather than depending on previous chat history.

Project code, tests, documentation, ADRs, CI/release conventions, repository-local instructions, and current Git state remain the source of truth.

### Add; do not replace

The harness must adapt to an existing project instead of forcing the project into a new structure.

Do not migrate or duplicate project-specific rules merely to fit the harness. Existing `.cursor/rules/`, repository instructions, documentation, ADRs, tests, skills, deployment conventions, and other local assets stay where they are unless the project independently decides to change them.

### Project-specific knowledge stays project-specific

Do not copy product names, business rules, architecture decisions, environment details, release procedures, language preferences, credentials, or domain knowledge into this shared harness repository.

The shared files define process defaults, not product truth.

### Prefer deterministic safeguards

Tests, type/schema constraints, analyzers, linters, builds, CI checks, and scripts are preferred to repeated model judgment when they can enforce the same rule reliably.

### Human approval is defined by effect, not tool

High-impact actions require explicit approval regardless of whether they are performed through Cursor, Claude Code, Codex, Antigravity, a CLI, an IDE, or another agent. The exact approval boundary is defined in `AGENTS.md`.

These files provide agent context, not hard enforcement. If an action must be technically impossible rather than merely prohibited by instruction, use the active tool's project-local permission, deny, or hook mechanism; that configuration stays outside this shared repository.

## Quick adoption

For a new project with no existing `AGENTS.md`, copy the shared files into the project root.

```bash
git clone --depth 1 https://github.com/BurakD/ai-engineering-harness /tmp/ai-engineering-harness
cp /tmp/ai-engineering-harness/{AGENTS.md,MODEL_ROUTING.md,CLAUDE.md} .
```

`CLAUDE.md` is only needed when Claude Code is used. If your shell does not support brace expansion, or on Windows, copy the same files by any normal file-copy method; no installer is required.

Before committing anything, review the diff. Adoption should not change application behavior.

## Existing-project adoption

The preferred model is **inspect, preserve, then add**.

1. Inspect the current branch and working-tree state before changing anything.
2. Discover existing AI/project instructions and canonical documentation. Typical locations include `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.github/`, `CONTRIBUTING.md`, project docs, ADRs, tests, CI/release files, and deployment documentation.
3. Add or update `AGENTS.md` using the applicable case below.
4. Add `MODEL_ROUTING.md` unless the project already has an equivalent policy. If it does, reconcile the policies instead of creating competing routing systems.
5. If Claude Code is used, add the thin `CLAUDE.md` adapter. If a `CLAUDE.md` already exists, preserve its Claude-specific value and add `@AGENTS.md` rather than replacing it.
6. Do not create `.ai/`, `.agents/`, installers, manifests, skills, or extra adapters solely because this harness exists.
7. Review the final Git diff. Do not commit, push, deploy, publish, or perform unrelated cleanup unless explicitly requested.

### If the project has no `AGENTS.md`

Copy `AGENTS.md` byte-for-byte from this repository. Do not summarize, rewrite, or regenerate it from the README.

### If the project already has `AGENTS.md`

Do not rewrite or condense the existing file. Append the shared baseline as one clearly marked block:

```text
<!-- BEGIN shared engineering baseline — ai-engineering-harness @ YYYY-MM-DD -->
[verbatim contents of this repository's AGENTS.md]
<!-- END shared engineering baseline -->
```

Change nothing outside the markers. If the markers already exist, updating the harness means replacing only the content between them with the current shared `AGENTS.md` and updating the date. Do not create a sync script merely for this.

Project-local rules remain authoritative even when the shared block appears later in the file.

### Optional AI-assisted adoption prompt

Use this only when a model is needed to inspect an existing project and perform the safe append/update path:

```text
Adapt the AI Engineering Harness from https://github.com/BurakD/ai-engineering-harness into the current project.

First inspect the current Git state, existing AGENTS.md / CLAUDE.md, repository-local AI rules, docs, ADRs, tests, and release/deployment conventions.

Preserve all existing project-specific content. Copy the shared files and shared AGENTS.md baseline verbatim; do not summarize, rewrite, or regenerate them from the README.

If AGENTS.md already exists, change nothing outside the documented BEGIN/END shared-baseline markers. If the markers do not exist, append one marked shared-baseline block. If they already exist, replace only the content inside them.

Do not create a new framework, installer, orchestrator, manifest, skills directory, or project overlay.

Show the resulting diff and explain conflicts or choices. Do not commit, push, deploy, publish, or change production.
```

## New-project growth

Start with only the shared files you actually use. Add project-specific information to the project's normal documentation, rules, tests, ADRs, configuration, or code as real needs emerge. Do not grow a separate harness-specific project structure pre-emptively.

## Model routing

`MODEL_ROUTING.md` defines stable capability tiers rather than making the project depend on model version names.

- **FAST** — small/mechanical work.
- **STANDARD** — normal implementation and bounded fixes.
- **REASONING** — difficult, ambiguous, architectural, security-sensitive, compatibility-sensitive, or release-sensitive work.
- **FRONTIER** — exceptional hardest cases; manual escalation only.

Exact model catalogs and subscription economics change frequently. Tool mappings are therefore expressed as capabilities rather than pinned model versions.

Project-specific rules may raise the minimum tier for a sensitive area. Such overrides belong in that project, not in the shared harness.

## Durable learning from AI mistakes

The normative durable-learning rule is in `AGENTS.md`: when a correction is likely to matter again, prefer a durable test/check, code or schema invariant, linter/build/CI rule, or project-local rule/documentation improvement instead of relying on chat memory.

Project-specific mistakes stay project-specific. Do not grow the shared baseline from one product's local lessons.

## Maintenance

Keep the stable process in `AGENTS.md` and the stable tier definitions in `MODEL_ROUTING.md`.

When tools or models change, update only guidance that is actually stale. Avoid propagating model-version churn into every project.

## Possible future extensions

Earlier design work considered richer layers such as templates, project overlays, reusable skills, additional adapters, automated installation, and orchestration. Those remain valid options only if repeated real-world adoption pain proves they are necessary.

They are intentionally **not implemented in v1**. Add them only when they remove a demonstrated recurring cost or risk that the current Markdown-only approach cannot solve cleanly.
