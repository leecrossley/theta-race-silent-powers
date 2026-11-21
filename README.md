# Exceptional powers of two in the 547/727 prime race

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24412102.svg)](https://doi.org/10.5281/zenodo.24412102)

This result is now maintained in [theta-host-split-inert-race](https://github.com/leecrossley/theta-host-split-inert-race/tree/main/results/theta-race-silent-powers). This repository is archived and keeps its releases and DOI.

**Every one of the first billion exponents gives both large gains and large losses. Yet some larger powers of two suppress both moves at every sufficiently high start.** For the weighted 547/727 split–inert prime race let $`D_n(y)=S(2^n y)-S(y)`$ and $`\tau=1.9735\log2`$. The width of the score is fixed at $`b=2`$. [Full theorem](PROOF.md)

| Exponents | What is proved |
|---|---|
| Every integer $`1\le n\le10^9`$ | Gains above $`14/5`$ and losses below $`-14/5`$ occur at arbitrarily high starts. |
| Every block of 1,000,000,001 consecutive positive exponents | At most one can fail to give gains and losses of magnitude greater than $`\tau`$ arbitrarily far out. |
| A set of exponents of lower uniform density at least $`2^{-90000}`$ | Every start $`y\ge e^{1000}/(2\sqrt2)`$ satisfies $`\lvert D_n(y)\rvert \lt4/3\lt\tau`$. |

For every positive integer $`m`$, some multiple $`mj`$, with $`1\le j\le2^{90000}`$, has the last property. The same lower density applies to the multipliers of each $`m`$. The proof gives existence and bounds for the first such exponent. Its value is open. [Prior work](PRIOR-WORK.md)

Two independent integer scans find two distinct Fourier modes for every exponent through one billion. An even spectral moment bounds the total mass of all omitted zeros, and the prime-only error bound makes the conclusion uniform over the height of the prime sum. [Binary scan](scan_powers.c) · [Decimal sieve](decimal_check.c) · [Full verification output](evidence/check.txt)

## Replay

Use Python 3.10+, a C compiler supporting unsigned 128-bit integers such as GCC or Clang, and the pinned Python package.

```sh
python -m pip install -r requirements.txt
python power_phases.py
cc -std=c11 -O3 scan_powers.c -o /tmp/theta-scan-powers
/tmp/theta-scan-powers evidence/low-phases.tsv
python independent.py
python check_source.py
```

On x86-64 Linux with Git, curl, tar and zstd, `bash verify-release.sh` runs the two billion-exponent scans, upstream source checks and seven local Lean deductions. With Lean 4.33.1 on PATH and a built Git checkout of Mathlib at commit `0df444a360eaa60ab8c11dca51a86af692955474` with no local changes, run `bash verify-release.sh /path/to/mathlib4`. The optional second argument gives the directory of the five upstream records. The compact explicit formula, Fourier and counting arguments are written proofs. [Lean deductions](DyadicPowers.lean) · [Hashes](SHA256SUMS) · [Original zero brackets and Hardy-sign replay](https://github.com/leecrossley/theta-race-factor-400/releases/tag/v1.0.0)
