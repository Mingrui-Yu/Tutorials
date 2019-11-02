# 安装Ubuntu导致Windows时间错误解决方案

Ubuntu 默认硬件时间为UTC（Coordinated Universal Time）即协调世界时，中国时间为UTC+8；而Windows则认定硬件时间为系统时间。这就造成了当先开启Ubuntu系统时，系统从网络得到本地时间例如为8点钟，然后其修改硬件时间为0点，再次启用Windows时，Windows读取硬件时间为本地时间，这就造成了系统显示时间比实际时间慢8小时的问题

目前通用的解决方法有两种：一种是修改Ubuntu系统时间的读取方式，另一种是修改Windows系统时间的读取方式。在此推荐修改Ubuntu系统，因为修改方式极其简单。

在终端输入：
```
#安装时间校准服务
sudo apt-get install ntpdate

#从time.windows.com获取本地时间
sudo ntpdate time.windows.com

#同步时间到硬件
sudo hwclock --localtime --systohc
```