[OpenAI baselines](https://github.com/openai/baselines)


 You'll also need system packages CMake, OpenMPI and zlib. Those can be installed as follows
 
```
 sudo apt-get update && sudo apt-get install cmake libopenmpi-dev python3-dev zlib1g-dev
 ```
 
 ```
 git clone https://github.com/openai/baselines.git
 cd baselines
 pip3 install -e .
  ```
 
 ## Testing the installation
 
 All unit tests in baselines can be run using pytest runner:
 
 ```
 pytest-3
 ```
 
 ## 使用例子
 初始训练：
 ```
 python3 -m baselines.run --alg=ppo2 --env=HalfCheetah-v2 --num_timesteps=5e4 --save_path=~/models --log_path=~/lo
```
接着之前训练的模型继续训练：
```
python3 -m baselines.run --alg=ppo2 --env=HalfCheetah-v2 --num_timesteps=1e6 --load_path=~/models --save_path=~/models --log_path=~/lo --play
```
训练好了，测试，展示：
```
python3 -m baselines.run --alg=ppo2 --env=HalfCheetah-v2 --num_timesteps=0 --load_path=~/models --play
 ```
 
