 You'll also need system packages CMake, OpenMPI and zlib. Those can be installed as follows
 
 sudo apt-get update && sudo apt-get install cmake libopenmpi-dev python3-dev zlib1g-dev
 
 git clone https://github.com/openai/baselines.git
 
 cd baselines
 
 pip install -e .
 
 # Testing the installation
 
 All unit tests in baselines can be run using pytest runner:
 
 pip install pytest
 
 pytest
