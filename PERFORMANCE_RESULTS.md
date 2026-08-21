# Performance Results

> **DRAFT — FOR REVIEW BEFORE PUBLIC RELEASE**

The benchmark compares the current high-precision cosine kernel directly against FLINT 3.6.0 `arb_cos`.

## Final benchmark table

| Decimal digits | Seed | Kernel ms/call | FLINT `arb_cos` ms/call | Speedup | Correctness |
|---:|---:|---:|---:|---:|---:|
| 5,000 | 90210 | 0.2599 | 0.5173 | 1.99× | 100/100 |
| 5,000 | 762391 | 0.2513 | 0.4988 | 1.98× | 100/100 |
| 20,000 | 90210 | 2.3457 | 3.6750 | 1.57× | 100/100 |
| 20,000 | 762391 | 2.3623 | 3.7414 | 1.58× | 100/100 |

The kernel outperformed FLINT in every reported configuration.

## Certified accuracy

| Decimal digits | Target bits | Minimum certified bits | Minimum certified margin |
|---:|---:|---:|---:|
| 5,000 | 16,610 | 16,874 | +264 bits |
| 20,000 | 66,439 | 66,730 | +291 bits |

All **400 reported outputs** met or exceeded the requested precision target under machine-checked interval containment.

## What these results establish

The measurements establish a reproducible advantage for the tested workload:

- exact dyadic inputs;
- 32-bit numerator over `2^32`;
- 100 inputs per seed;
- two independent random seeds;
- 5,000 and 20,000 decimal digits;
- single-threaded execution;
- warm/cache-ready evaluation.

They do not establish universal superiority outside that workload.

## Timing interpretation

The reported values are warm per-call timings after an explicit warm-up pass. One-time reusable setup is excluded from the timed region.

The benchmark used a rotating/interleaved schedule and the median of 15 timing cycles per configuration to reduce systematic timing bias.

All values in a given benchmark row were measured in the same process against the same input set.
