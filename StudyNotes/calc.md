# calc

记录一下 calc 编译过程中遇到的一些问题

## TrainAndTest

其他需要 pip 的依赖：

```
pip install lmdb
pip install psutil
pip install click
```

### 编译 TrainAndTest 中的 DBoW2

报错：

```
calc/TrainAndTest_origin_backup/ThirdParty/DBoW2/build/dependencies/src/DLib/src/DUtilsCV/Drawing.cpp
error: no matching function for call to ‘_IplImage::_IplImage(cv::Mat&)’
   IplImage ipl_im = IplImage(im);
```

解决：在源代码中将 IplImage(im) 改为 cvIplImage(im)  [参考](https://github.com/davisking/dlib/commit/54a9a5bbf3267386dd39a82fb792bab1bb60796c)

报错：

```
error: ‘boost::python::numeric’ has not been declared
  boost::python::numeric::array::set_module_and_type("numpy", "ndarray");
```

解决：

boost::python::numeric 在 boost >= 1.65 中已经没有了。[参考](https://github.com/AcademySoftwareFoundation/openvdb/issues/170)

似乎将``` boost::python::numeric::array::set_module_and_type("numpy", "ndarray");```在源代码中注释掉就可以了。

