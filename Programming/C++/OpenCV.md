# OpenCV C++ 相关

[OpenCV Tutorials](https://docs.opencv.org/master/d9/df8/tutorial_root.html)

## 头文件
```
#include <opencv2/core.hpp>  // 核心功能，包括基本数据结构
#include <opencv2/opencv.hpp>
#include <opencv2/highgui.hpp>  // 高层GUI图像交互
#include <opencv2/features2d.hpp>  // 特征提取、描述、匹配
#include "opencv2/xfeatures2d.hpp"  // 特征提取、描述、匹配
```


## 读取图像
```
Mat img = imread("file_name", 0); //　读取灰度图像，8位深度，1通道，数据类型uchar
Mat img = imread("file_name", -1); //　读取原始图像，原通道，数据类型根据原始图像的类型来
Mat img = imread("file_name", 1); //　读取彩色图像，8位深度，3通道
```

* IMREAD_UNCHANGED (<0) loads the image as is (including the alpha channel if present)
* IMREAD_GRAYSCALE ( 0) loads the image as an intensity one
* IMREAD_COLOR (>0) loads the image in the RGB format


参考：  
flag=-1，8位深度，原通道  
flag=0，8位深度，1通道  
flag=1,   8位深度  ，3通道  
flag=2，原深度，1通道  
flag=3,  原深度，3通道  
flag=4，8位深度 ，3通道  

参考：[OpenCV之通道和位深的理解（CV_8UC1,CV_8SC1,CV_32FC1）](https://blog.csdn.net/u011028345/article/details/75415914)



## 新建图像
```
Mat img(height, width, CV_64F); // CV_64F: 64位浮点类型
```

## 展示图像
```
cv::imshow("img_name", img);
cv::waitKey(0);
```

## 写入图像
```
cv::imwrite("file_name", img);
// 如果img是double格式的，则需要×255后write
cv::imwrite("file_name", img * 255);
```

## 图像的基本信息
```
image.cols
image.rows
image.channels()
image.type()  // 图像的类型

```
```
if(image.data == nullptr){}  // 用来判断是否读取到图像
```

## 使用图像中的一个像素
像素坐标(x, y)：即第y行，第x列
```
// 注意，以下所有方式中的数据类型需要和图像的数据类型对应好
//　方式１
image.ptr<double>(y)[x]
// 如果是三通道图像
image.ptr<double>(y)[x * image.channels()][c]

//　方式２：最慢
image.at<double>(y, x)
```
 双线性灰度插值：这种方式可能比上面的要快一些
```
inline float GetPixelValue(const cv::Mat &img, float x, float y) {
    // boundary check
    if (x < 0) x = 0;
    if (y < 0) y = 0;
    if (x >= img.cols) x = img.cols - 1;
    if (y >= img.rows) y = img.rows - 1;
    uchar *data = &img.data[int(y) * img.step + int(x)];
    float xx = x - floor(x);
    float yy = y - floor(y);
    return float(
        (1 - xx) * (1 - yy) * data[0] +
        xx * (1 - yy) * data[1] +
        (1 - xx) * yy * data[img.step] +
        xx * yy * data[img.step + 1]
    );
}
```

## 图像拷贝
```
image_clone = image.clone();
```

## 矩阵拼接
eg: 令T2 = [R, t]
```
Mat T2;
hconcat(R, t, T2);
```

## 判断图像是否为空（空指针）
```
if (image.data == nullptr)
```

## OpenCV随机数产生器
```
cv::RNG rng;
rng.gaussian(sigma * sigma)  // 服从(0, sigma^2)高斯分布的一个值
```