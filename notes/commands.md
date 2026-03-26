## Train Task
python scripts/train.py [task] --env.scene.num-envs [4096] --video True --video-interval [500] --video-length [150]
python scripts/train.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096 --video True --video-interval [2000] --video-length [150]

python scripts/train.py Unitree-G1-Tracking-No-State-Estimation --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096 --video True --video-interval [2000] --video-length [150]

## Resume Training
python scripts/train.py [task] --agent.resume True --env.scene.num-envs 4096 --video True --video-interval [500] --video-length [150]
python scripts/train.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/dance1_subject2.npz --agent.resume True --env.scene.num-envs 4096 --video True --video-interval [2000] --video-length [150]

python scripts/train.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096

## View your policy
python scripts/play.py [task] --checkpoint-file logs/rsl_rl/[task_log_name]/<timestamp>/model_[].pt --num-envs [shadow clone jutsu num]
for entire checkpoint param -> copy relative path of model_[].pt from .code view 

python scripts/play.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/dance1_subject2.npz --checkpoint_file=logs/rsl_rl/g1_tracking/2026-xx-xx_xx-xx-xx/model_xx.pt --num-envs 16
