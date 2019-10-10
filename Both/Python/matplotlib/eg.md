# import matplotlib.pyplot as plt

## 显示图片 & 设置图片label的内容及颜色
```
plt.grid(False)
plt.xticks([])
plt.yticks([])

plt.imshow(img, cmap=plt.cm.binary)

plt.xlabel("{} {:2.0f}% ({})".format(class_names[predicted_label],
                            100*np.max(predictions_array),
                            class_names[true_label]),
                            color=color)
```



## 同时显示多张图片
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
