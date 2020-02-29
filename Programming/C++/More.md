
# 拼接string

eg:
```
#include <string>

string path = "./data/"+to_string(i+1)+".png";
```

# std::chrono 计时
使用std::chrono，不要用ctime：
```
#include <chrono>

std::chrono::steady_clock::time_point t1 = std::chrono::steady_clock::now();

std::chrono::steady_clock::time_point t2 = std::chrono::steady_clock::now();

std::chrono::duration<double> time_used = std::chrono::duration_cast <std::chrono::duration<double>> (t2 - t1);
std::cout << time_used.count() << " second"; 
```

# 智能指针shared_ptr
```
#include <memory>
```

# size_t
size_t在32位系统和64位系统分别代表了unsigned int 与unsigned long 类型，这样的话方便代码在各类型机器中移植。

常用于循环中：
```
for (size_t i = 0; i < ...; i++)
```

# std::thread
[Multithreading in C++ | GeeksforGeeks](https://www.geeksforgeeks.org/multithreading-in-cpp/) 
* 必看，适合第一次看

[Learn C++ Multi-Threading in 5 Minutes](https://hackernoon.com/learn-c-multi-threading-in-5-minutes-8b881c92941f)
* 相对更全面
* 三种定义方法：
    * 函数指针
    * 使用 functor (Class operator)
    * lambda 函数
* 防止多线程同时对某一共享源进行操作而出错
    * 使用 std::mutex & std::unlock_guard
* 查看本机 CPU 的 core 个数

[C++ std::thread | 菜鸟教程](https://www.runoob.com/w3cnote/cpp-std-thread.html)
* 参考其中原址操作：若函数传入的是参数的reference，则调要时的参数传递要使用std::ref()


## 运行程序报错 undefined reference to 'pthread_create'
需要在 CMakeLists.txt 中对 FLAGS 进行设置，添加 -pthread
```
SET(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-std=c++11 -pthread")
```

使用 g++ 的话，同样需要在编译的时候在命令后添加 -pthread：
```
g++ xxx.cpp -pthread -std=c++11
```