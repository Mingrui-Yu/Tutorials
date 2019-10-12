# import tensorflow as tf

推荐参考教程：

[简单粗暴 TensorFlow 2.0 | A Concise Handbook of TensorFlow 2.0](https://tf.wiki/index.html#tensorflow-2-0-a-concise-handbook-of-tensorflow-2-0)

[TensorFlow官方教程](https://tensorflow.google.cn/tutorials/)

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




## model.compile()
```
model.compile(optimizer='', loss='', metrics=[''])
```
### optimizer 优化方法
```
optimizer = tf.keras.optimizers.RMSprop(0.001)
```

### loss
```
loss = 'mse'
```

### metrics 度量指标
```
metrics = ['mae', 'mse']
```

## model.fit()
```
history = model.fit(
  train_data, train_labels,
  epochs=EPOCHS, validation_split = 0.2, verbose=0,
  callbacks=[])
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

## 可视化模型的训练进度
```
history = model.fit(
  train_data, train_labels,
  epochs=EPOCHS)

def plot_history(history):
  hist = pd.DataFrame(history.history)
  hist['epoch'] = history.epoch

  plt.figure()
  plt.xlabel('Epoch')
  plt.ylabel('Mean Abs Error [MPG]')
  plt.plot(hist['epoch'], hist['mae'],
           label='Train Error')
  plt.plot(hist['epoch'], hist['val_mae'],
           label = 'Val Error')
  plt.ylim([0,5])
  plt.legend()

  plt.figure()
  plt.xlabel('Epoch')
  plt.ylabel('Mean Square Error [$MPG^2$]')
  plt.plot(hist['epoch'], hist['mse'],
           label='Train Error')
  plt.plot(hist['epoch'], hist['val_mse'],
           label = 'Val Error')
  plt.ylim([0,20])
  plt.legend()
  plt.show()

plot_history(history)
```







***
## MNIST手写数字网络搭建
[初学者的 TensorFlow 2.0 教程](https://tensorflow.google.cn/tutorials/quickstart/beginner)

* 构建一个简单的模型

## 搭建一个基础的分类网络：衣服分类 
[Basic classification: Classify images of clothing](https://tensorflow.google.cn/tutorials/keras/classification)

## 用 tf.data 加载 CSV 数据
[用 tf.data 加载 CSV 数据](https://tensorflow.google.cn/tutorials/load_data/csv)

## 文本分类
[使用 Keras 和 Tensorflow Hub 对电影评论进行文本分类](https://tensorflow.google.cn/tutorials/keras/text_classification_with_hub)

* tensorflow_hub: 提供预训练模型
* 文本嵌入 text embedding
* model.summary()  # 输出模型概览

## 回归
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
* 可视化训练的训练进度
* Early stopping: 如果经过一定数量的 epochs 后没有改进，则自动停止训练