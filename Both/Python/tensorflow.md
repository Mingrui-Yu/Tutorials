# import tensorflow as tf

推荐参考教程：

[简单粗暴 TensorFlow 2.0 | A Concise Handbook of TensorFlow 2.0](https://tf.wiki/index.html#tensorflow-2-0-a-concise-handbook-of-tensorflow-2-0)

[TensorFlow官方教程](https://tensorflow.google.cn/tutorials/)

tf 2.0 API:

[TensorFlow 2.0 API](https://tensorflow.google.cn/api_docs/python/tf)

## 构建模型总体流程：
```
model = tf.keras.Sequential()  # keras建立一个网络
model.add(hub_layer)  # 添加一个预训练层
model.add(tf.keras.layers.Dense(nodes_num, activation=''))  # 添加层
model.add(tf.keras.layers.Dense(nodes_num, activation=''))

model.summary()  # 输出模型概览

model.compile(optimizer='', loss='', metrics=[''])  # 模型优化器

train_history = model.fit(train_data, train_label, epochs=epoch_num, validation_split= , verbose=0)  # 喂数据，训练

test_loss, test_acc = model.evaluate(test_data, test_label, verbose=2)  # 用test set评估

test_prediction = model.predict(test_data)  # 用训练好的模型进行预测
```

## 添加layer
```
model.add()
```

### 不同类的layer
讲数据集展开成一个一个数据的层：
```
tf.keras.layers.Flatten(input_shape=(28, 28))
```

全连接层：
```
tf.keras.layers.Dense(nodes_num, activation='relu')
```

Dropout层：
```
tf.keras.layers.Dropout(0.2)
```

### regularization
```
kernel_regularizer=keras.regularizers.l2(0.001)
```

### activation function
```
activation = 'relu'
activation = 'sigmoid'
activation = 'softmax'
```


## model.compile()
```
model.compile(optimizer='', loss='', metrics=[''])
```
### optimizer 优化方法
```
optimizer = tf.keras.optimizers.RMSprop(0.001)
optimizer='adam'
```

### loss
```
loss = 'mse'
loss = 'binary_crossentropy'
```

### metrics 度量指标
```
metrics = ['mae', 'mse']
metrics = ['accuracy', 'binary_crossentropy']
```

## model.fit()
```
history = model.fit(
  train_data, train_labels,
  epochs=EPOCHS, validation_split = 0.2, verbose=0,
  callbacks=[])
```
[绘制训练过程](https://tensorflow.google.cn/tutorials/keras/regression#%E8%AE%AD%E7%BB%83%E6%A8%A1%E5%9E%8B)

### verbose
```
verbose：日志显示
verbose = 0 为不在标准输出流输出日志信息
verbose = 1 为输出进度条记录
verbose = 2 为每个epoch输出一行记录
注意： 默认为 1
```

### validation_data
使用test set进行训练过程中的评估:
```
validation_data=(test_data, test_labels)
```

### callbacks
#### 可以在每个完成的时期执行一次自定义函数
```
callbacks=[PrintDot()]

其中：
class PrintDot(keras.callbacks.Callback):
  def on_epoch_end(self, epoch, logs):
    if epoch % 100 == 0: print('')
    print('.', end='')
```
#### Early stopping 提前退出
如果经过一定数量的 epochs 后没有改进，则自动停止训练：
```
early_stop = keras.callbacks.EarlyStopping(monitor='val_loss', patience=10)

callbacks = [early_stop]
```

## model.evaluate()
```
test_loss, test_acc = model.evaluate(test_data, test_label, verbose=2)
```
注意test_acc要和model.fit(metrics=[])对应起来

## model.predict()
```
test_prediction = model.predict(test_data)
```
注意:test_prediction的格式为array



***
## ML basics with Keras
### MNIST手写数字网络搭建
[初学者的 TensorFlow 2.0 教程](https://tensorflow.google.cn/tutorials/quickstart/beginner)

* 构建一个简单的模型

### 搭建一个基础的分类网络：衣服分类 
[Basic classification: Classify images of clothing](https://tensorflow.google.cn/tutorials/keras/classification)

### 用 tf.data 加载 CSV 数据
[用 tf.data 加载 CSV 数据](https://tensorflow.google.cn/tutorials/load_data/csv)

### 文本分类
[使用 Keras 和 Tensorflow Hub 对电影评论进行文本分类](https://tensorflow.google.cn/tutorials/keras/text_classification_with_hub)

* tensorflow_hub: 提供预训练模型
* 文本嵌入 text embedding
* model.summary()  # 输出模型概览

### 回归
[Basic regression: Predict fuel efficiency](https://tensorflow.google.cn/tutorials/keras/regression)

* pandas 数据集处理 基础使用
    * csv 数据导入
    * 删除未知值所在的行
    * 拆分训练数据集和测试数据集
    * 查看总体的数据统计
    * 数据规范化
* 快速查看训练集中几对列的联合分布 (using seaborn)
* 通过为每个完成的时期打印一个点来显示训练进度
* 在 history 对象中记录训练和验证的准确性
* [可视化训练的训练进度](https://tensorflow.google.cn/tutorials/keras/regression#%E8%AE%AD%E7%BB%83%E6%A8%A1%E5%9E%8B)

* Early stopping: 如果经过一定数量的 epochs 后没有改进，则自动停止训练

### Overfit & Underfit
[Explore overfit and underfit](https://tensorflow.google.cn/tutorials/keras/overfit_and_underfit)
* [multi-hot encoding](https://tensorflow.google.cn/tutorials/keras/overfit_and_underfit#download_the_imdb_dataset)
* [loss='binary_crossentropy'](https://tensorflow.google.cn/tutorials/keras/overfit_and_underfit#demonstrate_overfitting)
* [L1/L2 regularization](https://tensorflow.google.cn/tutorials/keras/overfit_and_underfit#add_weight_regularization)
* [Dropout layer](https://tensorflow.google.cn/tutorials/keras/overfit_and_underfit#add_dropout)

### 保存和恢复模型
[保存和恢复模型](https://tensorflow.google.cn/tutorials/keras/save_and_load)
* [在训练期间保存模型权重 & 新模型加载权重](https://tensorflow.google.cn/tutorials/keras/save_and_load#%E5%9C%A8%E8%AE%AD%E7%BB%83%E6%9C%9F%E9%97%B4%E4%BF%9D%E5%AD%98%E6%A8%A1%E5%9E%8B%EF%BC%88%E4%BB%A5_checkpoints_%E5%BD%A2%E5%BC%8F%E4%BF%9D%E5%AD%98%EF%BC%89)
* [手动保存权重](https://tensorflow.google.cn/tutorials/keras/save_and_load#%E6%89%8B%E5%8A%A8%E4%BF%9D%E5%AD%98%E6%9D%83%E9%87%8D)
* [保存整个模型](https://tensorflow.google.cn/tutorials/keras/save_and_load#%E4%BF%9D%E5%AD%98%E6%95%B4%E4%B8%AA%E6%A8%A1%E5%9E%8B)

## Load and preprocess data

### CSV
[用 tf.data 加载 CSV 数据](https://tensorflow.google.cn/tutorials/load_data/csv)

### Numpy
[使用 tf.data 加载 NumPy 数据](https://tensorflow.google.cn/tutorials/load_data/numpy)
* [打乱和批次化数据集](https://tensorflow.google.cn/tutorials/load_data/numpy#%E6%89%93%E4%B9%B1%E5%92%8C%E6%89%B9%E6%AC%A1%E5%8C%96%E6%95%B0%E6%8D%AE%E9%9B%86) & [tf.data.Dataset.shuffle(buffer_size)中buffer_size的理解](https://www.jianshu.com/p/1285036e314c)

### Pandas
[使用 tf.data 加载 pandas dataframes
](https://tensorflow.google.cn/tutorials/load_data/pandas_dataframe)
* [使用 pandas 读取csv数据
](https://tensorflow.google.cn/tutorials/load_data/pandas_dataframe#%E4%BD%BF%E7%94%A8_pandas_%E8%AF%BB%E5%8F%96%E6%95%B0%E6%8D%AE)
* [将某列转换为离散数值](https://tensorflow.google.cn/tutorials/load_data/pandas_dataframe#%E4%BD%BF%E7%94%A8_pandas_%E8%AF%BB%E5%8F%96%E6%95%B0%E6%8D%AE)

### Images
[用 tf.data 加载图片](https://tensorflow.google.cn/tutorials/load_data/images)

## Estimator
[预创建的 Estimators](https://tensorflow.google.cn/tutorials/estimator/premade)

## Customization 定制化
### Tensors and operations
[Customization basics: tensors and operations](https://tensorflow.google.cn/tutorials/customization/basics)
* [Tensors的基础运算](https://tensorflow.google.cn/tutorials/customization/basics#tensors)
* [Tensor和numpy之间的转换](https://tensorflow.google.cn/tutorials/customization/basics#numpy_compatibility)
* [tf.data.Dataset API的各种使用](https://tensorflow.google.cn/tutorials/customization/basics#datasets)

### Custom layers
[Custom layers：定制自己的special模型](https://tensorflow.google.cn/tutorials/customization/custom_layers)
* [使用layer进行运算](https://tensorflow.google.cn/tutorials/customization/custom_layers#layers_common_sets_of_useful_operations)
* [定制特殊的layers](https://tensorflow.google.cn/tutorials/customization/custom_layers#implementing_custom_layers)
* [Resnet Block的建立方法](https://tensorflow.google.cn/tutorials/customization/custom_layers#models_composing_layers)
* [简单网络堆叠：使用tf.keras.Sequential](https://tensorflow.google.cn/tutorials/customization/custom_layers#models_composing_layers)

### Automatic differentiation
[Automatic differentiation and gradient tape](https://tensorflow.google.cn/tutorials/customization/autodiff)
* [求导：Gradient tapes](https://tensorflow.google.cn/tutorials/customization/autodiff#gradient_tapes)
* [高阶求导 higher-order gradients](https://tensorflow.google.cn/tutorials/customization/autodiff#higher-order_gradients)

### Custom training
[定制化训练：基础](https://tensorflow.google.cn/tutorials/customization/custom_training)

### Custom training: walkthrough 演示 (重要)
[自定义训练: 演示](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough)
* [tf.data.Dataset读取csv文件](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA_tfdatadataset)
* [tf.stack:以将特征字典重新打包为形状为 (batch_size, num_features) 的单个数组](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA_tfdatadataset)
* [不用model.fit，自定义训练过程](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E8%AE%AD%E7%BB%83%E6%A8%A1%E5%9E%8B)
* [定义损失和梯度函数](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E5%AE%9A%E4%B9%89%E6%8D%9F%E5%A4%B1%E5%92%8C%E6%A2%AF%E5%BA%A6%E5%87%BD%E6%95%B0)
* [创建优化器](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E5%88%9B%E5%BB%BA%E4%BC%98%E5%8C%96%E5%99%A8)
* [训练循环](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E8%AE%AD%E7%BB%83%E5%BE%AA%E7%8E%AF)
* [可视化损失函数随时间推移而变化的情况](https://tensorflow.google.cn/tutorials/customization/custom_training_walkthrough#%E5%8F%AF%E8%A7%86%E5%8C%96%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E9%9A%8F%E6%97%B6%E9%97%B4%E6%8E%A8%E7%A7%BB%E8%80%8C%E5%8F%98%E5%8C%96%E7%9A%84%E6%83%85%E5%86%B5)