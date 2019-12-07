# Ubuntu VScode 相关

## ubuntu vscode上使用cmake、编译、调试
安装VScode插件：
* c++
* cmake
* cmake-tool

编写代码

编写CMakeFileLists.txt

![2019-11-03 09-21-13 的屏幕截图.png](https://i.loli.net/2019/11/03/P4DIYXcMxoHNuA6.png)

上图下方蓝条：点击build

选择GCC6.5.0

然后编写launch.json文件:　
    
    按F5，选择default，生成lauch.json文件后将其中的"program"的内容改为："${workspaceFolder}/build/待执行文件的名字"

都搞定之后按F5，就可以直接执行程序了。

如果想添加task文件自动cmake，可参考[vscode + cmake + cpp 多文件编译、断点调试](https://blog.csdn.net/zhulinmanbu114/article/details/90754803)

### VScode中的图床插件：PicGo

[PicGo](https://marketplace.visualstudio.com/items?itemName=Spades.vs-picgo)，用vscode编辑markdown时，可以安装这个插件，从而很方便地上传并插入图像。

操作|快捷键
---|---
Uploading an image from clipboard | Ctrl + Alt + U 
Uploading images from explorer | Ctrl + Alt + E
Uploading an image from input box | Ctrl + Alt + O
