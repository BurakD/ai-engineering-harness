---
name: delegation-strategy
description: Decides when and how to delegate work to subagents, workers, or isolated reviewer contexts. Use when verified runtime capabilities can improve parallel investigation, specialized analysis, test triage, implementation isolation, or independent review.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Delegation strategy

1. Verify that the active runtime actually supports the proposed agent, subagent, worker, parallel-session, or delegation mechanism. If support cannot be verified, continue without delegation and do not claim that delegation is active.

2. Keep small, coherent, low-risk tasks in one context unless delegation provides a clear benefit.

3. Delegate when isolation or parallelism materially improves the work, such as noisy read-heavy exploration, independent investigation of competing hypotheses, focused research, test-failure triage, specialized analysis, or fresh-context review.

4. Choose the lowest sufficient capability tier for each delegated role according to the project's model-routing and cost policy. Do not hard-code a vendor model or assume additional paid capacity.

5. Give each delegated task an explicit scope, expected output, relevant constraints, and evidence requirement. Avoid broad or overlapping assignments that duplicate work without a reason.

6. Do not allow concurrent writers to modify the same working tree or overlapping files. If parallel implementation is justified, use repository- and runtime-supported isolation only when it is permitted by project policy and the task's authorization. Otherwise serialize write work.

7. Keep project-specific rules, approval boundaries, and source-of-truth documents in force for every delegated task. Delegation does not reduce safety or scope requirements.

8. Require the coordinating agent or human to inspect consequential delegated results before integrating or acting on them.

9. When independent review is delegated, prefer a fresh context that reconstructs the change from repository evidence and apply the project's change-review procedure rather than treating the delegated verdict as automatically authoritative.

Avoid agent fan-out for its own sake. Additional agents increase context, cost, latency, integration work, and the chance of contradictory conclusions.

Report the delegation strategy used, why delegation was or was not beneficial, any isolation mechanism used, evidence returned by delegated work, and unresolved coordination risk.