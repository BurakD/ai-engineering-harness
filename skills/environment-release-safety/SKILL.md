---
name: environment-release-safety
description: Validates release and deployment actions against the project's actual environment topology, triggers, versions, configuration, compatibility, recovery path, and approval boundaries. Use before or after actions that may change a deployed or customer-facing system.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Environment and release safety

1. Discover the project's actual release, deployment, publication, and environment topology from repository rules, `AGENTS.md`, canonical documentation, automation, configuration, infrastructure definitions, and other authoritative project evidence.

2. Do not assume that deployment environments exist, that there are a particular number of them, that they have conventional names, or that changes move through a fixed promotion sequence. Mark deployment-specific checks not applicable when the project has no such workflow.

3. Before a consequential action, identify the exact action, target, source branch or revision, artifact or version, configuration context, automation trigger, and expected externally visible effect when those concepts apply.

4. Determine whether the action affects a customer-facing, live, externally published, shared operational, or otherwise high-impact system from its actual effect and project policy. Do not infer this solely from a hostname, label, branch name, local configuration file, or remembered convention.

5. Identify relevant migrations, compatibility constraints, feature controls, configuration or secret prerequisites, dependency ordering, health checks, observation signals, and rollback or recovery requirements.

6. Prefer validation against a lower-impact or non-customer-facing target first when such a target actually exists, project policy permits it, and doing so provides meaningful evidence. Do not invent a validation environment merely because one would be convenient.

7. Respect the project's approval policy and the shared Harness approval boundaries. Customer-facing or live publication, destructive or irreversible actions, credential changes, risky data operations, and other explicitly gated actions require the applicable human approval before execution.

8. After any authorized release or deployment, verify the actual resulting revision, artifact, version, configuration, target, and externally observable behavior instead of assuming the command or automation succeeded.

9. Run the project's documented smoke checks or equivalent post-change validation when applicable and report anything that could not be verified.

Report the discovered topology, exact target and revision when applicable, validation performed, observed result, rollback or recovery readiness, and any action still requiring human approval.