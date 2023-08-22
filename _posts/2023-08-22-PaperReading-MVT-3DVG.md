---
title: 'Multi-View Transformer for 3D Visual Grounding Paper Reading'
date: 2023-08-22
permalink: /posts/PaperReading/MVT-3DVG/
tags:
  - Computer Vision
  - Paper Reading
---

Easy and effective 3D visual grounding.

# Multi-View Transformer for 3D Visual Grounding

## Abstract

The work is about proposing a new approach to 3D visual grounding, called the Multi-View Transformer (MVT), that outperforms all state-of-the-art methods. The MVT approach uses a multi-view space to learn a more robust multi-modal representation for 3D visual grounding.

## Gaps of existing works and motivations

According to the paper, the existing works in 3D visual grounding mainly follow a two-stage scheme, i.e., first generating all candidate objects in 3D scene and then selecting the most matched one. These two-stage approaches in 3D visual grounding are tailored from 2D visual grounding methods, which have not considered the unique property of 3D data. The paper argues that these methods have limitations in handling view changes and do not learn a view-robust representation. Therefore, the paper proposes a new approach, the Multi-View Transformer (MVT), that addresses these limitations and outperforms all state-of-the-art methods.

In the context of the 3D visual grounding task, query data can be categorized into two fundamental groups: explicit view-related queries and implicit view-related queries. Taking the Nr3D as an illustration, consider querying for the same nightstand. In this scenario, diverse utterances emerge, such as "if you face the bed, you need to select the nightstand that is on the right" and "nightstand closer to the desk." The initial query explicitly indicates the direction of the view, while the latter query does not provide this specific information.

![Untitled](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/MVT-3DVG/Dataset.png)

The paper states that the motivation for the research is to address the limitations of existing methods in 3D visual grounding by making full use the view property in queries. 

## Methodology

The Multi-View Transformer (MVT) technique addresses the limitations of existing approaches through a series of steps.

Initially, the MVT method leverages a multi-view space to develop a more resilient multi-modal representation for 3D visual grounding. This strategy eliminates reliance on the initial view and amalgamates all information to create a viewpoint-agnostic representation. According to information available in their public repository, this is achieved by rotating the entire point cloud four times to generate four sets of new coordinates, which are then integrated into the training dataset for subsequent training phases.

Subsequently, the MVT approach disentangles the computation of 3D object representations by separately calculating point cloud features and object coordinates. This separation facilitates the sharing of point cloud features across various viewpoints. Based on their publicly available codes, this is accomplished by passing all coordinate information through a Multi-Layer Perceptron module and subsequently adding it into the object feature matrix as the new object feature.

Lastly, the Multi-Modal Feature Fusion employs a conventional transformer decoder, where BERT-encoded language features serve as queries and object features as keys. The outcome of the transformer decoder is dimensionally reduced by averaging across the view dimension.

![Untitled](https://github.com/MRTater/MRTater.github.io/raw/master/_posts/PaperReading-Image/MVT-3DVG/Network.png)

The MVT approach outperforms all state-of-the-art methods on several datasets, demonstrating its effectiveness in addressing the gaps of existing methods.

The paper uses several evaluations to validate the design of the proposed Multi-View Transformer (MVT) approach. First, the paper compares the performance of the MVT approach with several state-of-the-art methods on three datasets: Nr3D, CLEVR-Ref+, and CLEVRER. The results show that the MVT approach outperforms all other methods on all three datasets. Second, the paper conducts an ablation study to analyze the effectiveness of different components of the MVT approach. The results show that each component contributes to the overall performance of the MVT approach. Third, the paper analyzes the effectiveness of multi-view modeling by comparing the performance of the MVT approach with different numbers of views. The results show that multi-view modeling can learn an effective representation that can benefit different views and that increasing the view number during testing can still improve the grounding accuracy. The paper also provides visualization results to show the effectiveness of the MVT approach in localizing objects in 3D scenes.

## Constraint

The paper does not directly discuss any limitations related to the proposed Multi-View Transformer (MVT) technique. Nevertheless, it does highlight that the MVT method necessitates the independent computation of point cloud features and object coordinates. This separation is intended to facilitate the sharing of point cloud features across different viewpoints. However, this design choice might result in the model's performance being constrained by the weakest aspect among these multiple modalities. Moreover, the paper acknowledges that for intricate queries or scenes, the network's capacity to comprehend the scene and establish associations between objects and queries requires further enhancement.

## Future direction

Regarding possible future works, the paper suggests several directions for future research. First, the paper notes that the proposed Multi-View Transformer (MVT) approach can be extended to other tasks, such as 3D object detection and segmentation. Second, the paper suggests that the MVT approach can be further improved by incorporating additional information, such as object attributes and relations. Third, the paper suggests that the MVT approach can be applied to other modalities, such as audio and haptic data, to enable multi-modal grounding. Fourth, the paper suggests that the MVT approach can be extended to handle more complex scenes, such as scenes with occlusions and clutter. Finally, the paper suggests that the MVT approach can be used to generate natural language descriptions of 3D scenes, which can be useful for applications such as virtual assistants and robotics.