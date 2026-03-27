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

## Algorithm changes       
— PPO vs SAC vs DDPG, changing how gradients are computed, changing the optimizer itself

## Hyperparameter tuning   
— learning rate, entropy coef, batch size, clip range — knobs on the algorithm

## Reward shaping           
— adding/removing/reweighting reward terms, changing what behavior gets positive signal

## Env tuning               
— termination thresholds, episode length, domain randomization, observation noise —changing the MDP structure itself
