## Train Task
python scripts/train.py [task] --env.scene.num-envs [4096] --video True --video-interval [500] --video-length [150]

## Resume Training
python scripts/train.py [task] --agent.resume True --env.scene.num-envs 4096 --video-interval [500] --video-length [150]

## View your policy
python scripts/play.py [task] --checkpoint-file logs/rsl_rl/[task_log_name]/<timestamp>/model_[].pt --num-envs [shadow clone jutsu num]
for entire checkpoint param -> copy relative path of model_[].pt from .code view 