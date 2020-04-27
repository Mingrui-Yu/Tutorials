## 根据 prototxt 绘制网络结构示意图

![](https://pic3.zhimg.com/80/v2-ca03df14a573bfedb17a5f89c165613a_720w.png)

## 添加 triplet loss layer

参考 [GitHub](https://github.com/jmfacil/single-view-place-recognition) 中的 models/fine_tuned/triplet_vgg16_pool4_fc_128_fine_train.prototxt 中的实现方法（使用 caffe 自带的简单层叠加实现）

## 添加 L2 normalization layer

[参考](https://groups.google.com/d/msg/caffe-users/rSuLJ_cSqUg/st875SgVAwAJ)，（使用 caffe 自带的简单层叠加实现）

## 对预训练的模型进行 net surgery

[参考](https://nbviewer.jupyter.org/github/BVLC/caffe/blob/master/examples/net_surgery.ipynb)

## 不同 layers 之间参数共享

[参考](http://caffe.berkeleyvision.org/gathered/examples/siamese.html)

## lr_mult / decay_mult

[参考]()

[How to reuse same network twice within a new network in CAFFE](https://stackoverflow.com/questions/33983627/how-to-reuse-same-network-twice-within-a-new-network-in-caffe)

## pycaffe 常用 API

[参考-Caffe-Python接口常用API](http://wentaoma.com/2016/08/10/caffe-python-common-api-reference/)