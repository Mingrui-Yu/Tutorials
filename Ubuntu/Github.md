# Ubuntu下进行Github环境配置

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
git push -u origin master 
```



