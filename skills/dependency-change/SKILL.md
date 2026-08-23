---
name: dependency-change
description: Evaluates dependency additions, removals, and upgrades for necessity, maintenance, security, licensing, compatibility, operational impact, and rollback. Use when changing third-party packages, libraries, modules, plugins, runtimes, or external components.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Dependency change

1. Define the capability or problem that motivates the dependency change and confirm whether existing platform, standard-library, or project capabilities already solve it adequately.

2. Identify the exact dependency, source, maintained version line, intended scope, and any replacement or removal implications.

3. Evaluate maintenance status, release activity, security posture, licensing, ecosystem fit, platform support, runtime or bundle impact, and compatibility with the project's supported environments and consumers.

4. Inspect important transitive dependencies, native or system requirements, generated artifacts, lockfile changes, and operational prerequisites introduced or removed by the change.

5. Prefer the smallest dependency surface and narrowest reasonable integration that solves the problem. Avoid overlapping dependencies for the same concern without explicit justification.

6. For upgrades or replacements, review release notes, migration guidance, breaking changes, deprecations, configuration changes, data-format implications, and minimum supported runtime requirements.

7. Keep the implementation change separate from unrelated dependency cleanup so regressions and rollback remain understandable.

8. Run the affected build, tests, static checks, packaging, startup, or integration validation appropriate to the project.

9. Define a practical rollback or recovery path when the dependency change can affect compatibility, persistent data, deployment, or runtime operation.

10. Document durable architectural, security, licensing, or operational consequences when future maintainers need to know them.

Do not introduce a dependency merely to avoid a small amount of straightforward, maintainable local code.

Report the dependency decision, alternatives considered when relevant, compatibility and security findings, validation evidence, and residual operational risk.