# import numpy as np

## 基础属性
```
Array = np.array([[1,2,3], [2,3,4]])
Array.ndim #维度
Array.shape #行数和列数
Array.size #元素个数

a = np.array([2, 23, 4])
a = np.array([2, 23, 4], dtype = np.int) #int64
			 dtype = np.int32 #int32
			 dtype = np.float
			 dtype = np.float32
							
							
a = np.zeros((3,4))
a = np.ones((3,4), dtype = np.int)
a = np.empty((3,4))

a = arange(10,20,2)
a = arange(12).reshape(3,4)

a = np.linspace(1,10,20)
```

## 基础运算
```
c = a + b
c = a - b

c = a*b #对应元素相乘

c = a**b #乘方

c = np.sin(a)

a = b<3 #判断，a为bool型


# 矩阵乘法
c = np.dot(a, b)
c = a.dot(b)
c = np.matmul(a, b)

np.sum(a, axis=0) # 每个行向量取均值
np.sum(a, axis=1) # 每个列向量取均值
最终的结果都为向量，如果要表达成矩阵形式，需要reshape或keepdim

np.min
np.max
np.mean(A)
np.average(A)
A.mean()
A.median()


np.cumsum(A) #累加
np.diff(A) #累差分：每一行中后一项与前一项之和
np.nonzeros(A) #将所有非零元素的行坐标放在一个矩阵中，所有纵坐标放在一个矩阵中

np.sort(A) #每个行向量中的元素从小到大排序

A.T #矩阵转置

np.clip(A, min, max) 将矩阵中的元素，小于设定最小值的令其等于最小值，大于设定最大值的令其等于最大值
```