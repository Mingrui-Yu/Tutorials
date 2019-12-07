## cmake 相关

## find_package  相关

参考资料：[cmake教程4(find_package使用)](https://blog.csdn.net/haluoluo211/article/details/80559341)

## Debug 断点调试
CMakeLists中：
```
set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")
```

不需要debug模式的话，就使用Release模式：
```
set(CMAKE_BUILD_TYPE "Release")
```