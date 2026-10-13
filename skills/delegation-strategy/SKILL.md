---
name: delegation-strategy
description: Decides when and how to delegate work to subagents, workers, or isolated reviewer contexts. Use when verified runtime capabilities can improve parallel investigation, specialized analysis, test triage, implementation isolation, or independent review.
metadata:
  ai-engineering-harness: "2.2.0"
---

# Delegation strategy

1. Verify that the active runtime actually supports the proposed agent, subagent, worker, parallel-session, or delegation mechanism. If support cannot be verified, continue without delegation and do not claim that delegation is active.

2. Keep small, coherent, low-risk tasks in one context unless delegation provides a clear benefit.

3. Delegate when isolation or parallelism materially improves the work, such as noisy read-heavy exploration, independent investigation of competing hypotheses, focused research, test-failure triage, specialized analysis, or fresh-context review.

4. Choose the lowest sufficient capability tier for each delegated role according to the project's model-routing and cost policy. Do not hard-code a vendor model or assume additional paid capacity.

5. Give every delegated task a **bounded contract**: the precise outcome and acceptance criteria; files or components it may touch; explicit out-of-scope work; available context; allowed tools, effort/spend and iteration limits when supported; expected verification; and a short evidence-based return format. Delegate one coherent outcome, not a vague mandate to optimize or redesign.

6. Prefer the smallest correct change. Workers must not add speculative features, unnecessary abstraction, dependencies, broad refactors, or extra files merely because they are convenient. A discovered issue outside the contract is reported, not automatically fixed. Material scope growth returns to the coordinator and, when required, the human for authorization.

7. Require meaningful progress checks where the runtime exposes them. A worker that repeats a failed action without new evidence, exhausts its agreed budget, or reaches **two materially distinct unsuccessful approaches** should stop, summarize attempts and observed evidence, and escalate to the coordinator. The coordinator may change strategy or narrow scope; do not blindly retry or spawn more agents. These are procedural stop conditions, **not** a claim of automatic hang detection or guaranteed wall-clock enforcement.

8. If a runtime has verified native step/turn/time/spend limits, use bounds proportional to task size as safeguards. Do not fabricate an unsupported command, hard-code the same small turn limit for all tasks, or terminate legitimate slow work without checking actual progress and risk.

9. Do not allow concurrent writers to modify the same working tree or overlapping files. If parallel implementation is justified, use repository- and runtime-supported isolation only when authorized; otherwise serialize write work.

10. Keep project-specific rules, approval boundaries, and source-of-truth documents in force for every delegated task. Delegation never reduces safety or scope requirements, and does not authorize production, external spend, or destructive actions.

11. Require each worker to return a concise, factual handoff: outcome, changed files or findings, tests/evidence, failed attempts or remaining blocker, and any requested decision. The coordinator inspects consequential changes and validation before integrating them or acting on findings.

12. For independent reviews, prefer fresh context reconstructed from the repository and follow `change-review`. A worker's own confidence is not evidence of correctness or a substitute for deterministic tests.
Avoid agent fan-out for its own sake. Additional agents increase context, cost, latency, integration work, and the chance of contradictory conclusions.

Report the delegation strategy used, why delegation was or was not beneficial, any isolation mechanism used, evidence returned by delegated work, and unresolved coordination risk.