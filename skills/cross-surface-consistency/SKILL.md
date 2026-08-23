---
name: cross-surface-consistency
description: Checks that equivalent capabilities behave consistently across multiple interfaces or channels such as web, mobile, desktop, CLI, APIs, admin tools, or partner integrations. Use when one change can create accidental behavioral drift between surfaces.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Cross-surface consistency

1. Identify every interface, client, channel, integration, or operational surface that exposes, controls, or depends on the affected capability.

2. Determine the canonical behavior or contract that should be shared across those surfaces and identify where intentional differences are permitted.

3. Compare relevant inputs, validation, defaults, permissions, state transitions, outputs, terminology, error semantics, availability rules, and side effects across surfaces.

4. Check authentication, authorization, feature availability, data representation, analytics or event behavior, and compatibility expectations where they form part of the shared capability contract.

5. Distinguish intentional platform- or audience-specific behavior from accidental drift. Do not force identical presentation where only semantic consistency is required.

6. Prefer shared domain or service logic for shared rules when the project's architecture supports it, while allowing interface-specific adaptation at appropriate boundaries.

7. Add targeted parity or contract tests, shared fixtures, schema checks, or deterministic comparisons when they can protect important cross-surface behavior.

8. Document intentional asymmetry when future maintainers could otherwise mistake it for a defect.

9. When a defect is isolated to the quality of one individual interface rather than inconsistency between interfaces, use the interface QA procedure instead of expanding this review unnecessarily.

Report the surfaces examined, shared behavior verified, intentional differences, accidental drift found, validation evidence, and deferred consistency risks.