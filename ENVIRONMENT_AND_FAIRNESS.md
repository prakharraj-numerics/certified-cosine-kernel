# Benchmark Environment and Fairness

> **DRAFT — FOR REVIEW BEFORE PUBLIC RELEASE**

## Documented environment

- CPU: Intel(R) Xeon(R) Processor @ 2.10 GHz
- architecture: x86_64
- logical CPUs available: 1
- operating system: Ubuntu 24.04.4 LTS
- kernel: Linux 6.18.44, x86_64
- RAM: 3.9 GiB total
- compiler: GCC 13.3.0
- compile flags: `-O3 -march=native -DNDEBUG`
- `-march=native` resolved to `sapphirerapids`
- GMP: 6.3.0
- MPFR: 4.2.1
- reference library: FLINT 3.6.0
- threads used: 1 for both kernel and FLINT

The FLINT 3.6.0 shared library used by the benchmark was the build distributed with the `python-flint 0.9.0` PyPI wheel and was linked through an explicit library path and runtime search path.

The benchmark program checked the linked FLINT version at runtime, and `ldd` was also used to confirm the library actually loaded by the executable.

## Timing protocol

The reported methodology used:

- kernel and FLINT in the same compiled benchmark process;
- the same input set at the same requested precision;
- rotating/interleaved timing order;
- an explicit warm-up pass;
- median of 15 timing cycles per configuration;
- 100 random inputs per seed;
- two independent seeds;
- single-threaded execution for both methods.

## Setup treatment

One-time reusable setup is excluded from the reported warm per-call timing.

The public benchmark claims therefore concern the repeated-evaluation operating regime after precision-specific setup has been completed.

## Evidence limits

The benchmark was performed on one machine and one execution model. No claim is made that the same speedup necessarily transfers unchanged to other CPUs, compilers, batch sizes, precision ranges, or input representations.
