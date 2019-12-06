# Ubuntu18.04 pppoe 拨号上网

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