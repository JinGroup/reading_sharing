# IRGAN: A Minimax Game for Unifying Generative and Discriminative Information Retrieval Models 

## 总结和亮点

- 不同于之前的GAN的思路进行类似图像生成、超分辨率之类的任务，这一篇文章拓展了思路进行IR任务的文档生成。相当于是应用minimax的思路解决传统问题，这个方向是我们可以尝试的。
- 文章中巧妙地应用上了IR任务的两个思路，生成模型和判别模型，将其与GAN的G、D相对应。除此之外就是引入了强化学习的policy gradient来进行G的训练。



## Abstract

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709281124_974.png" width="500">

## Method

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709281125_577.png" width="500">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709281126_337.png" width="500">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709281126_971.png" width="500">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709281127_536.png" width="500">


  - > 为了进一步解释这个过程，让我们用水中的肥皂打个比方，如图1 所示。在未观察到的 positive 肥皂与观察到的 positive 肥皂之间存在着潜在的连接线（即正相关性），观察到的 positive 肥皂永久漂浮在水面（即判别器的判定边界）上。判别器起着将浮在水面上的未观察到的肥皂敲下水面的作用，而生成器充当选择性地将肥皂浮上水面的水。即使生成器不能完全适应条件数据分布，也仍然可能存在动态平衡，这是在水的不同深度下，positive 和 negative 的未观察肥皂的分布取得稳定时获得的。由于未观察到的 positive 肥皂与水面上的观察到的 positive 肥皂相连接。因此总体而言，它们最后应该能够达到比（未观察到的）negative 肥皂更高的位置。