# 在树莓派上安装基于python的opencv 

## python2 + opencv
```
sudo pip install opencv-python
```


## python3 + opencv

### 在树莓派设置中把根目录扩大到整个SD卡
```
sudo raspi-config
```
Advanced Options -- Expand Filesystem

### 不成功：直接使用pip3安装
（最新版树莓派系统2019.10已经可以通过此方式直接安装）

若使用：
```
sudo pip3 install opencv-python

# 安装依赖库
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install qt4-dev-tools libatlas-base-dev
``` 
不成功

### 成功：离线安装
首先在浏览器中输入下载地址：
(https://www.piwheels.org/simple/opencv-python/opencv_python-3.4.3.18-cp34-cp34m-linux_armv7l.whl)
注意网址对应版本：opencv3.4.3 + python3.4

下载好后，将该whl文件导入树莓派中；

在树莓派上离线安装：
```
sudo pip3 install opencv_python-3.4.3.18-cp34-cp34m-linux_armv7l.whl
```

成功后，安装依赖库：
```
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install qt4-dev-tools libatlas-base-dev
```
(可能还有其他依赖库)

测试，在Terminal中输入：
```
python3
import cv2
```

# python脚本调用摄像头
可以直接使用opencv调用摄像头

在 ```sudo raspi-config``` 中启用Camera，然后重启。

之后参考 [树莓派（Raspberry Pi）中PiCamera+OpenCV的使用](https://blog.csdn.net/u012005313/article/details/70244747#C0)

***
***
***
参考资料：

[树莓派python3使用pip3安装opencv3.4](https://blog.csdn.net/weixin_42834671/article/details/100620865)