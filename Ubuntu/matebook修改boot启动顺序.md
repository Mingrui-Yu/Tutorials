# matebook14 修改boot启动顺序
在终端中输入：
```
sudo efibootmgr
```
可以看到当前的启动项和启动顺序

修改启动顺序：
```
efibootmgr -o X,Y   # 指定标号为X的启动项顺序在Y之前，注意要包括所有启动项
```
