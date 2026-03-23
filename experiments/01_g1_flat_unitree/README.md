# Experiment 01 — Unitree G1 Flat Terrain Velocity Tracking

## What this is
Trained a locomotion policy for the Unitree G1 humanoid robot to follow 
velocity commands on flat terrain using PPO (Proximal Policy Optimization).

## Task
- **Robot:** Unitree G1 humanoid
- **Environment:** Flat terrain
- **Goal:** Follow commanded linear (forward/sideways) and angular (turning) velocity
- **Framework:** unitree_rl_mjlab + mjlab
- **Algorithm:** PPO via rsl-rl

## Training setup
- **Hardware:** RTX 3070 8GB, WSL2, Ubuntu 22.04
- **Parallel environments:** 4096 (training), 16 (visualization)
- **Iterations:** ~3000
- **Training time:** ~2.5 hours across multiple runs

## What I observed
| Iteration | Behavior |
|---|---|
| 0 | Falling instantly, no stability |
| 900 | Fighting gravity, starting to stabilize |
| 1100 | Stable standing, no linear movement yet |
| 1400 | Moving slowly and unconfidently |
| 3000 | Confidently following velocity commands in any direction |

## Why I stopped at 3000
Mean reward began to saturate and `fell_over` terminations 
approached near zero — signs the policy had converged.

## Results
- See `videos/` for checkpoint progression clips
- See `results/` for wandb reward curves

## Key learnings
- Reward is a sum of many terms — positive for good behavior, 
  negative for bad (jerky movement, falling, self collision)
- Episode length increasing over time = robot surviving longer = learning
- 4096 parallel envs on a single RTX 3070 is feasible for flat terrain
- Rough terrain exceeded VRAM limits at 4096 envs
