# Ubuntu18.04 安装最新版firefox浏览器（国内版）

firefox浏览器分：国际版和国内版。

二者之间账户不互通（我可以用同一个邮箱分别在国际版和国内版上注册）

所以，如果想同步书签啥的的化，需要统一使用国内版。

windows上官网下载的就是国内版。

ubuntu默认安装(apt-get)的firefox是国际版，所以需要自己去官网下载最新的国内版

## 安装

先卸载国际版：
```
sudo apt-get remove firefox
```

[Firefox官网](http://www.firefox.com.cn/)， 下载下来的是一个tar.bz2文件。(解压后其中/foxfire/foxfire可以直接绿色运行(可能需要邮件属性更改为可执行))

之后：

```
# 解压该文件
tar -xvf Firefox-latest-x86_64.tar.bz2

# 将解压的中文版 Firefox 移动到应该的位置
sudo mv firefox  /opt

cd  /usr/share/applications

# 创建firefox.desktop文件
sudo touch firefox.desktop

sudo gedit firefox.desktop
```
编辑内容为：
```
[Desktop Entry]
Name=firefox
Name[zh_CN]=火狐浏览器
Comment=火狐浏览器
Exec=/opt/firefox/firefox
Icon=/opt/firefox/browser/chrome/icons/default128.png #可能在其他位置
Terminal=false
Type=Application
Categories=Application
Encoding=UTF-8
StartupNotify=true
```
保存后退出，重启后应该可以了。
```
sudo reboot
```
在DASH下搜索firefox即可找到我们安装的中文版火狐浏览器了，拖到Dock中固定即可。

**但是，火狐的图标未能正确显示，可以点开，但图标缺失（透明）**

## 使用shadowsocks科学上网

在shadowsocks已经配置好的情况下，chrome已经可以科学上网，但firefox不行。

需要再配置：Firefox-首选项-常规-网络设置：  
* 手动配置代理: SOCKS主机：127.0.0.1 端口：1080
* 下方勾选“使用SOCKS v5时代理DNS查询”。