# Wasserstein GAN 

## 精读

- 一开始首先阐述的是unsupervised learning的核心问题：如何学习样本概率分布。 一般度量模型学习的分布和真实分布的距离，使用KL divergence
- 但是使用DL散度度量相似性的前提是能够获取得到Model density，这个条件是比较harsh的。所以本文选择使用EM distance作为度量分布相似性的准则。
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709151038_334.png" width="600">
- EM距离：
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709151041_862.png" width="800">
  - 用来度量从一个分布转移到另外一个分布的最短”距离“(mass/ cost)。



- 近似求解
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709151057_871.png" width="800">
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709151059_165.png" width="800">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709151059_443.png" width="800">

