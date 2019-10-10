# Python安装升级 & 软链接 & pip

## python 安装
ubuntu18.04自带python3.6.8

## 建立软链接
用于使python指令指向某一特定版本：


eg：python3指向python3.5:

查询python3软链接地址：
```
which python3
```
查询python3.5的目录地址：
```
which python3.5
```

创建软链接：
```
ln -s [目录地址] [软链接地址]
```
删除：
```
rm -rf [软链接地址]
```
修改：
```
ln -snf [新的目录地址][软链接地址]
```
NOTICE：

* 如果软链接指向失败，可以通过ls查看链接文件的颜色，如果颜色为浅蓝色，说明软链接有效；如果颜色为红色，说明软链接无效；可以删除软链接，重新建立软链接试试。
* 通过在软链接python3的目录里运行指令 ```ls -al python3``` 可以查看python软链接指向哪里。

## pip3
```
sudo apt-get install python3-pip
```
