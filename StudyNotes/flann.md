# FLANN

[GitHub](https://github.com/mariusmuja/flann)

[教程 PDF](https://www.cs.ubc.ca/research/flann/uploads/FLANN/flann_manual-1.8.4.pdf)

## pyflann

[安装](https://pypi.org/project/flann/)

## 使用

Eigen matrix 转换为 flann::Matirx: [参考](https://stackoverflow.com/questions/13465890/eigenmatrixxd-to-flannmatrixdouble-conversion)

[报错 ... has no member named serialize](https://github.com/mariusmuja/flann/issues/214) : 解决：在OpenCV之前include flann

[undefined reference to LZ4 for flann 1.8.5 or later](https://github.com/mariusmuja/flann/issues/384#issuecomment-432637533) : 解决：手动在CMakeLists.txt中链接该库