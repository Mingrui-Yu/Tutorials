# 经典控制理论
## 控制系统微分方程的数值解
Matlab提供了一个采用龙格库塔法求解微分方程数值解的函数ode113()，具有很高的计算精度：
```
[t, y] = ode113('F', tspan, y0, options)
% t是时间向量；
% y是与t相互对应的方程的数值解；
% 'F'是对于系统微分方程的描述，一般由用户编写特定的odefile()函数；
% tspan是1*2的向量，表示计算开始和结束的时间；
% y0是微分方程的初始条件；
% options是控制精度的可选参数，由odese()函数来设置，常用的参数值有'RelTol'(表示1e-3精度)，'AbsTol'(表示1e-6精度)。
```
odefile()函数的功能是描述系统的微分方程和一些相关参数，提供ode113()的接口：
```
function F = odefile(t, y)
```
注意：ode113()函数只接受一阶微分方程的形式，因此对于高阶微分方程，首先要化为若干个一阶微分方程，然后再使用odefile()函数。


eg：
设系统的微分运动方程为：![](https://latex.codecogs.com/png.latex?%5Cinline%20M%20%5Cfrac%7B%5Cmathrm%7Bd%7D%5E2%20x%28t%29%7D%7B%5Cmathrm%7Bd%7D%20t%7D%20&plus;%20B%5Cfrac%7B%5Cmathrm%7Bd%7D%20x%28t%29%7D%7B%5Cmathrm%7Bd%7D%20t%7D&plus;Kx%28t%29%20%3Df%28t%29)


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
## 设计状态反馈和状态观测器
### 设计状态反馈
求解极点配置的反馈增益矩阵：
```
K = acker(A, B, p)  
% A为系统矩阵，B为输入矩阵，p是由期望的闭环极点组成的行向量
% 仅适用于SISO系统的极点配置，期望的闭环极点中可以包含多重极点
```
```
K = place(A, B, p)
% 既适用于SISO系统的极点配置，也适用于MIMO系统的极点配置，但要求在期望的闭环极点中，极点的重数不大于矩阵B的秩。所以在SISO系统的极点配置中使用place()不能包含重极点
```

### 设计状态观测器
观测器的设计与状态反馈的极点配置具有对偶性，所以可以直接求解其对偶系统的状态反馈矩阵K，然后将其转置，得到观测器的增益矩阵G：
```
K = acker(A.T, C.T, p) or K = place(A.T, C.T, p)
G = K.T
```