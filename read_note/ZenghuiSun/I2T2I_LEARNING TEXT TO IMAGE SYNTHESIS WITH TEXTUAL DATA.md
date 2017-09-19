# I2T2I: LEARNING TEXT TO IMAGE SYNTHESIS WITH TEXTUAL DATA AUGMENTATION 

## 总结及亮点

- 在GAN—CLS的基础上，加上了image caption以及image/ text embedding 模块， 搜索候选的图片描述生成sentence，并且进行embedding feature 的cosine比对。将生成的sentence判别出是否matched之后，输入到GAN-CLS模块进行对应的图片合成。
- 相比于传统的GAN-CLS，这篇文章加入了image caption和image embedding，丰富了合成图片的候选描述。



## Abstract

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709110958_955.png" width="500">



## Introduction

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709110959_31.png" width="500">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709111000_875.png" width="500">



## Method

### Image Caption

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709111001_61.png" width="500">

### Image-Text Embedding

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709111002_704.png" width="500">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709111002_137.png" width="500">

### GAN-CLS

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709111003_673.png" width="500">
- ​