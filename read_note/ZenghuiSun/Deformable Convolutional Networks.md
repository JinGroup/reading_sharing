# Deformable Convolutional Networks 

## 总结和亮点

- 一篇比较有新意的文章，主要argue的点就是传统卷积在学习过程中会学习到固定的pattern，无法根据当前输入的sample进行变化。在deformable CNN架构里面，每次根据支路学习到的additional offset进行卷积位置的调整，从而达到不同的global structure使用不同的卷积结构进行学习。
- 目前只有mxnet的实现代码，复现本篇论文的工作有一定的困难。
- 自己感觉Deformable ROIPooling相对于Deformable CNN更可解释。
- ​

## Abstract

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251443_465.png" width="500">





## Method

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251445_481.png" width="500">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251446_500.png" width="500">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709251446_765.png" width="500">