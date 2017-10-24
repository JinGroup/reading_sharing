# Focusing Attention: Towards Accurate Text Recognition in Natural Images 

## 总结和亮点

- 有干货的一篇OCR主题文章，相当地有借鉴意义。在attention模型的基础上，因为attention模型存在attention drift的问题，提出起到纠正作用的focus network。
- 效果上提升相当显著，相比baoguang Shi的TPAMI 2016的baseline在IIIT5K数据上提升了5个百分点。



## Abstract

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251631_497.png" width="500">



## Method

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251632_318.png" width="500">



### Attention Network

- 这一块还是和之前的工作差不多，使用的是attention encoder-decoder的思路。location-based and content based attention。
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251642_876.png" width="500">



### Focusing network

- 分为两步，首先计算attention中心点，然后将attention区域crop出来，根据其以及feature vector计算概率分布。
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251646_126.png" width="500">



### 训练参数

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251646_860.png" width="500">

