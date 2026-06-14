---
title: OOD-Enhanced Self-Supervised Visual Learning
publishDate: 2024-09-01 00:00:00
img: /assets/stock-3.jpg
img_alt: Abstract visualization of a neural network distinguishing rare objects in a long-tailed dataset
description: |
  Novel framework integrating OOD detection into DINO self-supervised pretraining via a dynamic memory buffer — improving rare-object representation on long-tailed autonomous driving datasets.
tags:
  - Computer Vision
  - Deep Learning
  - Self-Supervised Learning
---

## The Problem

Standard self-supervised learning methods like DINO and SimCLR learn powerful visual representations — but on long-tailed datasets, the training signal is dominated by frequent classes. Rare objects get underrepresented in the learned embedding space. In safety-critical domains like autonomous driving, this is directly consequential: the objects that appear least often (pedestrians at night, cyclists, unusual vehicles) are often the ones where failure matters most.

## Approach

The framework integrates OOD detection directly into the SSL pretraining loop without requiring any labels.

**OOD detection:** A ResNet-50 encoder pretrained with DINO extracts features for each sample. Samples with high embedding distance from the running mean are flagged as out-of-distribution — likely rare or underrepresented.

**Dynamic memory buffer:** Flagged samples are stored in a FIFO queue and reintroduced into training batches repeatedly, giving the model stronger exposure to rare examples. Buffer size is fixed at 32 rare crops per batch.

**DINO integration:** Augmented batches — mixing regular samples with memory-buffered rare samples — are fed into standard DINO self-supervised training with 8-crop augmentation (2 global + 6 local per frame).

## Evaluation

Evaluated on BDD100K (autonomous driving scenes) and an ImageNet subset. Training ran for 100 epochs with a cosine LR schedule and AdamW optimizer (lr=5e-4), batch size 1024.

The approach improved rare-object identification precision and recall on BDD100K relative to the unmodified DINO baseline, with the largest gains at lower detection thresholds where rare objects are hardest to surface.

## Context

This was a NYU capstone project. The research question — how to make SSL more equitable across frequency tiers without labels — generalizes well beyond computer vision. Any domain where the hardest cases are also the rarest faces the same underlying problem.
