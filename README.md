# AI Engineering Harness

A reusable, vendor-neutral engineering harness for AI-assisted software development across existing and new projects.

This repository contains the **shared core** only. Project-specific business rules, architecture notes, environment details, release procedures, and domain-specific skills must stay inside each project repository.

## Goals

- Keep one durable engineering workflow across Cursor, Claude Code, Codex, Antigravity, and future agents.
- Route work by complexity and risk instead of manually choosing a model for every task.
- Prefer deterministic checks, explicit release gates, and fresh-context review for higher-risk work.
- Make adoption practical for both mature repositories and greenfield projects.
- Avoid copying project-specific rules from one product into another.

## Architecture

The harness is split into three layers:

1. **Shared core** — reusable workflow, model policy, generic engineering skills, release-safety principles, and tool adapters maintained in this repository.
2. **Project overlay** — project identity, stacks, surfaces, environments, critical areas, validation commands, documentation map, and local rules maintained in the target project.
3. **Tool adapter** — thin integration files that help Cursor, Claude Code, Codex, Antigravity, or another agent discover the shared/project instructions without duplicating them.

The target project remains the source of truth for its code, tests, documentation, Git history, deployment rules, and product behavior.

## Adoption modes

### Existing project

Start by inspecting the repository before generating any overlay. Preserve existing agent rules, skills, CI, release conventions, and documentation. Add the harness incrementally and validate that product behavior does not change.

### New project

Start from a minimal project overlay and grow it only when the repository gains real capabilities such as authentication, payments, mobile apps, databases, migrations, staging, production, or store releases.

## Core workflow

`DISCOVER -> MODEL -> BUILD -> VERIFY/REVIEW`

Work is classified into four levels:

- **C0** — trivial/mechanical; build and validate directly.
- **C1** — normal/default; compact task artifact when useful.
- **C2** — significant/ambiguous; stronger discovery, specification, and fresh-context review.
- **C3** — critical; C2 discipline plus critical-area review and explicit release gates.

Typical C3 triggers include authentication/authorization, payments/IAP, credit ledgers, production data, credentials, public contracts, irreversible migrations, and store releases.

## Safety principles

- Never treat a development branch, staging deployment, green tests, or merged development PR as production approval.
- Production merge, production deployment, destructive/irreversible changes, production data operations, secret rotation, paid model usage outside policy, and store publication require the appropriate explicit human approval.
- Never overwrite unrelated uncommitted work.
- Never expose secrets; fail closed when required secrets are missing.
- Prefer additive compatibility for supported clients and public APIs.
- Preserve existing project-specific rules unless an explicit migration retires them.

## Repository plan

This repository will contain:

- `core/` — vendor-neutral workflow, model policy, generic skills, and safety defaults.
- `templates/` — minimal overlays for new projects and adoption templates for existing projects.
- `adapters/` — thin Cursor / Claude Code / Codex / Antigravity integration templates.
- `docs/` — adoption, customization, validation, and maintenance guidance.

The first validated pilot is maintained separately in its own product repository; project-specific content is intentionally not copied into this shared core.
