# More

## copy
a = b.copy()  # 可以不用import copy

## enumerate() 同时返回数据下标和数据
enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。
```
for i, element in enumerate(seq):
    print(i, element)

OUTPUT:
0, seq[0]
1, seq[1]
......
```

## iter() next() 迭代
[python中的iter()函数与next()函数](https://blog.csdn.net/xun527/article/details/76652189)

## random

```
import random

# 生成随机整数
r = random.randint(a, b)  # [a, b] 区间内的随机整数
```

## 分离文件名和路径

```
import os

# 分离路径和文件名
file_full_path = '/home/mingrui/a.txt'
(filepath, filename_ex) = os.path.split(file_full_path)
# 分离文件名中的名字和后缀
(filename, extension) = os.path.splitext(filename_ex)
```

