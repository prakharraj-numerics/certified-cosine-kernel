# Public Technical Overview

## Purpose

This project evaluates a specialized high-precision cosine kernel for **exact dyadic (binary fixed-point) inputs**.

The objective is repeated high-precision evaluation with rigorous numerical certification and lower warm per-call cost than a general-purpose reference implementation within the validated workload.

## Reference implementation

The primary comparator is FLINT 3.6.0 `arb_cos`.

## Validated workload

The current evidence covers exact inputs represented by a 32-bit numerator over `2^32`, tested at 5,000 and 20,000 decimal digits using two independent random seeds and 100 inputs per seed.

The benchmark is single-threaded and warm/cache-ready, with one-time reusable setup excluded from per-call timing.

## Measured result

Across the reported configurations, the kernel achieved:

- approximately **1.98–1.99× speedup** at 5,000 decimal digits;
- approximately **1.57–1.58× speedup** at 20,000 decimal digits;
- **400 / 400 certified outputs meeting the requested precision target**.

## Certification model

Each reported result is checked against a separately recomputed higher-precision Arb reference interval using full interval containment.

The public claim is limited to machine-checked numerical containment for the reported benchmark cases. It is not a claim of formal verification of the entire implementation.

## Current maturity

The software is an experimental research prototype.

The current evidence does not establish:

- cross-machine portability of the speedup;
- superiority for arbitrary input representations;
- behavior across all precision ranges;
- behavior across all batch sizes;
- production API stability;
- complete adversarial coverage.

## Confidentiality boundary

This public repository intentionally discusses **capability, measured performance, certification methodology, tested scope, environment, and limitations only**.

It does not disclose source code, pseudocode, derivation, proprietary mathematical formulation, implementation architecture, data structures, or optimization strategy.
