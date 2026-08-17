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

High-impact actions require explicit approval regardless of whether they are performed through Cursor, Claude Code, Codex, Antigravity, a CLI, an IDE, or another agent.

## Existing-project adoption

The preferred adoption model is **inspect, preserve, then add or merge**.

1. Inspect the current branch and working-tree state before changing anything.
2. Discover existing AI/project instructions and canonical documentation. Typical locations include `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.github/`, `CONTRIBUTING.md`, project docs, ADRs, tests, CI/release files, and deployment documentation.
3. If the project does not have `AGENTS.md`, add the shared `AGENTS.md` from this repository.
4. If the project already has `AGENTS.md`, preserve its project-specific content and merge the shared engineering baseline into it. Do not overwrite it.
5. Add `MODEL_ROUTING.md` unless the project already has an equivalent policy. If it does, reconcile the policies instead of creating competing routing systems.
6. If Claude Code is used, add the thin `CLAUDE.md` adapter. If a `CLAUDE.md` already exists, preserve its Claude-specific value and add the `AGENTS.md` import/link rather than replacing it.
7. Do not create `.ai/`, `.agents/`, installers, manifests, skills, or extra adapters solely because this harness exists.
8. Review the final Git diff. Adoption should not alter application behavior.
9. Do not commit, push, deploy, publish, or perform unrelated cleanup unless explicitly requested.

### Suggested prompt for an existing repository

```text
Adapt the AI Engineering Harness from this repository into the current project.

Follow the README adoption instructions. First inspect the repository, Git state, existing AGENTS.md / CLAUDE.md, repository-local AI rules, docs, ADRs, tests, and release/deployment conventions.

Preserve all existing project-specific value. Do not overwrite existing instructions. Add or merge only what is necessary for the shared engineering baseline, model routing, and thin tool adapter.

Do not create a new framework, installer, orchestrator, manifest, skills directory, or project overlay unless the existing repository already requires one.

Show the resulting diff and explain any conflicts or choices. Do not commit, push, deploy, publish, or change production.
```

## New-project adoption

For a new project, the initial harness can be only:

```text
AGENTS.md
MODEL_ROUTING.md
CLAUDE.md   # when Claude Code is used
```

Add project-specific information to the project's normal documentation, rules, tests, ADRs, configuration, or code as real needs emerge. Do not grow a separate harness-specific project structure pre-emptively.

## Model routing

`MODEL_ROUTING.md` defines stable capability tiers rather than making the project depend on model version names.

- **FAST** — small/mechanical work.
- **STANDARD** — normal implementation and bounded fixes.
- **REASONING** — difficult, ambiguous, architectural, security-sensitive, compatibility-sensitive, or release-sensitive work.
- **FRONTIER** — exceptional hardest cases; manual escalation only.

Exact model catalogs and subscription economics change frequently. Tool mappings are therefore expressed in terms of current equivalents and stable aliases where practical instead of pinning the harness to version names that will quickly become stale.

Project-specific rules may raise the minimum tier for a sensitive area. Such overrides belong in that project, not in the shared harness.

## Durable learning from AI mistakes

Repeated AI mistakes should reduce the chance of the same mistake recurring.

When a correction is likely to matter again, prefer the smallest durable guard in roughly this order:

1. deterministic test or check,
2. type/schema/code invariant,
3. linter/build/CI rule,
4. project-local rule, ADR, or documentation clarification.

Do not add a shared harness rule for a project-specific mistake. A shared rule is justified only when the lesson is genuinely tool-independent and reusable across projects.

## Human-approval boundary

At minimum, explicit approval for the exact action is required for:

- production or store publication,
- production/server mutation,
- destructive or irreversible operations,
- production data operations with meaningful risk,
- secret or credential rotation,
- release tagging when it triggers publication,
- spend outside the agreed policy.

Development success, green CI, a merged development branch, or a successful staging deployment is not production approval.

Project-specific rules may require approval for additional actions.

## Maintenance

Keep the stable process in `AGENTS.md` and the stable tier definitions in `MODEL_ROUTING.md`.

When tools or models change, update only the small tool-mapping guidance that is actually stale. Avoid propagating model-version churn into every project.

## Possible future extensions

Earlier design work considered richer layers such as templates, project overlays, reusable skills, additional adapters, automated installation, and orchestration. Those remain valid options if repeated real-world adoption pain proves they are necessary.

They are intentionally **not implemented in v1**. Add them only when they remove a demonstrated recurring cost or risk that the current Markdown-only approach cannot solve cleanly.
