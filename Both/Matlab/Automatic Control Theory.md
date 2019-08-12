# 传递函数
简单模型：
```
num=[1,10]；
den=[1,5,4,3,2];
G=tf(num,den)
```

零极点模型：
```
KGain=K;  %系统增益K
Z=[1; 2; 3]； %零点
P=[4; 5; 6];  %极点
G=zpk(Z,P,KGain)
```

# 根轨迹
## 绘制根轨迹
```
num = conv([1 1], [1,3]); % 分子系数数组，因子相乘形式
den = [1 0 0 0]; % 分母系数数组

rlocus(num,den); % 绘制根轨迹
```
使用tf函数
```
h = tf(num, den);
rlocus(h); % 绘制根轨迹
``` 



# 伯德图
```
num = [2000 2000];
den = conv([1 0.5 0], [1 14 400]);
bode(num, den)
grid
```
如果希望绘制频率范围从0.1rad/s到100rad/s的伯德图：
```
num = [2000 2000];
den = conv([1 0.5 0], [1 14 400]);
w = logspace(-1,2,100)
bode(num, den, w)
grid
```

# 极坐标图
```
num = [0 20 20 10];
den = conv([1 1 0], [1 10]);
nyquist(num, den)
```
只绘制w>0部分：
```
num = [0 20 20 10];
den = conv([1 1 0], [1 10]);
[re, im] = nyquist(num, den);
plot(re, im)
axis ([-2 3 -3 1])
grid
```

## 绘制具有延迟环节的系统频率特性
![](https://latex.codecogs.com/gif.latex?G_k%28s%29%20%3D%20%5Cfrac%7Be%5E%7B-%5Ctau%20s%7D%7D%7Bs%28s&plus;1%29%28s&plus;2%29%29%29%7D)
