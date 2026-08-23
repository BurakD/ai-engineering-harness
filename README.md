# AI Engineering Harness

**Languages:** **English** · [Türkçe](i18n/README.tr.md) · [Español](i18n/README.es.md) · [Português (Brasil)](i18n/README.pt-BR.md) · [Deutsch](i18n/README.de.md) · [Français](i18n/README.fr.md) · [Русский](i18n/README.ru.md) · [简体中文](i18n/README.zh-CN.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [العربية](i18n/README.ar.md) · [हिन्दी](i18n/README.hi.md)

A minimal, vendor-neutral baseline for AI-assisted software development.

Switching between AI coding tools or models usually means losing the project's engineering context and re-explaining it. AI Engineering Harness is a small, portable policy and context layer that prevents that. It is not an agent runtime or orchestrator. Cursor, Claude Code, Codex, and Antigravity provide their own execution and orchestration capabilities; this repository is designed to sit alongside them, not replace them. When you switch tools or models, this is the layer that carries the project's shared engineering context, quality-and-cost routing policy, and operating constraints forward.

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

### What this is — and is not

The shared value is the policy content: repository-first context, model-routing tiers, fail-closed runtime-capability handling, effect-based human approval, scope discipline, durable handoff, and safe adoption/update behavior.

It is **not** a spec-driven workflow engine, multi-agent framework, runtime, rule-sync generator, or replacement for tool-native rules and skills. Tool-native mechanisms remain useful for runtime-specific activation; the harness keeps portable policy and durable project truth from being trapped in any one tool.

### Runtime compatibility and native bridges

`AGENTS.md` is an external cross-tool convention rather than a format invented by this repository. Runtimes that consume it directly need no harness-specific adapter.

Claude Code reads `CLAUDE.md`, so this repository includes only the minimal documented bridge: `CLAUDE.md` imports `@AGENTS.md`. That adapter exists for compatibility, not vendor preference.

Antigravity-specific behavior such as `.agents/skills/` and `.agents/workflows/` remains tool-native and project-local. The harness does not copy, generate, or mirror those files. The same rule applies to other runtime-specific rule/skill systems: if a runtime needs its own documented project-context configuration, use that mechanism locally rather than adding shared adapters merely for symmetry.

## License

This project is open source under the **Apache License 2.0**.

You may use, modify, redistribute, and use the project commercially under the license terms. Copyright, license, patent, trademark, and attribution obligations remain governed by `LICENSE`.

Contributions are welcome and are submitted under the Apache License 2.0 unless explicitly stated otherwise, as described in `CONTRIBUTING.md`.

## Install / adopt in 3 steps

For an existing project, the recommended path is **in-place AI-assisted adoption**.

1. Open the project exactly where you normally work, on the branch you normally intend to use.
2. Paste the adoption prompt below into a capable coding agent.
3. Review the resulting Git status, diff, backup locations, skill-placement report, and project-readiness findings before accepting or committing anything.

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
- identify which AI runtimes are actually used by this repository from repository evidence. A CLI or application merely being installed on the machine is not evidence that this repository uses that runtime;
- identify every existing file you may need to modify.

For native shared-skill placement, use only currently verified project-level paths:
- Cursor, Antigravity, and Codex may use `.agents/skills/`;
- Claude Code uses `.claude/skills/`;
- Cursor can also read `.claude/skills/` for compatibility.
If all detected runtimes can use one verified project-level skill root, install one copy there. Do not create a second copy merely for symmetry. If a detected runtime's native skill path cannot be verified, do not guess one; use the neutral `harness/skills/` location for the Harness-owned skills that cannot be safely placed natively and do not claim native activation for that copy.

Before writing any Harness skill anywhere:
- enumerate the 14 canonical Harness skill names from the upstream `skills/` directory;
- determine every target skill root that would be used;
- scan all target roots for collisions for all 14 names before writing any skill;
- a same-name skill whose frontmatter metadata contains the `ai-engineering-harness` key is a managed Harness-owned copy and may be updated;
- a same-name skill without that metadata key is project-local or otherwise unowned by the Harness: do not overwrite, rename, merge, or modify it. Stop the shared-skill installation phase and report the collision. The rest of the Harness adoption may continue if it is otherwise safe.

Do not ask me to restate facts that the repository already answers. Do not assume environment names such as dev, stage, staging, prod, or production, and do not assume that the project has exactly two environments or any deployment environments at all.

If repository evidence is missing, stale, contradictory, or genuinely ambiguous:
- do not invent a deployment, release, approval, build/test, model-routing, runtime, native skill path, or tool-native policy;
- ask only focused questions that materially affect safe harness adoption itself;
- otherwise continue the minimal harness adoption without guessing, and report the unresolved item in the final Project readiness section for human follow-up.

Backup requirement:
- before modifying any existing file, including an existing Harness-owned skill, create a byte-for-byte backup of that file outside the repository, preferably in the operating system's temporary directory;
- report the exact backup path(s) in your final summary;
- do not create backup copies inside the repository unless I explicitly ask for that;
- if you cannot create a safe backup outside the repository, stop before modifying the file and explain why.

Preserve all existing project-specific content, rules, skills, docs, tests, deployment conventions, uncommitted work, and tool-specific value.

Apply the harness minimally:
- if AGENTS.md does not exist, copy the harness AGENTS.md verbatim;
- if AGENTS.md already exists, preserve it exactly outside the documented shared-baseline markers and append/update the shared harness AGENTS.md verbatim inside those markers;
- MODEL_ROUTING.md must remain a verbatim copy of the harness MODEL_ROUTING.md when harness-owned;
- MODEL_CATALOG.md must remain a verbatim copy of the shared current catalog when harness-owned; do not move project-local model preferences into it;
- install the canonical Harness-owned `skills/<name>/SKILL.md` files verbatim into the selected verified native skill root(s), or into neutral `harness/skills/` when native activation cannot be verified or is not desired;
- never edit a copied Harness skill to make it project-specific; project-specific guidance stays in project-local rules, docs, tests, configuration, or separate project-owned skills;
- if the project already has local model/tool routing rules, preserve them where they are; do not copy, summarize, map, or duplicate those project-specific model names or policies into MODEL_ROUTING.md or MODEL_CATALOG.md;
- if existing project-local routing appears semantically incompatible with the shared tier policy, do not invent a reconciliation or mapping. Stop and report the conflict for human review;
- add the thin CLAUDE.md adapter if Claude Code is used now or is intended to be used with this project. If CLAUDE.md already exists, preserve its existing value and add the shared AGENTS.md reference rather than replacing it. If Claude Code is definitely not used for this project, CLAUDE.md may be omitted.

Do not copy, symlink, generate, mirror, or synchronize project-local/tool-native skills or rules merely to make them look portable across tools.
Do not create `.agents/workflows/`, `.ai/`, installers, manifests, orchestration, project overlays, extra adapters, or unrelated process files. `.agents/skills/` may be created only when needed for verified native activation of Harness-owned shared skills.
Do not modify application code merely to install the harness.
Do not silently edit existing project-local deployment, release, environment, Git, model-routing, rules, skills, or documentation files merely to resolve a discovered ambiguity. In the final report, recommend the smallest existing project-local file(s) that should record each durable clarification, and wait for explicit approval before changing them.
Do not commit, push, merge, deploy, publish, access production/live systems, or perform unrelated cleanup.

When finished:
1. show git status;
2. show the exact harness-related diff;
3. list every file changed or added;
4. list the backup path for every existing file you modified;
5. explain what project-specific content/rules you preserved and any conflicts;
6. confirm that AGENTS.md shared content, MODEL_ROUTING.md, MODEL_CATALOG.md, the shared portion of CLAUDE.md, and every installed Harness-owned skill follow the upstream Harness source as required;
7. report the detected AI runtimes and the repository evidence for each;
8. report the selected skill root(s), why each root was chosen, how many Harness skills were installed or updated, every collision found, and whether each managed installed copy is verbatim-equal to its canonical upstream `skills/<name>/SKILL.md`;
9. report the exact upstream Harness commit used;
10. confirm that no unrelated file was changed and that no branch/worktree/project copy was created for adoption;
11. provide a Project readiness section covering, when applicable:
   - environment/deployment topology;
   - customer-facing/live publication boundary;
   - branch/tag/release/deployment triggers;
   - build/test/lint/analysis commands;
   - model/tool-specific routing or cost policy;
   - runtime/skill activation status;
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

Do not migrate or duplicate project-specific rules merely to fit the harness. Existing tool-native rules and skills (for example `.cursor/rules/`, `.cursor/skills/`, `.agents/skills/`, `.agents/workflows/`, and `.claude/skills/`), repository instructions, documentation, ADRs, tests, deployment conventions, and other local assets stay where they are unless the project independently decides to change them.

Tool-native rule and skill directories such as `.cursor/rules/`, `.cursor/skills/`, `.agents/skills/`, `.agents/workflows/`, and `.claude/skills/` are runtime features of one tool, not shared project truth. The harness deliberately does not copy, symlink, generate, or synchronize them across tools: formats and invocation differ, and mirrored copies can go stale while still carrying authority. Durable project truth must therefore not live only inside one tool's skill or rule directory — keep it in docs, ADRs, tests, scripts, code/configuration, and `AGENTS.md`, where any tool or human can reconstruct it.

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
3. Discover existing AI/project instructions and canonical documentation. Typical locations include `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/`, `.cursor/skills/`, `.agents/skills/`, `.agents/workflows/`, `.github/`, `CONTRIBUTING.md`, project docs, ADRs, tests, CI/release files, and deployment documentation.
4. Reconstruct the project's environment/release topology and documented validation commands from repository evidence. Do not assume environment names, count, promotion flow, or deployment automation.
5. Detect which AI runtimes are genuinely used by the repository from repository evidence; an installed CLI alone is insufficient. Determine verified project-level skill roots for those runtimes before choosing any native skill placement.
6. Select the smallest set of verified skill roots that covers the detected runtimes. Current verified shared roots are `.agents/skills/` for Cursor, Antigravity, and Codex, and `.claude/skills/` for Claude Code; Cursor can also consume `.claude/skills/`. If one root covers all detected runtimes, use one copy. If a runtime cannot be mapped to a verified native root, use neutral `harness/skills/` for the Harness-owned skills that need a non-native placement and do not claim native activation.
7. Before writing any skill, scan all selected target roots for all canonical Harness skill names. A same-name skill with `metadata.ai-engineering-harness` is managed; a same-name skill without that key is not Harness-owned. Do not overwrite an unowned collision: stop only the skill-installation phase, report it, and continue the rest of adoption when safe.
8. If a material fact needed for safe adoption is genuinely unresolved, ask only the focused question needed. Otherwise do not block adoption: preserve the ambiguity, report it in Project readiness, and recommend where the durable answer belongs project-locally.
9. Before modifying an existing target file, including a managed Harness skill, make a byte-for-byte backup outside the repository and report its path. Do not place adoption backups in the project tree by default.
10. Add or update `AGENTS.md` using the applicable case below.
11. Add `MODEL_ROUTING.md` as a verbatim shared policy file and `MODEL_CATALOG.md` as the verbatim current shared catalog. Existing project-local model/tool routing rules remain where they are and authoritative for their local mechanics.
12. Install Harness-owned shared skills verbatim from canonical `skills/` into the selected skill root(s). Do not edit project-local skills or rules and do not create redundant copies merely for symmetry.
13. Add the thin `CLAUDE.md` adapter when Claude Code is used now or is expected to be used with the project. If a `CLAUDE.md` already exists, preserve its Claude-specific value and add `@AGENTS.md` rather than replacing it. If Claude Code is definitely not used, it may be omitted.
14. Do not create `.ai/`, `.agents/workflows/`, installers, manifests, orchestration, project overlays, or extra adapters solely because this harness exists. `.agents/skills/` may be created only for verified Harness-owned skill activation.
15. Do not silently edit project-local policy files to make the adoption look conflict-free. Surface unresolved/stale policy, recommend the smallest canonical file(s) to update, and wait for explicit approval.
16. Review the final Git diff, verify every managed skill copy against canonical upstream content, and report the exact upstream commit. Do not commit, push, deploy, publish, or perform unrelated cleanup unless explicitly requested.

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

Use the repository as the update source of truth rather than maintaining a separate installer. An update refreshes only Harness-owned shared content and must preserve project-local value.

Recommended update behavior:

1. Inspect the target repository and the current upstream Harness before editing, including all installed Harness-owned skill roots and their `metadata.ai-engineering-harness` ownership markers.
2. Record the exact upstream Harness commit being applied.
3. Preserve the existing Harness skill placement. Do not migrate a managed skill root merely because another runtime path is now preferred or newly supported.
4. Before changing any existing Harness-owned file, including any managed skill, make a byte-for-byte backup outside the repository.
5. If `AGENTS.md` contains the shared-baseline markers, replace only the content between the markers with the current upstream `AGENTS.md` verbatim and update the marker date. Preserve everything outside the markers exactly.
6. Refresh `MODEL_ROUTING.md` from upstream verbatim when it is Harness-owned.
7. Refresh `MODEL_CATALOG.md` from upstream verbatim when it is Harness-owned. Do not rewrite project-local model preferences merely because the catalog changed; report stale local choices for human review.
8. Refresh only the shared adapter portion of `CLAUDE.md` where applicable; preserve existing Claude-specific project value.
9. For each currently installed Harness-owned skill that still exists upstream, back up the existing file and replace it verbatim from the corresponding canonical upstream `skills/<name>/SKILL.md`.
10. For a new upstream Harness skill, add it to the existing managed Harness skill root(s) only when no unowned same-name collision exists there. If an unowned collision exists, do not overwrite or merge it; stop that skill update and report the collision.
11. Never modify project-local or otherwise unowned skills and rules as part of a Harness update.
12. If a managed Harness-owned skill is installed locally but no longer exists upstream, do **not** delete it automatically. Report it as an **orphaned Harness skill** and ask for a human decision.
13. Do not copy, translate, migrate, or synchronize project-local/tool-native rules, skills, model mappings, or workflows between runtimes.
14. Surface semantic conflicts or newly stale project-local rules instead of silently rewriting them.
15. Verify every managed installed Harness skill that has a current canonical upstream counterpart is verbatim-equal to that canonical file; report any mismatch, collision, orphan, backup path, managed root, and the exact upstream commit.
16. Review the exact diff and run the current installation tests, including the cross-tool runtime-capability test when multiple AI runtimes are used.
17. Do not commit, push, deploy, publish, or change application code merely to update the Harness.

### Copy/paste update prompt

```text
Update the AI Engineering Harness already installed in this repository from the current upstream source:
https://github.com/BurakD/ai-engineering-harness

Follow the upstream README's current "Update an existing installation" procedure exactly. Treat the upstream README as the maintenance source of truth; do not rely on an older copied prompt or previous chat history.

Stay in this repository and on the current branch unless this repository's own documented policy requires otherwise. Do not create a branch, worktree, duplicate checkout, installer, or synchronization script merely for this update.

Before changing anything:
- inspect the current branch and working-tree status;
- inspect the currently installed AGENTS.md, MODEL_ROUTING.md, MODEL_CATALOG.md, CLAUDE.md where present, existing shared-baseline markers, and relevant project-local/tool-native rules;
- discover every installed Harness-owned skill root and every skill whose frontmatter metadata contains the `ai-engineering-harness` key;
- inspect current upstream AGENTS.md, MODEL_ROUTING.md, MODEL_CATALOG.md, CLAUDE.md, README.md, and canonical `skills/`;
- record the exact upstream commit you are applying;
- identify every existing file that would be modified.

Do not relocate existing Harness-owned skills during an update. Preserve each managed installation root even if a different native path is now preferred or newly available.

Before modifying each existing file, including each managed Harness skill, create a byte-for-byte backup outside the repository, preferably in the operating system's temporary directory, and report its exact path.

Preserve all project-local content, rules, docs, skills, model mappings, uncommitted work, application code, deployment conventions, and tool-specific value.

Update only Harness-owned shared content according to the current upstream README:
- refresh only the shared AGENTS.md baseline inside its markers; preserve everything outside the markers exactly;
- keep MODEL_ROUTING.md a verbatim upstream shared policy file when it is Harness-owned;
- keep MODEL_CATALOG.md a verbatim upstream current catalog when it is Harness-owned; do not use catalog refreshes to overwrite project-local model preferences;
- refresh only the shared CLAUDE.md adapter portion where applicable, preserving project-specific Claude instructions;
- for each installed skill carrying `metadata.ai-engineering-harness`, if the same canonical skill exists upstream, back up the installed SKILL.md and replace it verbatim with the upstream canonical SKILL.md;
- when upstream contains a new Harness skill, add it to the existing managed Harness skill root(s) only if no unowned same-name skill exists there;
- if the same name already exists without the `ai-engineering-harness` metadata key, do not overwrite, merge, rename, or modify it; report the collision;
- if a locally installed managed Harness skill no longer exists upstream, do not delete it. Report it as an orphaned Harness skill and ask for a human decision;
- never copy, translate, migrate, synchronize, or treat project-local/tool-native model names, agents, subagents, skills, rules, workflows, or invocation syntax as Harness-owned content or as capabilities of another runtime.

If current project-local instructions conflict semantically with the new shared policy, do not invent a reconciliation. Stop before rewriting project-local policy and report the exact conflict for human review.

If a project-local preferred model is no longer supported by the current catalog or live runtime, do not silently replace it. Report the stale preference and the closest current options for human review.

Do not modify application code, project-local deployment/release policy, tool-native rules/skills, or project documentation merely to make the Harness update look clean.
Do not commit, push, merge, deploy, publish, or access production/live systems.

When finished:
1. show git status;
2. show the exact Harness-related diff;
3. report the exact upstream Harness commit used;
4. list every changed file and every backup path;
5. list every discovered managed Harness skill root and explain that the existing placement was preserved;
6. report skills updated, newly added, skipped because of unowned collisions, and orphaned Harness skills awaiting human review;
7. verify and report verbatim equality between every managed installed Harness skill with an upstream counterpart and its canonical upstream `skills/<name>/SKILL.md`;
8. identify any semantic conflicts, stale project-local model choices, or project-local instructions made stale by the new shared policy/catalog;
9. confirm that unrelated and project-local content was preserved;
10. run the README's current installation tests that are applicable, including the cross-tool runtime-capability test where multiple runtimes are used;
11. stop for human review.
```

This update prompt is intentionally thin: the durable update algorithm lives in the current upstream README, so future maintenance changes do not require distributing a new project-specific installer or prompt file.

## Manual fallback

If your coding agent cannot access this repository or you prefer manual installation, copy only the shared files you need into the project root.

For a new project with no existing `AGENTS.md`:

```bash
git clone --depth 1 https://github.com/BurakD/ai-engineering-harness /tmp/ai-engineering-harness
cp /tmp/ai-engineering-harness/{AGENTS.md,MODEL_ROUTING.md,MODEL_CATALOG.md,CLAUDE.md} .
```

`CLAUDE.md` is only needed when Claude Code is used. Other runtimes should use their documented project-context mechanisms when needed; do not add adapters solely for symmetry. If your shell does not support brace expansion, or on Windows, copy the same files by any normal file-copy method.

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
