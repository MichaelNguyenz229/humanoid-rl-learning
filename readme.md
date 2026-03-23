# humanoid-rl-learning

Robotics and reinforcement learning are vast, niche, and deeply complex fields.
Rather than studying them top-down, I'm learning by doing — tackling hard tasks,
breaking them down to first principles, and documenting what I figure out along the way.

This repo is a living log of that process. Each experiment is a real training run
with real results, real hardware constraints, and honest observations about what
worked and what didn't.

---

## Approach

I learn best by building. So instead of reading textbooks first, I picked a hard
problem — training a humanoid robot to walk — set up the full pipeline from scratch,
and worked backwards from what I saw to understand why things behaved the way they did.

Every concept in this repo was learned in context, not in isolation.

---

## Stack

- **Simulation:** MuJoCo Warp (GPU-accelerated physics)
- **Framework:** mjlab + unitree_rl_mjlab
- **Algorithm:** PPO via rsl-rl
- **Hardware:** RTX 3070 8GB, WSL2, Ubuntu 22.04 on Windows
- **Tracking:** Weights & Biases

---

## Experiments

| # | Task | Robot | Status |
|---|---|---|---|
| 01 | Flat terrain velocity tracking | Unitree G1 | ✅ Complete |
| 02 | Flat terrain velocity tracking | Unitree G1 (mjlab env) | 🔄 In progress |

---

## Notes
- [`concepts.md`](notes/concepts.md) — RL and robotics concepts explained in my own words
- [`commands.md`](notes/commands.md) — training, eval, and play command reference
- [`hardware_limits.md`](notes/hardware_limits.md) — what runs on an RTX 3070 8GB and what doesn't

---

## Frameworks Used
- [mjlab](https://github.com/mujocolab/mjlab)
- [unitree_rl_mjlab](https://github.com/unitreerobotics/unitree_rl_mjlab)
