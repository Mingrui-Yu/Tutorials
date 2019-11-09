# collect() 合并同类项
```
syms a;
f = a^2 + a^2;
collect(f)
```

# factor() 因式分解
```
syms a;
f = a^2 + a;
factor(f)
```

# inline() 构造函数
构造函数x^2:
```
h = inline('x^2');
```
计算x=2时h的值：
```
h(2)
```




# polyval() 多项式的值计算
```
y = polyval(p,x)  % 计算多项式p在x的每个点处的值。参数 p 是长度为 n+1 的向量，其元素是 n 次多项式的系数（降幂排序）
```

# polyvalm() 矩阵多项式的值计算
```
Y = polyvalm(p,X)  % 以矩阵方式返回多项式 p 的计算值
```
例如计算
![](https://latex.codecogs.com/gif.latex?p%28X%29%20%3D%20a_3X%5E3&plus;%20a_2X%5E2%20&plus;%20a_1X%20&plus;%20a_0)，则p = [a3, a2, a1, a0], X为矩阵。

# roots() 求有理多项式方程的根
```
r = roots(d)
% r为代数方程的根， d为代数方程的系数降幂排列行向量
```

# syms 定义符号变量
```
syms a b;

syms a real;  % 定义a是实数

syms a positive;  % 定义a是正数
```