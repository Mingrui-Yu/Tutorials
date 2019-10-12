# import pandas as pd

## 基础操作
取出数据集中的一列，并从数据集中删除此列:
```
column = dataset.pop('its_name')  
# 注意column的shape为(row_num,)。
```
添加新列：
```
dataset['new_name'] = new_column
```


## 导入csv数据集
```
raw_dataset = pd.read_csv(dataset_path, names=column_names,
                      na_values = "?", comment='\t',
                      sep=" ", skipinitialspace=True)
```

## 剔除数据中的未知值
删除带有未知值(na)的行：
```
dataset.dropna()
```
## 打印数据集的最后５行
print(dataset.tail())

## 将数据集拆分成两部分：训练数据集和测试数据集
```
train_dataset = dataset.sample(frac=0.8,random_state=0)
test_dataset = dataset.drop(train_dataset.index)
```

## 查看数据集总体的数据统计
```
train_stats = train_dataset.describe()
# train_stats的每一列是一个column的各项数据统计值
```

## 数据规范化
```
def norm(x):
  return (x - train_stats['mean']) / train_stats['std']  # 利用之前计算的总体数据统计

normed_train_data = norm(train_dataset)
normed_test_data = norm(test_dataset)
```