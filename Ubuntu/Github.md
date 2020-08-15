# Ubuntu Github

https://blog.csdn.net/m0_37592397/article/details/78664757

https://www.cnblogs.com/haoxr/p/7693927.html

https://www.runoob.com/w3cnote/git-guide.html

[ubuntu下github的使用](https://blog.csdn.net/u012411498/article/details/80675608)





## 前期配置。。。

1 在github网站上新建一个仓库

2 本地文件夹中打开终端，执行：git init

3 配置git

git add./ :添加托管文件，将目录下的所有文件添加

git commit -m "#description#"  :commit推送，“”内是commit的描述

上传文件到远程库：需要该仓库额SSH KEY，从网页上点击Clone or download，复制

git remote add origin #SSH KEY#   添加远程仓库

git remote set-url #SSH KEY#    添加文件到远程库

git push origin master 第一次进行push

***

git add

git commmit

git pull 从远程拿到最新代码版本

git push 更新远程



## 从网站上clone一个已有项目

```
git clone https://github.com//username//test_project.git 
```
修改项目后：
```
git add .   // .代表添加所有文件  
git commit -m "对文件操作的简易描述"  
git push
```



## git中submodule子模块的使用

### 在自己的项目中添加 submodule

[参考1](https://git-scm.com/book/en/v2/Git-Tools-Submodules) [参考2](https://www.activestate.com/blog/getting-git-submodule-track-branch/)

具体，如果在一个父项目中需要添加一个子项目，则在需要添加的位置：

```
git submodule add SUBMODULE_URL

# 如果需要指定 branch 则
git submodule add -b BRANCH_NAME https://github.com/XXX/XXXX
```

这会在父项目根目录创建.gitmodules，但还没有真正把submodule clone 下来。之后更新：

```
git submodule update --init
git submodule update --remote
```

### clone 别人的项目并 clone下来其中的 submodule

参考[git中submodule子模块的添加、使用和删除 | CSDN](https://blog.csdn.net/guotianqing/article/details/82391665)



## 使用socks5代理，加速git clone
[git 设置和取消代理](https://gist.github.com/laispace/666dd7b27e9116faece6)
```
git config --global http.proxy socks5h://127.0.0.1:1080

```
若要取消：
```
git config --global --unset http.proxy
```



## 使用 .gitignore 上传时忽略指定文件

https://www.liaoxuefeng.com/wiki/896043488029600

注意：在编写 .gitignore 之前就已经上传了的文件无法被之后添加的 .gitignore 管理，需要先在云端删除：

```
git rm -r --cached FILE_NAME
git commit -m "delete xxx"
git push
```



## 重命名 repo

https://help.github.com/cn/github/administering-a-repository/renaming-a-repository