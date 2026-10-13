# Model Catalog

Last broad verification: **2026-10-13** (official vendor/runtime documentation; not a live check of any particular user's account).

This is the time-sensitive companion to `MODEL_ROUTING.md`. That file defines the stable FAST / STANDARD / REASONING / FRONTIER capability tiers; this catalog provides **current, runtime-specific starting points**, not permanent model assignments or claims of cross-vendor equivalence.

## Precedence and safety

1. **The active runtime/session is authoritative.** A published model or catalog entry does not establish access through a particular account, plan, client, region, provider, or tool.
2. Check the runtime's model picker/discovery first. If discovery fails or returns incomplete information, treat named models as **unverified**, not as a reason to guess.
3. Project-local tool-specific preferences remain authoritative where compatible with project safety, quality, and cost rules.
4. Use included or already-approved capacity. Do not automatically opt into usage credits, pay-as-you-go, premium routing, or other new spend. Ask before material quality downgrades or unapproved spending.
5. Keep model capability/effort selection separate from **communication style**. Concise, decision-oriented explanations must not silently reduce analysis, implementation quality, testing, or required review.
6. Model choice does not authorize broader scope, additional subagents, or deployment actions. Delegation and approvals follow `AGENTS.md` and the relevant skills.

## Current recommended mappings

Recommendations are starting points, **not exhaustive supported-model lists**. Verify exact availability at runtime, especially after new releases.

| Runtime / tool | FAST | STANDARD | REASONING | FRONTIER | Runtime-specific discovery and cautions |
| --- | --- | --- | --- | --- | --- |
| **Cursor** | Composer 2.5 for scoped routine work; non-Fast variant when cost matters | Composer 2.5 or another verified balanced coding model | Claude Opus 5.5 for difficult engineering; Fable 5.1 only when its additional capacity/cost is justified and approved | Strongest verified capable model, deliberately selected for an exceptional task | Use Cursor's current model picker and official Models & Pricing page. Cursor Models (including Composer 2.5) and Other Models have different usage pools; Auto/Router is dynamic, not a stable named-model mapping. |
| **Claude Code** | Claude Haiku 5.5 when available in the current provider/session | Claude Sonnet 5.5 for daily coding | Claude Opus 5.5 at suitable/high effort for complex architecture, debugging, and review; choose stronger available capability if the actual task requires it | Claude Fable 5.1 for exceptional, long-running work **only when available within agreed spend**, otherwise the strongest verified permitted option | Check `/model`. Aliases `haiku`, `sonnet`, `opus`, `fable` follow provider-dependent mappings. Fable can require usage credits, even when other models are included. Claude Code/client versions and provider gateways can affect availability. |
| **OpenAI Codex CLI / IDE** | GPT-6 Luna for narrow, repeatable implementation or triage | GPT-6.1 Sol at ordinary reasoning effort when available | GPT-6.1 Sol at High/higher verified effort for difficult coding and review | GPT-6 Astra for hardest work when exposed by this client/account and within agreed spend | Use `/model` or `codex --model <id>`. Current documented IDs include `gpt-6-luna`, `gpt-6.1-sol`, and `gpt-6-astra`. Availability/effort settings and included usage depend on plan, sign-in, client, and rollout. Do **not** infer Codex access from API availability. |
| **Antigravity CLI (`agy`)** | Lowest sufficient available fast/low-effort model | Verified balanced coding model | Strongest verified reasoning-capable choice within agreed capacity | Strongest explicitly verified permitted option for exceptional work | Run `agy models` and use the current model picker/`--model`. Google's first-party CLI guide gives examples, not a guarantee of the exact models visible to this account today. |
| **Kiro** | Claude Haiku 4.5 or GPT-5.6 Luna where exposed; otherwise lowest-cost sufficient option | Claude Sonnet 5.5 or GPT-5.6 Terra, where available and economical | Claude Opus 5.5 or GPT-5.6 Sol for difficult agentic work | Claude Fable 5.1 **only for approved Enterprise Preview access**, otherwise strongest available permitted option | Use IDE/CLI picker or `/model` and Kiro's live catalog. Kiro still lists GPT-5.6 tiers alongside Claude 5.5. Sonnet/Opus 5.5 have rollout, region, plan, and credit implications; Fable 5.1 is limited to Kiro Enterprise Preview. |

### Important release distinctions as of 2026-10-13

- **Anthropic**: Claude Sonnet 5.5 (2026-09-28), Opus 5.5 (2026-09-22), and Haiku 5.5 (2026-10-07) supersede earlier default recommendations where the relevant runtime/provider supports them. Fable 5.1 is a separate, higher-capability/availability-constrained choice, not a routine default. In Claude Code on Anthropic API, `sonnet`, `opus`, and `haiku` currently point to 5.5; some hosted providers resolve aliases differently.
- **OpenAI**: GPT-6 Astra, GPT-6.1 Sol (released 2026-09-29), and GPT-6 Luna are current starting points in OpenAI's API guidance. Codex/Work documentation separately describes rollout and model selection; models listed for the API or ChatGPT chat are not automatically available in Codex. GPT-5.6 remains available in some contexts during the transition.
- **Cursor**: Composer 2.5 remains a documented economical baseline. Cursor's live model page now also lists Claude 5.5 models; the two usage pools and changing Auto routing matter more than a static cross-vendor tier table.
- **Kiro**: Its October 2026 catalog continues to expose GPT-5.6 Sol/Terra/Luna, plus Claude Opus 5.5 and Sonnet 5.5. Do not replace Kiro's GPT-5.6 entries with OpenAI's API/Codex GPT-6 models without Kiro-specific evidence.
- **Google Antigravity CLI**: Use `agy models`, since its available set can change independently of Gemini API releases.

## Dynamic routers, effort and communication

Auto/Router modes dynamically select a model. They can be useful for routine work but are not auditable fixed mappings. For explicit quality/cost comparisons or stable reviewer/planner identity, select a named capability that the active runtime actually exposes.

A user's preference for high effort on complex work should be respected where available. **High reasoning effort does not require a long user-facing answer.** Output style should favor a brief recommendation, rationale and decision needed, while retaining full technical analysis, verification and risks.

## Planner / worker and delegation patterns

Prefer a strong verified planner/reviewer for ambiguous or high-risk decisions and the lowest sufficient verified implementation worker for bounded tasks, **only when the active runtime supports the intended arrangement**. This is a portable role pattern, not a promise that Claude, Codex, Cursor, Kiro, or Antigravity can invoke one another's native agents.

Use the `delegation-strategy` skill to decide whether delegation is worthwhile and to bound agent scope, evidence, attempts and escalation. Do not launch extra agents merely to speed up a task that one agent can complete clearly. If a worker stalls or cannot demonstrate progress, stop or narrow the task and report the blocker instead of repeating attempts indefinitely.

## User and project overrides

Keep personal preferences, approval authority, cost ceilings, product-specific decisions, sensitive-area minimum tiers, and user/teammate communication profiles **outside this shared catalog**, in the adopting project's existing instructions or an explicitly agreed local/profile location. When a Harness update changes a suggested model, preserve project-local overrides and report unavailable or stale choices rather than silently replacing them.

## Maintaining this catalog

1. Check **current first-party product/runtime documentation** for each listed tool and relevant recent release notes. General API release pages are not sufficient evidence of availability in an IDE/CLI.
2. Prefer the runtime's live model discovery; document where account-specific confirmation cannot be performed.
3. Verify tool access, region/plan conditions, effort settings, paid-credit implications and any special preview restrictions before recommending a default.
4. Update the relevant date, change only affected rows, and demote stale models instead of accumulating historical options.
5. Do not change `MODEL_ROUTING.md` merely because model names changed. Do not promise a provider-native capability in another runtime.
6. Keep refreshes concise, evidence-based and separated from project-specific settings.

### Copy/paste catalog refresh prompt

```text
Refresh MODEL_CATALOG.md in AI Engineering Harness against current first-party
runtime docs and recent changelogs for the runtimes already covered.

Preserve MODEL_ROUTING.md tiers and project-local preferences. Verify model
availability in each specific runtime, not merely in the vendor's API. Identify
newer releases, retired choices, effort controls, subscription/paid-credit and
preview restrictions, live-discovery commands, and any dynamic router behavior.

Replace stale mappings conservatively. If runtime availability is unclear,
state that clearly; never invent a model name or automatic fallback.
Update the verification date and official sources. Show the exact diff.
Do not update unrelated project files, publish a release, or incur new spend.
```

## Primary sources checked (2026-10-13)

- Cursor model catalog / usage pools: https://cursor.com/docs/models-and-pricing
- Cursor Composer 2.5 announcement: https://cursor.com/blog/composer-2-5
- Claude Code models, aliases, effort and Fable usage: https://code.claude.com/docs/en/model-config
- Anthropic 2026 model releases: https://www.anthropic.com/news
- OpenAI Codex/Work model selection and rollout: https://learn.chatgpt.com/docs/models
- OpenAI API current model catalog (not by itself Codex access): https://developers.openai.com/api/docs/models
- OpenAI API changelog: https://developers.openai.com/api/docs/changelog
- Google Antigravity CLI official live-discovery guide: https://codelabs.developers.google.com/antigravity-cli-hands-on
- Kiro models and plan/region constraints: https://kiro.dev/docs/models/
- Kiro Sonnet 5.5 availability and October rollout: https://kiro.dev/changelog/models/claude-sonnet-5-5/
- Kiro Opus 5.5 availability and rollout: https://kiro.dev/changelog/models/claude-opus-5-5/
- Kiro Fable 5.1 Enterprise Preview restrictions: https://kiro.dev/changelog/models/claude-fable-5-1-for-enterprise/

Vendor and model names are trademarks of their respective owners. This catalog does not guarantee availability, price, entitlement or performance.
