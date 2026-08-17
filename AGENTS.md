# Shared AI Development Instructions

This repository uses a lightweight, reusable AI-development harness. Repository-local project rules, documentation, ADRs, tests, CI/release conventions, deployment procedures, and Git state remain authoritative for project-specific behavior.

## Rebuild context from the repository

Before non-trivial work:

1. Read this file.
2. Discover and read the relevant repository-local project instructions and canonical documentation.
3. Inspect the current branch and working-tree status before editing or giving implementation guidance. This is mandatory even for non-trivial read-only investigation. Inspect relevant recent commits or diffs when needed.
4. Inspect the affected code and tests before editing.
5. Treat repository code, tests, docs, ADRs, configuration, CI/release conventions, and Git state as the source of truth; do not depend on prior chat history.

## Development process

- Small/mechanical work (FAST): implement directly and validate the affected area.
- Normal work (STANDARD): understand the affected code, acceptance criteria, and project constraints before editing.
- Difficult, architectural, security-sensitive, compatibility-sensitive, release-sensitive, or ambiguous work (REASONING): plan when useful, use stronger reasoning, validate thoroughly, and use a fresh or independent review when it materially reduces risk.
- Prefer deterministic tests, analyzers, linters, builds, CI checks, and scripts over model judgment when available.
- Use the project's documented build, test, lint, and analysis commands. If relevant commands are not documented and cannot be safely inferred from repository configuration, ask before inventing them; after confirmation, record them in project-local instructions.
- Report validation that was skipped or unavailable.
- Do not add process artifacts unless they materially help the work.

## Preserve project-specific value

Existing repository-local instructions, documentation, ADRs, CI/release conventions, dependency rules, protocol constraints, deployment procedures, skills, and other project guidance remain authoritative. Do not silently replace, weaken, duplicate, or generalize them merely to fit this harness.

Project-specific rules may raise the minimum model-routing tier or require additional review for sensitive areas.

## Safety and human approval

- Never overwrite unrelated uncommitted work.
- Never expose secrets.
- Development success, green CI, a merged branch, or a successful staging deployment is not approval to release or deploy to production.
- Production or store publication (including any push or merge that triggers deployment), production/server mutation, destructive or irreversible operations (for example force-push, history rewrite, hard reset, or branch deletion), risky production-data operations, secret or credential rotation, release tagging when it triggers publication, and spend outside the agreed policy require explicit human approval for that exact action.
- Preserve supported-client, protocol, data, and public-contract compatibility by default unless the project explicitly decides otherwise.

## Durable handoff between models

When work changes durable project truth, update the appropriate project documentation, test, ADR, rule, configuration, or code in the same work. A different model or agent should be able to reconstruct the current state from the repository without needing the previous model's chat history.

If the same mistake or correction is likely to recur, prefer the smallest durable guard: a deterministic test/check, code or schema invariant, linter/build/CI rule, or project-local rule/documentation improvement. Do not rely on chat memory.

See `MODEL_ROUTING.md` for the shared quality/cost model-routing policy.
