# Research Methodology

## Research question

How does a hand-designed rule-based controller compare with a DQN policy on Gymnasium `LunarLander-v3` under a fixed evaluation seed set?

## Environment and task

- Environment ID: `LunarLander-v3`
- Action space: discrete actions (confirm exact environment version and action mapping in the committed code).
- Observation: eight-dimensional state vector used by the controller.
- Evaluation seeds: 1000-1099.

## Methods

### Rule-based baseline

A deterministic hand-designed controller maps the observation vector to discrete actions using target angle and hover heuristics. Its exact source file should be committed to make the baseline independently reproducible.

### DQN

Stable-Baselines3 DQN trained for 500,000 timesteps with training seed 2026 and the hyperparameters listed in [DQN Evaluation](DQN_EVALUATION.md). The saved model should be preserved alongside a checksum or release artifact.

## Evaluation measures

Primary measures:
- Mean episode return
- Median episode return
- Fraction of episodes with return >= 200

Additional measures:
- Standard deviation, minimum and maximum return
- Episode length
- Termination and truncation counts
- Explicitly defined crash/landing outcomes
- Stability of final lander position and attitude

## Current results

The recorded summaries are:

| Metric | Rule-based | DQN |
|---|---:|---:|
| Mean reward | 76.11 | 171.24 |
| Median reward | 24.42 | 221.15 |
| Reward standard deviation | 107.81 | 114.62 |
| Reward >= 200 | 23% | 60% |
| Mean steps | 146 | 406 |

Both evaluations used seeds 1000-1099 according to the run notes. The raw rule-based episode data is not presently available, so the per-seed pairing cannot yet be independently checked.

## Statistical analysis plan

Once both episode CSV files are committed and aligned by seed:

1. Validate that there is exactly one row per seed and no missing or duplicate seeds.
2. Compute per-seed reward differences (DQN minus rule-based).
3. Report the mean and median paired difference and a bootstrap confidence interval.
4. Use a paired permutation test or Wilcoxon signed-rank test as a sensitivity analysis; state assumptions and handle ties/zero differences transparently.
5. Compare success/failure classifications with a paired binary method only after applying the same predeclared outcome definition to both controllers.
6. Avoid treating the 100 evaluation episodes from one trained DQN model as 100 independent training replications.

## Reproducibility requirements

Commit the following before claiming a final result:
- controller source code
- DQN training and evaluation scripts
- exact environment and dependency versions
- training seed and evaluation seed list
- raw per-episode CSVs
- model checkpoint and training logs (or stable artifact links)
- timeout diagnostic data
- plotting/analysis scripts

## Limitations

- Only one DQN training seed is currently documented.
- The baseline per-episode CSV is not verified.
- The DQN CSV and model are not yet in this repository.
- Timeout trajectories have not been analyzed.
- Performance summaries alone cannot establish statistical significance or robust generalization.
