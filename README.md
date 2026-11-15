# pypi-behaviour-audit

Leakage-aware evaluation of runtime-behaviour detectors for malicious PyPI packages, using QUT-DV25.

## Why

Machine-learning detectors for malicious Python packages often report accuracy above 95% on laboratory datasets, yet PyPI administrators have said that even a 0.01% false positive rate is too high for the volume of new releases (Vu, Newman and Meyers, 2023). This project asks how much of that gap comes from how detectors are evaluated, using [QUT-DV25](https://arxiv.org/abs/2505.13804), a public dataset of install-time and post-install runtime traces for 14,271 PyPI packages.

## Research questions

1. **Leakage.** How much do accuracy and false positive rate change when near-duplicate packages (same family, different version) are kept on one side of the train/test split, and when name-derived signals are removed?
2. **Feature value.** Which of the six trace tables (Filetop, Install, Opensnoop, Pattern, SysCall, TCP) carry signal under the stricter split, alone and when left out?
3. **Base rates.** What precision does a detector deliver when malicious packages are 1%, 0.1% or 0.01% of releases rather than 50%?
4. **Evasion sensitivity (simulated).** How quickly does detection degrade if an attacker suppresses the behaviours that are cheapest to hide?

## Data

The dataset is not included in this repository. Download QUT-DV25 from [doi.org/10.7910/DVN/LBMXJY](https://doi.org/10.7910/DVN/LBMXJY) and check its licence terms before redistributing anything.

Only the six processed tables (about 28 MB) are needed, not the raw traces. Place them here:

```
data/processed/
    QUT-DV25_Filetop_Traces.csv
    QUT-DV25_Install_Traces.csv
    QUT-DV25_Opensnoop_Traces.csv
    QUT-DV25_Pattern_Traces.csv
    QUT-DV25_SysCall_Traces.csv
    QUT-DV25_TCP_Traces.csv
```

The `data/` folder is git-ignored. In the tables, `Package_Name` identifies a package and `Level` is the label (1 = malicious, 0 = benign).

## Status

Early stage. Study design is in progress and no results are published here yet. Planned deliverables:

- A small Python package for loading the tables, building leakage-safe splits and reporting base-rate-aware metrics
- Reproducible experiments with fixed seeds, a pinned environment and one command per results table
- A paper draft written from the results

## Scope

In scope: evaluation of runtime-trace detectors on QUT-DV25. Out of scope for now: static or hybrid detection (needs a second dataset with static features for malicious packages), time-based evaluation (the tables carry no upload dates) and re-running packages in a sandbox.

## Safety

This repository contains analysis code only. It does not include or distribute malicious packages.

## Citation

Mehedi, S.T., Jurdak, R., Islam, C. and Ramachandran, G.S. (2025) 'QUT-DV25: A dataset for dynamic analysis of next-gen software supply chain attacks', *Advances in Neural Information Processing Systems 38 (NeurIPS 2025), Datasets and Benchmarks Track*.

Vu, D.-L., Newman, Z. and Meyers, J.S. (2023) 'Bad snakes: Understanding and improving Python Package Index malware scanning', *Proceedings of the 45th International Conference on Software Engineering (ICSE 2023)*.

## Licence

Not yet chosen.
