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
6. If the **Last verified** date is no longer reasonably current for the decision at hand, treat concrete catalog entries as unverified until refreshed from current official sources or confirmed by live runtime discovery.

## Current recommended mappings

These are starting points, not literal cross-vendor equivalences. The table is a maintained set of useful runtime mappings, **not an exhaustive list of tools supported by the shared harness**; a runtime does not need a catalog row in order to consume the vendor-neutral policy.

| Runtime / tool | FAST | STANDARD | REASONING | FRONTIER | Live discovery / notes |
|---|---|---|---|---|---|
| **Cursor** | Composer 2.5 for inexpensive routine execution; Composer 2.5 Fast when latency matters more than token price | Composer 2.5 is a strong default for hands-on coding; Cursor Auto/Router is acceptable when exact model identity is not required | Claude Fable 5 at a suitable reasoning level when available; otherwise another strong reasoning model exposed by Cursor | Claude Fable 5 at the highest justified reasoning level when available | Use the model picker / current Cursor model list. Auto/Router is dynamic and does not provide a stable, auditable underlying-model mapping, so select explicitly when a workflow requires a known planner or reviewer. |
| **Claude Code** | Claude Haiku 4.5 for small, latency/cost-sensitive work when available | Claude Sonnet 5 | **Claude Fable 5 when quality-first reasoning is justified and the account/runtime exposes it**; Claude Sonnet 5 at higher effort is the lower-cost default alternative, with Claude Opus 4.8 as another strong fallback where useful | Claude Fable 5 at the highest justified effort for the hardest long-horizon work | Fable 5 is Anthropic's most capable generally available Claude model and is officially supported in Claude Code. Availability can still depend on plan, credits, workspace policy, or temporary capacity. |
| **OpenAI Codex CLI / IDE** | GPT-5.6 Luna | GPT-5.6 Terra | GPT-5.6 Sol with an appropriate reasoning effort | GPT-5.6 Sol with the strongest reasoning setting actually exposed by the current Codex runtime | Current OpenAI guidance exposes Sol, Terra, and Luna in Codex according to plan. Do not assume every API reasoning mode is exposed identically in every Codex client/version. |
| **Antigravity CLI (`agy`)** | Prefer the fastest/lowest-effort model shown by `agy models` that is adequate for the task | Prefer the balanced coding model shown by `agy models` | Prefer the strongest reasoning-capable model shown by `agy models` | Prefer the strongest model/effort actually shown by `agy models`; manual escalation | Run `agy models` before relying on a named model. Google's official codelab explicitly documents this command because the available model set is dynamic. |

## Dynamic routers and auto-selection

Auto-selection or router modes can be useful, but they are runtime routers rather than stable model mappings. Their model pools and selection logic may change with task fit, reliability, capacity, product policy, or other runtime signals. Cursor Auto / Router is one concrete example. When repeatability, model-specific evaluation, planner/worker separation, or cost predictability matters, choose a concrete verified capability instead of treating any dynamic router as a fixed tier-to-model mapping.

## Planner / worker patterns

A project may intentionally use a stronger planner/reviewer and a cheaper implementation worker when the active runtime supports that orchestration. The portable pattern is the separation of roles, not any particular vendor model or subagent API.

For example, Cursor can support patterns such as **Fable 5 planning/review + Composer 2.5 implementation** when those models and the required agent/subagent mechanics are genuinely available in the current Cursor runtime. In another runtime, preserve the same semantic intent only with capabilities that runtime actually exposes.

Claude Code, Codex, Antigravity, or another tool must not pretend it can invoke Cursor-native subagents merely because a project file describes them.

## User and project overrides

Do not edit this shared catalog merely to record one project's personal preference. Keep durable project-specific choices in that project's existing rules/docs/configuration, for example:

- a preferred planner model for a particular runtime;
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
- Cursor Composer 2.5: https://cursor.com/blog/composer-2-5
- Cursor model-economics research using Fable 5 + Composer 2.5: https://cursor.com/blog/agent-swarm-model-economics
- Anthropic Claude Fable 5: https://www.anthropic.com/claude/fable
- Anthropic Fable 5 redeployment / Claude Code availability: https://www.anthropic.com/news/redeploying-fable-5
- Anthropic Claude Sonnet 5: https://www.anthropic.com/news/claude-sonnet-5
- Anthropic Claude Haiku 4.5: https://www.anthropic.com/claude/haiku
- Anthropic model system cards (includes Opus 4.8): https://www.anthropic.com/system-cards
- OpenAI GPT-5.6 / Codex availability: https://help.openai.com/en/articles/20001354-gpt-56-in-chatgpt/
- Google Antigravity CLI model discovery: https://codelabs.developers.google.com/antigravity-cli-hands-on

Vendor and model names are trademarks of their respective owners. This catalog is informational and is not an endorsement or guarantee of availability, pricing, or performance.