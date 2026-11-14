# LunarLander RL Research

A reproducible research workspace for comparing a hand-designed rule-based controller with a Deep Q-Network (DQN) agent on Gymnasium's `LunarLander-v3` environment.

## Research objectives

1. Establish a rule-based control baseline.
2. Train and evaluate a DQN agent using Stable-Baselines3.
3. Compare episode-level performance using matched evaluation seeds.
4. Diagnose failure modes, including episodes that reach the time limit.
5. Record methodology, software setup, metrics, and limitations so results can be reproduced.

## Current experiment snapshot

| Experiment | Evaluation episodes | Mean reward | Median reward | Reward >= 200 |
|---|---:|---:|---:|---:|
| Rule-based controller | 100 | 76.11 +/- 107.81 | 24.42 | 23/100 (23%) |
| DQN | 100 | 171.24 +/- 114.62 | 221.15 | 60/100 (60%) |

Evaluation seeds: 1000-1099.

The DQN run is stronger on these observed metrics, but its mean reward is below the commonly used 200-point solved threshold. This is one training run and does not establish reproducibility across training seeds.

## Repository layout

- `reports/BASELINE_REPORT.md`: rule-based controller and baseline results.
- `reports/DQN_EVALUATION.md`: DQN configuration and evaluation results.
- `reports/TIMEOUT_ANALYSIS.md`: timeout episode summary and diagnostic status.
- `reports/RESEARCH_METHODOLOGY.md`: experimental design and comparison requirements.
- `docs/ENVIRONMENT_SETUP.md`: local Windows/Python environment notes.
- `CHANGELOG.md`: research record updates.
- `requirements.txt`: core Python dependencies (version-pinned where known).

## Important data status

The numerical summaries in this repository reflect the experiment outputs recorded during the research session. The DQN episode CSV was reported as available locally as `dqn_evaluation.csv`, but it has not yet been uploaded here. The rule-based per-episode CSV and timeout diagnostic CSV have not been verified as available. Therefore, this repository currently contains reports, not the raw datasets or plots.

## Reproducibility

See [Research Methodology](reports/RESEARCH_METHODOLOGY.md) and [Environment Setup](docs/ENVIRONMENT_SETUP.md). Before making a final comparative claim, preserve the exact source scripts, raw per-episode outputs, package versions, and run logs.

## Current conclusion

The observed DQN evaluation mean (171.24) exceeds the observed rule-based mean (76.11). However, DQN did not reach a 100-episode mean of 200, and further runs with independent training seeds plus paired episode-level analysis are required.

## License

No license has been selected. All rights reserved by default unless a license is added.
