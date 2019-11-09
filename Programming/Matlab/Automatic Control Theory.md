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
% options是控制精度的可选参数，由odeset()函数来设置，常用的参数值有'RelTol'(表示1e-3精度)，'AbsTol'(表示1e-6精度)。
```
odefile()函数的功能是描述系统的微分方程和一些相关参数，提供ode113()的接口：
```
function F = odefile(t, y)
```
注意：ode113()函数只接受一阶微分方程的形式，因此对于高阶微分方程，首先要化为若干个一阶微分方程，然后再使用odefile()函数。


eg：
设系统的微分运动方程为：![](https://latex.codecogs.com/png.latex?%5Cinline%20M%20%5Cfrac%7B%5Cmathrm%7Bd%7D%5E2%20x%28t%29%7D%7B%5Cmathrm%7Bd%7D%20t%7D%20&plus;%20B%5Cfrac%7B%5Cmathrm%7Bd%7D%20x%28t%29%7D%7B%5Cmathrm%7Bd%7D%20t%7D&plus;Kx%28t%29%20%3Df%28t%29)，式中，K=20，B=5，M=1，f(t)=30：

解：将二阶微分方程化为两个一阶微分方程的格式，然后求解，令：
![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cleft%5C%7B%5Cbegin%7Bmatrix%7D%20x_1%28t%29%20%3D%20x%28t%29%20%5C%5C%20x_2%28t%29%20%3D%20%5Cfrac%7B%5Cmathrm%7Bd%7D%20x%28t%29%7D%7B%5Cmathrm%7Bd%7D%20t%7D%20%5Cend%7Bmatrix%7D%5Cright.)

则有：![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cleft%5C%7B%5Cbegin%7Bmatrix%7D%20%5Cfrac%7B%5Cmathrm%7Bd%7D%20x_1%28t%29%7D%7B%5Cmathrm%7Bd%7D%20x%7D%20%3D%20x_2%28t%29%20%5C%5C%20%5Cfrac%7B%5Cmathrm%7Bd%7D%20x_2%28t%29%7D%7B%5Cmathrm%7Bd%7D%20x%7D%20%3D%20%5Cfrac%7B1%7D%7BM%7D%28f%28t%29-Bx_2%28t%29-Kx_1%28t%29%29%20%5Cend%7Bmatrix%7D%5Cright.)

根据上式编写odefile()函数：
```
function xt = F(t, x)
ft = 30; M = 1; B=5; K = 20;
xt = [x(2); 
      1/M*(ft-B*x(2)-K*x(1))];
```
仿真程序：
```
t0 = 0; tfinal = 5;
tspan = [t0, tfinal];  % 设置仿真开始和结束的时间
x0 = [0, 0]；  % 系统初始值
options = odeset('AbsTol', [1e-6;1e-6]);  % 设置仿真精度
[t, x] = ode113('F', tspan, x0, options);  % 微分方程求解
```


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

求传递函数的零点和极点：
```
[z, p, k] = tf2zp(num, den)
```
求传递函数的部分分式展开：
```
[r, p, k] = residue(num, den)
% r为部分分式展开的各分式系数，p是系统的极点，k是常数项
```
根据部分分式展开式求原传递函数表达式：
```
[num, den] = residue(r, p, k)
```

## 控制系统的时域响应
### 单位阶跃和单位脉冲响应
单位阶跃响应：
```
step(sys1, sys2, ... , t)
% sys1是传递函数描述
% 在一张图上绘制出系统sys1，sys2...的阶跃响应曲线，t是时间向量（可选）
step(sys1, 'y-', sys2, 'b--', ... , t)
% 还可以指定每个系统响应曲线的颜色线性标记等


[y, t] = step(sys1, sys2, ... , t)
% t为时间向量，根据时间t计算出响应的响应值y
```

单位脉冲响应：
```
impulse(sys1, sys2, ... , t)
[y, t] = impulse(sys1, sys2, ... , t)
```
使用方法与step()一致。

### 瞬态性能指标的计算
```
sys = tf(num, den);
t = 0:0.0005:20;

[y, t] = step(sys, t);  % 求单位阶跃响应

r1 = 1; 
while y(r1) < 1.00001
    r1 = r1+1;
end
rise_time = (r1-1) * 0.0005;  % 计算上升时间

[ymax, tp] = max(y);  % 计算最大输出量值
peak_time = (tp-1)*0.0005;  % 计算峰值时间
max_overshoot = ymax - 1;  % 计算超调量

s = 20/0.0005;
while y(s)>0.98 && y(s)<1.02
    s = s - 1;
end
settle_time = (s-1)*0.0005;  % 计算调整时间（误差带宽度取2%）
```

### 对任意输入信号的响应
绘制单输入线性时不变系统的时间相应曲线：
```
lsim(sys1, sys2, sys3, ... ,r, t)
% r为任意输入信号；t为时间向量

y = lsim(sys1, sys2, sys3, ... ,r, t)
```

### 控制系统的稳定性
直接使用 tf2zp() 或者求根函数 roots() ，求出零极点即可判断系统的稳定性。

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
K = acker(A', C', p) or K = place(A', C', p)
G = K'
```