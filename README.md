# Certified High-Precision Cosine Kernel

Experimental high-precision software for repeated cosine evaluation on **exact dyadic (binary fixed-point) inputs**.

The project evaluates a specialized cosine fast path against FLINT 3.6.0 `arb_cos`. In the currently validated workload, the kernel is approximately **1.98–1.99× faster at 5,000 decimal digits** and **1.57–1.58× faster at 20,000 decimal digits**, while every reported output meets a machine-checked interval-containment certificate.

## Current validated scope

The present benchmark evidence covers:

- exact dyadic inputs represented as a 32-bit numerator over `2^32`;
- inputs uniformly sampled across the tested numerator space;
- 5,000 and 20,000 decimal digits;
- 100 random inputs per seed;
- two independent random seeds;
- single-threaded execution;
- warm/cache-ready repeated evaluation;
- FLINT 3.6.0 `arb_cos` as the reference comparator.

The kernel is **not** presented as a universal replacement for a general-purpose cosine implementation.

## Performance summary

| Decimal digits | Seed | Kernel ms/call | FLINT 3.6.0 ms/call | Speedup | Correctness |
|---:|---:|---:|---:|---:|---:|
| 5,000 | 90210 | 0.2599 | 0.5173 | 1.99× | 100/100 |
| 5,000 | 762391 | 0.2513 | 0.4988 | 1.98× | 100/100 |
| 20,000 | 90210 | 2.3457 | 3.6750 | 1.57× | 100/100 |
| 20,000 | 762391 | 2.3623 | 3.7414 | 1.58× | 100/100 |

Across all four reported configurations, the kernel outperformed FLINT 3.6.0.

## Certification

Every one of the **400 reported outputs** was checked using an independently recomputed higher-precision Arb reference interval and a full interval-containment test.

Minimum certified margins for the current kernel were:

- 5,000 digits: **+264 bits** beyond the requested target;
- 20,000 digits: **+291 bits** beyond the requested target.

This establishes rigorous numerical containment for the reported outputs. It is not a claim of formal verification of the complete implementation or execution stack.

## Benchmark methodology

- same machine and same process for kernel and FLINT;
- rotating/interleaved execution order;
- explicit warm-up before measurement;
- median of 15 timing cycles per configuration;
- identical 100-input set for both methods within each seed;
- one thread for both implementations;
- one-time reusable setup excluded from warm per-call timing.

## Proprietary details

This public repository describes **capability, benchmark results, validation methodology, tested scope, environment, and limitations only**.

It intentionally does **not** disclose source code, pseudocode, mathematical derivation, proprietary mathematical formulation, implementation architecture, data structures, or optimization strategy.

## Documentation

- [`Public technical overview`](PUBLIC_TECHNICAL_OVERVIEW.md)
- [`Performance results`](PERFORMANCE_RESULTS.md)
- [`Validation summary`](VALIDATION_SUMMARY.md)
- [`Supported scope and limitations`](SUPPORTED_SCOPE.md)
- [`Benchmark environment and fairness`](ENVIRONMENT_AND_FAIRNESS.md)

## Status

**Experimental prototype.** The current evidence establishes a reproducible performance advantage only within the tested high-precision exact-dyadic workload. Broader input forms, additional precision ranges, other hardware, other batch sizes, and other execution regimes require separate qualification.

## Version

Public package: **0.1.0**
