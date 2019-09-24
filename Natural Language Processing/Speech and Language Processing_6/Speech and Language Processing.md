# Speech and Language Processing

## Introduction

相似内容的词语具有相似的含义

distributional hypothesis

- 相似内容的词语有相似的意思

- 描述词语如何分布以及其相似性
- 同义词往往发送在相同的情况下

vector semantics：

- 通过词在文本中的分布来学习词的意思

lemma：词根，词元

word sense：词义

synonyms：同义词

相同的逻辑意思：在一个句子中一个词能替换另外一个

principle of contrast：相同的词性的词会在不同的语境下出现

Antonyms：反义词

Reversives：可逆的词，类似于上升/下降

Similar words：相似的词，比如说猫和狗

处理相似的词很重要

Word relatedness

- 词于词之间的联系程度
- coffee和cup
  - 虽然没有相似性，但是经常出现在一个句子中
- 看他们的词是否属于同一类表达（semantic field）
  - 对于医院（hospital），有surgeon，nurse等

语义框架（Semantic frame）

- 通过很多个名字作为角色来描述一个事件

分类学关系（Taxonomic Relations）

- 下位词（hyponym），上位词（hypernym）
  - a是b的抽象形式
    - car is a hyponym of vehicle
  - a是b的具体形式
    - vehicle is a hypernym of car
  - superordinate,subordinate
    - vehicle是superordinate，car是subordinate
  - hyponym和hypernym包含关系
  - $\forall {\rm{x,A(x)}} \Rightarrow {\rm{B(x)}}$等价于A is a hyponym of B等价于A IS-A B

内涵（Connotations）

- 用来表示读者的观点，心情等
- 情绪（sentiment）
- 单词在其表述意义可以被三个参数具体的量化
  - valence：刺激引发的快感
  - arousal：刺激引发的情绪波动
  - dominance：刺激所激发的控制强度
- vector semantics models：将单词的含义表述成空间中的一个点

## Vector Semantics

两个经常能够相互替换的词通常具有相同的意思

包括了两个直觉

- 分布式直觉（distributionalist intuition）
  - 通过其他出现在句子中的词定义一个词语
- 向量直觉（vector intuition）
  - 将一个词语w定义为一个向量

用来表示单词的向量：embeddings

可以实现单词的相似度

tf-idf模型

- 使用了一个基线
- 单词的意思被定义为一个由临近词的计数组成的简单函数
- 在非常长的向量中是稀疏的，即包括了很多个零

word2vec模型

- 构造有语义特性的短的，密集的向量

cosine

- 使用向量计算一些参数
- 比如：语义相似度

## Words and Vector

向量，分布模型基于co-occurrence matrix

- 表示词语相互之间出现的频率

### term-document matrix

document指的是不同的训练集，可以认为是一本书中的词汇统计量

一开始被定义为vector space model的一部分

向量空间

- 一群向量

- 通过其维度特别的进行表示

向量比较

观察向量和向量之间的相似程度

### Words as Vector

word vector

- 就是行向量
- 每一行代表了同一个单词在不同书中的数量

对于document来说，相似的document就有相似的向量

相似的单词就有相似的向量

term-document matrix通过单词在document中出现的次数来表示一个词的意思

更喜欢用word-word matrix（term-context matrix）

- 这是一个$|V| \times|V|$的矩阵
- 每一个元素（i，j）代表着行单词$r_{i}$和列单词$c_{i}$在某个训练集中一起出现的次数

## Cosine for measuring similarity

用来描述两个单词之间的相似度

单词向量的大小很大程度上由其出现的频率决定

将单词向量单位化，计算两个单位向量的夹角，通过夹角即可知道这两个向量的相似程度，计算公式如（2）
$$
\operatorname{cosine}(\vec{v}, \vec{w})=\frac{\vec{v} \cdot \vec{w}}{|\vec{v}||\vec{w}|}=\frac{\sum_{i=1}^{N} v_{i} w_{i}}{\sqrt{\sum_{i=1}^{N} v_{i}^{2}} \sqrt{\sum_{i=1}^{N} w_{i}^{2}}}
$$
算出来的cos值越大，两个单词的相似度越大

## TF-IDF：Weighting terms in the vector

使用夹角计算虽然能得到相似度，但是不是很准确

有一些单词，比如说good,they,the出现频率很高，可能会使得计算不准确

对于经常出现在目标周边的单词比只出现一两次的单词重要，但是如果出现了太多次，就不那么重要（比如说he，she）

tf-idf就是解决这个问题

### tf-idf原理

首先是term frequency，就是出现在文本中的单词的次数

1. 使用对数将每一个单词的出现频率降低（出现频率和单词的相似度没有必然的关系），得到（3）式

$$
\mathrm{tf}_{t, d}=\left\{\begin{array}{ll}{1+\log _{10} \operatorname{count}(t, d)} & {\text { if } \operatorname{count}(t, d)>0} \\ {0} & {\text { otherwise }}\end{array}\right.
$$

2. 给只出现在很少的文档中的单词赋予更高的权重
   - document frequency $df_{t}$是单词t在文档中出现的数量
   - 一个单词的collection frequency是该单词在文档中出现的总的数量
   - 将一些明显分布不均匀的单词通过inverse document frequency（$\mathrm{idf}$）来赋予更高的权值
     - 使用公式$N/\mathrm{df}_{t}$对其进行赋值
       - N是在语料库中文档的总数量
       - $\mathrm{df}_{t}$是包含单词t的文档个数
     - 需要自行定义document的意思
     - 综上，公式为

$$
\mathrm{idf}_{t}=\log _{10}\left(\frac{N}{\mathrm{df}_{t}}\right)
$$

3. 综上，tf-idf算法给单词t在文档d中赋的值为

$$
w_{t, d}=\mathrm{tf}_{t, d} \times \mathrm{idf}_{t}
$$

## tf-idf的应用

在语料库中找到与单词w最相似的10个单词

1. 在同一个文档中算出所有单词对应的向量，并计算这些向量的质心，得到这个文档的向量，k个单词向量，计算公式为

$$
d=\frac{w_{1}+w_{2}+\ldots+w_{k}}{k}
$$

2. 给定两个文档，就可以算出其document vector$d_{1}$和$d_{2}$，再通过向量点乘算出cos值，从而比较相似度

## Pointwise Mutual Information（PMI）

tf-idf的一个权值函数叫PPMI（positive pointwise mutual information）

给两个单词赋值的最好方式是他们在语料库中一起出现的频率

Pointwise Mutual Information用来衡量两个事件x和y出现的频率，来查看他们是否是独立事件
$$
I(x, y)=\log _{2} \frac{P(x, y)}{P(x) P(y)}
$$
一般的，令x为目标单词，c为语料库中的单词，则有
$$
\operatorname{PMI}(w, c)=\log _{2} \frac{P(w, c)}{P(w) P(c)}
$$
PMI取值为R，负的PMI意味着这两个事件不怎么相互独立，所以除非数据很大，不然不会相互独立

如果这两个单词出现的频率过小，人类一般也无法感觉到这些词有非必然的联系，所以，如果算出了负数，我们一般都取为0
$$
\operatorname{PPMI}(w, c)=\max \left(\log _{2} \frac{P(w, c)}{P(w) P(c)}, 0\right)
$$
假定一个矩阵F有W行（单词），C列（文本），$f_{ij}$值单词$w_{i}$出现在文本$c_{j}$的次数

因此就可以算出单词和文本之间的PPMI
$$
\begin{aligned} p_{i j}=\frac{f_{i j}}{\sum_{i=1}^{W} \sum_{j=1}^{C} f_{i j}} &, p_{i *}=\frac{\sum_{j=1}^{C} f_{i j}}{\sum_{i=1}^{W} \sum_{j=1}^{C} f_{i j}}, p_{* j}=\frac{\sum_{i=1}^{W} f_{i j}}{\sum_{i=1}^{W} \sum_{j=1}^{C} f_{i j}} \\ \operatorname{PPM}_{i j} &=\max \left(\log _{2} \frac{p_{i j}}{p_{i *} p_{* j}}, 0\right) \end{aligned}
$$
一些很稀有的单词c，在计算过程中就会有很高的PMI

- 方法一：轻微的改变$P(c)$的计算，就是使用参数α来改变参数

$$
\operatorname{PPMI}_{\alpha}(w, c)=\max \left(\log _{2} \frac{P(w, c)}{P(w) P_{\alpha}(c)}, 0\right)
$$

$$
P_{\alpha}(c)=\frac{\operatorname{count}(c)^{\alpha}}{\sum_{c} \operatorname{count}(c)^{\alpha}}
$$

当α等于0.75时，就会有很好的效果

- 方法二：使用拉普拉斯平滑法，在计算PMI之前，对每一个参数都加上常数k，k的值越大，计算时非零的数就越容易被忽略

## Word2vec

使用一个方法来代表一个单词：使用短（short）和密集（大多数的值都是非零的）的向量

这一节讲的是skipgram with negative smapling（SGNS）

原本是计算单词w距离目标词汇有多近，现在是在二进制预测任务上面训练（就是回答是和不是），关心的是分类的权重作为单词的嵌入