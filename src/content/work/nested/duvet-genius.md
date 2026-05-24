---
title: OOD-Enhanced Self-Supervised Visual Learning
publishDate: 2024-09-01 00:00:00
img: /assets/stock-3.jpg
img_alt: Abstract visualization of a neural network distinguishing rare objects in a dataset
description: |
  Novel OOD detection pipeline integrated into DINO self-supervised pretraining — achieving a 47% increase in rare object identification on autonomous driving datasets.
tags:
  - Computer Vision
  - Deep Learning
  - Self-Supervised Learning
---

## Overview

Self-supervised learning methods like DINO learn powerful visual representations — but they tend to underfit rare classes, because the training signal is dominated by frequent objects. In safety-critical domains like autonomous driving, this is a real problem: the rare cases are often the most important ones.

This project developed a novel pipeline that integrates out-of-distribution (OOD) detection directly into the SSL pretraining loop, prioritizing rare samples to improve balanced representation learning.

## Method

**OOD detection with dynamic memory buffer:** We built an OOD detector that maintains a running buffer of training embeddings. Samples whose representations are far from the buffer's distribution — likely rare or underrepresented objects — are flagged and upweighted during pretraining.

**Integration with DINO:** The OOD signal is used to modulate the self-supervised loss, giving the model stronger training signal on rare and difficult samples without requiring any labels.

**Dataset:** Evaluated on BDD100K, a large-scale autonomous driving dataset with a long-tailed object distribution — pedestrians, cyclists, and unusual vehicle types are significantly underrepresented relative to cars.

## Results

- **47% increase in true positive rate** (from a base of 22%) for rare object identification
- Improved feature representations for safety-critical classes in autonomous driving scenarios
- The dynamic memory buffer approach generalizes beyond DINO and could be applied to other SSL methods

## Context

This was a NYU capstone project, but the problem it addresses is real: SSL pretraining at scale doesn't automatically produce fair representations, and in deployment contexts where rare-class performance matters most, that gap has consequences.
