# Model Routing

Goal: keep quality high without paying high-model cost for every task, while allowing different AI tools and models to continue from the same repository context.

## Capability tiers

| Work type | Tier | Typical examples |
|---|---|---|
| Small / mechanical | FAST | rename, formatting, narrow edit, repetitive change |
| Normal implementation | STANDARD | clear feature, routine bug fix, bounded refactor |
| Difficult / ambiguous / critical | REASONING | architecture, hard debugging, security-sensitive work, compatibility or protocol risk, release review |
| Exceptional hardest case | FRONTIER | only when lower tiers are insufficient or explicitly requested |

The tier definitions are stable policy. Exact model names and subscription economics are temporary implementation details.

## Tool mapping

Choose the closest current model or mode in the active tool that matches the requested tier. Prefer subscription-included or otherwise agreed capacity before paid escalation.

- **FAST**: inexpensive, fast coding model/mode suitable for low-risk mechanical work.
- **STANDARD**: default general coding model/mode with a balanced quality/cost profile.
- **REASONING**: stronger reasoning model/mode for difficult, ambiguous, architectural, security-sensitive, compatibility-sensitive, or release-sensitive work.
- **FRONTIER**: strongest available model/mode only when explicitly justified; manual escalation by default.

A project may document current preferred mappings for its actual tools when that is useful, but version-specific model names are guidance rather than durable policy.

## Start low, escalate deliberately

Start no higher than necessary. Escalate when one or more of these apply:

- serious attempts at the current tier fail,
- the task crosses an important security, data, compatibility, deployment, or release boundary,
- architecture or requirements remain materially unclear or contradictory,
- protocol or compatibility risk cannot be resolved confidently,
- migration or release risk benefits from stronger reasoning or fresh review,
- repository-local project rules require a higher minimum tier.

Do not automatically escalate to FRONTIER.

## Project-specific overrides

Project-specific rules may raise the minimum tier or require additional review for particular areas, for example authentication, payments, production data, public APIs, device protocols, migrations, or store releases.

Keep those overrides in the project repository's normal rules, docs, ADRs, tests, or configuration. Do not copy them into this shared harness.

## Cross-model handoff

A model switch should not require copying chat history. The next model should first read:

1. `AGENTS.md`,
2. relevant repository-local project instructions,
3. relevant canonical docs and ADRs,
4. current branch and working-tree status,
5. relevant recent commits or diffs,
6. affected code and tests.

If the previous model made a durable decision, that decision belongs in the repository: code, test, config, doc, ADR, or project-local rule.

## Review independence

For high-risk work, a fresh-context review can be more valuable than simply increasing model size. When practical, use a separate model/session that reconstructs context from the repository and reviews the actual diff rather than inheriting the implementation conversation.

This file is guidance. It does not itself switch models or spend money; the active tool/runtime and the human operator perform the actual selection.
