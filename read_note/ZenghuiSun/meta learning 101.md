# Meta learning

## 定义以及分类

[One-shot Learning with Memory-Augmented Neural Networks ](https://arxiv.org/pdf/1605.06065.pdf)

> meta-learning generally refers to a scenario in which an agent learns at two levels, each associated with different time scales. Rapid learning occurs within a task, for example, when learning to accurately classify within a particular dataset. This learning is guided by knowledge accrued more gradually across tasks, which captures the way in which task structure varies across target domains. Given its two-tiered organization, this form of meta learning is often described as “learning to learn.” 



[wiki of meta learning](https://en.wikipedia.org/wiki/Meta_learning_(computer_science))

> **Meta learning** is a subfield of [Machine learning](https://en.wikipedia.org/wiki/Machine_learning) where automatic learning algorithms are applied on [meta-data](https://en.wikipedia.org/wiki/Meta-data) about machine learning experiments. Although different researchers hold different views as to what the term exactly means (see below), the **main goal** is to *use such meta-data to understand how automatic learning can become flexible in solving different kinds of learning problems*, hence to improve the performance of existing [learning algorithms](https://en.wikipedia.org/wiki/Learning_algorithms).
>
> Flexibility is very important because each learning algorithm is based on a set of assumptions about the data, its [inductive bias](https://en.wikipedia.org/wiki/Inductive_bias). This means that **it will only learn well if the bias matches the data in the learning problem**. A learning algorithm may perform very well on one learning problem, but very badly on the next. From a non-expert point of view, this poses strong restrictions on the use of [machine learning](https://en.wikipedia.org/wiki/Machine_learning) or [data mining](https://en.wikipedia.org/wiki/Data_mining) techniques, since the relationship between the learning problem (often some kind of [database](https://en.wikipedia.org/wiki/Database)) and the effectiveness of different learning algorithms is not yet understood.
>
> By using different kinds of meta-data, like properties of the learning problem, algorithm properties (like performance measures), or patterns previously derived from the data, **it is possible to select, alter or combine different learning algorithms to effectively solve a given learning problem.** Critiques of meta learning approaches bear a strong resemblance to the critique of [metaheuristic](https://en.wikipedia.org/wiki/Metaheuristic), which can be said to be a related problem.

## meta learning 分类

### [知乎问答](https://www.zhihu.com/question/41979241)

> Dynamic learning. 标志作品是AlphaGo，或者也称reinforcement learning， 能通过非暴力的方法对一些非常复杂的且定义模糊的任务有着全局观的理解，以此来take action 最大化获得reward。这块我并特别熟悉所以不详细解释来误导大众了。相关文章：[Human-level control through deep reinforcement learning : Nature : Nature Research**](https://link.zhihu.com/?target=http%3A//www.nature.com/nature/journal/v518/n7540/abs/nature14236.html) ， [http://www.nature.com/nature/journal/v529/n7587/full/nature16961.html**](https://link.zhihu.com/?target=http%3A//www.nature.com/nature/journal/v529/n7587/full/nature16961.html) 
>
> Transfer learning / progressive (continual) learning. 就如刚才所说的，现在所有的deep learning模型都是learn from scratch 而并不像人类一样，可以很快速的上手一些类似的游戏，或者永远不会忘掉骑自行车那样的特征。所以一定程度的share parameter是非常必要的，不仅加速模型的训练还可以节省内存避免对已有类似的问题重复学习。
>
> One/zero-shot learning. 现在在vision领域里，基本上所有的recognition和classification task都需要大量的数据集。而事实上，人类并不是通过这样的方式去认识一个新事物。比如说，当人类看到一个恐龙的图片，之后给的恐龙多么古怪，毛发，颜色，特征都不一样，但是人类依然可以相当轻松的知道这是恐龙。或者说， 通过已学到的特征，我们通过文字描述，这是一只白色的毛茸茸的兔子，我们自己脑子里就可以大致想象出他的样子。所以在recognition和classification task里还有很大的提升空间。相关文章：[http://vision.stanford.edu/documents/Fei-FeiFergusPerona2006.pdf**](https://link.zhihu.com/?target=http%3A//vision.stanford.edu/documents/Fei-FeiFergusPerona2006.pdf), [https://arxiv.org/pdf/1605.06065v1.pdf**](https://link.zhihu.com/?target=https%3A//arxiv.org/pdf/1605.06065v1.pdf)
>
> Generative learning. 或者俗称举一反三。现在已有的作品：Variational autoencoder (VAE)，generative adversarial network (GAN) 通过将probabilistic graphical model与Bayesian stat和deep learning相结合，把所有数据看做一个概率分布，而deep learning是用来学习概率分布的参数，最后通过sample分布在得到一个类似数据集里的数据但并不完全相等的新数据。同样是DeepMind，最近发布的WaveNet就是通过generative model来学习人声，demo可见：[https://deepmind.com/blog/wavenet-generative-model-raw-audio/**](https://link.zhihu.com/?target=https%3A//deepmind.com/blog/wavenet-generative-model-raw-audio/).
>
> Hierarchical learning. (?) 这块纯粹想象，并没有任何paper出现。大致想法是希望model能跟人类一样从1+1=2 慢慢学会微积分。从而真正达到强人工智能。



# Transfer learning

## motivation

Transfer Learning的初衷是**节省人工标注样本**的时间，让模型可以通过**已有的标记数据（source domain data）向未标记数据（target domain data）迁移**。从而训练出适用于target domain的模型。我在某篇论文当中引用了一些图片来帮助大家更好的理解：

![](https://pic1.zhimg.com/50/v2-e92213c12444fc75ec3e9f5514e1ac28_hd.png)



上图是某行人检测任务数据集当中的4张图片，假设前两张正对着摄像机的行人作为训练集，后两张背对着的行人图片作为测试集，结果该模型的测试评分会很差，因为训练时没有考虑到摄像机观察角引起的问题，相类似在图像识别领域会有很多因素会降低识别率（例如光照，背景等）。ok，那能否用一些未标记的图片（类似图3，4这样的图），增强我们的行人检测模型，让它不仅可以识别正对着的行人，还可以识别背对着的行人？这就是迁移学习要干的事。

既然说到这个问题，就不得不提**domain adaptation**了，domain adaptation是迁移学习原先就有的概念，在研究source domain和target domain时，基于某一特征，会发现两个domain的数据分布差别很大，比如说选择某一区域的颜色信息作为图像特征，下图红线表示source dataset的颜色信息值分布，蓝线表示target dataset的颜色信息值分布，很明显对于这一特征来讲，两个域的数据本来就是有shift的。而这个shift导致我们evaluate这个模型的时候准确率会大大降低。

![](https://pic1.zhimg.com/50/v2-8da69cb2647edf0ce726fa5391837e78_hd.png)

既然这个特征不合适，那我们就换特征，没错，domain adaptation旨在利用各种的feature transformation手段，学习一个域间不变的特征表达，基于这一特征，我们就可以更好的同时对两个域的数据进行分类了。



# 各个领域的前景

![img](https://pic4.zhimg.com/50/v2-ea506047eafc7d53d653cd9828f8f24f_hd.png)



![](https://pic1.zhimg.com/50/v2-c005d3cff8100bb69c41ac4c04a28fe8_hd.png)