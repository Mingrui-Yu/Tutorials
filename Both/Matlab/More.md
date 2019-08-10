# inline() 构造函数
构造函数x^2:
```
h = inline('x^2');
```
计算x=2时h的值：
```
h(2)
```

# factor() 因式分解
```
syms a;
f = a^2 + a;
factor(f)
```

# collect() 合并同类项
```
syms a;
f = a^2 + a^2;
collect(f)
```
