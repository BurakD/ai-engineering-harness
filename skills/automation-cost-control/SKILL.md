---
name: automation-cost-control
description: Controls metered compute cost in automated pipelines by attributing real spend, moving work to the cheapest capable executor, bounding job runtime, and verifying that cost-motivated conditions did not silently disable required work. Use when changing build, test, or release automation.
metadata:
  ai-engineering-harness: "2.2.0"
---

# Automation cost control

Use this procedure when automated build, test, validation, packaging, or release work consumes metered compute whose cost can vary materially with executor choice, runtime, repetition, storage, or triggering behavior.

1. Attribute actual consumption and spend from the provider's own usage data before optimizing, grouped by pipeline, job, and executor class when that breakdown is available. Do not optimize from intuition, wall-clock duration alone, or the component that merely feels expensive.

2. Establish the relative cost of the executor classes the project can actually use. When classes differ by an order of magnitude, placement can matter more than small runtime reductions.

3. Run portable work once on the cheapest capable executor. Keep specialized or materially costlier executors for work that genuinely requires them, and remove duplicated validation rather than leaving equivalent work on multiple executor classes.

4. Determine why a costly job takes the time it does before shortening it. Repeated dependency resolution, ineffective caching, duplicated validation, unnecessary setup, and idle waiting can dominate the work the job exists to perform.

5. Build caches from version-controlled dependency or build metadata that actually exists and changes with the inputs being cached. Verify cache-key inputs resolve as intended; missing inputs must not silently collapse into a constant or stale key.

6. Give metered automated jobs explicit runtime bounds derived from observed legitimate duration plus reasonable variance. Treat the bound as a failure limit for hung or runaway work, not as a substitute for diagnosing slow jobs.

7. Trigger materially costly work only on events that genuinely require it. If an explicit opt-in or non-consuming mode is safe for the workflow, prefer the non-consuming path by default. Never weaken required validation, release safety, or approval boundaries merely to reduce cost.

8. Cancel superseded runs when they are validation-only and no longer useful. Do not automatically cancel work that publishes artifacts, mutates external systems, records durable state, or otherwise has consequences that must complete or be reviewed.

9. When conditional execution is introduced for cost reasons, verify the automation system's dependency and skip-propagation semantics. Confirm required downstream paths still run in every intended mode; a skipped prerequisite must not silently remove required work.

10. Bound retention of generated artifacts and logs to what is actually needed for diagnosis, audit, handoff, or recovery, consistent with project policy.

11. Expose cost-relevant pipeline health in normal automation output where practical, such as cache effectiveness and duration against an expected range. Prefer durable signals over recurring human reminders to inspect usage manually.

12. Use provider-account spend ceilings, budgets, or alerts when available and authorized. Repository configuration alone cannot guarantee a hard spending boundary; report account-level controls that remain outside repository scope.

Report the attributed cost drivers, executor-placement and duplication decisions, cache changes, runtime bounds and how they were derived, conditional paths whose semantics were verified, retention changes, and the status of any account-level spend boundary that remains outside repository scope.
