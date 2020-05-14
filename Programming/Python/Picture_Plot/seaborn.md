# import seaborn as sns

## 快速绘制数据集中几对列的联合分布
```
sns.pairplot(dataset[["MPG", "Cylinders", "Displacement", "Weight"]], diag_kind="kde")
# dataset格式为pandas
```

## 绘制多次实验的平均值

![](https://pic4.zhimg.com/80/v2-52a9c2b8f9a652e08c851e4a327c9857_720w.jpg)

[参考](https://zhuanlan.zhihu.com/p/75477750)

```python
sns.tsplot(time=time, data=x1, color="r", condition="LABEL_NAME")
# x1 (numpy)  每一行是一次实验的序列，多次试验的行堆叠起来行车x1矩阵
```

## 对数据进行移动平均

```python
# sm 是移动平均的窗大小、d是需要移动平均的数据
y = np.ones(sm)*1.0/sm
d = np.convolve(y, d, "same")
```

