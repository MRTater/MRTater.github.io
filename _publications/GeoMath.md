---  
title: "Geo-LLaVA: A Large Multi-Modal Model for Solving Geometry Math Problems with Meta In-Context Learning"  
authors: [Shihao Xu*, Yiyang Luo*, Wei Shi]  
venue: "ACM MM 2024 LGM3A Workshop"  
date: 2024-11-16  
tags: [Multi-Modality, RAG]  
teaser: "/images/paper/GeoMath.svg"  
# link: ""  
# paperurl: "https://example.com/paper-url.pdf"  
# slidesurl: "https://example.com/slides-url.pdf"  
# codeurl: "https://github.com/AInnovateLab/ViRED"  
# projecturl: "https://ainnovatelab.github.io/ViRED/"  
abstract: "Geometry mathematics problems pose significant challenges for large language models because they involve visual elements and spatial reasoning. Current methods primarily rely on symbolic character awareness to address these problems. Considering geometry problem solving is a relatively nascent field with limited suitable datasets and currently almost no work on solid geometry problem solving, we collect a geometry question-answer dataset by sourcing geometric data from Chinese high school education websites, referred to as GeoMath. It contains solid geometry questions and answers with accurate reasoning steps as compensation for existing plane geometry datasets. Additionally, we propose a Large Multi-modal Model framework named Geo-LLaVA, which incorporates retrieval augmentation with supervised fine-tuning in the training stage, called meta-training, and employs in-context learning during inference to improve performance. Our fine-tuned model with ICL attains the state-of-the-art performance of 65.25% and 42.36% on selected questions of the GeoQA dataset and GeoMath dataset respectively with proper inference steps. Notably, our model initially endows the ability to solve solid geometry problems and supports the generation of reasonable solid geometry picture descriptions and problem-solving steps. Our research sets the stage for further exploration of LLMs in multi-modal math problem-solving, particularly in geometry math problems."  
---  
