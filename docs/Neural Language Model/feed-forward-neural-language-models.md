# 前馈神经语言模型

---

![](../img/LM-1.png)

上图表示了一个5元的神经网络语言模型。网络中的结点代表上下文中的单词，与隐藏层连接，隐藏层连接至输出层进行单词预测。

## 词语表示

首先，我们用bit编码的方法来进行词语的表示，也就是**独热编码\(one hot encoding\)**。我们将每个词表示成一个高维向量，每一维代表词典里的一个单词，一个单词的向量表示则为该单词对应的向量元素值为1，其余位为0。例如：

* dog = $(0,0,0,1,0,0,0,0,...)^T$

* cat = $(0,0,0,0,0,0,1,0,...)^T$

* eat = $(0,1,0,0,0,0,0,0,...)^T$

因此，由于向量的维度等于词典的大小，这些向量的维度可能会非常大，一种限制词典大小的方法就是将语料中频率出现最高的一部分词加入词典（例如频率最高的前20000个词），其它词用OTHER标记代替。或者还可以通过给词语分类的方法（自动聚类或者使用词性标签）去降维。

现在重新回到我们的语言模型，为了汇集这些上文词语的信息（word1-word4） ，我们在隐藏层和输入层直接加一层，在这一层中，每一个上文的词语都被映射到了一个低维空间中。我们对每个上下文单词使用相同的权重矩阵，从而为每个单词生成连续的空间表示形式，该表示与它在条件上下文中的位置无关。这种表示方法通常叫做**word embedding**。![](../img/word_embedding.png)

## 神经网络架构



