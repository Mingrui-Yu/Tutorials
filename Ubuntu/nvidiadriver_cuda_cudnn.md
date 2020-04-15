# Ubuntu 18.04 安装 NVIDIA Driver + cuda + cudnn

## 安装 NVIDIA driver

在　软件和更新　中选择　附加驱动，选择合适的驱动，点击应用更改。

之后重启电脑。

终端输入　```nvidia-smi``` 查看是否成功安装.

注意：430是长期支持，435是短期支持。

## 安装 cuda

注意：cuda 有两个API，一个是和driver装在一起的，另一个是需要在这里单独安装的。两者的版本不用相同。[参考](https://stackoverflow.com/questions/53422407/different-cuda-versions-shown-by-nvcc-and-nvidia-smi)

参考 [Ubuntu18.04安装CUDA10、CUDNN](https://blog.csdn.net/qq_32408773/article/details/84112166)

https://developer.nvidia.com/cuda-toolkit-archive 找到合适的版本下载

所有配置选项选好之后，选择runfile(local)，下载

之后，在下载目录中：

```
sudo sh cuda_10.0.130_410.48_linux.run
```

之后会出一个声明，不断按Enter看下一行，直到最后。

之后，

![](https://pic1.zhimg.com/80/v2-d0cbc3346c466bb90d7566ae6a904cb4_720w.jpg)

注意：Install NVIDIA Accelerated Graphics Driver for ... 选择no

如果想同时安装多版本的cuda，参考[知乎－Ubuntu安装 cuda10 + cudnn7.5 + Tensorflow2.0](https://zhuanlan.zhihu.com/p/65557545)

配置到环境变量：

```
sudo gedit ~/.bashrc

# 打开文件后，在文件末尾添加路径
export PATH=/usr/local/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64:$LD_LIBRARY_PATH　

# 之后更新
source ~/.bashrc
```

!!!特别重要：

```
sudo apt install xserver-xorg-input-all

# 如果没进行这步，重启电脑后进入ubuntu桌面后，鼠标键盘均无法操作
```

重启。如果重启后出现鼠标键盘无法操作状况：[参考](https://blog.csdn.net/qq_38145502/article/details/104898072)。之后cuda安装完毕。

测试是否安装成功：

```
cd /usr/local/cuda/samples/1_Utilities/deviceQuery 
sudo make
./deviceQuery
```

出　Result = PASS 则安装成功.

## 安装 cudnn

在[官网](https://developer.nvidia.com/cudnn)下载安装包，需要注册登录才能下载。选择适合自己的版本(要与cuda的版本对应)

[官网安装教程](https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html)，使用Tar File 进行安装。验证工作不用做。

查看安装的 cuda cudnn 版本：[参考](https://medium.com/@changrongko/nv-how-to-check-cuda-and-cudnn-version-e05aa21daf6c)

```
# 查看cuda
cat /usr/local/cuda/version.txt

# 查看cudnn
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```

