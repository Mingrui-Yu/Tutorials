# import matplotlib.pyplot as plt

## 基础：显示图片
```python
# 新建一个图片
plt.figure()

# 添加图片内容
......

# 显示图片 (图片窗口弹出后，不关闭窗口，程序不会继续运行)
plt.show()
```

## color表

https://finthon.com/matplotlib-color-list/

## 折线图 & 设置曲线label

```
plt.plot(x_data, y_data, '--', label='LABELNAME')

plt.legend(loc="upper right") ＃ 显示曲线label, loc="upper right"表示label显示在右上角
```
线型：
```
'--': 虚线
```

## 散点图
```
plt.scatter(x_data, y_data)
```

## 显示image
```
plt.grid(False)
plt.xticks([])
plt.yticks([])

plt.imshow(img, cmap=plt.cm.binary)
```



## 设置图片label:内容 & 颜色
```
plt.xlabel("{} {:2.0f}% ({})".format(class_names[predicted_label],
                            100*np.max(predictions_array),
                            class_names[true_label]),
                            color=color)
```
## 设置坐标轴范围
```
plt.xlim([min, max])
plt.ylim([min, max])
```


## 同时显示多张图片(subplot)
```
plt.figure(figsize=(10,10))
for i in range(25):
    plt.subplot(5,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(train_images[i], cmap=plt.cm.binary)
    plt.xlabel(class_names[train_labels[i]])
plt.show()
```

## 画直方图 & 设置直方图颜色
```
plt.grid(False)
plt.xticks(range(10))
plt.yticks([])

thisplot = plt.bar(range(10), predictions_array, color="#777777")
plt.ylim([0, 1])

predicted_label = np.argmax(predictions_array)

thisplot[predicted_label].set_color('red')
thisplot[true_label].set_color('blue')
```

## 频率统计图
```
plt.hist(data, bins=)
```
* bins为直方图的柱数

## 绘制 x y z 轴比例相同的 三维图

```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

def set_aspect_equal_3d(ax):
    """Fix equal aspect bug for 3D plots."""

    xlim = ax.get_xlim3d()
    ylim = ax.get_ylim3d()
    zlim = ax.get_zlim3d()

    from numpy import mean
    xmean = mean(xlim)
    ymean = mean(ylim)
    zmean = mean(zlim)

    plot_radius = max([abs(lim - mean_)
                       for lims, mean_ in ((xlim, xmean),
                                           (ylim, ymean),
                                           (zlim, zmean))
                       for lim in lims])

    ax.set_xlim3d([xmean - plot_radius, xmean + plot_radius])
    ax.set_ylim3d([ymean - plot_radius, ymean + plot_radius])
    ax.set_zlim3d([zmean - plot_radius, zmean + plot_radius])
    
# 使用：
fig = plt.figure()
ax = fig.gca(projection='3d')
ax.plot(x, y, z)
set_aspect_equal_3d(ax)
plt.show()
```

