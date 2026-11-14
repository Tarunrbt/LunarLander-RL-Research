# DQN Timeout Analysis

## Purpose

Investigate DQN evaluation episodes that reached the environment time limit (1000 steps) without ending earlier.

## Recorded timeout episodes

The DQN evaluation identified 13 truncated episodes:

| Seed | Reward |
|---:|---:|
| 1012 | -14.35 |
| 1016 | -7.80 |
| 1019 | 8.36 |
| 1027 | 1.82 |
| 1043 | -19.52 |
| 1059 | 18.04 |
| 1060 | -9.09 |
| 1063 | -1.94 |
| 1075 | -10.19 |
| 1088 | -24.59 |
| 1091 | -22.82 |
| 1093 | -28.71 |
| 1097 | -9.01 |

Mean reward across these listed timeout episodes is approximately -10.71.

## What the current evidence shows

The episodes reached the 1000-step time limit and were truncated. Their rewards are generally near zero or negative. The aggregate CSV summary does not reveal whether the agent was hovering, oscillating, drifting, or following another trajectory.

Do not label all timeouts as hovering without trajectory evidence.

## Diagnostic data required

For each timeout episode, record:

- seed and total reward
- final observation vector
- final position and velocity
- final angle and angular velocity
- left/right leg contact flags
- action counts and action sequence
- trajectory samples across the episode
- distance from landing pad over time
- environment terminated/truncated flags

A diagnostic script was prepared locally as `timeout_diagnostics.py`, but its execution and output CSV `timeout_diagnostics.csv` have not yet been verified. No diagnostic conclusions should be claimed until this file is generated and inspected.

## Next action

Run diagnostics first on one timeout seed (for example 1012) with progress output before and after model loading. Confirm that a row and trajectory are produced. Then expand to all 13 timeout seeds and commit the resulting CSV and plots.
