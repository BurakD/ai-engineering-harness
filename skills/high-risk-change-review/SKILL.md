---
name: high-risk-change-review
description: Applies additional planning, validation, review, and approval discipline to changes with elevated security, privacy, authorization, financial, data-loss, secret, public-contract, migration, release, or other material operational risk.
metadata:
  ai-engineering-harness: "2.0.0"
---

# High-risk change review

1. Determine whether the change is high risk from the project's applicable rules, `AGENTS.md`, canonical documentation, ADRs, configuration, contracts, and the behavior actually affected. Do not classify risk from file names or change size alone.

2. Identify the assets, users, data, permissions, contracts, money, credentials, availability, or irreversible state that could be affected by failure.

3. Require explicit acceptance criteria, important failure modes, compatibility impact, validation strategy, and rollback or recovery approach before implementation when the risk justifies them.

4. Prefer additive, reversible, least-privilege, and narrowly scoped changes when those properties reduce the identified risk.

5. Require deterministic tests, analyzers, validation, rehearsal, or other evidence for the critical properties that can be checked mechanically.

6. Check authorization, data integrity, confidentiality, failure isolation, auditability, and externally visible compatibility where relevant.

7. Use an independent fresh-context review after implementation when it materially reduces risk. Use the general change-review procedure for the completed diff in addition to the risk-specific checks in this skill.

8. Respect all project approval boundaries. This skill never authorizes deployment, publication, destructive operations, credential changes, spending, or other high-impact actions.

9. Record durable architectural, operational, security, or risk decisions in the project's canonical source when future maintainers would otherwise need to rediscover them.

Do not waive high-risk review because the implementation is short or apparently simple. Risk is determined by potential impact and affected behavior.

Report why the change is or is not high risk, the safeguards applied, validation evidence, required human decisions, and residual risk.