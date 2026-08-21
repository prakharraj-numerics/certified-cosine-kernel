# Supported Scope and Limitations

> **DRAFT — FOR REVIEW BEFORE PUBLIC RELEASE**

## Validated input form

The current evidence is for exact dyadic inputs represented as a **32-bit numerator over `2^32`**.

The benchmark sampled uniformly across the tested 32-bit numerator space.

No claim is made here for arbitrary real-number input representations or arbitrary-width rational front ends.

## Validated precision

The current public benchmark evidence covers:

- **5,000 decimal digits**;
- **20,000 decimal digits**.

Performance at lower, intermediate, or substantially higher precision should be measured separately before being represented as established behavior.

## Execution model

The validated workload is:

- single-threaded;
- warm/cache-ready;
- repeated evaluation at a fixed working precision;
- batch size of 100 inputs in the reported benchmark.

Behavior at very different batch sizes was not systematically swept in the reported final results.

## Hardware scope

The published result comes from one x86_64 environment with one logical CPU available to the benchmark process.

Cross-machine and cross-microarchitecture portability of the speedup has not yet been established.

## Current non-goals

This public prototype should not be represented as:

- a universal replacement for `arb_cos`;
- universally faster for every input representation;
- validated across all precision ranges;
- validated across all batch sizes;
- validated on all processor architectures;
- production-hardened software.
