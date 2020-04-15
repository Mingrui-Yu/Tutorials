# Ubuntu 18.04 caffe

# caffe-cpu

## 安装
[官网教程](http://caffe.berkeleyvision.org/install_apt.html)，其中提到 18.04 可以通过 apt-get 直接安装，但实测好像只装了 python 版本，没有找到 cpp 等源码在哪里。所以还是得通过源码编译安装。

### 安装依赖
```
sudo apt install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt install -y --no-install-recommends libboost-all-dev
sudo apt install -y libatlas-base-dev
sudo apt install -y libgflags-dev libgoogle-glog-dev liblmdb-dev
```
 [参考资料](https://github.com/BVLC/caffe/issues/2704)

### 下载源码
```
git clone https://github.com/BVLC/caffe.git
cd caffe
```

### 修改 CMakeLists.txt
可以使用 makefile，也可以使用 cmake，这里使用 cmake。

为了安装 caffe-cpu，CMakeList.txt 需要做修改：
```
caffe_option(CPU_ONLY  "Build Caffe without CUDA support" ON)  # 从 OFF 改为 ON

set(python_version "3" CACHE STRING "Specify which Python version to use")  # 从 "2" 改成 "3"
```
 [参考资料](https://github.com/BVLC/caffe/pull/1667)

### 编译
```
mkdir build
cd build
cmake ..
make all
make install
make runtest
```
 [参考资料](http://caffe.berkeleyvision.org/installation.html#compilation)

## 使用 caffe-cpu 的其他项目，在编译时报错 cublas_v2.h can't find

这是因为没有安装 cuda，自然也没有 cublas_v2.h。但 caffe-cpu 不需要 cuda。在 caffe 编译的过程中，通过设置 
```
caffe_option(CPU_ONLY  "Build Caffe without CUDA support" ON)  # 从 OFF 改为 ON
```
避免了这个问题，但这个问题在其他使用 caffe-cpu 的项目编译时再次出现。

解决办法，在项目的 CMakeLists.txt 中添加：
```
add_definitions( -DCPU_ONLY=1 )
```
 [参考资料](https://github.com/BVLC/caffe/issues/2704)

# caffe-cuda + anaconda3 + python2.7

[官网教程](http://caffe.berkeleyvision.org/install_apt.html)

#### 首先安装相关依赖

```
sudo apt build-dep caffe-cuda       # dependencies for CUDA version

# 似乎不全，上文cpu教程中的那些依赖也装了吧
```

#### 下载源码

eg. 下载在　~/

```
git clone https://github.com/BVLC/caffe.git
cd caffe
```

#### 建立anaconda虚拟环境

```
conda create --name ENV_NAME python=2.7      # ENV_NAME 可以命名为caffe_py27

source activate ENV_NAME

# 在该环境内安装caffe相关依赖
cd ~/caffe/python
for req in $(cat requirements.txt); do pip install $req; done
```

#### 修改caffe/Makefile.config

```
cp Makefile.config.example Makefile.config
# 在Makefile.config中进行修改
```

去掉注释： USE_CUDNN := 1

去掉注释： OPENCV_VERSION := 3

去掉注释：CUDA_DIR := /usr/local/cuda　（检查cuda的path对不对）

CUDA_ARCH中按提示注释掉该注释的

注释：PYTHON_INCLUDE

去掉注释：ANACONDA_HOME　及后面几行，注意修改为　anaconda 虚拟环境中　python 的 path。eg: ANACONDA_HOME := $(HOME)/anaconda3/envs/ENV_NAME

注释：PYTHON_LIB := /usr/lib

去掉注释：PYTHON_LIB := $(ANACONDA_HOME)/lib

去掉注释：WITH_PYTHON_LAYER := 1

在相应位置进行如下修改：否则运行时报错 没有"hdf5.h" [参考](https://github.com/BVLC/caffe/issues/2690)

```
# Whatever else you find you need goes here.
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
```

#### 编译

使用 make 不使用 cmake

```
make all -j4
make test
make runtest
make pycaffe
make distribute
```

#### 其他操作

运行时报错：fatal error: caffe/proto/caffe.pb.h: No such file or directory 

解决：[参考](https://github.com/muupan/dqn-in-the-caffe/issues/3)

```
# In the directory you installed Caffe to
protoc src/caffe/proto/caffe.proto --cpp_out=.
mkdir include/caffe/proto
mv src/caffe/proto/caffe.pb.h include/caffe/proto
```

另外，若使用 make 安装的 头文件目录在 ~/caffe/include，而如果使用 cmake 安装的头文件目录在 ~/caffe/build/install/include。在使用caffe的项目中，需要注意caffe的路径

为了使用pycaffe，需要进行如下操作才能正常 import caffe: [参考](https://yangcha.github.io/Caffe-Conda/)

```
 sudo gedit ~/.bashrc

# 在末尾添加
export PYTHONPATH=~/caffe/python:${PYTHONPATH:+:${PYTHONPATH}}

# 更新
 source ~/.bashrc
```

重启终端。

# 在服务器安装时出现的问题

1. 重装一下 cudnn