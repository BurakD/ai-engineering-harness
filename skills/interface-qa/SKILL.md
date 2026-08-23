---
name: interface-qa
description: Validates changed interfaces and user-facing flows across web, mobile, desktop, CLI, or APIs. Use after interface changes to check expected states, interaction behavior, errors, accessibility or usability concerns, and relevant client-side evidence.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Interface QA

1. Identify the affected interface, acceptance criteria, supported clients or platforms, relevant versions, and expected user or consumer behavior from project evidence.

2. Establish the exact build, commit, version, environment, local state, or endpoint being tested when that distinction matters. Do not infer it from stale context.

3. Test the primary successful flow plus relevant loading, empty, invalid-input, error, permission, authentication, unavailable, interrupted, retry, and boundary states.

4. Verify inputs, outputs, state transitions, persistence, navigation, cancellation, recovery, and error feedback that are observable through the interface.

5. Apply interface-specific checks where relevant:
   - **Browser:** inspect responsive layouts, keyboard and focus behavior, semantic labels, browser console errors, failed network requests, navigation, refresh, and back/forward behavior.
   - **Mobile or desktop UI:** check lifecycle transitions, permissions, supported window or viewport changes, interrupted flows, platform interaction conventions, and relevant application logs.
   - **CLI:** check exit status, standard output and error output, help text, invalid arguments, non-interactive behavior, piping or scripting behavior, and interruption handling.
   - **API:** check request and response contracts, status or error semantics, authentication and authorization behavior, validation, idempotency where relevant, and documented compatibility expectations.

6. Check accessibility and usability properties that apply to the interface rather than assuming every surface has the same interaction model.

7. Record defects with the smallest reliable reproduction steps and enough evidence to identify the tested state.

8. After a fix, re-run the affected flow and nearby behavior with meaningful regression risk.

This skill validates each interface against its own expected behavior. Use a cross-surface consistency review separately when equivalent capabilities must remain aligned across multiple interfaces.

Report what was tested, the exact test context when relevant, evidence collected, failures found, and anything intentionally not tested.