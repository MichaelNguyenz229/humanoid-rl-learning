# Concepts & Resources

A running log of concepts encountered while building this project.
Updated as I learn more.

---

## Comfortable With

**Policy**
The neural network that controls the robot. Takes observations as input, 
outputs actions. Learned through training, saved as a `.pt` checkpoint file.

**Observation Space**
Everything the robot can "sense" — joint angles, velocity, orientation, etc.
Represented as a vector of numbers fed into the network each step.

**Action Space**
What the robot can control — in this case, target joint positions for all 
29 joints. The network outputs one number per joint per step.

**Reward Function**
A score given to the robot at each step. Sum of positive terms (doing good 
things) and negative terms (penalties). The robot learns to maximize this.

**Episode**
One run of the simulation from start to termination (fell over or timed out).
Longer episodes = robot surviving longer = learning working.

**Iteration**
One full cycle of: collect experience from all parallel envs → update the 
neural network once. Model checkpoints are saved every 50 iterations.

**Convergence**
When mean reward stops consistently improving. Signal to stop training —
more iterations won't meaningfully change the policy.

**Mean Reward**
Average total reward per episode across all parallel environments. 
The primary metric to watch during training.

**Terminations**
Conditions that end an episode early — `fell_over` or `time_out`. 
Watching `fell_over` trend toward 0 is a good sign of learning.

---

## Needs Work

**PPO (Proximal Policy Optimization)**
The algorithm that updates the neural network during training. After each 
batch of simulation data it nudges the network toward actions that got 
higher rewards — but only by a small controlled amount each update to keep 
training stable.
- [Paper](https://arxiv.org/abs/1707.06347)
- [Good visual explainer](https://spinningup.openai.com/en/latest/algorithms/ppo.html)

**Actor / Critic (Value Function)**
PPO uses two networks. The actor decides what action to take. The critic 
estimates how good the current situation is (not what to do, but how 
promising the state looks). The critic helps the actor learn faster.

**Entropy (Mean Entropy Loss)**
A measure of how random the policy's actions are. High entropy early = 
robot exploring many options. Entropy decreasing over time = policy becoming 
more confident/deterministic. Too low too fast = bad, robot stops exploring.

**Curriculum Learning**
Gradually increasing task difficulty during training. In your logs this 
showed up as `Curriculum/command_vel` — the velocity command range started 
small and expanded as the robot improved.

**rsl-rl**
The RL training library used under the hood by mjlab. Implements PPO and 
manages the training loop, logging, and checkpointing.
- [GitHub](https://github.com/leggedrobotics/rsl_rl)
- [Paper](https://arxiv.org/html/2509.10771v1)

---

## For Later

**Sim-to-Real Transfer**
Why a policy trained in simulation doesn't always work on a real robot —
physics gaps, sensor noise, unmodeled dynamics. The core challenge in 
deploying RL policies to hardware.

**Domain Randomization**
Randomly varying simulation parameters (friction, mass, motor strength) 
during training to make policies more robust to sim-to-real gaps.

**Observation Noise / Corruption**
Deliberately adding noise to observations during training to simulate 
imperfect real-world sensors. In mjlab this is `enable_corruption` — 
disabled during play mode for clean evaluation.
