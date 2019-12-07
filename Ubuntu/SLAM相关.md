# SLAM需要的配置: Eigen, OpenCV, PCL

## Eigen
```
sudo apt-get install libeigen3-dev
```
之后创建链接：
```
sudo ln -sf eigen3/Eigen Eigen
sudo ln -sf eigen3/unsupported unsupported
```

## OpenCV
安装依赖项：（其中有些需要新版本）
```
sudo apt-get install build-essential libgtk2.0-dev libvtk5-dev libjpeg-dev libtiff4-dev libjasper-dev
libopenexr-dev libtbb-dev
```
在OpenCV官网下载OpenCV for linux （Source），解压后进入目标文件夹cmake：
```
mkdir build
cd build
cmake ..
make
sudo make install
```

### 可能出现程序错误及解决方法

一、错误：error while loading shared libraries: libopencv_core.so.3.x: cannot open shared object file: No such file or directory


解决方法:

如果共享库文件已经安装到了/lib或/usr/lib目录下，需要再执行一下ldconfig命令：
```
sudo ldconfig
```
如果共享库文件安装到了/usr/local/lib(很多开源的共享库都会安装到该目录下)或其它"非/lib或/usr/lib"目录下, 那么在执行ldconfig命令前, 还要把新共享库目录加入到共享库配置文件/etc/ld.so.conf中, 参考[error while loading shared libraries: xxx.so.x" 错误的原因和解决办法](https://www.cnblogs.com/Anker/p/3209876.html)

二、错误：Failed to load module "canberra-gtk-module"

解决办法：
```
sudo apt-get install libcanberra-gtk-module
```

## PCL 安装
```
sudo apt-get install libpcl-dev pcl-tools
```
可能会报错：

    有一些软件包无法被安装。如果您用的是 unstable 发行版，这也许是
    因为系统无法达到您要求的状态造成的。该版本中可能会有一些您需要的软件
    包尚未被创建或是它们已被从新到(Incoming)目录移出。
    下列信息可能会对解决问题有所帮助：
    下列软件包有未满足的依赖关系：
此时可以这样解决：安装aptitude，aptitude可以比apt-get更加智能地解决依赖问题。
```
sudo apt-get install aptitude
sudo aptitude install libpcl-dev
sudo apt-get install pcl-tools
```

