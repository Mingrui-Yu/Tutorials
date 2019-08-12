# 传递函数
简单模型：
```
num=[1,10]；
den=[1,5,4,3,2];
G=tf(num,den)
```

零极点模型：
![avatar](https://img-blog.csdnimg.cn/20190122173117994.png)
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
