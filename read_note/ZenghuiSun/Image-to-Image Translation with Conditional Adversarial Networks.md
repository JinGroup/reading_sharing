# Image-to-Image Translation with Conditional Adversarial Networks 

## 总结及亮点

- 这一篇主要着眼于paired images的风格迁移。是像素级别(pixel-to-pixel)的风格转换。
- 主要的亮点在于discriminator那里，不同于经典的GAN网络架构中的整张feature进行是否真伪的判断，在本文中提出了 patch GAN的思路，将discriminator的输出映射到一个NXN的patch，每一块分别进行真伪判断。这样细粒度的判别有利于模型对于细节的学习和结构的把握。



## Abstract

<img src="http://ovy9iv9f2.bkt.clouddn.com/201709260935_841.png" width="500">



## Method

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709260936_430.png" width="500">

