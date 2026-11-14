# Rule-Based Controller Baseline Report

## Purpose

This report records the hand-designed controller benchmark on Gymnasium `LunarLander-v3`.

## Controller

The controller uses the eight-element LunarLander observation to derive target angle and hover behaviour, then selects one of the discrete actions. The logic recorded for the experiment was:

```python
def rule_based_controller(s):
    angle_target = np.clip(s[0] * 0.5 + s[2] * 1.0, -0.4, 0.4)
    hover_target = 0.55 * abs(s[0])
    angle_todo = (angle_target - s[4]) * 0.5 - s[5] * 1.0
    hover_todo = (hover_target - s[1]) * 0.5 - s[3] * 0.5

    if s[6] or s[7]:
        angle_todo = 0
        hover_todo = -s[3] * 0.5

    if hover_todo > abs(angle_todo) and hover_todo > 0.05:
        return 2 if hover_todo > 0.12 else 0
    elif angle_todo < -0.05:
        return 3
    elif angle_todo > 0.05:
        return 1
    return 0
```

The snippet assumes NumPy is imported as `np`. The action mapping should be checked against the exact Gymnasium environment version used for the run.

## Evaluation protocol

- Environment: `LunarLander-v3`
- Episodes: 100
- Seeds: 1000 through 1099
- Recorded summary: one benchmark run

## Results

| Metric | Result |
|---|---:|
| Episodes | 100 |
| Mean reward | 76.11 |
| Reward standard deviation | 107.81 |
| Median reward | 24.42 |
| Minimum reward | -59.05 |
| Maximum reward | 314.43 |
| Episodes with reward >= 200 | 23 (23%) |
| Mean episode length | 146 steps |

## Interpretation

The controller can achieve high-reward landings in some episodes, but performance varies substantially. The mean reward is far below 200, and only 23% of evaluated episodes reached at least 200 reward.

A previous console summary showed “Crashed 77/100”. That number is not accepted as a verified crash count: it appears to have been derived as the complement of the reward >= 200 count. Reward threshold failure is not equivalent to a physical crash. Use termination/truncation flags and explicit landing/crash conditions to classify outcomes.

## Data limitations

The per-episode baseline CSV has not been verified or uploaded. Consequently, paired per-seed statistical tests against DQN cannot yet be performed. Re-run the baseline and save one row per seed with at least:

- seed
- total_reward
- episode_length
- terminated
- truncated
- final_x, final_y, final_angle
- left_leg_contact, right_leg_contact
- outcome classification and its explicit rule

## Status

Baseline summary recorded. Raw episode-level data and validated crash classification remain pending.
