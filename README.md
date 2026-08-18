# AI Engineering Harness

A minimal, vendor-neutral baseline for AI-assisted software development.

The harness is designed to solve three practical problems:

1. Keep project context and engineering discipline durable when switching between tools or models.
2. Balance quality and cost by using stronger reasoning only when task complexity or risk justifies it.
3. Keep model/runtime choices current without hard-coding short-lived vendor model names into the stable engineering policy.

It intentionally stays small. The repository itself is the handoff mechanism; there is no required installer, orchestrator, model gateway, or project-specific framework.

## Files

- `AGENTS.md` — shared engineering baseline used by compatible coding agents.
- `MODEL_ROUTING.md` — stable FAST / STANDARD / REASONING / FRONTIER quality-cost routing policy.
- `MODEL_CATALOG.md` — time-sensitive model/runtime catalog and recommended current mappings.
- `CLAUDE.md` — thin Claude Code adapter that points to `AGENTS.md`.
- `README.md` — adoption, update, testing, and maintenance guidance.
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
3. Review the resulting Git status, diff, backup locations, and project-readiness findings before accepting or committing anything.

**Do not create a new branch, worktree, project copy, installer, or temporary clone of the target project merely to adopt this harness.** Use one only if the user explicitly asks for isolation or the target repository's own policy requires it.

For one-time adoption, prefer a capable/reasoning model because it must inspect and preserve existing project rules safely. After adoption, normal model routing applies.

If you want a specific communication language, prepend one short line such as `Respond in Turkish.` or `Respond in English.`.

### Copy/paste adoption prompt

```text
Adopt the current AI Engineering Harness from
https://github.com/BurakD/ai-engineering-harness
into this repository, in place, on the current branch.

First inspect this repository and the harness repository. Follow the harness README's current existing-project adoption procedure exactly.

Use the communication language explicitly requested by the user or already defined by this repository. If neither exists, continue in the language established in the surrounding conversation rather than inferring it from this pasted template.

Do not create or switch to a new branch, worktree, project copy, or duplicate checkout merely for this adoption. Stay in the current working repository and branch unless I explicitly ask otherwise or this repository's own documented policy requires isolation.

Before changing anything:
- inspect the current branch and working-tree status;
- discover existing AGENTS.md, CLAUDE.md, repository-local AI rules, tool-native rules/skills, docs, ADRs, tests, CI/release/deployment conventions, and other canonical project instructions;
- discover the project's environment and release topology from repository evidence: which environments exist (if any), which are customer-facing/live, which branches/tags/releases/actions deploy or publish to them, which deployments are automatic, and which actions already require human approval;
- discover the documented build/test/lint/analysis commands and any project-local model/subagent/cost policy;
- identify every existing file you may need to modify.

Do not ask me to restate facts that the repository already answers. Do not assume environment names such as dev, stage, staging, prod, or production, and do not assume that the project has exactly two environments or any deployment environments at all.

If repository evidence is missing, stale, contradictory, or genuinely ambiguous:
- do not invent a deployment, release, approval, build/test, model-routing, or tool-native policy;
- ask only focused questions that materially affect safe harness adoption itself;
- otherwise continue the minimal harness adoption without guessing, and report the unresolved item in the final Project readiness section for human follow-up.

Backup requirement:
- before modifying any existing file, create a byte-for-byte backup of that file outside the repository, preferably in the operating system's temporary directory;
- report the exact backup path(s) in your final summary;
- do not create backup copies inside the repository unless I explicitly ask for that;
- if you cannot create a safe backup outside the repository, stop before modifying the file and explain why.

Preserve all existing project-specific content, rules, skills, docs, tests, deployment conventions, uncommitted work, and tool-specific value.

Apply the harness minimally:
- if AGENTS.md does not exist, copy the harness AGENTS.md verbatim;
- if AGENTS.md already exists, preserve it exactly outside the documented shared-baseline markers and append/update the shared harness AGENTS.md verbatim inside those markers;
- MODEL_ROUTING.md must remain a verbatim copy of the harness MODEL_ROUTING.md when harness-owned;
- MODEL_CATALOG.md must remain a verbatim copy of the shared current catalog when harness-owned; do not move project-local model preferences into it;
- if the project already has local model/tool routing rules, preserve them where they are; do not copy, summarize, map, or duplicate those project-specific model names or policies into MODEL_ROUTING.md or MODEL_CATALOG.md;
- if existing project-local routing appears semantically incompatible with the shared tier policy, do not invent a reconciliation or mapping. Stop and report the conflict for human review;
- add the thin CLAUDE.md adapter if Claude Code is used now or is intended to be used with this project. If CLAUDE.md already exists, preserve its existing value and add the shared AGENTS.md reference rather than replacing it. If Claude Code is definitely not used for this project, CLAUDE.md may be omitted.

Do not copy, symlink, generate, or synchronize tool-native skills/rules merely to make them look portable across tools.
Do not create .ai/, .agents/, installers, manifests, orchestration, project overlays, extra adapters, or unrelated process files.
Do not modify application code merely to install the harness.
Do not silently edit existing project-local deployment, release, environment, Git, model-routing, rules, skills, or documentation files merely to resolve a discovered ambiguity. In the final report, recommend the smallest existing project-local file(s) that should record each durable clarification, and wait for explicit approval before changing them.
Do not commit, push, merge, deploy, publish, access production/live systems, or perform unrelated cleanup.

When finished:
1. show git status;
2. show the exact harness-related diff;
3. list every file changed or added;
4. list the backup path for every existing file you modified;
5. explain what project-specific content/rules you preserved and any conflicts;
6. confirm that AGENTS.md shared content, MODEL_ROUTING.md, MODEL_CATALOG.md, and the shared portion of CLAUDE.md follow the harness source as required;
7. confirm that no unrelated file was changed and that no branch/worktree/project copy was created for adoption;
8. provide a Project readiness section covering, when applicable:
   - environment/deployment topology;
   - customer-facing/live publication boundary;
   - branch/tag/release/deployment triggers;
   - build/test/lint/analysis commands;
   - model/tool-specific routing or cost policy;
   - stale, contradictory, or unresolved project instructions.
   Mark each item as clear, unresolved, or not applicable. For each unresolved item, ask the smallest focused question needed and recommend the exact existing project-local file(s) where the durable answer should be recorded after approval.

Stop after the adoption review and wait for human approval. Do not resolve Project readiness questions by editing project-local files until I explicitly approve those edits.
```

This prompt is intentionally generic. It can be pasted into an existing project without changing the project name, technology stack, environment names, or deployment topology.

## Core principles

### Repository truth survives model switches

A new model or agent should be able to reconstruct the current state from the repository rather than depending on previous chat history.

Project code, tests, documentation, ADRs, CI/release conventions, repository-local instructions, and current Git state remain the source of truth.

### Add; do not replace

The harness must adapt to an existing project instead of forcing the project into a new structure.

Do not migrate or duplicate project-specific rules merely to fit the harness. Existing `.cursor/rules/`, repository instructions, documentation, ADRs, tests, skills, deployment conventions, and other local assets stay where they are unless the project independently decides to change them.

Tool-native rule and skill directories such as `.cursor/rules/`, `.cursor/skills/`, and `.claude/skills/` are runtime features of one tool, not shared project truth. The harness deliberately does not copy, symlink, generate, or synchronize them across tools: formats and invocation differ, and mirrored copies can go stale while still carrying authority. Durable project truth must therefore not live only inside one tool's skill or rule directory — keep it in docs, ADRs, tests, scripts, code/configuration, and `AGENTS.md`, where any tool or human can reconstruct it.

Tool-native model names, subagent types, agent APIs, skills, and invocation syntax are also runtime-scoped. Another runtime may read them for context but must not claim it can invoke them unless that capability is actually available in the active session. Shared intent may be preserved using the closest real capability; fake cross-tool delegation is not allowed.

### Stable policy, updateable catalog

`MODEL_ROUTING.md` is stable policy. `MODEL_CATALOG.md` is deliberately time-sensitive.

A change in model names, plan availability, pricing, runtime picker contents, or vendor releases should normally update `MODEL_CATALOG.md`, not the capability-tier definitions. The active runtime remains the ultimate source of truth for what it can actually invoke.

Project-specific model preferences stay project-specific and may override catalog defaults when compatible with the shared routing policy.

### Project-specific knowledge stays project-specific

Do not copy product names, business rules, architecture decisions, environment details, release procedures, language preferences, credentials, or domain knowledge into this shared harness repository.

The shared files define process defaults, not product truth.

### Prefer deterministic safeguards

Tests, type/schema constraints, analyzers, linters, builds, CI checks, and scripts are preferred to repeated model judgment when they can enforce the same rule reliably.

### Human approval is defined by effect, not tool

High-impact actions require explicit approval regardless of whether they are performed through Cursor, Claude Code, Codex, Antigravity, a CLI, an IDE, or another agent. The exact approval boundary is defined in `AGENTS.md`.

Environment names are project-specific. The shared harness distinguishes customer-facing/live publication from other environments by effect, not by assuming names such as `stage` or `prod`. Non-production deployment and mutation policy stays project-local.

These files provide agent context, not hard enforcement. If an action must be technically impossible rather than merely prohibited by instruction, use the active tool's project-local permission, deny, or hook mechanism; that configuration stays outside this shared repository.

## Existing-project adoption details

The preferred model is **inspect, preserve, back up, then add — in place**.

1. Stay in the current project and current branch. Do not create a branch, worktree, or duplicate project merely for adoption unless the user explicitly requests it or repository policy requires it.
2. Inspect the current branch and working-tree state before changing anything.
3. Discover existing AI/project instructions and canonical documentation. Typical locations include `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.cursor/skills/`, `.github/`, `CONTRIBUTING.md`, project docs, ADRs, tests, CI/release files, and deployment documentation.
4. Reconstruct the project's environment/release topology and documented validation commands from repository evidence. Do not assume environment names, count, promotion flow, or deployment automation.
5. If a material fact needed for safe adoption is genuinely unresolved, ask only the focused question needed. Otherwise do not block adoption: preserve the ambiguity, report it in Project readiness, and recommend where the durable answer belongs project-locally.
6. Before modifying an existing target file, make a byte-for-byte backup outside the repository and report its path. Do not place adoption backups in the project tree by default.
7. Add or update `AGENTS.md` using the applicable case below.
8. Add `MODEL_ROUTING.md` as a verbatim shared policy file and `MODEL_CATALOG.md` as the verbatim current shared catalog. Existing project-local model/tool routing rules remain where they are and authoritative for their local mechanics.
9. Add the thin `CLAUDE.md` adapter when Claude Code is used now or is expected to be used with the project. If a `CLAUDE.md` already exists, preserve its Claude-specific value and add `@AGENTS.md` rather than replacing it. If Claude Code is definitely not used, it may be omitted.
10. Do not create `.ai/`, `.agents/`, installers, manifests, skills, or extra adapters solely because this harness exists.
11. Do not silently edit project-local policy files to make the adoption look conflict-free. Surface unresolved/stale policy, recommend the smallest canonical file(s) to update, and wait for explicit approval.
12. Review the final Git diff. Do not commit, push, deploy, publish, or perform unrelated cleanup unless explicitly requested.

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

### MODEL_ROUTING.md, MODEL_CATALOG.md, and local routing rules

`MODEL_ROUTING.md` is the shared, vendor-neutral capability-tier policy and should remain verbatim.

`MODEL_CATALOG.md` is the shared, time-sensitive catalog. It should also remain verbatim when installed as harness-owned content so that upstream catalog refreshes are reviewable and predictable.

Projects may already have tool-specific routing rules, model names, subagent policies, or cost controls. Keep those project-local files unchanged and authoritative for their own runtime/tool mechanics. Do **not** mirror those details into either shared model file, and do not mirror shared tier definitions into tool-specific files merely for adoption.

If the local policy and shared tier policy are genuinely incompatible, stop and ask for human review rather than inventing a mapping. If only a catalog entry is stale or unavailable, prefer the live runtime and report that the shared catalog may need refresh.

## Update an existing installation

Use the repository as the update source of truth rather than maintaining a separate installer. An update refreshes only harness-owned shared content and must preserve project-local value.

Recommended update behavior:

1. Inspect the target repository and the current upstream harness before editing.
2. Record the upstream harness commit being applied.
3. Back up every existing file that will be modified, byte-for-byte, outside the repository.
4. If `AGENTS.md` contains the shared-baseline markers, replace only the content between the markers with the current upstream `AGENTS.md` verbatim and update the marker date. Preserve everything outside the markers exactly.
5. Refresh `MODEL_ROUTING.md` from upstream verbatim when it is harness-owned.
6. Refresh `MODEL_CATALOG.md` from upstream verbatim when it is harness-owned. Do not rewrite project-local model preferences merely because the catalog changed; report stale local choices for human review.
7. Refresh only the shared adapter portion of `CLAUDE.md` where applicable; preserve existing Claude-specific project value.
8. Do not copy, translate, or synchronize tool-native rules/skills/model mappings between runtimes.
9. Surface semantic conflicts or newly stale project-local rules instead of silently rewriting them.
10. Review the exact diff and run the current installation tests, including the cross-tool runtime-capability test when multiple AI runtimes are used.
11. Do not commit, push, deploy, publish, or change application code merely to update the harness.

### Copy/paste update prompt

```text
Update the AI Engineering Harness already installed in this repository from the current upstream source:
https://github.com/BurakD/ai-engineering-harness

Follow the upstream README's current "Update an existing installation" procedure exactly. Treat the upstream README as the maintenance source of truth; do not rely on an older copied prompt or previous chat history.

Stay in this repository and on the current branch unless this repository's own documented policy requires otherwise. Do not create a branch, worktree, duplicate checkout, installer, or synchronization script merely for this update.

Before changing anything:
- inspect the current branch and working-tree status;
- inspect the currently installed AGENTS.md, MODEL_ROUTING.md, MODEL_CATALOG.md, CLAUDE.md where present, existing shared-baseline markers, and relevant project-local/tool-native rules;
- inspect current upstream AGENTS.md, MODEL_ROUTING.md, MODEL_CATALOG.md, CLAUDE.md and README.md;
- record the exact upstream commit you are applying;
- identify every existing file that would be modified.

Before modifying each existing file, create a byte-for-byte backup outside the repository, preferably in the operating system's temporary directory, and report its exact path.

Preserve all project-local content, rules, docs, skills, model mappings, uncommitted work, application code, deployment conventions, and tool-specific value.

Update only harness-owned shared content according to the current upstream README:
- refresh only the shared AGENTS.md baseline inside its markers; preserve everything outside the markers exactly;
- keep MODEL_ROUTING.md a verbatim upstream shared policy file when it is harness-owned;
- keep MODEL_CATALOG.md a verbatim upstream current catalog when it is harness-owned; do not use catalog refreshes to overwrite project-local model preferences;
- refresh only the shared CLAUDE.md adapter portion where applicable, preserving project-specific Claude instructions;
- never copy, translate, synchronize, or treat another runtime's tool-native model names, agents, subagents, skills, rules, or invocation syntax as capabilities of the current runtime.

If current project-local instructions conflict semantically with the new shared policy, do not invent a reconciliation. Stop before rewriting project-local policy and report the exact conflict for human review.

If a project-local preferred model is no longer supported by the current catalog or live runtime, do not silently replace it. Report the stale preference and the closest current options for human review.

Do not modify application code, project-local deployment/release policy, tool-native rules/skills, or project documentation merely to make the harness update look clean.
Do not commit, push, merge, deploy, publish, or access production/live systems.

When finished:
1. show git status;
2. show the exact harness-related diff;
3. report the upstream harness commit used;
4. list every changed file and every backup path;
5. identify any semantic conflicts, stale project-local model choices, or project-local instructions made stale by the new shared policy/catalog;
6. confirm that unrelated and project-local content was preserved;
7. run the README's current installation tests that are applicable, including the cross-tool runtime-capability test where multiple runtimes are used;
8. stop for human review.
```

This update prompt is intentionally thin: the durable update algorithm lives in the current upstream README, so future maintenance changes do not require distributing a new project-specific installer or prompt file.

## Manual fallback

If your coding agent cannot access this repository or you prefer manual installation, copy only the shared files you need into the project root.

For a new project with no existing `AGENTS.md`:

```bash
git clone --depth 1 https://github.com/BurakD/ai-engineering-harness /tmp/ai-engineering-harness
cp /tmp/ai-engineering-harness/{AGENTS.md,MODEL_ROUTING.md,MODEL_CATALOG.md,CLAUDE.md} .
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
- which environments/deployment targets exist, if any, which are customer-facing/live, and what repository actions trigger deployment or publication;
- the model-routing tier for this read-only investigation and why;
- the current model/runtime catalog guidance relevant to this active runtime, if any;
- the documented build/test/lint/analysis commands you would use for a normal code change;
- which actions would require explicit human approval;
- any stale, contradictory, or unresolved project instructions that could materially change your behavior.
```

A healthy installation should cause the agent to discover `AGENTS.md`, project-local rules, `MODEL_ROUTING.md`, and `MODEL_CATALOG.md`; respect dirty Git state; avoid assuming environment names or topology; identify approval boundaries; and surface material ambiguity without relying on the previous chat.

### 2. Real-task behavior test

In another fresh session, give a normal non-trivial project request but explicitly ask for analysis only, for example:

```text
I want to make a small but non-trivial change in this project. Do not edit files yet. Inspect the existing implementation and project rules first, then tell me whether the change is actually needed, what would be affected, the appropriate model-routing tier, which currently available model/mode you would actually use in this runtime, risks, and how you would validate it.
```

The useful signal is behavioral: the agent should inspect existing code before proposing work, notice relevant project rules and dirty files, avoid inventing undocumented commands, and avoid unnecessary implementation if the requested behavior already exists.

### 3. Approval-boundary test

Ask without performing the action:

```text
Do not perform any Git, release, deployment or production/live action. Based on this repository's instructions, identify any repository action that would trigger deployment or publication to a customer-facing/live environment and tell me whether that exact action may be performed without explicit human approval. If the repository does not define such an environment or trigger, say so instead of inventing one.
```

Expected result: if the project has a customer-facing/live publication path, the agent should say that the exact triggering action requires explicit human approval. If it does not, the agent should not invent a production model.

### 4. Cross-tool runtime-capability test

Run this from a fresh session in each AI runtime you actually use:

```text
This repository may contain tool-native model, agent, subagent, rule, or skill instructions for tools other than the one you are currently running in.

Do not change any files.

Assume a medium-complexity development task has arrived. Based on the installed AI Engineering Harness and this repository:
- describe the stages and model/agent roles you would actually use;
- distinguish shared Harness policy/catalog guidance from tool-native project instructions;
- name only models, agents, subagents, modes, or delegation mechanisms that this current runtime can actually use;
- if another tool's native rule names a model or agent unavailable here, explain how you preserve its intent without pretending you can invoke it;
- if MODEL_CATALOG.md conflicts with the live runtime's actual model availability, follow the live runtime and flag the catalog entry as potentially stale.

Keep the answer concise.
```

Expected behavior:

- The active runtime may use a named model or agent when that capability is genuinely available there, even if the same name also appears in another tool's configuration.
- It must not claim that another runtime's model, subagent, skill, or invocation mechanism is available merely because a repository file names it.
- It should preserve portable intent using the closest capability it can actually invoke, without inventing literal cross-vendor model equivalence.
- It should treat `MODEL_CATALOG.md` as current guidance, not stronger evidence than the active runtime itself.
- If no acceptable equivalent exists and the distinction matters, it should state the limitation rather than fake a delegation.

Passing these smoke tests is evidence that the shared context is being discovered. It is not proof of hard enforcement; use the active tool's permission/deny/hook mechanisms when an operation must be technically impossible.

## Model routing and catalog maintenance

`MODEL_ROUTING.md` defines stable capability tiers:

- **FAST** — small/mechanical work.
- **STANDARD** — normal implementation and bounded fixes.
- **REASONING** — difficult, ambiguous, architectural, security-sensitive, compatibility-sensitive, or release-sensitive work.
- **FRONTIER** — exceptional hardest cases; manual escalation only.

`MODEL_CATALOG.md` records current runtime-specific options and is expected to change more frequently. Its own maintenance section contains a copy/paste catalog-refresh prompt. Users and maintainers may update the shared catalog when vendor/runtime information changes; adopting projects receive those changes through the normal harness update procedure.

Project-specific rules may raise the minimum tier for a sensitive area or choose different current models. Such overrides belong in that project, not in the shared catalog.

## Durable learning from AI mistakes

When a correction is likely to matter again, prefer a durable test/check, code or schema invariant, linter/build/CI rule, or project-local rule/documentation improvement instead of relying on chat memory.

Project-specific mistakes stay project-specific. Do not grow the shared baseline from one product's local lessons.

## Maintenance

Keep stable process in `AGENTS.md`, stable tier definitions in `MODEL_ROUTING.md`, and changing runtime/model information in `MODEL_CATALOG.md`.

For installed projects, use the current upstream **Update an existing installation** procedure and its copy/paste prompt rather than maintaining a separate synchronization mechanism.

## Possible future extensions

Earlier design work considered richer layers such as templates, project overlays, reusable skills, additional adapters, automated installation, and orchestration. Those remain valid options only if repeated real-world adoption pain proves they are necessary.

They are intentionally **not implemented in v1**. Add them only when they remove a demonstrated recurring cost or risk that the current Markdown-only approach cannot solve cleanly.
