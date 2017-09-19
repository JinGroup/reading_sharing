# Enriched Deep Recurrent Visual Attention Model for Multiple Object Recognition 

## 总结及亮点

- 一个结合了attention和STN的多物体识别的任务。跟我们之前的思路很像，这篇论文做得更加完整，有一定的借鉴作用
- 有一个之前没有关注的数据集，可以考虑尝试：MNIST Clutter
- 亮点：这篇文章将STN和Attention做了一个比较好的整合，可以考虑这个框架的模式
- ​



## Abstact

<img src="http://ovy9iv9f2.bkt.clouddn.com/201709101454_200.png" width="400">



## Enriched Deep Recurrent Visual Attention Model 

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101455_744.png" width="500">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101455_924.png" width="400">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101455_747.png" width="400">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101457_148.png" width="500">
- 有一个疑问点：如何进行STN的参数loss计算？
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101518_816.png" width="400">
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709101533_223.png" width="400">
  - 确实是需要数据提供有其中的参数