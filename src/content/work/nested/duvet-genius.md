---
title: OOD-Enhanced Self-Supervised Visual Learning
publishDate: 2024-09-01 00:00:00
img: /assets/ood-thumbnail.jpg
img_alt: Autonomous driving scene with object detection bounding boxes highlighting pedestrians and cars
description: |
  Novel framework integrating OOD detection into DINO self-supervised pretraining via a dynamic memory buffer — improving rare-object precision and recall on long-tailed autonomous driving datasets.
tags:
  - Computer Vision
  - Deep Learning
  - Self-Supervised Learning
type: project
---

**GitHub:** [Lake-Wang/OOD\_Enhanced\_Dino\_Vision](https://github.com/Lake-Wang/OOD_Enhanced_Dino_Vision)

## The Problem

Standard self-supervised learning methods like DINO and SimCLR learn powerful visual representations — but on long-tailed datasets, the training signal is dominated by frequent classes. Rare objects get underrepresented in the learned embedding space. In safety-critical domains like autonomous driving, this is directly consequential: the objects that appear least often (pedestrians, cyclists, unusual vehicles) are often the ones where failure matters most.

## Pipeline

![OOD Detection and SSL Integration Pipeline](/assets/ood-flowchart.png)

The framework integrates OOD detection directly into the SSL pretraining loop without requiring any labels, in three stages:

**Step 1 — Threshold calibration:** A sample of augmented images is passed through the encoder to compute embedding statistics (mean, covariance). These determine the distance threshold for flagging rare samples.

**Step 2 — Memory buffer warmup:** A warmup pass populates the FIFO memory buffer with OOD-flagged samples before training begins, ensuring the buffer isn't empty in early iterations.

**Step 3 — SSL training loop:** Each training batch is passed through the OOD detector. Samples whose embedding distance from the mean exceeds the threshold are flagged as rare and routed into the memory buffer. Each batch fed to DINO concatenates regular samples with rare samples drawn from the buffer.

## Results

Experiments used the BDD10K dataset with per-pixel semantic labels. Because the memory buffer must be populated with *truly* rare samples to be useful, **precision is the primary metric** — false positives waste buffer capacity on common objects.

| Pre-trained Model | Threshold | Precision | Recall | F1 |
|---|---|---|---|---|
| Random baseline | — | 0.158 | — | — |
| DINO-ImageNet | 0.80 | 0.184 | 0.209 | 0.196 |
| **DINO-BDD100K** | **0.80** | **0.202** | **0.244** | **0.221** |

The domain-adapted model (pretrained on BDD100K rather than ImageNet) consistently outperforms across all threshold settings — confirming that in-domain pretraining produces a better embedding space for distinguishing rare driving-scene objects. At the 0.80 threshold, DINO-BDD100K achieves a 28% precision improvement over the random baseline.

## Context

NYU capstone project, mentored by Mengye Ren and Chris Hoang. The research question — how to make SSL more equitable across frequency tiers without labels — generalizes beyond computer vision. Any domain where the hardest cases are also the rarest faces the same underlying problem.
