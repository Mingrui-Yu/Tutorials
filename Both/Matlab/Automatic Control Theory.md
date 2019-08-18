# 经典控制理论
## 传递函数
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

## 根轨迹
### 绘制根轨迹
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
## 系统的频域分析
### 伯德图
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

### 极坐标图
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

### 绘制具有延迟环节的系统频率特性
#### 伯德图
![传递函数](https://latex.codecogs.com/gif.latex?G_k%28s%29%20%3D%20%5Cfrac%7Be%5E%7B-%20s%7D%7D%7Bs%28s&plus;1%29%28s&plus;2%29%29%29%7D)
```
num = [1];
den = conv([1 1 0], [1 2]);
w = logspace(-2, 1, 100);
[mag, phase, w] = bode(num, den, w); % 计算频率特性的幅值和相角

%利用相频特性求加上延迟环节后的相频特性
phase = phase - w*57.3

%绘制幅频特性
subplot(211),semilogx(w, 20*log10(mag)); 
v = [0.01, 10, -60, 40]; axis(v);
grid

%绘制相频特性
subplot(212),semilogx(w, phase);
axis([0.01 10 -270 -90])
grid
```
#### 极坐标图
```
num = [1];
den = conv([1 1 0], [1 2]);
w = logspace(-2, 1, 100);
[mag, phase, w] = bode(num, den, w); % 计算频率特性的幅值和相角

%利用相频特性求加上延迟环节后的相频特性
phase = phase - w*57.3

%用极坐标曲线绘制函数画出Nyquist图
polar(phase*pi/180, mag)
axis([-2.5 1 -2 1])
grid
```

### 求系统的稳定裕度
```
num = [2000 2000];
den = conv([1 0.5 0], [1 14 400]);
margin(num,den) %画伯德图并计算幅值裕度和相位裕度
```

# 现代控制理论
## 建立系统模型
将传递函数转换为状态空间表达式：
```
[A, B, C, D] = tf2ss(num, den)  % 分子多项式和分母多项式的系数
[A, B, C, D] = zp2ss(z, p, k)  % 系统的零点、极点、增益
[A, B, C, D] = ssdata(sys)  % sys为系统的传递函数表达式
```

由状态空间表达式求解传递函数：
```
[num, den] = ss2tf(A, B, C, D)
[z, p, k] = ss2zp(A, B, C, D)
```
## 系统的时间响应
计算给定时刻的状态转移矩阵：
```
phi = expm(A*t)  % t为求取相应时间的时刻，phi为t时刻的矩阵指数函数
```
计算系统的状态响应和输出响应：
```
[y, x] = lsim(A, B, C, D, u, t, x0)  
% y为t0~t时刻的输出响应，x为t0~t时刻的状态响应，u为t0~t时刻的系统输入，t为t0~t时刻的时间向量，x0为系统初始状态
```

## 能控性能观性
求取系统的能控性判别矩阵Qc；
```
Qc = ctrb(A, B)  % A为系统矩阵，B为输入矩阵
raQc = rank(Qc)  % 判断Qc是否满秩
```
求取系统的能观性判别矩阵Qo:
```
Qo = obsv(A, C)  % A为系统矩阵，C为输出矩阵
```
