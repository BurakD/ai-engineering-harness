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

## Runtime and tool capability boundaries

- Tool-native instructions — including a tool's rules, skills, agent definitions, model names, subagent types, or invocation syntax — are authoritative for that tool/runtime only. Other runtimes may read them for context, but must not pretend those native capabilities exist.
- Before naming or promising a concrete model, agent, subagent, mode, or delegation mechanism, confirm that it is actually available in the active runtime/session. A model or agent name mentioned in another tool's configuration is not evidence that this runtime can invoke it.
- Capability discovery must fail closed. If live model/agent discovery is unavailable, hangs, is interrupted, returns incomplete output, or otherwise fails to establish availability, treat the concrete capability as **unverified**. Do not fall back to remembered, guessed, inferred, or merely typical model names, agent APIs, subagent types, aliases, or delegation mechanisms. This prohibition includes parenthetical examples, "likely" fallback candidates, and illustrative concrete names. In that case describe the role/tier generically or state the limitation instead.
- If a tool-native instruction expresses a portable intent — for example separating planning from implementation, using cheaper workers for routine execution, or requiring an independent review — preserve that intent with the closest capability the active runtime actually supports, consistent with `MODEL_ROUTING.md`. If there is no equivalent, state the limitation rather than inventing a cross-tool mapping or fake delegation.
- If the same named model or mechanism is genuinely available in the active runtime, it may be used; availability must come from the active runtime, not from another tool's configuration.
- Behavior intended to bind every tool should live in shared or project-canonical locations, not only in one tool's native rule, skill, or agent directory.

## Preserve project-specific value

Existing repository-local instructions, documentation, ADRs, CI/release conventions, dependency rules, protocol constraints, deployment procedures, skills, and other project guidance remain authoritative. Do not silently replace, weaken, duplicate, or generalize them merely to fit this harness.

Project-specific rules may raise the minimum model-routing tier or require additional review for sensitive areas.

## Safety and human approval

- Never overwrite unrelated uncommitted work.
- Never expose secrets.
- Development success, green CI, a merged branch, or a successful non-production deployment is not approval to release or deploy to a production/live/customer-facing environment.
- Production/live/customer-facing publication (including any push or merge that triggers such deployment or publication), mutation of a production/live/customer-facing environment or its infrastructure, destructive or irreversible operations (for example force-push, history rewrite, hard reset, or branch deletion), risky production-data operations, secret or credential rotation, release tagging when it triggers publication, and spend outside the agreed policy require explicit human approval for that exact action.
- Non-production environments may be named development, test, QA, staging, preview, sandbox, or something else, and a project may have none, one, or many of them. Actions that deploy to or mutate those environments follow the repository's project-local deployment and approval policy. If that policy is absent or genuinely ambiguous, do not invent an autonomy rule; report the ambiguity before performing the action.
- Preserve supported-client, protocol, data, and public-contract compatibility by default unless the project explicitly decides otherwise.

## Durable handoff between models

When work changes durable project truth, update the appropriate project documentation, test, ADR, rule, configuration, or code in the same work. A different model or agent should be able to reconstruct the current state from the repository without needing the previous model's chat history or any single tool's native features.

If the same mistake or correction is likely to recur, prefer the smallest durable guard: a deterministic test/check, code or schema invariant, linter/build/CI rule, or project-local rule/documentation improvement. Do not rely on chat memory.

See `MODEL_ROUTING.md` for the shared quality/cost model-routing policy and `MODEL_CATALOG.md` for the current time-sensitive model/runtime catalog.
