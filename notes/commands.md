## Train Task
python scripts/train.py [task] --env.scene.num-envs [4096] --video True --video-interval [500] --video-length [150]

python scripts/train.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096 

python scripts/train.py Unitree-G1-Tracking-No-State-Estimation --motion_file=src/assets/motions/g1/dance1_subject2.npz --env.scene.num-envs=4096 

## Resume Training
python scripts/train.py [task] --agent.resume True --env.scene.num-envs 4096

python scripts/train.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/g1_ch12.npz --agent.resume True --env.scene.num-envs 4096 


## View your policy
python scripts/play.py [task] --checkpoint-file logs/rsl_rl/[task_log_name]/<timestamp>/model_[].pt --num-envs [shadow clone jutsu num]

python scripts/play.py Unitree-G1-Tracking --motion_file=src/assets/motions/g1/g1_ch12.npz --checkpoint_file=logs/rsl_rl/g1_tracking/2026-03-25_22-29-46/model_100.pt --num-envs 16
