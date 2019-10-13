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
