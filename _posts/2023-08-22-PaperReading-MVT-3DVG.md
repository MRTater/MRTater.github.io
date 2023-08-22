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

According to the paper, the existing works in 3D visual grounding mainly follow a two-stage scheme, i.e., first generating all candidate objects in 3D scene (by classification) and then selecting the most matched one. These two-stage approaches in 3D visual grounding are tailored from 2D visual grounding methods, which have not considered the unique property of 3D data. The paper argues that these methods have limitations in handling view changes and do not learn a view-robust representation.

In the context of the 3D visual grounding task, query data can be categorized into two fundamental groups: explicit view-related queries and implicit view-related queries. Taking the Nr3D as an illustration, consider querying for the same nightstand. In this scenario, diverse utterances emerge, such as "if you face the bed, you need to select the nightstand that is on the right" and "nightstand closer to the desk." The initial query explicitly indicates the direction of the view, while the latter query does not provide this specific information.

![Figure 1. The Nr3D visualization. There are two different types of query, view-explicit and view-implicit.](Multi-View%20Transformer%20for%203D%20Visual%20Grounding%202c383f289d1442d2a11d3e78d358ce58/Untitled.png)

Figure 1. The Nr3D visualization. There are two different types of query, view-explicit and view-implicit.

The paper states that the motivation for the research is to address the limitations of existing methods in 3D visual grounding by making full use the view property in queries. 

## Methodology

The Multi-View Transformer (MVT) technique addresses the limitations of existing approaches through a series of steps.

Initially, the MVT method leverages a multi-view space to develop a more resilient multi-modal representation for 3D visual grounding. This strategy eliminates reliance on the initial view and amalgamates all information to create a viewpoint-agnostic representation. According to codes available in their public repository, this is achieved by rotating the entire point cloud four times to generate four sets of new coordinates, which are then integrated into the training dataset for subsequent training phases.

Subsequently, the MVT approach disentangles the computation of 3D object representations by separately calculating point cloud features and object coordinates. This separation facilitates the sharing of point cloud features across various viewpoints. Based on their publicly available codes, this is accomplished by passing all coordinate information through a Multi-Layer Perceptron module and subsequently adding it into the object feature matrix as the new object feature.

Lastly, the Multi-Modal Feature Fusion employs a conventional transformer decoder, where BERT-encoded language features serve as queries and object features as keys. The outcome of the transformer decoder is dimensionally reduced by averaging across the view dimension.

![Figure 2. The network structure of Multi-View Transformer.](Multi-View%20Transformer%20for%203D%20Visual%20Grounding%202c383f289d1442d2a11d3e78d358ce58/Untitled%201.png)

Figure 2. The network structure of Multi-View Transformer.

The MVT approach outperforms all state-of-the-art methods on several datasets, demonstrating its effectiveness in addressing the gaps of existing methods.

The paper uses several evaluations to validate the design of the proposed Multi-View Transformer (MVT) approach. First, the paper compares the performance of the MVT approach with several state-of-the-art methods on three datasets: Nr3D, CLEVR-Ref+, and CLEVRER. The results show that the MVT approach outperforms all other methods on all three datasets. Second, the paper conducts an ablation study to analyze the effectiveness of different components of the MVT approach. The results show that each component contributes to the overall performance of the MVT approach. Third, the paper analyzes the effectiveness of multi-view modeling by comparing the performance of the MVT approach with different numbers of views. The results show that multi-view modeling can learn an effective representation that can benefit different views and that increasing the view number during testing can still improve the grounding accuracy. The paper also provides visualization results to show the effectiveness of the MVT approach in localizing objects in 3D scenes.

## Constraint

The paper does not directly discuss any limitations related to the proposed Multi-View Transformer (MVT) technique. Nevertheless, it does highlight that the MVT method necessitates the independent computation of point cloud features and object coordinates. This separation is intended to facilitate the sharing of point cloud features across different viewpoints. However, this design choice might result in the model's performance being constrained by the weakest aspect among these multiple modalities. Moreover, the paper acknowledges that for intricate queries or scenes, the network's capacity to comprehend the scene and establish associations between objects and queries requires further enhancement.

## Future direction

The technique presented in this paper is characterized by its simplicity and remarkable effectiveness. This success serves as an inspiration, prompting us to emphasize the distinct attributes of 3D scenes, rather than solely applying 2D methodologies to tasks involving 3D contexts. 

In terms of potential avenues for future exploration, the paper puts forth several directions for forthcoming research endeavors. To begin with, the paper acknowledges the prospect of extending the proposed Multi-View Transformer (MVT) methodology to encompass other tasks, including but not limited to 3D object detection and segmentation. This could be extremely useful in VR or meta universe. Additionally, the paper proposes an enhancement of the MVT approach through the incorporation of supplementary information, such as object attributes and relationships. Furthermore, the paper highlights the potential to apply the MVT technique to alternate modalities like audio and haptic data, thus enabling comprehensive multi-modal grounding. The next suggestion involves the expansion of the MVT approach to tackle more intricate scenes, such as those involving occlusions and clutter. Lastly, the paper presents the prospect of leveraging the MVT approach for the generation of natural language descriptions pertaining to 3D scenes. Such capabilities could find utility in applications such as virtual assistants and robotics.