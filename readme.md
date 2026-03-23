# RL Training with mjlab


## training a certain task
python scripts/train.py [task] --env.scene.num-envs [4096] --video True --video-interval [500] --video-length [150]

## resume training
python scripts/train.py [task] --agent.resume True --env.scene.num-envs 4096
