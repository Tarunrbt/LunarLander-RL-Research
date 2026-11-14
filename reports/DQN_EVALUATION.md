# DQN Training and Evaluation Report

## Objective

Train a Deep Q-Network agent on Gymnasium `LunarLander-v3` using Stable-Baselines3, then evaluate deterministically on 100 fixed seeds.

## Training configuration

| Parameter | Value |
|---|---:|
| Algorithm | DQN |
| Environment | `LunarLander-v3` |
| Learning rate | 0.0005 |
| Replay buffer size | 100,000 |
| Learning starts | 10,000 |
| Batch size | 64 |
| Discount factor (gamma) | 0.99 |
| Train frequency | 4 |
| Gradient steps | 1 |
| Target update interval | 1,000 |
| Exploration fraction | 0.20 |
| Initial epsilon | 1.00 |
| Final epsilon | 0.05 |
| Network architecture | [128, 128] |
| Training seed | 2026 |
| Training timesteps | 500,000 |
| Saved model | `dqn_lunar_lander.zip` |

## Evaluation protocol

- Deterministic policy evaluation.
- 100 episodes.
- Seeds 1000-1099.
- Episode-level results reportedly saved locally as `dqn_evaluation.csv`; this file is not yet committed to this repository.

## Results

| Metric | Result |
|---|---:|
| Episodes | 100 |
| Mean reward | 171.24 |
| Reward standard deviation | 114.62 |
| Median reward | 221.15 |
| Minimum reward | -41.62 |
| Maximum reward | 306.10 |
| Episodes with reward >= 200 | 60 (60%) |
| Mean episode length | 406 steps |
| Crashes (as defined by evaluation script) | 15 |
| Timeouts / truncations | 13 |

The “crash” count above is the count produced by the recorded evaluation script, described as terminal episodes with final reward <= -100. Preserve that operational definition when interpreting it; it is not necessarily identical to every possible physical crash classification.

## Interpretation

The DQN agent outperformed the observed rule-based baseline on mean reward (171.24 versus 76.11), median reward (221.15 versus 24.42), and fraction of episodes with reward >= 200 (60% versus 23%).

However, the DQN mean reward remains below 200. It should therefore not be reported as solved under the commonly used criterion of a mean reward of at least 200 over 100 consecutive evaluation episodes.

This result comes from one training seed (2026). It does not establish training-run reproducibility or robust generalization.

## Recommended next experiments

1. Repeat training with multiple independent training seeds.
2. Preserve the training reward curve and exact software versions.
3. Re-run the baseline with a per-episode CSV on the identical evaluation seed set.
4. Perform paired analysis on per-seed reward differences once both CSV files are available.
5. Investigate the 13 truncated episodes using full trajectories and final observations.
6. Report uncertainty across training runs, not only across evaluation episodes from one trained policy.

## Artifacts status

- Model file: reported as saved locally; not uploaded here.
- DQN evaluation CSV: reported as saved locally; not uploaded here.
- Training logs/curves: not verified in repository.
- Evaluation script: not yet committed.
