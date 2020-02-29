# Ubuntu 18.04 caffe

caffe-cpu

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
