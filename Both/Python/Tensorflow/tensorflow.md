# import tensorflow as tf

推荐参考教程：

[简单粗暴 TensorFlow 2.0 | A Concise Handbook of TensorFlow 2.0](https://tf.wiki/index.html#tensorflow-2-0-a-concise-handbook-of-tensorflow-2-0)

[TensorFlow官方教程](https://tensorflow.google.cn/tutorials/)

## 通用操作
构建模型：
```
model = tf.keras.Sequential()  # keras建立一个网络
model.add(hub_layer)  # 添加一个预训练层
model.add(tf.keras.layers.Dense(nodes_num, activation=''))  # 添加层
model.add(tf.keras.layers.Dense(nodes_num, activation=''))

model.summary()  # 输出模型概览

model.compile(optimizer='', loss='', metrics=[''])  # 模型优化器

model.fit(train_data, train_label, epochs=epoch_num)  # 喂数据，训练

test_loss, test_acc = model.evaluate(test_data, test_label, verbose=2)  # 用test set评估

test_prediction = model.predict(test_data)  # 用训练好的模型进行预测
```

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
