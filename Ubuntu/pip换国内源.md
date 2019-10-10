# 换国内源

## pip 换国内源
注意：pip和pip3的操作方式一样。

首先在当前用户目录下建立文件夹.pip，然后在文件夹中创建pip.conf文件，再将源地址加进去即可。
```
sudo mkdir ~/.pip
sudo nano ~/.pip/pip.conf
```

然后将下面这两行复制进去就好了
```
[global]
timeout = 6000
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

***
参考资料：

[pip/pip3更换国内镜像源|CSDN](https://blog.csdn.net/zwliang98/article/details/83546788)

[pip或pip3更换源为国内源|Linux公社](https://www.linuxidc.com/Linux/2019-04/158178.htm)
