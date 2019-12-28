## cmake 相关

## CMakeLists 模板
```

cmake_minimum_required(VERSION 2.8)
project(xxx)

# 添加C++11标准支持
set(CMAKE_CXX_FLAGS "-std=c++11")  

# 设置Debug模式或Release模式
set(CMAKE_BUILD_TYPE "Debug")

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)


# Eigen
include_directories("/usr/include/eigen3")

# OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIR})

# Ceres
find_package(Ceres REQUIRED)
include_directories(${CERES_INCLUDE_DIRS})


add_executable(xxx xxx.cpp)
target_link_libraries(xxx ${OpenCV_LIBS})
target_link_libraries(xxx ${CERES_LIBRARIES})

```

## find_package  相关

参考资料：[cmake教程4(find_package使用)](https://blog.csdn.net/haluoluo211/article/details/80559341)

## Debug 断点调试
CMakeLists中：
```
set(CMAKE_BUILD_TYPE "Debug")
```

不需要debug模式的话，就使用Release模式：
```
set(CMAKE_BUILD_TYPE "Release")
```
不设置，默认是debug模式。