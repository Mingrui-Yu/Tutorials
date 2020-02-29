# Ubuntu 18.04 ROS melodic

## 安装
[官方安装教程](http://wiki.ros.org/melodic/Installation/Ubuntu)，其中第一步使用国内镜像：
```
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ $DISTRIB_CODENAME main" > /etc/apt/sources.list.d/ros-latest.list'
```
参考资料：[在Ubuntu 18.04 LTS安装ROS Melodic](https://blog.csdn.net/ZhangRelay/article/details/80241758)

### sudo rosdep init 出错
sudo  rosdep init 报错：
```
ERROR: cannot download default sources list from:
https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list
Website may be down.
```
首先试一试在浏览器中能不能打开，如果打不开的话，说明该网站需要翻墙。

因为在终端中安装，所以光浏览器能翻不够，还得配置终端翻墙，配置方法可见 shadowsocks.md 相关教程。

成功配置终端翻墙后，如果还报这个错，则需要：
```
sudo c_rehash /etc/ssl/certs 
sudo -E rosdep init
```
之后再 rosdep update 就可以了。

参考资料：
* [sudo rosdep init出错的解决方案](https://zhuanlan.zhihu.com/p/43345574)
* [sudo rosdep init 错误 ](https://wenda.ncnynl.com/question/116401)

## 学习教程
[ROS-Tutorials](http://wiki.ros.org/ROS/Tutorials)