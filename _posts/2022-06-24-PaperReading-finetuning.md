---
title: 'Bag of Freebies for Training Object Detection Neural Networks 论文笔记'
date: 2022-06-24
permalink: /posts/PaperReading/BFTOD 
tags:
  - Computer Vision
  - Paper Reading
---

想要白赚的性能提升吗？那你来对地方了！

## 目录
- [目录](#目录)
- [作者信息](#作者信息)
- [问题定义](#问题定义)
- [相关工作](#相关工作)
- [动机和思路](#动机和思路)
- [算法流程](#算法流程)
- [实验结果](#实验结果)

## 作者信息
亚马逊的AI团队，一作现在在字节。通讯作者李沐，在B站发的论文精读视频还挺好看。


## 问题定义
本文主要讨论针对object detection的神经网络优化方法。 object detection神经网络可以分为两类：
以YOLO为代表的single-stage object detection networks、以Faster-RCNN为代表的multi-stage object detection networks
本文涉及的优化包括：
 - MixUp
 - head label smoothing
 - transformations（random crop等）
 - 学习率schedule
 - synchronized batch normalization
 - random shape training


## 相关工作
多种调优模型的方法，包括
 - learning rate warmup
 - label smoothing
 - 以及object detection的两种分类
     - multiple stage
     - single stage

本文以这些工作为基础讨论应该如何进一步调优object detection的模型，探讨哪些方法对于哪些模型表现有进一步的帮助


## 动机和思路
作者讨论应该如何进一步调优object detection的模型，探讨哪些方法对于哪些模型表现有进一步的帮助


## 算法流程
 - MixUp：保留了完整信息（object label也被整合成了新的array）的geometry preserved alignment of mixed images也能够提升目标检测的准确性
 - data prepossessing
   - single stage（YOLOv3）：对transformation更加敏感，包括random flip, rotate和crop之类的常规transform方式
   - multiple stage（Faster-RCNN）：对transformation不敏感，本文给出的理由是sampling-based方法在获取ROI的时候要在feature map上做大量的crop，这个过程代替了数据预处理中的crop
 - training schedule
   - step schedule的学习率变化过于剧烈，并且会导致优化器需要重新稳定momentum
   - cosine schedule的学习率变化更加平滑，效果更好
   - warmup schedule对于一部分的物体检测算法影响很大，如YOLOv3（起始时负样本的梯度作为主导，因此如果一开始学习率就很大会导致对于主要的样本得分接近于0）
    设置的当的cosine schedule和warmup schedule配合能让整体训练效果提升
 - synchronized batch normalization
   - 非同步的bn无论如何都会造成一定程度的batchsize减少和数据差异（每张卡做归一化），这种问题在小batchsize的时候可能会更加严重（如高分辨率图片训练时可能出现的，1张图片一张卡）
 - 随机大小的图片（仅限single-stage网络）
   - faster RCNN本身就能够接受多种不同大小的图片
   - 随机大小的图片可以降低过拟合风险和提升模型泛化能力


## 实验结果

| 数据集     | Single stage（YOLOv3）                                                                                                                                             | Multiple stage（Faster-RCNN）                                                                                                                                  |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pascal  | 去除data augmentation带来巨额性能损失（16%mAP），证明single stage模型严重依赖数据增强来创造之前没见过的特征以提升模型的预测能力；其余提到的方法共提升了约3.43%mAP，其中mixup提升最大（1.54），进一步佐证的本文所说：single stage模型严重依赖于各类数据增强方法。 | 	去除data augmentation带来非常轻微的性能损失（0.16%mAP），证明proposal层大量的采样实际上替代了在single stage中大量使用的random cropping；其余本文提到的方法共带来3.55%的性能提升，其中cosine lr schdule带来的提升占比最大（1.82） |
| MS COCO | 同样各种方法一起安排能够提点（4-5.4），并且在输入图片分辨率较低的时候效果更加明显。最终达到的准确率与Faster-RCNN差不多，同时推理速度更快	                                                                                    | 相对而言提升更小（1-1.7），但许多category都能够有提升                                                                                                                            |

Mixup的使用可以在两个不同的阶段，分别是预训练backbone和训练检测头。实验结果证明Mixup方法能对两个阶段分别起作用，并且在两个阶段同时使用最终能够产生更佳的效果。


