# Anonymous distribution: verification and scope

The CPU checks below were run on an isolated copy of this distribution using
Python 3.12.14 on macOS ARM64. Package versions are recorded in
`requirements-verify.txt`. The original numerical artifacts and tolerances were
retained.

## Passed checks

| Check | Result |
|---|---|
| Full test suite, including released-data integrity | 76 passed; no skipped tests |
| `scripts/check_paper_numbers.py --strict --only-mismatches` | 413 of 413 saved-result comparisons agree with the reference values embedded in the checker at printed precision |
| `examples/minimal_example.py` | Output matches the README |
| Exact attribution comparison with `shapiq` 1.3.1 | Maximum absolute discrepancy 1.78e-15 |
| Analytic kernel equivalence | Maximum absolute discrepancy 4.58e-10 |
| 8-group cube self-check | Passed |
| Attribution smoke test | Passed; 3,600 synthetic result rows produced |
| Python source parsing | 109 files passed |
| Shell syntax | 15 scripts/templates passed |
| Relative Markdown links | All resolved |
| AG News command-line parsing and run metadata | Passed |
| Atomic claim-once output handling | Passed |

The attribution smoke test was run with one linear-algebra and PyTorch thread.

## Integrity and packaging

All 371 shipped NumPy, CSV, JSON, YAML, and frozen-mask text artifacts are
byte-identical to the source release. The 27 coalition cubes retain their
recorded checksums. Executable core-package code matches the original package;
core edits are confined to documentation.

The distribution excludes repository history, local environments, editor and
operating-system artifacts, scheduler logs, and model checkpoints. Inspection
covers shipped text, known source-history identities, string arrays in all 77
NumPy archives, text and metadata in all six PDFs, and metadata in all four PNGs.
No personal identifier, author-owned repository link, personal absolute path,
or institution identifier was found in those checks. Third-party source credit
and model/dataset identifiers are retained. Slurm templates leave the partition
to the submitting system. `SHA256SUMS` lists every shipped file except itself.

## Probe regeneration limitation

The full seed-31 representation-probe regeneration completed, but its original
`--check` returned a nonzero status on this platform. With NumPy 1.26.4,
131 of 1,024 utilities differed from the saved outcomes by more than 1e-6.
Maximum absolute gaps were:

| Quantity | Maximum gap |
|---|---:|
| Utility | 0.0202 |
| Pair interactions | 0.00286 |
| Shapley | 0.000644 |
| Banzhaf | 0.0000981 |
| Leave-one-out | 0.00519 |

The leave-one-out gap exceeds the original 0.005 threshold. A second check with
NumPy 2.2.6 also exceeded that threshold (leave-one-out gap 0.00519; maximum
utility gap 0.0236). This is consistent with the documented sensitivity of the
randomized projection and the loosely converged probe solver to platform and
linear-algebra rounding. Neither saved outcomes nor solver/check tolerances
were changed. Tests recomputing exact attributions from the saved probe games
pass, as do the saved-result comparisons for Tables 17 and 19. Fresh probe
regeneration on other platforms should be assessed independently.

## Reproduction boundaries

GPU retraining and full datamodel refits were not repeated for this packaging
check. The numerical checker validates saved artifacts against embedded
reference values; it is not an independent comparison with a separate paper
manuscript. The original verification record remains in `REPRODUCIBILITY.md`.

The Sport–Music fine-tuning pipeline needs source inputs and a tokenisation
stage that are absent from this distribution. Its saved utilities and CPU
datamodel fits are included. The 12- and 24-group reasoning refitters need
regenerated per-coalition records; their frozen predictions and CPU analyses
are included. See each experiment README for the applicable entry points.
