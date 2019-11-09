# import seaborn as sns

## 快速绘制数据集中几对列的联合分布
```
sns.pairplot(dataset[["MPG", "Cylinders", "Displacement", "Weight"]], diag_kind="kde")
# dataset格式为pandas
```