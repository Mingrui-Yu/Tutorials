# 给予jekyll和GitHub Pages搭建个人主页

## 使用GitHub Pages搭建个人主页
在github上建立一个repo，名为"username.github.io" (eg: Mingrui-Yu.github.io)

将此repo clone到本地。

## 使用jekyll-theme-next主题搭建个人主页
clone the repo [jekyll-theme-next on GitHub](https://github.com/Simpleyyt/jekyll-theme-next)

将里面的内容全部复制到刚才自己建立"username.github.io" repo中。

此时git push一下，就可以在https://mingrui-yu.github.io看到自己的个人主页了。

这里可以用jekyll进行本地编辑 [参考文档](http://theme-next.simpleyyt.com/getting-started.html)，但我没试成功，以后有空再试，现在先不断push，凑合着用。

## 编辑主页的内容

Next主题具有详细的[说明文档](http://theme-next.simpleyyt.com/)，其中常用的内容包括：
* 更改Scheme，我使用Pisces
* 更改菜单栏的内容，若要添加一项菜单，总共需要修改：
    * config中menu下属目录。
    * _data/languages/{language}.yml中对应的菜单项显示文本。
    * _data/languages/{language}.yml中对应的菜单项显示图标。
    * 在repo根目录下添加相应文件夹，其中写index.md文件，layout选用pages。
* 侧栏的设置
    * 社交链接
    * 个人照片：需要将个人照片放在/assets/images/目录下。同时，讲config中Sidebar Avatar下面的in directory和avatar后面都加上图片的位置(eg: /assets/images/mingrui.jpg)
* 新的文章放在_post文件夹中
    * 命名需要用'2019-11-30-name'的格式来命名，否则报错。
    * 添加categories
    * 添加tags
* 设置背景动画（取消动画）