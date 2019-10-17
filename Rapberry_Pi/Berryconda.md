# Berryconda

Berryconda是适用于树莓派的conda

## Berryconda 安装
[Quick start](https://github.com/jjhelmus/berryconda#quick-start)

## conda 换国内源
直接在终端下运行修改命令即可：
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --set show_channel_urls yes
```

## conda 虚拟环境
```
conda create --name my_env_name python=3.6  # 创建名为my_env_name的虚拟环境
conda remove --name my_env_name --all  # 删除名为my_env_name的虚拟环境
```