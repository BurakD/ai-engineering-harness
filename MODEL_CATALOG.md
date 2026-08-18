# Model Catalog

Last verified: **2026-08-18**

This file is the time-sensitive companion to `MODEL_ROUTING.md`.

`MODEL_ROUTING.md` defines the stable FAST / STANDARD / REASONING / FRONTIER policy. This catalog records current, evidence-based model/runtime options and recommended starting points. It is intentionally easier to update as vendors, products, pricing, plans, and model names change.

## Precedence and safety

1. **The active runtime/session is authoritative for what can actually be invoked.** A model listed here is not proof that the current account, plan, region, client version, or session can use it.
2. **Project-local tool-specific rules may choose a different model for that tool** when the model is genuinely available there.
3. This catalog provides shared defaults and discovery guidance; it does not override project-specific risk, cost, compliance, or approval policy.
4. Never claim a model switch, subagent call, or cross-tool delegation that the active runtime cannot actually perform.
5. Prefer live discovery over stale catalog entries. If the live runtime contradicts this file, follow the runtime and report that the catalog may need refresh.

## Current recommended mappings

These are starting points, not literal cross-vendor equivalences.

| Runtime / tool | FAST | STANDARD | REASONING | FRONTIER | Live discovery / notes |
|---|---|---|---|---|---|
| **Cursor** | Composer 2.5 for inexpensive routine execution; Composer 2.5 Fast when latency matters more than token price | Composer 2.5 is a strong default for hands-on coding; Cursor Auto/Router is acceptable when exact model identity is not required | Claude Fable 5 at a suitable reasoning level when available; otherwise another strong reasoning model exposed by Cursor | Claude Fable 5 at the highest justified reasoning level when available | Use the model picker / current Cursor model list. Auto/Router is dynamic and does not provide a stable, auditable underlying-model mapping, so select explicitly when a workflow requires a known planner or reviewer. |
| **Claude Code** | Claude Haiku 4.5 for small, latency/cost-sensitive work when available | Claude Sonnet 5 | Claude Sonnet 5 at higher effort or Claude Opus 4.8 when deeper reasoning is useful | Claude Fable 5 for the hardest quality-first work when the account/runtime exposes it | `claude --model <model>` selects a model for the session. Fable 5 and Sonnet 5 are officially available in Claude Code; account/credit availability can still vary. |
| **OpenAI Codex CLI / IDE** | GPT-5.6 Luna | GPT-5.6 Terra | GPT-5.6 Sol with an appropriate reasoning effort | GPT-5.6 Sol with the strongest reasoning setting actually exposed by the current Codex runtime | Current OpenAI guidance exposes Sol, Terra, and Luna in Codex according to plan. Do not assume every API reasoning mode is exposed identically in every Codex client/version. |
| **Antigravity CLI (`agy`)** | Prefer the fastest/lowest-effort model shown by `agy models` that is adequate for the task | Prefer the balanced coding model shown by `agy models` | Prefer the strongest reasoning-capable model shown by `agy models` | Prefer the strongest model/effort actually shown by `agy models`; manual escalation | Run `agy models` before relying on a named model. Google's official codelab explicitly documents this command because the available model set is dynamic. |

## Why Cursor Auto is not the catalog

Cursor Auto / Router is useful, but it is a runtime router rather than a stable model mapping. Cursor documents that Auto chooses a model dynamically based on task fit, reliability/capacity and related signals, and the exact pool can change. When repeatability, model-specific evaluation, planner/worker separation, or cost predictability matters, choose a concrete model instead of treating Auto as a fixed tier-to-model mapping.

## Planner / worker patterns

A project may intentionally use a stronger planner/reviewer and a cheaper implementation worker when the active runtime supports that orchestration. For example, Cursor can support patterns such as **Fable 5 planning/review + Composer 2.5 implementation** when those models and the required agent/subagent mechanics are genuinely available in the current Cursor runtime.

The same semantic pattern may be useful elsewhere, but the concrete model names and delegation mechanism must be re-selected from that runtime's real capabilities. Claude Code, Codex, Antigravity, or another tool must not pretend it can invoke Cursor-native subagents merely because a project file describes them.

## User and project overrides

Do not edit this shared catalog merely to record one project's personal preference. Keep durable project-specific choices in that project's existing rules/docs/configuration, for example:

- a preferred planner model for Cursor;
- a cost ceiling;
- a minimum tier for auth, payments, migrations, or release work;
- a prohibition on a provider or model for privacy/compliance reasons.

During a harness update, shared catalog changes should not overwrite those project-local preferences. If an upstream catalog change makes a local preference stale or unavailable, report the conflict for human review.

## Maintaining this catalog

Catalog updates should be small and evidence-based:

1. Check the vendor/tool's current official documentation first.
2. Prefer runtime-specific availability evidence over general API availability.
3. Record only models or discovery mechanisms that are reasonably current and useful to the tier policy.
4. Update the **Last verified** date.
5. Remove or demote stale entries instead of accumulating historical model names.
6. Keep pricing details minimal unless they directly affect the routing recommendation; prices and subscription entitlements change faster than capability tiers.
7. Do not modify `MODEL_ROUTING.md` merely because model names changed.

### Copy/paste catalog refresh prompt

```text
Refresh MODEL_CATALOG.md in this AI Engineering Harness repository.

Use current official primary sources for the runtimes already covered by the catalog. Verify current model availability, runtime-specific selection/discovery mechanisms, and whether the existing FAST / STANDARD / REASONING / FRONTIER starting recommendations are still sensible.

Treat MODEL_ROUTING.md as stable policy. Do not change tier definitions merely because model names or vendor offerings changed.

Requirements:
- prefer official vendor/tool docs, changelogs, model pages, and runtime documentation;
- distinguish general API availability from actual availability in Cursor, Claude Code, Codex, Antigravity, or another runtime;
- never infer that a model available in one runtime is callable from another;
- prefer live-discovery commands or runtime model pickers when the available set is dynamic;
- keep the catalog concise and current rather than exhaustive;
- update the Last verified date;
- preserve project-neutral wording;
- report any uncertain or unverified entry instead of guessing.

Show the exact diff and sources used. Do not modify application/project-specific files, publish a release, or change repository visibility.
```

## Sources used for the 2026-08-18 verification

Primary or first-party sources:

- Cursor models / Auto: https://docs.cursor.com/models/
- Cursor Composer 2.5: https://cursor.com/composer
- Cursor model-economics research using Fable 5 + Composer 2.5: https://cursor.com/blog/agent-swarm-model-economics
- Cursor Fable 5 availability confirmation: https://forum.cursor.com/t/claude-fable-5-out-now/162816/46
- Anthropic Claude Fable 5: https://www.anthropic.com/claude/fable
- Anthropic Fable 5 redeployment / Claude Code availability: https://www.anthropic.com/news/redeploying-fable-5
- Anthropic Claude Sonnet 5: https://www.anthropic.com/news/claude-sonnet-5
- Anthropic Claude Haiku 4.5: https://www.anthropic.com/claude/haiku
- Anthropic model system cards (includes Opus 4.8): https://www.anthropic.com/system-cards
- OpenAI GPT-5.6 guidance: https://developers.openai.com/api/docs/guides/latest-model
- OpenAI GPT-5.6 / Codex availability: https://help.openai.com/en/articles/20001354-gpt-56-in-chatgpt/
- Google Antigravity CLI model discovery: https://codelabs.developers.google.com/antigravity-cli-hands-on

Vendor and model names are trademarks of their respective owners. This catalog is informational and is not an endorsement or guarantee of availability, pricing, or performance.
