---
title: "Uniﬁed Feature Fusion Network with Path Router for Multi-task Image Restoration"
collection: publications
permalink: /publication/UFFNPR
date: 2021-10-13
venue: 'ICCT 2021'
citation: 'J. Zhou, C. Leong, Y. Luo, M. Lin, W. Liao and C. Li, "Unified Feature Fusion Network with Path Router for Multi-task Image Restoration," 2021 IEEE 21st International Conference on Communication Technology (ICCT), Tianjin, China, 2021, pp. 1206-1210, doi: 10.1109/ICCT52962.2021.9658001.'
---
Full paper please click [here](https://ieeexplore.ieee.org/document/9658001).

# Abstract #
Image restoration is an important low-level vision task, which includes various sub-tasks such as deraining, dehazing, denoising, raindrop removal, etc. Although current researches have achieved significant results in various sub-tasks, only a few of them are designed for multiple degradation factors. However, in the actual natural environment, the weather is complex and changeable so the networks designed for a single task are usually inapplicable. In this paper, we propose an unified network that can effectively restore images in a variety of weather conditions (rain, haze, and raindrops). The network is mainly divided into three parts. The first part is the shared multi-expert feature extraction module. We introduce the multi-task learning with multi-gate mixture-of-experts(MMoE) architecture and propose the smooth dilated residual group to extract the low-level features. Furthermore, the gate fusion sub-network is proposed to weigh and sum the output of each expert, so the correlation and difference between tasks can be captured. The second part is the path router sub-network, which can select branches of different tasks, and only open one branch at a time. The third part is multi-gated feature fusion branch, which can extract high-level feature and fuse different levels of features. Finally, we add the output of the third part to the input image and get the clean image. Our model cam deal with a variety of weather conditions and the experiments show competitive results compared with state-of-the-art models for single tasks.
