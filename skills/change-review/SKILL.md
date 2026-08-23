---
name: change-review
description: Reviews a completed code or configuration change for correctness, regressions, edge cases, architecture violations, security issues, compatibility risks, and missing validation. Use for diffs, pull requests, or completed implementations before acceptance or release.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Change review

1. Read the task, specification, acceptance criteria, and relevant project rules before judging the implementation.

2. Inspect the complete relevant diff and trace the affected control flow, data flow, contracts, state transitions, and externally observable behavior as needed.

3. Review correctness, regression risk, error handling, security, privacy, compatibility, concurrency, performance, observability, maintainability, and tests in proportion to the change.

4. Look for missing states and failure paths, not only defects visible on the primary successful path.

5. Prefer concrete evidence from code, tests, specifications, runtime behavior, static analysis, or reproducible scenarios over stylistic preference or speculation.

6. Classify findings by impact and urgency. Clearly separate correctness or safety problems from optional improvements.

7. Do not modify unrelated code or fix findings merely because they were discovered. Make changes only when they are within the authorized scope.

8. Run or request deterministic checks that can confirm or disprove material findings when practical.

9. For significant or high-risk work, prefer a reviewer with fresh context that reconstructs the change from the repository rather than relying on the implementation conversation.

Report findings first, ordered by impact, followed by validation evidence, assumptions, and residual risk. If no material findings remain, say so explicitly.