# fire-detection-overview
fire detection overview


最近在研究火灾检测算法，网上看了一些论文和代码，暂总结如下，供参考：

# 初级版检测：

   主要就是通过颜色（一般是在RGB空间处理）提取检测火灾，对于火焰而言，红色分量(R )和绿色分量(G)会很大，并且绿色分量(G)会大于蓝色分量(B)。其中，Rt是红色分量阈值，St是饱和度阈值,火焰像素主要取决于红色分量(R )的色度和饱和度。其中，Rt是红色分量阈值，St是饱和度阈值，具体值是自己设置的，此外还增加了一些饱和度条件。此外还有一些对RGB颜色模型（不过通常认为在HUY颜色模型下提取效果更好些，因为RGB对亮度敏感）的改进，例如下面参考论文3，我对其进行了实现，效果参见：https://blog.csdn.net/zhou4411781/article/details/100917496

 * (1)利用颜色检测的python版的火灾检测：https://blog.csdn.net/weixin_41987641/article/details/81812823
 * (2)利用颜色检测的C++版的火灾检测：https://blog.csdn.net/coldplayplay/article/details/70212483
 * (3)利用颜色检测论文：https://www.sciencedirect.com/science/article/pii/S1047320306000927

# 进阶版检测：
   只利用颜色进行火灾检测会有很多误检测，特别是颜色与火焰颜色相近时，所以有论文提出了先根据帧差法（参见我的博客：https://blog.csdn.net/zhou4411781/article/details/99413894） 找到变化的前景（一般假设火灾是不断变化的），在前景中再根据颜色、形状、运动变化等检测。具体为：根据YUV颜色过滤模型筛选关键区域，再根据轮廓周长和面积的关系设置一定阈值筛选；实际情况下，火灾形状是在不断变化的而且变化方向是随机的，最后通过前后两帧关键点的方向变化统计判断是否是火灾（下图为火灾关键点变化与人的关键点变化对比）。

 * (1)利用颜色+形状+运动的火灾检测：https://ieeexplore.ieee.org/document/7014233

# 高级版检测：
   利用机器学习训练模型进行检测，Toby Breckon在github上给出了三种不同的网络模型进行火灾检测，不过暂没有给出训练模型代码，包括firenet、inceptionV1、superpixel-inceptionV1，检测效果我都做过测试，效果还可以，superpixel-inceptionV1效果最好，但最耗时。

 * (1)利用机器学习的火灾检测：https://github.com/tobybreckon/fire-detection-cnn


# 自己总结的火焰数据集
https://blog.csdn.net/zhou4411781/article/details/100537926
