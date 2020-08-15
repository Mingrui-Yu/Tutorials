# win10 安装使用 Endnote x9

## 安装

[参考](https://zhuanlan.zhihu.com/p/61958997)

## 使用

[Endnote 插入文献导致word崩溃！！解决方法](https://blog.csdn.net/u012236241/article/details/87910304)

[解决误识别中括号、自动搜索中括号](https://jingyan.baidu.com/article/fc07f98956c52e12fee5196a.html)

[在endnote中制作GB/T7714《文后参考文献著录规则》的输出格式](http://blog.sciencenet.cn/blog-485-448980.html)

[GB/T 7714-2015格式文件](https://cnzhx.net/blog/endnote-output-style-cnzhx/) (endnote 官网提供的不准确)

[修改Endnote插入Word参考文献中位置](https://blog.csdn.net/qq_21095607/article/details/60868392)

## 配置使用GB/T 7714-2015

具体的规则可见该标准的[pdf](http://www.ggzzchina.com/Upload/2016-02/20160223155134487.pdf)

Style 文件下载：[GB/T 7714-2015格式文件](https://cnzhx.net/blog/endnote-output-style-cnzhx/)

word中无法正常导入该Sytle：上述网址中也有响应的解决方案

### 参考文献的缩进不正确

具体表现为：第一行缩进了，第二行却没缩进。应该第一行不缩进，第二行与第一行的文字部分对齐。

第一步：

Word工具栏 - 开始 - 样式 - 第三个向下的箭头 - 应用样式 - 修改

“样式基准”改为无样式

第二步：

Endnote中 编辑 - 输出样式 - 编辑XXX样式 - 参考文献 - 布局

右上角 - 插入字段：制表符 （如果没有这一步，word中参考文献序号是1位数和2位数时对不齐）

右下角 - 悬挂式缩进：选择全部段落

Ctrl + s 保存

第三步：

Word工具栏 - EndNote - Bibliography - 右下角箭头 - Layout - 左下方Hanging indent：调整为合适的值（多试试，大概0.8cm）- 确定

第四步：

Word工具栏 - 开始 - 样式 - 第三个向下的箭头 - 应用样式 - 修改

左下角-格式：根据需要调整字体、行距等等

### 修改会议的参考文献格式

需要将 [C].XXXXComference 改为 [C]// XXXXConference