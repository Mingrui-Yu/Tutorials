# Ubuntu：Anaconda & vscode & TensorFlow

## 安装Anaconda
1. 下载：
    ```
    wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.0.0-Linux-x86_64.sh
    ```
    其他版本可以到https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/自行查找。

2. 安装：
    ```
    sudo bash Anaconda3-5.0.0-Linux-x86_64.sh
    ```
    按照提示安装即可，默认将安装在~目录下，如需更改，可以自行指定。
    
最后允许将Anaconda路径添加到bashrc中。
    
    （似乎可以没有这一步）
    
```
    source ~/anaconda3/etc/profile.d/conda.sh 
    ```
    
3. 激活安装：
    ```
    source ~/.bashrc
    ```

4. 检查是否安装成功
    ```
    conda --version
    ```

### 换国内源
添加清华源：
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
#设置搜索时显示通道地址
conda config --set show_channel_urls yes

```

### 升级
```
conda update -n base -c defaults conda  # 似乎可以没有
conda upgrade --all
```

* 如果出现error：```PermissionError: [Errno 13] Permission denied: '/home/ymr/anaconda3/.condatmp'```，则(设置管理员权限)：
    ```
    sudo chown -R ymr:ymr /home/ymr/anaconda3 
    ```

* Anaconda中的pip换国内源的方式与ubuntu的pip的一样，不用重复操作。

### conda虚拟环境
[TensorFlow 安装与环境配置/Conda虚拟环境](https://tf.wiki/zh/basic/installation.html#tensorflow)

***

## 安装TensorFlow
[TensorFlow 安装与环境配置](https://tf.wiki/zh/basic/installation.html#tensorflow)

## vscode
### 切换不同python版本
IDE左下角显示python版本，点击即可切换。从中找到Anaconda中需要的虚拟环境中的python版本即可。
