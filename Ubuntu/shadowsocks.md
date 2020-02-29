# ubuntu 中配置shadowsocks


### 安装及初始配置
安装shadowsocks3.0:
```
sudo pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U
```

配置：
```
sudo nano /etc/shadowsocks.json
```
内填入：

```
{
    "server":"服务器的ip",
    "server_port":xxxxx,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"密码",
    "timeout":300,
    "method":"aes-256-gcm"
}
```

### 每次开机

运行：
```
sslocal -c /etc/shadowsocks.json
```
之后配置网络代理：ubuntu设置-网络-网络代理-手动：在Socks中填入127.0.0.1和1080。

若不运行，需要讲网络代理再改回来


## 终端翻墙

### 安装及初始配置
**安装 Polipo:** Shadowsocks 默认是用 Socks5 协议的，对于 Terminal 的 get,wget 等走 Http 协议的地方是无能为力的，所以需要转换成 Http 代理，加强通用性。
```
sudo apt-get install polipo
```
修改配置文件：
```
sudo gedit /etc/polipo/config
```
将下面的内容整个替换到文件中并保存：
```
# This file only needs to list configuration variables that deviate
# from the default values.  See /usr/share/doc/polipo/examples/config.sample
# and "polipo -v" for variables you can tweak and further information.
logSyslog = false
logFile = "/var/log/polipo/polipo.log"
 
socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5
 
chunkHighMark = 50331648
objectHighMark = 16384
 
serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32
 
proxyAddress = "0.0.0.0"
proxyPort = 8123
```
重启 Polipo：
```
/etc/init.d/polipo restart
```

### 需要终端翻墙时:
启动 Polipo：
```
/etc/init.d/polipo start
```

在需要翻墙的终端中配置代理（以下配置只对当前终端有效），在终端输入：
```
export http_proxy="http://127.0.0.1:8123/"
export https_proxy="https://127.0.0.1:8123/"
```
（Optional）输入查看代理的设置情况：
```
env | grep proxy
```
如果想撤销当前会话的http_proxy代理，使用：
```
unset http_proxy
unset https_proxy
```

参考资料：
* [Ubuntu配置Shadowsocks实现终端代理](https://www.meirenji.info/2017/12/09/Ubuntu%E9%85%8D%E7%BD%AEShadowsocks%E5%AE%9E%E7%8E%B0%E7%BB%88%E7%AB%AF%E4%BB%A3%E7%90%86/)
* [为终端设置Shadowsocks代理](https://droidyue.com/blog/2016/04/04/set-shadowsocks-proxy-for-terminal/)