# Ubuntu 终端常用命令

```
# 列出当前目录下所有文件
ls

# 删除文件夹
sudo rm- r FOLDER_NAME

# 删除文件
sudo rm -f FILE_NAME


```

## 压缩/解压文件

```
# 解压 tar.xz 
# 分两步：
xz -d FILE_NAME.tar.xz
tar -xvf FILE_NAME.tar

# 压缩
tar -cvf FILE_NAME
xz -z FILE_NAME
```

## 下载文件

多种用法 [参考](https://www.cnblogs.com/wuheng1991/p/5332764.html)

```
wget URL
```

## 杀死进程

```
ps -aux # 查看进程

kill ID # 根据进程编号杀死进程
```

## 查看磁盘空间

```
df -hl  # 查看磁盘剩余空间
df -sh NAME  # 查看目录的大小
```

