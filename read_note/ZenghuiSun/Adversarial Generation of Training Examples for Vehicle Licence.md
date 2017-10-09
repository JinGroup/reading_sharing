# Adversarial Generation of Training Examples for Vehicle License Plate Recognition 



## 总结和亮点

- 比较有意思的一篇文章，也让我们重新燃起了进行文本序列伪样本生成的动力。主要使用cycle GAN的思路进行车牌文本序列的伪样本生成，并且将其作为训练样本，实现不错的训练效果。
- 主要是合成的图片既可以保留人工合成的label，又能在hand-craft合成图片基础上增加真实性。
- 同时加入WGAN，使得合成效果更佳。
- 先用GAN合成图片训练网络，再用真实samples进行fine-tune



## Abstract

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709141620_80.png" width="700">



## Method

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709141623_775.png" width="800">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709141625_290.png" width="700">





- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709141624_187.png" width="500">

