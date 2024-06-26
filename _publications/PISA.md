---
title: "PISA: Point Cloud-based Instructed Scene Augmentation"
collection: publications
permalink: /publication/PISA
date: 2023-11-07
venue: 'arXiv'
citation: 'Luo, Y.* & Lin, K.* (2023). PISA: Point-cloud-based Instructed Scene Augmentation. arXiv preprint [Cs.CV] arXiv: arXiv.2311.16501.'
---
Full paper please click [here](https://arxiv.org/abs/2311.16501).

# Abstract #
Indoor scene augmentation has become an emerging topic in the field of computer vision with applications in augmented and virtual reality. However, existing scene augmentation methods mostly require a pre-built object database with a given position as the desired location. In this paper, we propose the first end-to-end multi-modal deep neural network that can generate point cloud objects consistent with their surroundings, conditioned on text instructions. Our model generates a seemly object in the appropriate position based on the inputs of a query and point clouds, thereby enabling the creation of new scenarios involving previously unseen layouts of objects. Database of pre-stored CAD models is no longer needed. We use Point-E as our generative model and introduce methods including quantified position prediction and Top-K estimation to mitigate the false negative problems caused by ambiguous language description. Moreover, we evaluate the ability of our model by demonstrating the diversity of generated objects, the effectiveness of instruction, and quantitative metric results, which collectively indicate that our model is capable of generating realistic in-door objects. For a more thorough evaluation, we also incorporate visual grounding as a metric to assess the quality of the scenes generated by our model.
