# 	Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks 

## 总结及亮点

- 一篇比较成功的GAN论文，cycleGAN，Github源码的star有7.5K，相当有影响力。（才发表半年时间）

- 主要用于进行风格迁移等，使用重映射的思路进行风格变换以及逆变换的学习。

- 因为从X映射到Y有几乎无穷的映射关系$G$，可以使得$G(x)  ≈ Y$，但是G不一定是有效的转换。为了使得X和Y pair up.所以为了学习有效的转换方法，需要$F(G(x) ) ≈ X$成立，这个就是cycle GAN的思路。

  ​

## Abstract

<img src="http://ovy9iv9f2.bkt.clouddn.com/201709121042_66.png" width="500">



## Method

<img src="http://ovy9iv9f2.bkt.clouddn.com/201709121043_226.png" width="800">



- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709121044_970.png" width="500">

## 网络结构

G和D都是使用较为新的网络结构。

G采用的是[Perceptual Losses for Real-Time Style Transfer and Super-Resolution](https://arxiv.org/abs/1603.08155)

D采用的是[patch GAN](https://arxiv.org/pdf/1611.07004.pdf)

- <img src="http://ovy9iv9f2.bkt.clouddn.com/201709131756_756.png" width="500">

## 实验观察

- 成功案例：
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709121643_146.png" width="500">
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709121648_139.png" width="500">
- 经过观察，初步判断是判断颜色的替换。网络会对于特定颜色的像素进行学习出来规则的替换。
- 同一种pattern在原图和目标图里面应该是相同的颜色，然后网络学到的就是如何将A/B中相同的pattern进行替换。
  - 最经典的做法就是使用土黄色的山包，看它是否替换成斑马条纹
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709121023_110.png" width="500">
    - 这张图里面，人身体部分就会被替换
  - <img src="http://ovy9iv9f2.bkt.clouddn.com/201709121031_319.png" width="500">
    - 这张图里面，白马就不能正常替换成斑马；只有棕色的马才能







## 代码剖析

### 实验设置

To train a model on your own datasets, you need to create a data folder with two subdirectories `trainA` and `trainB` that contain images from domain A and B. You can test your model on your training set by setting ``phase='train'`` in  `test.lua`. You can also create subdirectories `testA` and `testB` if you have test data.

You should **not** expect our method to work on just any random combination of input and output datasets (e.g. `cats<->keyboards`). From our experiments, we find it works better if two datasets share similar visual content. For example, `landscape painting<->landscape photographs` works much better than `portrait painting <-> landscape photographs`. `zebras<->horses` achieves compelling results while `cats<->dogs` completely fails.



### Generator 网络结构

```python
(0): ReflectionPad2d (3, 3, 3, 3)
(1): Conv2d(3, 64, kernel_size=(7, 7), stride=(1, 1))
(2): InstanceNorm2d(64, eps=1e-05, momentum=0.1, affine=False)
(3): ReLU (inplace)
(4): Conv2d(64, 128, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
(5): InstanceNorm2d(128, eps=1e-05, momentum=0.1, affine=False)
(6): ReLU (inplace)
(7): Conv2d(128, 256, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1))
(8): InstanceNorm2d(256, eps=1e-05, momentum=0.1, affine=False)
(9): ReLU (inplace)
(10): ResnetBlock (
  (conv_block): Sequential (
    (0): ReflectionPad2d (1, 1, 1, 1)
    (1): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1))
    (2): InstanceNorm2d(256, eps=1e-05, momentum=0.1, affine=False)
    (3): ReLU (inplace)
    (4): ReflectionPad2d (1, 1, 1, 1)
    (5): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1))
    (6): InstanceNorm2d(256, eps=1e-05, momentum=0.1, affine=False)
  )
)
【ResnetBlock重复9遍】
(19): ConvTranspose2d(256, 128, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1), output_padding=(1, 1))
(20): InstanceNorm2d(128, eps=1e-05, momentum=0.1, affine=False)
(21): ReLU (inplace)
(22): ConvTranspose2d(128, 64, kernel_size=(3, 3), stride=(2, 2), padding=(1, 1), output_padding=(1, 1))
(23): InstanceNorm2d(64, eps=1e-05, momentum=0.1, affine=False)
(24): ReLU (inplace)
(25): ReflectionPad2d (3, 3, 3, 3)
(26): Conv2d(64, 3, kernel_size=(7, 7), stride=(1, 1))
(27): Tanh ()
```


### Discriminator网络结构

    (0): Conv2d(3, 64, kernel_size=(4, 4), stride=(2, 2), padding=(1, 1))
    (1): LeakyReLU (0.2, inplace)
    (2): Conv2d(64, 128, kernel_size=(4, 4), stride=(2, 2), padding=(1, 1))
    (3): InstanceNorm2d(128, eps=1e-05, momentum=0.1, affine=False)
    (4): LeakyReLU (0.2, inplace)
    (5): Conv2d(128, 256, kernel_size=(4, 4), stride=(2, 2), padding=(1, 1))
    (6): InstanceNorm2d(256, eps=1e-05, momentum=0.1, affine=False)
    (7): LeakyReLU (0.2, inplace)
    (8): Conv2d(256, 512, kernel_size=(4, 4), stride=(1, 1), padding=(1, 1))
    (9): InstanceNorm2d(512, eps=1e-05, momentum=0.1, affine=False)
    (10): LeakyReLU (0.2, inplace)
    (11): Conv2d(512, 1, kernel_size=(4, 4), stride=(1, 1), padding=(1, 1))


### 训练过程

```python
self.forward()
# G_A and G_B
self.optimizer_G.zero_grad()
self.backward_G()
self.optimizer_G.step()
# D_A
self.optimizer_D_A.zero_grad()
self.backward_D_A()
self.optimizer_D_A.step()
# D_B
self.optimizer_D_B.zero_grad()
self.backward_D_B()
self.optimizer_D_B.step()
```


#### backward_G

- 分为GAN loss 、 forward cycle loss、backward cycle loss 三部分
- GAN loss 分别为A、B两个支路的D(G(X))的过程。以A为例，进行说明：
  - real_A - G_A - fake_B - D_A - loss_G_A
  - real-B - G_B - fake_A - D_B - loss_G_B
- cycle_loss:
  - fake_B - G_B - rec_A - rec_A/ real_A - loss_cycle_A
  - fake_A - G_A - rec_B - rec_B / real_B - loss_cycle_B 

#### backward_D_A

- ​