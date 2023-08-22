---
title: 'Fully Convolutional Networks for Semantic Segmentation 论文笔记'
date: 2022-06-07
permalink: /posts/PaperReading/FCN/
tags:
  - Computer Vision
  - Paper Reading
---

分割任务的开山鼻祖，至今仍然是广泛应用的head。  

## 目录
- [目录](#目录)
- [作者信息](#作者信息)
- [问题定义](#问题定义)
- [相关工作](#相关工作)
- [动机和思路](#动机和思路)
- [算法流程](#算法流程)
- [实验结果](#实验结果)

## 作者信息
 * 两个一作Jonathan Long和Even Shelhanmer。这两位都是caffe的开发者。
 * 通讯作者Trevor Darrell，UC Berkeley的教授and上述两位的导师，也是caffe的开发者之一。


## 问题定义
卷积神经网络原本主要是用于图像分类任务，能够通过卷积的方式抽象图像信息成特征图与特征向量。再通过全连接层和激活函数计算属于哪个类别的概率。本文讨论如何通过卷积神经网络来实现图像的语义分割和物体识别。


## 相关工作
 * 虽然卷积网络在这个文章很多年前就出现了，但是用卷积神经网络做物体检测的少，用fully convolutional network的少，能end-to-end训练的就少之又少了；
   * 其中比较接近的可能有Joint training of a convolutional network and a graphical model for human pose estimation，但是这篇文章用本文作者的话说就是虽然用了但没用明白，没有分析和解释这种网络结构的优点。
   * 还有一篇相关工作 Spatial pyramid pooling in deep convolutional networkds for visiual recognition,去除了分类神经网络中非卷积的部分，并且将spatial pyramid pooling和proposal结合起来获取localized特征，但是问题在于不能end-to-end训练。
 * 另外一个相关方向是dense prediction卷积，相关工作中通常都有很多小trick
 * 小模型，capacity和receptive field都有限
   * patchwise training（重要，本文使用了类似的思路）
   * shift-and-stitch（重要）
 * proposal算法，代表性的是R-CNN的微调版本，但是这个不是end-to-end的训练


## 动机和思路
作者的fully convolutional network主要解决几个问题：
 * end-to-end训练
 * 任意大小图像输入
 * 让卷积网络能够实现物体的分割检测
 * 提升计算效率
思路及实现见算法流程。


## 算法流程
 * 训练流程非常直白，作者做了一件事：把最后的全连接层换成卷积层，让最后输出的不是一个概率向量而是一个包含了label信息的coarse output maps（heat map)。
![Image](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/FCN/algo1.png)
 * 这个coarse output map再被连接至每一个像素，从而实现对于单个像素的分类并获取非常准确的图像分割结果。将coarse output map链接至每一个像素的过程，本文作者对比了shift-and-stitch和upsampling，
     * 前者存在一定程度的妥协，虽然感知野的大小不会被减小，但是filter也不能够调整大小
     * 后者是作者实际选择使用的方式，将前几层卷积、池化之后的feature map保留下来，然后通过反向卷积的方式进行对图像因为抽象而损失的细节进行补充，最后实现图像的还原
![Image](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/FCN/algo2.png)

 * 缺陷：
   * 上采样无论如何都会出现图像信息的损失，图片细节仍然会偏向模糊，图像分割只能描述大概的轮廓。
   * 对单个像素进行分类没有充分考虑像素与像素之间的关系。忽略了在通常的基于像素分类的分割方法中使用的空间规整步骤，缺乏空间一致性（来自知乎，对这个部分了解还不够深入）
![Image](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/FCN/algo3.png)

## 实验结果
第一组实验：将FCN和各个已经在分类任务上被证明有效的网络结构结合，目的是证明现有的卷积神经网络结构能够通过修改成FCN网络结构来完成分割与检测任务。测试数据集为VOC2011。

| 实验名           | mean IoU | comment |
|---------------|----------|---------|
| FCN-AlexNet   | 	39.8    | 	       |
| FCN-VGG16     | 	56.0    | 	       |
| FCN-GoogLeNet | 	42.5    | 	       |

实验结果符合预期，证明图像分类网络通过FCN可以转换成图像分割与检测网络，并且能够拥有相当程度的正确率

第二组实验：测试upsampling的表现情况，测试数据集为VOC2011。

| 实验名           | pixel acc. | mean IoU |
|---------------|------------|----------|
| FCN-32s-fixed | 	83.0      | 	45.4    |
| FCN-32s       | 	89.1      | 	59.4    |
| FCN-16s       | 	90.0      | 	62.4    |
| FCN-8s        | 	90.3      | 	62.7    |

实验结果也是符合预期的，数字越小的网络使用的来自pool的prediction越多，也就意味着获得的额外细节信息更多；以FCN-8s为例，8s的网络使用了pool3的stride 8的prediction，最终的上采样率是8x，也就保留了更多细节和更精确的像素预测。同样stride为8之后的提升已经不是很明显了，说明浅层信息学习已经接近极限了，也就没有必要继续学习进一步的浅层特征了。

第三组实验：与之前网络结构的结果做对比（baseline实验）。值得注意的是，计算时间也有显著减少。

| 实验名     | mean IoU (VOC2011) | mean IoU (VOC2012) | inference time |
|---------|--------------------|--------------------|----------------|
| R-CNN   | 	47.9              |
| SDS	    | 52.6               | 	51.6              | 	~50s          |
| FCN-8s	 | 62.7               | 	62.2              | 	~175ms        | 

第四组实验：RGBD，四维图像输入测试，在除了RGB之外还多了一个深度信息（depth information）。目的应该是测试多通道的情况下是不是仍然能够拥有较好表现。
![image](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/FCN/exp4.png)


第五组实验：SIFT包含图像分割信息和背景信息，多任务学习测试。
![image](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/FCN/exp5.png)


