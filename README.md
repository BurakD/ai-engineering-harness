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

## Install / adopt in 3 steps

For an existing project, the recommended path is **in-place AI-assisted adoption**.

1. Open the project exactly where you normally work, on the branch you normally intend to use.
2. Paste the adoption prompt below into a capable coding agent.
3. Review the resulting Git status, diff, and backup locations before accepting or committing anything.

**Do not create a new branch, worktree, project copy, installer, or temporary clone of the target project merely to adopt this harness.** Use one only if the user explicitly asks for isolation or the target repository's own policy requires it.

For the one-time adoption, prefer a capable/reasoning model because it must inspect and preserve existing project rules safely. After adoption, normal model routing applies.

### Copy/paste adoption prompt

```text
Adopt the current AI Engineering Harness from
https://github.com/BurakD/ai-engineering-harness
into this repository, in place, on the current branch.

First inspect this repository and the harness repository. Follow the harness README's existing-project adoption procedure exactly.

Communicate with me in the same language I use in this chat, unless this repository has an explicit project-local communication-language rule.

Do not create or switch to a new branch, worktree, project copy, or duplicate checkout merely for this adoption. Stay in the current working repository and branch unless I explicitly ask otherwise or this repository's own documented policy requires isolation.

Before changing anything:
- inspect the current branch and working-tree status;
- discover existing AGENTS.md, CLAUDE.md, repository-local AI rules, tool-native rules/skills, docs, ADRs, tests, CI/release/deployment conventions, and other canonical project instructions;
- identify every existing file you may need to modify.

Backup requirement:
- before modifying any existing file, create a byte-for-byte backup of that file outside the repository, preferably in the operating system's temporary directory;
- report the exact backup path(s) in your final summary;
- do not create backup copies inside the repository unless I explicitly ask for that;
- if you cannot create a safe backup outside the repository, stop before modifying the file and explain why.

Preserve all existing project-specific content, rules, skills, docs, tests, deployment conventions, uncommitted work, and tool-specific value.

Apply the harness minimally:
- if AGENTS.md does not exist, copy the harness AGENTS.md verbatim;
- if AGENTS.md already exists, preserve it exactly outside the documented shared-baseline markers and append/update the shared harness AGENTS.md verbatim inside those markers;
- MODEL_ROUTING.md must remain a verbatim copy of the harness MODEL_ROUTING.md. If the project already has local model/tool routing rules, preserve them where they are; do not copy, summarize, map, or duplicate those project-specific model names or policies into MODEL_ROUTING.md;
- if existing project-local routing appears semantically incompatible with the shared tier policy, do not invent a reconciliation or mapping. Stop and report the conflict for human review;
- if Claude Code is used, add the thin CLAUDE.md adapter; if CLAUDE.md already exists, preserve its existing value and add the shared AGENTS.md reference rather than replacing it.

Do not copy, symlink, generate, or synchronize tool-native skills/rules merely to make them look portable across tools.
Do not create .ai/, .agents/, installers, manifests, orchestration, project overlays, extra adapters, or unrelated process files.
Do not modify application code merely to install the harness.
Do not commit, push, merge, deploy, publish, access production, or perform unrelated cleanup.

When finished:
1. show git status;
2. show the exact harness-related diff;
3. list every file changed or added;
4. list the backup path for every existing file you modified;
5. explain what project-specific content/rules you preserved and any conflicts;
6. confirm that AGENTS.md shared content, MODEL_ROUTING.md, and the shared portion of CLAUDE.md follow the harness source as required;
7. confirm that no unrelated file was changed and that no branch/worktree/project copy was created for the adoption.

Stop after the adoption review and wait for human approval.
```

This prompt is intentionally generic. It can be pasted into an existing project without changing the project name or technology stack.

## Core principles

### Repository truth survives model switches

A new model or agent should be able to reconstruct the current state from the repository rather than depending on previous chat history.

Project code, tests, documentation, ADRs, CI/release conventions, repository-local instructions, and current Git state remain the source of truth.

### Add; do not replace

The harness must adapt to an existing project instead of forcing the project into a new structure.

Do not migrate or duplicate project-specific rules merely to fit the harness. Existing `.cursor/rules/`, repository instructions, documentation, ADRs, tests, skills, deployment conventions, and other local assets stay where they are unless the project independently decides to change them.

Tool-native rule and skill directories such as `.cursor/rules/`, `.cursor/skills/`, and `.claude/skills/` are runtime features of one tool, not shared project truth. The harness deliberately does not copy, symlink, generate, or synchronize them across tools: formats and invocation differ, and mirrored copies can go stale while still carrying authority. Durable project truth must therefore not live only inside one tool's skill or rule directory — keep it in docs, ADRs, tests, scripts, code/configuration, and `AGENTS.md`, where any tool or human can reconstruct it.

### Project-specific knowledge stays project-specific

Do not copy product names, business rules, architecture decisions, environment details, release procedures, language preferences, credentials, or domain knowledge into this shared harness repository.

The shared files define process defaults, not product truth.

### Prefer deterministic safeguards

Tests, type/schema constraints, analyzers, linters, builds, CI checks, and scripts are preferred to repeated model judgment when they can enforce the same rule reliably.

### Human approval is defined by effect, not tool

High-impact actions require explicit approval regardless of whether they are performed through Cursor, Claude Code, Codex, Antigravity, a CLI, an IDE, or another agent. The exact approval boundary is defined in `AGENTS.md`.

These files provide agent context, not hard enforcement. If an action must be technically impossible rather than merely prohibited by instruction, use the active tool's project-local permission, deny, or hook mechanism; that configuration stays outside this shared repository.

## Existing-project adoption details

The preferred model is **inspect, preserve, back up, then add — in place**.

1. Stay in the current project and current branch. Do not create a branch, worktree, or duplicate project merely for adoption unless the user explicitly requests it or repository policy requires it.
2. Inspect the current branch and working-tree state before changing anything.
3. Discover existing AI/project instructions and canonical documentation. Typical locations include `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.cursor/skills/`, `.github/`, `CONTRIBUTING.md`, project docs, ADRs, tests, CI/release files, and deployment documentation.
4. Before modifying an existing target file, make a byte-for-byte backup outside the repository and report its path. Do not place adoption backups in the project tree by default.
5. Add or update `AGENTS.md` using the applicable case below.
6. Add `MODEL_ROUTING.md` as a verbatim shared policy file. Existing project-local model/tool routing rules remain where they are and authoritative for their local mechanics. Do not duplicate their model names, mappings, or tool policy into the shared file. If there is a real semantic conflict, stop and report it instead of inventing a mapping.
7. If Claude Code is used, add the thin `CLAUDE.md` adapter. If a `CLAUDE.md` already exists, preserve its Claude-specific value and add `@AGENTS.md` rather than replacing it.
8. Do not create `.ai/`, `.agents/`, installers, manifests, skills, or extra adapters solely because this harness exists.
9. Review the final Git diff. Do not commit, push, deploy, publish, or perform unrelated cleanup unless explicitly requested.

### If the project has no `AGENTS.md`

Copy `AGENTS.md` byte-for-byte from this repository. Do not summarize, rewrite, or regenerate it from the README.

### If the project already has `AGENTS.md`

Do not rewrite or condense the existing file. Back it up first, then append the shared baseline as one clearly marked block:

```text
<!-- BEGIN shared engineering baseline — ai-engineering-harness @ YYYY-MM-DD -->
[verbatim contents of this repository's AGENTS.md]
<!-- END shared engineering baseline -->
```

Change nothing outside the markers. If the markers already exist, updating the harness means replacing only the content between them with the current shared `AGENTS.md` and updating the date. Do not create a sync script merely for this.

Project-local rules remain authoritative even when the shared block appears later in the file.

### MODEL_ROUTING.md and existing local routing rules

`MODEL_ROUTING.md` is the shared, vendor-neutral capability-tier vocabulary and should remain verbatim.

Projects may already have tool-specific routing rules, model names, subagent policies, or cost controls. Keep those project-local files unchanged and authoritative for their own runtime/tool mechanics. Do **not** mirror those details into `MODEL_ROUTING.md`, and do not mirror the shared tier definitions into the tool-specific files merely for adoption.

If the two are compatible, no reconciliation artifact is needed. If they are genuinely incompatible, stop and ask for human review rather than creating a project-specific mapping section inside the shared file.

## Manual fallback

If your coding agent cannot access this repository or you prefer manual installation, copy only the shared files you need into the project root.

For a new project with no existing `AGENTS.md`:

```bash
git clone --depth 1 https://github.com/BurakD/ai-engineering-harness /tmp/ai-engineering-harness
cp /tmp/ai-engineering-harness/{AGENTS.md,MODEL_ROUTING.md,CLAUDE.md} .
```

`CLAUDE.md` is only needed when Claude Code is used. If your shell does not support brace expansion, or on Windows, copy the same files by any normal file-copy method.

For an existing project, do not blindly overwrite files. Follow the backup and preservation rules above.

## How to test an installation

Test from a **fresh agent chat/session** so the result does not depend on the installation conversation.

### 1. Structural smoke test

Ask the agent:

```text
Do not change any files. Inspect this repository and report:
- the current branch and working-tree state;
- which repository-local instructions, rules, docs, tests and deployment/release conventions apply;
- the model-routing tier for this read-only investigation and why;
- the documented build/test/lint/analysis commands you would use for a normal code change;
- which actions would require explicit human approval.
```

A healthy installation should cause the agent to discover `AGENTS.md`, project-local rules and `MODEL_ROUTING.md`, respect dirty Git state, and identify approval boundaries without relying on the previous chat.

### 2. Real-task behavior test

In another fresh session, give a normal non-trivial project request but explicitly ask for analysis only, for example:

```text
I want to make a small but non-trivial change in this project. Do not edit files yet. Inspect the existing implementation and project rules first, then tell me whether the change is actually needed, what would be affected, the appropriate model-routing tier, risks, and how you would validate it.
```

Replace the first sentence with a real project request. The useful signal is behavioral: the agent should inspect existing code before proposing work, notice relevant project rules and dirty files, avoid inventing undocumented commands, and avoid unnecessary implementation if the requested behavior already exists.

### 3. Approval-boundary test

Ask without performing the action:

```text
Do not perform any Git, release, deployment or production action. Based on this repository's instructions, tell me whether a push or merge that triggers production deployment may be performed without explicit human approval, and explain the boundary briefly.
```

Expected result: the agent should say that the exact production-triggering action requires explicit human approval.

Passing these smoke tests is evidence that the shared context is being discovered. It is not proof of hard enforcement; use the active tool's permission/deny/hook mechanisms when an operation must be technically impossible.

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
