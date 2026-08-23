---
name: calculation-model-validation
description: Validates calculation and decision models such as pricing, scoring, ranking, allocation, quotas, credits, optimization, and aggregation. Use when changing formulas or investigating results where boundaries, precision, invariants, or ordering matter.
metadata:
  ai-engineering-harness: "2.0.0"
---

# Calculation model validation

1. Define the intended model and its invariants before changing formulas, transformations, aggregation, ordering, or allocation logic.

2. Identify relevant properties such as valid ranges, boundary behavior, null or unknown handling, rounding and precision, monotonicity, conservation or balance rules, ordering, uniqueness, idempotence, and impossible states.

3. Distinguish a deliberate business or policy change from an implementation defect. Do not silently convert one into the other.

4. Test boundary values and representative normal values, including values immediately on both sides of important thresholds.

5. Prefer property-based or invariant tests when they can validate a class of inputs more reliably than a collection of examples. Keep representative examples where they improve readability or protect important known cases.

6. When changing an existing model, compare previous and proposed behavior across meaningful fixtures or historical scenarios and investigate unexpected differences.

7. Treat unexplained invariant violations, precision drift, inconsistent ordering, impossible outputs, or unexplained balance differences as unresolved defects rather than weakening assertions to make tests pass.

8. Document intentional changes to model semantics when they affect stored data, consumers, compatibility, reporting, interpretation, or migration behavior.

Report the model properties and invariants checked, meaningful old-versus-new differences, validation evidence, and unresolved calculation or interpretation risks.