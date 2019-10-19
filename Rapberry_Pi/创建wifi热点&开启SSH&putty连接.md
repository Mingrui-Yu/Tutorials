# Pi3 创建wifi热点 & 开启SSH & putty连接


## 创建wifi热点并设置开机自启动
```
# 创建WiFi热点使用的GitHub上一个开源项目： 
https://github.com/oblique/create_ap
 
#将代码copy到本地，安装
sudo git clone https://github.com/oblique/create_ap
cd create_ap
sudo make install
 
#安装依赖的库
sudo apt-get install util-linux procps hostapd iproute2 iw haveged dnsmasq
 
# 此时你可以创建热点，通过以下命令：
sudo create_ap wlan0 eth0 热点名 密码
```
设置开机自启动：
```
sudo nano /etc/rc.local

# 在exit 0 之前加入
sudo create_ap wlan0 eth0 热点名 密码
```


## 开启SSH服务
在Pi终端中，输入：
```
sudo raspi-config
```
界面中选中Interfacing Optians, 然后再选SSH，Enable SSH。
