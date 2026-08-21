# Validation Summary

## Per-output certification

Every reported output is independently checked rather than accepted from timing measurements alone.

For each computed kernel result:

1. the result is treated as the center of a candidate numerical interval;
2. a separate higher-precision reference interval is recomputed using FLINT `arb_cos`;
3. the candidate interval must fully contain the independent reference interval;
4. the containment radius is tightened to determine the certified error bound.

The containment test is stronger than a simple overlap check: the full independently computed reference interval must be contained inside the candidate interval.

## Reported outcome

Across 2 precisions × 2 seeds × 100 inputs:

- **400 / 400 outputs met the required precision target**;
- minimum certified margin at 5,000 digits: **+264 bits**;
- minimum certified margin at 20,000 digits: **+291 bits**.

The independent reference calculation was performed at substantially higher precision than the target, so the reference interval itself did not limit the reported certification.

## Claim boundary

This validation establishes rigorous numerical interval containment for the reported benchmark outputs.

It is **not** a claim of formal verification of the complete source program, compiler, operating system, hardware, or full software stack.
