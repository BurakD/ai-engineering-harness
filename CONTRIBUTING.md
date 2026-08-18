# Contributing

Contributions are welcome through normal GitHub pull requests and discussions.

## Before contributing

Please keep the project deliberately small and vendor-neutral. Project-specific product rules, environment details, credentials, and domain knowledge belong in the adopting project, not in this shared repository.

For non-trivial changes, explain the problem the change solves and why the current Markdown-only approach is insufficient before adding new mechanisms, files, adapters, or automation.

Keep stable engineering policy separate from changing vendor/runtime data:

- changes to `AGENTS.md` or `MODEL_ROUTING.md` should represent durable cross-tool behavior;
- changes caused mainly by model launches, retirements, runtime availability, plan changes, or current model recommendations normally belong in `MODEL_CATALOG.md`;
- catalog changes should cite current first-party sources where possible, update its `Last verified` date, distinguish runtime availability from general API availability, and avoid pretending that one tool can invoke another tool's native model/agent mechanics.

Project-local model preferences, cost ceilings, provider restrictions, and sensitive-area overrides should remain project-local rather than being added to the shared catalog.

## Contribution licensing

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in this project is provided under the Apache License 2.0, consistent with Section 5 of `LICENSE`.

You retain copyright in your own contribution. By submitting it for inclusion, you grant the licenses described by Apache License 2.0 to recipients of the project.

If you are contributing work owned by an employer or another organization, you are responsible for ensuring that you have authority to submit it under these terms.

If you do not want a submission treated as a contribution under Apache License 2.0, clearly mark it as **Not a Contribution**.
