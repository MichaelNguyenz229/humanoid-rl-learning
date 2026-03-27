# Tuning the G1 

## anchor_pos 
— "anchor" refers to the root body, which is the pelvis/hip link. It's the parent of everything else in the kinematic tree. anchor_pos measures how far the robot's pelvis is from where the reference motion says the pelvis should be in world space (XYZ). If the reference says the pelvis should be at x=0.3m forward and the robot's pelvis is at x=0.0m, that's anchor_pos error.

## anchor_ori 
— same thing but for pelvis rotation. How much is the pelvis orientation (yaw/pitch/roll) diverging from the reference.

## ee_body_pos 
— "end effector body position." This tracks specific body link positions 
— hands, feet, maybe knees 
— against where the reference says they should be in world space. Not joint angles, but actual 3D positions of the limbs.

## 

## Layer 1: Algorithm changes       
— PPO vs SAC vs DDPG, changing how gradients are computed, changing the optimizer itself

## Layer 2: Hyperparameter tuning   
— learning rate, entropy coef, batch size, clip range — knobs on the algorithm

## Layer 3: Reward shaping           
— adding/removing/reweighting reward terms, changing what behavior gets positive signal

## Layer 4: Env tuning               
— termination thresholds, episode length, domain randomization, observation noise —changing the MDP structure itself

# Trainig Guidelines
Env tuning question: "Can the robot even try?"
Reward tuning question: "Is the robot trying the right thing?"
Reward shaping question: "Is the robot trying correctly?"

# MAIN TRACKING REWARDS — positive, these are what you want
"motion_global_root_pos":   weight= 2.0  # pelvis position
"motion_global_root_ori":   weight= 1.0  # pelvis orientation  
"motion_body_pos":          weight= 2.0  # all body links position
"motion_body_ori":          weight= 1.0  # all body links orientation
"motion_body_lin_vel":      weight= 1.0  # linear velocity matching
"motion_body_ang_vel":      weight= 2.0  # angular velocity (spin)
"torso_stability":          weight= 1.5  # your new custom term

# PENALTIES — negative, these punish bad behavior
"action_rate_l2":           weight=-0.01  # punish jerky actions
"joint_limit":              weight=-1.0   # punish hitting joint limits
"self_collisions":          weight=-1.0   # punish self hitting self
```

The policy is always trying to **maximize total reward** each episode. So it's naturally pulled toward the positive terms and pushed away from the negative ones.

---

## Why the balance matters

Think of it as a tug of war:
```
Positive side                    Negative side
─────────────────────────────────────────────
motion_body_pos    +2.0    vs    self_collisions  -1.0
motion_body_ang_vel +2.0   vs    joint_limit      -1.0
motion_global_root_pos +2.0 vs   action_rate_l2  -0.01
─────────────────────────────────────────────
Total positive ≈ +11.5      Total negative ≈ -2.01
```

With our changes, positive side wins clearly. The policy is incentivized to track the motion even if it causes some self collision.

**Before our changes it looked like this:**
```
Total positive ≈ +6.5       Total negative ≈ -20.1
```

Negative side was winning. The policy learned that the safest strategy — maximizing total reward — was to **stand still and avoid collisions** rather than attempt the motion. Standing still means no arm swings, no self collision, no joint limit violations. It scored better by doing nothing.

That's exactly the local optimum collapse we saw in your WandB graphs around iteration 200.

---

## Simple rule of thumb
```
Sum of all positive weights >> Sum of all negative weights
