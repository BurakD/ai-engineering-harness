---
name: documentation-sync
description: Keeps durable project documentation aligned with implementation and operating reality. Use when a change affects product behavior, architecture, data, APIs, configuration, environments, release procedures, commands, or other facts future maintainers need.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Documentation sync

1. Determine whether the change alters durable product behavior, architecture, data semantics, interfaces, configuration, operational procedures, release behavior, supported usage, or another fact that future maintainers need.

2. Discover the project's existing canonical documentation, `AGENTS.md`, ADRs, configuration, schemas, runbooks, API specifications, contribution guidance, or other source-of-truth locations. Do not invent a documentation hierarchy that the repository does not define.

3. Update the smallest canonical location that owns the changed fact. Avoid creating a new document when an established source already exists.

4. Record durable facts, decisions, constraints, commands, assumptions, and operational requirements rather than narrating the implementation conversation.

5. Do not duplicate code that is already self-explanatory unless the information is required to operate, integrate with, migrate, or safely modify the system.

6. Keep links, examples, command references, version references, and cross-document terminology consistent with the implementation.

7. Remove or correct stale guidance when the same change makes it demonstrably wrong. If authoritative sources contradict each other and the correct resolution is unclear, report the conflict rather than choosing silently.

8. Include required documentation updates in the same logical change when practical so durable truth does not lag behind implementation.

Report which canonical documentation changed, what durable truth was updated, any contradictions found, or why no documentation update was necessary.