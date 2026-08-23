---
name: compatibility-and-rollout
description: Plans and validates changes where old and new versions, schemas, protocols, data formats, clients, or services may coexist. Use for migrations, staged activation, backward compatibility, mixed-version operation, rollback, or deprecation.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Compatibility and rollout

1. Identify the affected contracts, producers, consumers, persisted formats, supported versions, external dependencies, and compatibility guarantees.

2. Determine which old and new components or data representations may coexist during the transition.

3. Prefer additive evolution, tolerant readers or writers, and reversible changes when they reduce compatibility risk.

4. Separate introducing a capability from activating or depending on it when independent activation, configuration, feature control, or gradual rollout provides a safer transition.

5. For data or schema evolution, use an expand → migrate or backfill → switch → contract sequence when practical. Do not remove the old path before the compatibility requirement has actually ended.

6. Define the rollout order, readiness criteria, observation signals, failure conditions, rollback or recovery path, and point of no return before consequential activation.

7. Validate representative old and new consumers, producers, data, and protocol paths. Include mixed-version behavior when coexistence is possible.

8. Make assumptions about compatibility windows, minimum supported versions, or migration completion explicit rather than inferring them.

9. Remove compatibility scaffolding only after evidence shows that remaining consumers or data no longer require it and the removal is separately reviewed.

Report the compatibility boundaries, coexistence assumptions, rollout sequence, validation evidence, activation criteria, and rollback or recovery path.