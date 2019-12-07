# OpenCV C++ 相关

## 读取图像
```
Mat img = imread("file_name", 0); //　读取灰度图像，8位深度，1通道，数据类型uchar
Mat img = imread("file_name", -1); //　读取原始图像，原通道，数据类型根据原始图像的类型来
Mat img = imread("file_name", 1); //　读取彩色图像，8位深度，3通道
```
参考：  
flag=-1，8位深度，原通道  
flag=0，8位深度，1通道  
flag=1,   8位深度  ，3通道  
flag=2，原深度，1通道  
flag=3,  原深度，3通道  
flag=4，8位深度 ，3通道  



## 新建图像
```
Mat img(height, width, CV_64F); // CV_64F: 64位浮点类型
```

## 写入图像
```
cv::imwrite("file_name", img);
// 如果img是double格式的，则需要×255后write
cv::imwrite("file_name", img * 255);
```

## 使用图像中的一个像素
像素坐标(x, y)：即第y行，第x列
```
// 注意，以下所有方式中的数据类型需要和图像的数据类型对应好
//　方式１
image.ptr<double>(y)[x]

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