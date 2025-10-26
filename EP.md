
## Prep
```

source /etc/network_turbo # autodl
git clone https://github.com/OpenRobotLab/HoST.git
cd HoST
conda env create -f conda_env.yml 
conda init bash
conda activate host
pip3 install torch==1.10.0+cu113 torchvision==0.11.1+cu113 torchaudio==0.10.0+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html

curl -L -IssacGym.tar.gz # Download and install [Isaac Gym](https://developer.nvidia.com/isaac-gym)
tar -xvf IssacGym.tar.gz
cd isaacgym/python && pip install -e . && cd ../..
cd rsl_rl && pip install -e . && cd .. 
cd legged_gym &&  pip install -e . && cd .. 

pip install numpy==1.21.5 torch==2.4.1+cu121 pandas==1.4.3
```

## G1 ground
Notes: reduce 1GB GPU RAM with headless mode

 4090 24G (10k:18GB 12k:21.4GB:37ksteps/s 13kenv:)

|num_envs | gpu ram | steps/sec
|10k      | 18GB    | 
|12k      | 21.4GB  | 37k
|13k      | 22.3GB  | 36k
|13.5k    | 23.6GB  | 37k
```

cd legged_gym
python legged_gym/scripts/train.py --task g1_ground --run_name test_g1 --num_envs 8000 --headless
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_4090/model_0.pt
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_4090/model_500.pt  # fail 2 hour train
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_4090/model_1000.pt # succ 4 hour train


################################################################################
                      Learning iteration 119/12000                      

                       Computation: 34814 steps/s (collection: 16.862s, learning 2.527s)
               Value function loss: 22.3836
                    Surrogate loss: -0.0080

################################################################################
                      Learning iteration 49/12000                       

                       Computation: 29515 steps/s (collection: 20.346s, learning 2.524s)
               Value function loss: 31.5798
                    Surrogate loss: -0.0054
             Mean action noise std: 0.84
                       Mean reward: -547.75
               Mean episode length: 502.00
          Mean episode base_height: 0.1168
 Mean episode rew_task_head_height: 11.1917
 Mean episode rew_task_orientation: 18.1201
 Mean episode rew_regu_action_rate: -0.3136
     Mean episode rew_regu_dof_acc: -2.7610
Mean episode rew_regu_dof_pos_limits: -54.2334
     Mean episode rew_regu_dof_vel: -2.8846
Mean episode rew_regu_dof_vel_limits: -0.5267
 Mean episode rew_regu_joint_power: -0.1554
Mean episode rew_regu_joint_tracking_error: -0.0039
  Mean episode rew_regu_smoothness: -0.9354
     Mean episode rew_regu_torques: -0.1346
Mean episode rew_style_feet_distance: -0.0347
Mean episode rew_style_ground_parallel: 0.0258
Mean episode rew_style_hip_roll_deviation: -0.4311
Mean episode rew_style_hip_yaw_deviation: -0.2423
Mean episode rew_style_knee_deviation: -0.0727
Mean episode rew_style_left_foot_displacement: 0.0011
Mean episode rew_style_right_foot_displacement: 0.0011
Mean episode rew_style_shank_orientation: 0.1383
Mean episode rew_style_shoulder_roll_deviation: -0.2087
Mean episode rew_style_style_ang_vel_xy: 0.0010
Mean episode rew_style_waist_deviation: -0.1067
Mean episode rew_target_ang_vel_xy: 0.0012
Mean episode rew_target_feet_height_var: 0.0014
Mean episode rew_target_lin_vel_xy: 0.0056
Mean episode rew_target_target_base_height: 0.0142
Mean episode rew_target_target_orientation: 0.0184
Mean episode rew_target_target_upper_dof_pos: 0.0080
             Mean episode rew_task: 0.0159
             Mean episode rew_regu: -0.1329
            Mean episode rew_style: -0.0014
           Mean episode rew_target: 0.0001
                Mean episode force: 100.0000
         Mean episode action_scale: 1.0000
--------------------------------------------------------------------------------
                   Total timesteps: 33750000
                    Iteration time: 22.87s
                        Total time: 1108.08s
                               ETA: 264853.5s

################################################################################
                     Learning iteration 1338/12000                      

                       Computation: 53454 steps/s (collection: 10.097s, learning 2.531s)
               Value function loss: 13.6643
                    Surrogate loss: 0.0029
             Mean action noise std: 0.74
                       Mean reward: 483.81
               Mean episode length: 502.00
          Mean episode base_height: 1.1127
 Mean episode rew_task_head_height: 43.8512
 Mean episode rew_task_orientation: 46.0649
 Mean episode rew_regu_action_rate: -0.3684
     Mean episode rew_regu_dof_acc: -0.4940
Mean episode rew_regu_dof_pos_limits: -32.7872
     Mean episode rew_regu_dof_vel: -0.5347
Mean episode rew_regu_dof_vel_limits: -0.0123
 Mean episode rew_regu_joint_power: -0.0234
Mean episode rew_regu_joint_tracking_error: -0.0004
  Mean episode rew_regu_smoothness: -1.0907
     Mean episode rew_regu_torques: -0.0200
Mean episode rew_style_feet_distance: -0.0208
Mean episode rew_style_ground_parallel: 13.2759
Mean episode rew_style_hip_roll_deviation: -0.0003
Mean episode rew_style_hip_yaw_deviation: -0.1447
Mean episode rew_style_knee_deviation: -0.1770
Mean episode rew_style_left_foot_displacement: 0.8744
Mean episode rew_style_right_foot_displacement: 0.8743
Mean episode rew_style_shank_orientation: 7.1154
Mean episode rew_style_shoulder_roll_deviation: -0.5488
Mean episode rew_style_style_ang_vel_xy: 0.2927
Mean episode rew_style_waist_deviation: -0.0653
Mean episode rew_target_ang_vel_xy: 2.6765
Mean episode rew_target_feet_height_var: 1.0108
Mean episode rew_target_lin_vel_xy: 3.6542
Mean episode rew_target_target_base_height: 4.6037
Mean episode rew_target_target_orientation: 5.8573
Mean episode rew_target_target_upper_dof_pos: 1.1711
             Mean episode rew_task: 0.0963
             Mean episode rew_regu: -0.0712
            Mean episode rew_style: 0.0503
           Mean episode rew_target: 0.0468
                Mean episode force: 0.0000
         Mean episode action_scale: 0.2500
--------------------------------------------------------------------------------
                   Total timesteps: 903825000
                    Iteration time: 12.63s
                        Total time: 20422.56s
                               ETA: 162617.8s


```

Training on 3070 8GB

```
python legged_gym/scripts/train.py --task g1_slope --run_name test_g1 --num_envs 1000 --headless
python legged_gym/scripts/train.py --task g1_wall --run_name test_g1 --num_envs 1000 --headless

python legged_gym/scripts/train.py --task g1_ground --run_name test_g1 --num_envs 1500 --headless
python legged_gym/scripts/train.py --task g1_ground --run_name test_g1 --num_envs 1500 --headless --checkpoint_path logs/g1_ground/g1_3070/model_7000.pt --checkpoint 7000 --resume
python legged_gym/scripts/train.py --task g1_ground --run_name test_g1 --num_envs 1500 --headless --checkpoint_path logs/g1_ground/g1_3070_2/model_12000.pt  --checkpoint 12000 --resume

python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070/model_2000.pt # 2 hour, some succ 
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070/model_3500.pt # 6 hour, part succ 
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070/model_7000.pt # 12 hour, all succ
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070_2/model_12000.pt # 24 hour, all succ
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070_3/model_19500.pt # 36 hour, all succ

python legged_gym/scripts/eval/eval_ground.py --task g1_ground --checkpoint_path logs/g1_ground/g1_3070_3/model_19500.pt 

python legged_gym/scripts/eval/eval_slope.py --task g1_slope --checkpoint_path logs/g1_slope/3070/model_10000.pt 
python legged_gym/scripts/eval/eval_ground.py --task g1_wall --checkpoint_path logs/g1_wall/3070/model_2500.pt 


################################################################################
Success rate:  100.0 0.0
Average feet movement:  1.1228190660476685 0.09850873798131943
Average smoothness:  2.6556499004364014 0.20296776294708252
Average motion tracking error:  4.020101547241211 0.04945862293243408
Average times before standing up:  0.0 0.0
Average energy:  1142.68359375 10.849494934082031
Average smoothness before standing up:  4.697909355163574 0.5012660026550293
double free or corruption (out)
Aborted (core dumped)

################################################################################
                     Learning iteration 7052/12000                      

                       Computation: 16818 steps/s (collection: 3.665s, learning 0.794s)
               Value function loss: 24.5021
                    Surrogate loss: -0.0163
             Mean action noise std: 0.84
                       Mean reward: 2.59
               Mean episode length: 502.00
          Mean episode base_height: 1.1627
 Mean episode rew_task_head_height: 44.6883
 Mean episode rew_task_orientation: 45.9099
 Mean episode rew_regu_action_rate: -0.4800
     Mean episode rew_regu_dof_acc: -0.6159
Mean episode rew_regu_dof_pos_limits: -89.0959
     Mean episode rew_regu_dof_vel: -0.6091
Mean episode rew_regu_dof_vel_limits: -0.0512
 Mean episode rew_regu_joint_power: -0.0232
Mean episode rew_regu_joint_tracking_error: -0.0005
  Mean episode rew_regu_smoothness: -1.4230
     Mean episode rew_regu_torques: -0.0278
Mean episode rew_style_feet_distance: -0.0498
Mean episode rew_style_ground_parallel: 15.0068
Mean episode rew_style_hip_roll_deviation: 0.0000
Mean episode rew_style_hip_yaw_deviation: -0.2164
Mean episode rew_style_knee_deviation: -0.1985
Mean episode rew_style_left_foot_displacement: 1.0418
Mean episode rew_style_right_foot_displacement: 1.0420
Mean episode rew_style_shank_orientation: 7.9974
Mean episode rew_style_shoulder_roll_deviation: -0.2285
Mean episode rew_style_style_ang_vel_xy: 0.3493
Mean episode rew_style_waist_deviation: -0.0242
Mean episode rew_target_ang_vel_xy: 3.3911
Mean episode rew_target_feet_height_var: 1.2417
Mean episode rew_target_lin_vel_xy: 5.3629
Mean episode rew_target_target_base_height: 6.3368
Mean episode rew_target_target_orientation: 7.1856
Mean episode rew_target_target_upper_dof_pos: 0.2574
             Mean episode rew_task: 0.0975
             Mean episode rew_regu: -0.2292
            Mean episode rew_style: 0.0601
           Mean episode rew_target: 0.0601
                Mean episode force: 0.0000
         Mean episode action_scale: 0.2500
--------------------------------------------------------------------------------
                   Total timesteps: 528975000
                    Iteration time: 4.46s
                        Total time: 28677.61s
                               ETA: 20118.6s


```

## Pi ground 
```
python legged_gym/scripts/train.py --task pi_ground --run_name test_pi_ground --checkpoint_path logs/pi_ground/3070 --checkpoint 0 --num_envs 1500
python legged_gym/scripts/play.py --task pi_ground --checkpoint_path logs/pi_ground/3070/model_12000.pt
```

## G1 ground prone
```
python legged_gym/scripts/train.py --task g1_ground_prone --run_name test_g1_ground_prone --num_envs 1000
python legged_gym/scripts/play.py --task g1_ground --checkpoint_path ${/path/to/ckpt.pt} # [ground, platform, slope, wall]

################################################################################
                      Learning iteration 213/12000                      

                       Computation: 3696 steps/s (collection: 12.959s, learning 0.568s)
               Value function loss: 17.4046
                    Surrogate loss: -0.0299
             Mean action noise std: 0.79
                       Mean reward: -189.28
               Mean episode length: 502.00
          Mean episode base_height: 0.4503
 Mean episode rew_task_head_height: 22.0941
 Mean episode rew_task_orientation: 22.7530
 Mean episode rew_regu_action_rate: -0.3079
     Mean episode rew_regu_dof_acc: -2.7262
Mean episode rew_regu_dof_pos_limits: -45.0532
     Mean episode rew_regu_dof_vel: -2.7580
Mean episode rew_regu_dof_vel_limits: -0.5351
 Mean episode rew_regu_joint_power: -0.1478
Mean episode rew_regu_joint_tracking_error: -0.0039
  Mean episode rew_regu_smoothness: -0.9150
     Mean episode rew_regu_torques: -0.1395
Mean episode rew_style_feet_distance: -0.0025
Mean episode rew_style_hip_pitch_deviation: -0.4431
Mean episode rew_style_hip_roll_deviation: -0.0313
Mean episode rew_style_hip_yaw_deviation: -0.4703
Mean episode rew_style_knee_deviation: -0.1105
Mean episode rew_style_left_foot_displacement: 0.1600
Mean episode rew_style_right_foot_displacement: 0.1570
Mean episode rew_style_shoulder_roll_deviation: -0.4778
Mean episode rew_style_style_ang_vel_xy: 0.2771
  Mean episode rew_style_thigh_ori: 6.9220
Mean episode rew_style_waist_deviation: -0.0239
Mean episode rew_target_ang_vel_xy: 0.0572
Mean episode rew_target_feet_height_var: 0.1307
Mean episode rew_target_lin_vel_xy: 0.2594
Mean episode rew_target_lower_body_deviation: 5.3677
Mean episode rew_target_target_base_height: 0.5461
Mean episode rew_target_target_orientation: 0.5921
Mean episode rew_target_target_upper_dof_pos: 0.5259
             Mean episode rew_task: 0.0363
             Mean episode rew_regu: -0.1022
            Mean episode rew_style: 0.0117
           Mean episode rew_target: 0.0152
                Mean episode force: 79.3648
         Mean episode action_scale: 0.9793
--------------------------------------------------------------------------------
                   Total timesteps: 10700000
                    Iteration time: 13.53s
                        Total time: 2834.40s
                               ETA: 156117.4s
```
