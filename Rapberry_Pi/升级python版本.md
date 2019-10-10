# 树莓派 升级python版本

## python安装
更新树莓派系统：
```
sudo apt-get update
sudo apt-get upgrade -y
```

安装python依赖环境：
```
sudo apt-get install build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev
```

下载python版本源码并解压：
```
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
tar zxvf Python-3.6.1.tgz
cd Python-3.6.1
```
编译安装：
```
sudo ./configure --prefix=/usr/local/python3
sudo make
sudo make install
```
## 建立软链接
创建：
```
# ln -s [目录地址] [软链接地址]
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
```
删除：
```
# rm -rf [软链接地址]
```
修改：
```
# ln -snf [新的目录地址][软链接地址]


***
参考资料：

[树莓派升级(安装)Python3.6|科技爱好者博客](http://blog.lxx1.com/3214)
