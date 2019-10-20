# Latex相关

CTex下载：https://mirrors.tuna.tsinghua.edu.cn/ctex/legacy/2.9/
full版本

CTex安装：https://blog.csdn.net/sinat_41805381/article/details/80185144

Texstudio下载：https://sourceforge.net/projects/texstudio/
安装：https://www.cnblogs.com/dingruihfut/p/9690073.html

MikTex下载：https://miktex.org/download
安装在CTex的文件夹中，覆盖原来的MikTex文件夹

## 自动化学报latex模板（这就是个傻逼）

居然图片和引用的下标都是手打，我服。

[官方模板下载](http://www.aas.net.cn/UserFiles/File/aas_template.zip)

[编译中缺少picins：下载picins宏包](http://mirrors.ctan.org/macros/latex209/contrib/picins.zip)，将picins.sty文件拷贝至for chinese paper文件夹里。

## 计算机学报latex模板
[官方模板下载](http://cjc.ict.ac.cn/wltg/new/submit/LatexTemplet.zip)

### TexStudio界面中中文乱码：
选项-设置TexStudio-编辑器-默认字体编码： 选GBK。

### 使用PDFLatex进行构建
构建的构成中会出现```
Sorry, but miktex-makemf did not succeed. The log file hopefully contains ...```的错误

经试验发现，是在引用\begin{CJK*}{GBK}{xxx}的时候就会出现这个错误。

实验发现，不用管他，等着，让他一直运行，跑完整个文档后就好了。