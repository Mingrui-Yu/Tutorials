# Ubuntu下进行Github环境配置

https://blog.csdn.net/m0_37592397/article/details/78664757

https://www.cnblogs.com/haoxr/p/7693927.html

https://www.runoob.com/w3cnote/git-guide.html


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

# Markdown
## 公式
GitHub Flavored Markdown 曾经是支持 LaTeX 的，但是现在不支持了……因此若想在 README 或者评论中插入数学公式，就得使用另外的方式。

CodeCogs 提供了一个[在线 LaTeX 编辑器](https://www.codecogs.com/latex/eqneditor.php)，可以将输入的数学公式转换为图片，并自动生成 HTML 代码（也支持其他格式）。

