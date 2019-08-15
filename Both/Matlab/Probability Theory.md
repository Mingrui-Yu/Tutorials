# 常见分布

字符 | 分布名称
----|--------
bino | 二项分布
geo | 几何分布
poiss | 泊松分布
unif | 均匀分布
exp | 指数分布
norm | 正态分布
chi2 | 卡方分布
logn | 对数正态分布
f | F分布
t | T分布

Matlab为每一种分布提供了5类命令函数：

命令|含义
---|---
pdf | 概率密度
cdf | 概率分布函数（累计概率）
inv | 逆概率分布函数
rnd | 生成相应分布的随机数
stat | 均值与方差

当需要一种分布的某一类命令函数时，只要将分布名称后缀命令函数字符并输入命令参数即可，例如：
```
binopdf(x,n,p) % 计算服从参数为n,p的二项分布的随机变量
```

# 随机数
分布名称字符+rnd，例如：
```
unifrnd(a,b) % 表示产生[a,b]上均匀分布的随机数
```
0-1上的随机数：
```
rand(m,n) % m*n维
```

# 统计命令
命令|含义
---|---
mean(x) | 样本均值
std(x) | 样本标准差
var(x) | 样本方差
conv(x,y) | 样本协方差
corrcoef(x,y) | 样本相关系数
hist(x) | 直方图
min(x) | 最小值
max(x) | 最大值
median(x) | 中位数
sort(x) | 升序排列
sum(x) | 元素求和
fix(x) | 取整部

# 计算置信区间
```
[muhat, sigmahat, muci, sigmaci] = normfit(X, a)
```
在显著性水平a下数据X的有关参数：muhat是X的均值的点估计值，sigmahat是均方差（标准差）的点估计值，muci是均值的区间估计，sigmaci是均方差的区间估计。
