# Ubuntu18.04 pppoe 拨号上网

## 据测试不太好用
首先，关闭有线连接，同时，有线连接设置中的“自动连接”不能勾选。

之后：
```
sudo pppoeconf
```
之后输入用户名（删除username）和密码。

一路yes即可。

```
# 启动
sudo pon dsl-provider

# 关闭
sudo poff dsl-provider
```

## 好用的
In Terminal：
```
nmcli con edit type pppoe con-name "networkname" # networkname 随便起

set pppoe.username wrangler  # wrangler是我的校园网账户名
save
quit
```
之后打开右上角网络设置，可以看到自己添加的networkname的网络。

点它，点设置图标，不填写，会弹出一个黑色的框框，里面填入 服务：networkname，密码：账号密码。之后点确定，框框不会消失，再点取消就可以了。（不出现框框的话就把这个网络删除，重新创建一个。删除方法如下文）

设置-常规里面选中自动连接。

有线网络1的设置-常规里面不选中自动连接。

这样基本就好了，以后连接该网络就可以直接点这个了。但是重启后会显示有线网络未托管。解决方法：
```
sudo gedit /etc/NetworkManager/NetworkManager.conf  # 打开后，找到 [ifupdown] managed=false 修改成： [ifupdown] managed=true

sudo service network-manager restart  # 其他地方可以也会用到
```
之后再重启就不会有这个问题了。

接入XJTU校园网需要在10.6.8.2上登录。

### 查看曾经创建的网络（创建、删除）
```
# sudo打开文件管理器
sudo nautilus  
```
之后找到/usr/share/applications/Network connections，里面可以看到创建的网络，也可以创建网络和删除网络。