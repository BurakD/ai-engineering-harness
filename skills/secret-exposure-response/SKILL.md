---
name: secret-exposure-response
description: Responds to suspected credential or secret exposure by containing access, determining scope, rotating or revoking safely, removing exposed material, validating recovery, and adding preventive controls without reproducing secret values.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Secret exposure response

1. Treat a credible suspected exposure as potentially real until evidence establishes otherwise.

2. Never reproduce, quote, log, paste, summarize, or unnecessarily retrieve the secret value. Refer to it by type, identifier, location, or affected system instead.

3. Determine the exposure scope, including relevant source files, repository history, build or CI artifacts, logs, caches, screenshots, generated output, deployed systems, clients, integrations, and third parties.

4. Identify what the exposed secret can access, its privilege level, expiration behavior, dependencies, and whether evidence suggests unauthorized use.

5. Contain access using the safest available mechanism and rotate, revoke, replace, or invalidate the credential according to project policy and applicable human approval requirements.

6. Remove the source of exposure and move ongoing secret handling to the project's documented secret-management mechanism. Do not invent or migrate secret infrastructure solely because this skill was invoked.

7. Consider repository-history rewriting, artifact deletion, cache invalidation, or other destructive cleanup only when necessary and authorized. Cleanup does not replace credential rotation or revocation.

8. Validate dependent applications and automation after remediation. When safe and practical, confirm that the old credential no longer provides access.

9. Add the smallest useful preventive control, such as secret scanning, least privilege, shorter-lived credentials, safer configuration, a deterministic check, or focused documentation.

10. Preserve incident evidence without preserving the secret itself when audit, investigation, or follow-up requires a record.

Credential rotation, access changes, destructive cleanup, or other high-impact remediation must respect the project's approval boundaries.

Report the exposure type and scope without secret values, containment and remediation status, affected systems, validation performed, and remaining human actions.