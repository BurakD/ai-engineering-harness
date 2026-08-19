# Model Routing

Goal: keep quality high without paying high-model cost for every task, while allowing different AI tools and models to continue from the same repository context.

## Capability tiers

| Work type | Tier | Typical examples |
|---|---|---|
| Small / mechanical | FAST | rename, formatting, narrow edit, repetitive change |
| Normal implementation | STANDARD | clear feature, routine bug fix, bounded refactor |
| Difficult / ambiguous / critical | REASONING | architecture, hard debugging, security-sensitive work, compatibility or protocol risk, release review |
| Exceptional hardest case | FRONTIER | only when lower tiers are insufficient or explicitly requested |

The tier definitions are stable policy. Exact model names and subscription economics are temporary implementation details. See `MODEL_CATALOG.md` for the current time-sensitive model/runtime catalog and recommended starting mappings.

## Tool mapping

Choose the closest current model, mode, or agent capability in the **active runtime** that matches the requested tier. Prefer subscription-included or otherwise agreed capacity before paid escalation.

If a preferred mapping would require additional paid credits, pay-as-you-go usage, or other spend that has not already been approved, treat that mapping as unavailable for automatic routing. Select the next-best **verified** capability that satisfies the tier within included or already-agreed capacity. Do not interrupt the user merely because the first-choice model is unavailable when an acceptable included fallback exists; ask only when no acceptable fallback exists or the downgrade would materially change quality, risk, or the requested outcome.

- **FAST**: inexpensive, fast coding model/mode suitable for low-risk mechanical work.
- **STANDARD**: default general coding model/mode with a balanced quality/cost profile.
- **REASONING**: stronger reasoning model/mode for difficult, ambiguous, architectural, security-sensitive, compatibility-sensitive, or release-sensitive work.
- **FRONTIER**: strongest available model/mode only when explicitly justified; manual escalation by default.

Use `MODEL_CATALOG.md` as current shared guidance when it covers the active runtime, but verify actual availability in the live runtime/session. A project may document current preferred mappings for the tools it actually uses when that is useful; project-local preferences remain authoritative for that project when compatible with this policy.

### Runtime capability rule

- A concrete model, agent, subagent, mode, or delegation mechanism may be selected only if the active runtime/session can actually invoke it.
- Tool-native mappings are scoped to the runtime that provides them. A Cursor rule naming a Cursor model or subagent does not make that model or subagent available in Claude Code, Codex, Antigravity, or another runtime; the same principle applies in every direction.
- Do not claim a delegation, model switch, or subagent call that the active runtime cannot perform.
- **Live capability discovery is fail-closed.** If the runtime's model/agent discovery command, picker, API, or equivalent check fails, hangs, is interrupted, returns incomplete output, or otherwise does not establish availability, the named capability is unverified. Do not substitute remembered or inferred model names. Continue with a generic role description or state the limitation until availability is actually verified.
- When another tool's native rule expresses a useful portable intent, preserve the intent with the closest capability that is genuinely available in the active runtime. Examples include separating planning from implementation, using a cheaper worker for routine execution, or requesting an independent review.
- Do not invent literal cross-vendor model equivalences. If the project requires a named model or mechanism that is unavailable in the active runtime and no acceptable equivalent is defined, state the limitation and ask for a decision when it materially affects the work.
- If the same named model or mechanism is genuinely available in the active runtime, it may be used; availability must be established by the active runtime, not inferred from another tool's config files.

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

Tool-specific mappings may also remain in tool-native project rules when they are genuinely useful for that tool. They do not automatically bind other runtimes.

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

This file is guidance. It does not itself switch models, create subagents, or spend money; the active tool/runtime and the human operator perform the actual selection.