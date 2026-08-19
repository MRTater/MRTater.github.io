---
title: "B³D-RWKV: Triplet-Block Diffusion RWKV"
authors: ["Ke Lin*", "Yiyang Luo*", "Zhaolong Su", "Yunya Song", "Anyi Rao"]
venue: "Preprint, 2026"
date: 2026-08-19
category: manuscripts
tags: [Language Models, Diffusion Models, Efficient Inference]
teaser: "/images/paper/b3d-rwkv.png"
codeurl: "https://github.com/leonardodalinky/B3D-RWKV"
abstract: "Causal Transformer language models suffer from strictly sequential decoding and a quadratic per-step attention cost. While linear-time causal models and discrete diffusion models each address these weaknesses, their integration remains inherently inconsistent: diffusion requires bidirectional attention, while causal models are unidirectional. We propose B³D-RWKV, a diffusion RWKV variant that combines RWKV's linear-time inference efficiency with parallel, bidirectional discrete diffusion through a triplet-block layout. B³D-RWKV-7.2B achieves comparable accuracy to existing models on an eight-task evaluation suite while delivering an average 1.6× decoding-throughput speedup over the RWKV baseline."
---

![Overview of the B³D-RWKV triplet-block layout](/images/paper/b3d-rwkv.png)

## Abstract

Causal Transformer language models suffer from strictly sequential decoding and a quadratic per-step attention cost. While linear-time causal models and discrete diffusion models each address these weaknesses, their integration remains inherently inconsistent: diffusion requires bidirectional attention, while causal models are unidirectional. We propose B³D-RWKV, a diffusion RWKV variant that combines RWKV's linear-time inference efficiency with parallel, bidirectional discrete diffusion through a triplet-block layout. B³D-RWKV-7.2B achieves comparable accuracy to existing models on an eight-task evaluation suite while delivering an average 1.6× decoding-throughput speedup over the RWKV baseline.

[Code](https://github.com/leonardodalinky/B3D-RWKV)
