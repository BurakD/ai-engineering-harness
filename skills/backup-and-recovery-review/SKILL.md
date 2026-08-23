---
name: backup-and-recovery-review
description: Reviews backup, restore, and recovery readiness for persistent data, configuration, and critical assets. Use when changing stateful systems or assessing whether important data and services can be recovered after loss, corruption, or outage.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Backup and recovery review

1. Identify persistent data, files, configuration, metadata, and other assets that would be costly, risky, or impossible to recreate.

2. For each asset, determine the backup mechanism, location, frequency, retention, integrity protection, access controls, and independence from the primary failure domain.

3. Identify credentials, encryption keys, configuration, infrastructure definitions, external dependencies, and other prerequisites required for recovery. Never copy or expose secret values while documenting recovery requirements.

4. Define or verify the restore procedure, dependency order, required tools, expected recovery destination, and any manual steps.

5. Prefer evidence from a recent restore test, recovery exercise, integrity check, or equivalent validation. A successful backup job alone is not proof that recovery works.

6. Evaluate recovery point and recovery time expectations when the project defines them or when the impact of data loss makes them relevant. Report any gap between expected and demonstrated recovery capability.

7. Check whether backup failures, capacity problems, retention failures, and unsuccessful recovery tests can be detected and acted on.

8. When a change introduces or materially alters persistent assets, verify that backup and recovery coverage changes with it.

Report the assets reviewed, demonstrated recovery evidence, uncovered or unverified recovery paths, material recovery risks, and the next safe corrective action.