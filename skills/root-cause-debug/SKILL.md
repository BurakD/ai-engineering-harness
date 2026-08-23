---
name: root-cause-debug
description: Investigates defects by reproducing or observing the failure, testing hypotheses, identifying the underlying cause, fixing the cause rather than the symptom, and proving the fix with targeted regression evidence.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Root-cause debug

1. Capture expected behavior, observed behavior, impact, and the smallest reliable reproduction or evidence available.

2. Confirm that the observed failure is real and identify the conditions under which it appears or disappears.

3. Inspect relevant recent changes, logs, state transitions, dependencies, configuration, and the actual control or data path before editing.

4. Form explicit hypotheses about possible causes and gather evidence that can distinguish or falsify them.

5. Identify the underlying cause, contributing conditions, affected components, and likely blast radius before choosing a fix.

6. Prefer the smallest coherent change that removes the cause rather than masking an error, suppressing a signal, weakening validation, or special-casing only the observed example.

7. Add or strengthen a regression test, invariant, diagnostic check, or reproducible verification when practical.

8. Run targeted validation first, followed by broader checks proportional to the potential blast radius and regression risk.

9. If repeated high-confidence fixes fail, stop blind iteration. Re-check assumptions, gather new evidence, reconsider the system model, or escalate reasoning rather than repeating the same strategy with more effort.

Avoid unrelated cleanup while diagnosing the defect unless it is necessary to isolate or safely correct the root cause.

Report the root cause, contributing conditions, implemented or proposed fix, regression evidence, affected scope, and remaining uncertainty.