

# DBoW

Bag of Words (BoW)，词袋模型。应该是说目前主流 SLAM 系统中应用最广泛且效果一流的回环检测方法。考虑到在完整的回环闭合模块中，回环检测之后还要进行回环校正，BoW 方法可以是目前最适合 SLAM 系统回环检测的方法了。

BoW 方法的原理可以概括为：系统会预先加载一个很大的字典，图像的每一个特征点的描述子可以转换为字典中的一个单词 (word)。图像的每个特征点对应一个 word，我们以一幅图像中是否出现过某个 word 以及出现次数，来对该图像统计一个词袋向量 (bag-of-words vector)，作为整幅图像的描述向量。两张图像的 bag-of-words vector 之间的距离就描述了两张图像的差异，从而可以计算出图像之间的相似度，进而进行图像匹配，找到可能的回环关键帧 (Candiate Loop KF)。

目前，基于 BoW 回环检测的主流 SLAM 系统包括：
* ORB-SLAM
* VINS-Mono
* LDSO (DSO with Loop closing)

提出将 BoW 方法应用于 SLAM 系统回环检测的论文很多，最经典论文应该是12年发表在 TRO 上的 [Bags of Binary Words for Fast Place Recognition in Image Sequences](https://ieeexplore.ieee.org/abstract/document/6202705)，论文的作者 Dorian 也是 [DBoW](https://github.com/dorian3d/DBow) 和 [DBoW2](https://github.com/dorian3d/DBoW2) GitHub 开源库的作者。

## BoW 原理

我们以 [Bags of Binary Words for Fast Place Recognition in Image Sequences](https://ieeexplore.ieee.org/abstract/document/6202705) 论文为参考，来分模块地介绍基于 BoW 的 SLAM 回环检测是如何实现的。

### 特征点描述

理论上，BoW 方法对图像的特征点类型和描述子类型并没有要求，只要描述子之间能进行距离描述就可以。

论文中，作者以 FAST 特征点 + BRIEF 描述子的搭配来进行特征点的提取和描述，这样形成的描述子是一个二进制的向量（这是 BRIEF 描述子带来的）。现在最常用的大概是 ORB 特征及 ORB 描述子（当然 ORB 是基于 FAST + BRIEF 改造而来）。

采用 BRIEF 描述子最大好处在于：因为其是二进制的向量，所以两个描述子之间计算距离非常迅速。二进制向量间的距离采用 Hamming 距离（两个向量某位不同的位数）描述，该距离可以直接通过异或运算求得。

### 构建图像数据集 & 词典

<div align=center><img src="../pics/BoW_vocabulary_tree.png" width = "80%" /></div>

上图展示了图像数据集和词典的示意图，其采用了几种方法（结构）来提高计算速度。

#### vocabulary tree

词典由一个 vocabulary tree 构成，该树的每个叶节点代表一个 word，其构建构成如下：
1. 从一个离线的很大的图像数据集中，提取很多很多很多特征点和相应的描述子
2. 对这些描述子聚类成 $k_w$ 个类（使用 k-means++ 聚类法），这 $k_w$ 个类就是 vocabulary tree 的根节点下一层的 $k_w$ 个节点。
3. 每一个类，再进行同样的聚类。每个类再细分出  $k_w$ 个子类
4. 以此类推，共进行 $L_w$ 次
5. 得到最终的 vocabulary tree，每个叶节点代表一个 word


这样最终，就形成了如图所示的一个树，该树有 $k_w + 1$ 层，共有 $k_w^{L_w}$ 个叶节点，也就是总共存储了 $k_w^{L_w}$ 个 words。采用树的结构的原因是：因为 word 会特别特别多，在寻找某特征对应的 word 时，如果是线性查询，则时间复杂度为 $O(n)$。若用这种树结构，则只需 $O(\log_{k_m}n)$。

另外，为了更好地计算图像相似度，所以给每个 word 赋予一个不同的权重。例如如果一个 word 特别经常出现，在每个图像中都出现，那么它对于计算相似度的贡献就很小，应该给一个很小的权重。权重的具体计算方法为 TF-IDF (Term Frequency-Inverse Document Frequency) ([参考文献](https://ieeexplore.ieee.org/abstract/document/1238663)): 

其中 IDF 部分（某word 在字典中出现的频率越低，则分类图像时区分度越高）：

$$\mathrm{IDF}_{i}=\log \frac{n}{n_{i}}$$

其中 $n$ 为数据集的总特征数量，$n_i$ 为 word $w_i$ 对应的特征的数量。

TF 部分（某 word 在一个图像中经常出现，它的区分度就高）：

$$\mathrm{TF}_{i}=\frac{n_{i}}{n}$$

其中 $n_i$ 为该图像中 word $w_i$ 出现的次数， $n$ 为该图像一共出现的 word 次数（等于特征点数）

而一个 word $w_i$ 在某图片中的权重 $\eta_{i}$ 即为：

$$\eta_{i}=\mathrm{TF}_{i} \times \mathrm{IDF}_{i}$$

所以一张图像 $I_t$ 的 bag-of-words vector $v_t$ 为：

$$\boldsymbol{v}_t = \left\{\eta_{1}, \eta_{2}, ... ,  \eta_{N}\right\}$$ 

其中 $N$ 为词典中的所有 word 类数。

计算两张图像的 bag-of-words vector 的距离的方法可以使用 $L_1$ 范数形式：

$$ s\left(\mathbf{v}_{1}, \mathbf{v}_{2}\right)=1-\frac{1}{2}\left|\frac{\mathbf{v}_{1}}{\left|\mathbf{v}_{1}\right|}-\frac{\mathbf{v}_{2}}{\left|\mathbf{v}_{2}\right|}\right| $$










