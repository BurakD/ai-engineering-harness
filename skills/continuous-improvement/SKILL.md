---
name: continuous-improvement
description: Turns repeated mistakes, costly failures, and recurring review findings into durable engineering safeguards. Use when a failure class should be prevented by a test, check, script, skill, concise rule, documentation change, or other maintainable control.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Continuous improvement

Use this procedure when a failure class repeats, a costly incident exposes a missing safeguard, or recurring manual review reveals a preventable source of engineering risk.

1. Describe the general failure class and its impact rather than preserving only the details of one incident.

2. Determine why existing safeguards did not prevent, detect, or clearly explain the failure.

3. Choose the smallest durable prevention or detection mechanism that reliably addresses the failure. Prefer, when appropriate:
   deterministic test or invariant → static or runtime check → script or hook → focused skill → concise always-on rule → documentation.

4. Prefer mechanisms that fail clearly and mechanically over reminders that require repeated model or human judgment.

5. Keep narrow or infrequent procedures out of always-on context when an on-demand skill or deterministic check is sufficient.

6. Keep project-specific lessons in the project. Promote a lesson into shared engineering guidance only when the failure class is genuinely reusable across unrelated projects and technologies.

7. Before adding a new safeguard, check whether an existing test, rule, skill, script, or document should be extended instead. Merge or remove duplicated guidance when practical.

8. Verify that the proposed safeguard would have prevented, detected, or made the original failure materially easier to diagnose without imposing disproportionate friction on unrelated work.

9. Record how the safeguard itself can be maintained, tested, or removed if its underlying risk disappears.

The goal is continuous reduction of repeated engineering failure, not accumulation of process artifacts.

Report the failure class, chosen safeguard, why that layer is appropriate, evidence that it addresses the problem, and any added maintenance cost.