# C++ Eigen 相关

## Eigen::aligned_allocator

如果STL容器中的元素是Eigen库数据结构，例如这里定义一个vector容器，元素是Matrix4d ，如下所示：
```
vector<Eigen::Matrix4d>;
```

这个错误也是和上述一样的提示，编译不会出错，只有在运行的时候出错。解决的方法很简单，定义改成下面的方式：
```
vector<Eigen::Matrix4d,Eigen::aligned_allocator<Eigen::Matrix4d>>;
```
其实上述的这段代码才是标准的定义容器方法，只是我们一般情况下定义容器的元素都是C++中的类型，所以可以省略，这是因为在C++11标准中，aligned_allocator管理C++中的各种数据类型的内存方法是一样的，可以不需要着重写出来。但是在Eigen管理内存和C++11中的方法是不一样的，所以需要单独强调元素的内存分配和管理。