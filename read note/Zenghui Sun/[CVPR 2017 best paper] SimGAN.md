## Learning from Simulated and Unsupervised Images through Adversarial Training 

### 总结&亮点

- 合成的样本，经过unlabeled的真实样本指导纠正之后，生成的样本更加真实。
- 相当于在人工合成样本的基础上，使用真实样本进行指导。
- 最良好的情况就是人工合成确定了**前景label**之后，使用simGAN进行**真实环境变换**。



### Abstract 

<img src="http://ovy9iv9f2.bkt.clouddn.com/201709081557_5.png" width="400">





### Introduction

- 主要就是提出一个观点：我们需要大量的训练样本，但是标记样本需要的成本太高。所以使用合成样本训练模型是有必要的，但是合成样本和真实样本存在一定差异。本文主要就是要解决如何让合成样本变得和真实样本更像。
- 相当于在真实样本没有标注的情况下，尽可能使用真实样本的分布。
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709081636_445.png" width="400">
- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709081637_822.png" width="500">
- **Contributions:**
  1. We propose S+U learning that uses unlabeled real
    data to refine the synthetic images.
  2. We train a refiner network to add realism to synthetic images using a combination of an adversarial
    loss and a *self-regularization loss*.
  3. We make several key modifications to the GAN
    training framework to stabilize training and prevent
    the refiner network from producing artifacts.
  4. We present qualitative, quantitative, and user study
    experiments showing that the proposed framework
    significantly improves the realism of the simulator
    output. We achieve state-of-the-art results, without
    any human annotation effort, by training deep neural networks on the refined output images. 




- self regularization loss:
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709081645_579.png" width="300">




- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709081638_142.png" width="900">

