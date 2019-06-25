# Ubuntu 18.04 NVIDIA driver installation (Failure in Thinkpad S5)

[1050Ti Ubuntu18.04](https://blog.cnblogs.com/devilmaycry812839668/p/10351400.html)

[Ubuntu18.04](https://blog.csdn.net/chentianting/article/details/85089403)


## 禁用nouveau驱动
Ubuntu系统集成的显卡驱动程序是nouveau，我们需要先将nouveau从Linux内核卸载掉才能安装NVIDIA官方驱动。 
将nouveau添加到黑名单blacklist.conf中，linux启动时，就不会加载nouveau. 

由于blacklist.conf文件的属性不允许修改。所以需要先修改文件属性。
```
sudo chmod 666 /etc/modprobe.d/blacklist.conf
``` 
```
sudo vi /etc/modprobe.d/blacklist.conf
```
在文件末尾添加如下几行：
```
blacklist vga16fb 
blacklist nouveau 
blacklist rivafb 
blacklist rivatv 
blacklist nvidiafb
```
修改并保存文件后，记得把文件属性复原：
```
sudo chmod 644 /etc/modprobe.d/blacklist.conf
```

再更新一下内核：
```
sudo update-initramfs -u
``` 
修改后需要重启系统。

重启系统确认nouveau是已经被屏蔽掉，使用lsmod命令查看：
```
lsmod | grep nouveau
```
---
安装驱动之前另一个重要的事情就是确认系统里面没有旧版本的驱动，以免发生冲突，因此需要卸载旧版本的驱动。
```
sudo apt-get  autoremove --purge nvidia*
```
## PPA方式安装显卡驱动：

在Linux系统里面安装显卡驱动使用PPA的方式成功率一般比较高，但是安装的版本有限:

使用如下命令添加Graphic Drivers PPA：
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
寻找合适的驱动版本
```
ubuntu-drivers devices
```
安装NVIDIA driver ,如上图显示recommand的驱动, 按ctrl+alt+F1进入tty文本模式[tty注意事项](https://github.com/Mingrui-Yu/Tutorials/blob/master/Ubuntu/tty.md) , 关闭(图形)桌面显示管理器LightDM
```
sudo service lightdm stop
``` 
如果提示unit lightdm.service not loaded, 则先安装LightDm： 
```
sudo apt install lightdm
```
安装完毕后跳出一个界面，选择lightdm，再
```
sudo service lightdm stop
```

```
sudo apt-get install nvidia-390
sudo reboot
```
安装完成后重启。

重启系统后，执行下面的命令查看驱动的安装状态显示安装成功
```
sudo nvidia-smi
sudo nvidia-setting
```

重启X-window 服务
```
sudo service lightdm start
```
