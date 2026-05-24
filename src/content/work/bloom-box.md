---
title: Automated Medical Coding at XpertDox
publishDate: 2025-10-01 00:00:00
img: /assets/stock-1.jpg
img_alt: Abstract visualization of a neural network processing medical data
description: |
  End-to-end ML system for automated CPT, ICD, and billing classification — scaling prediction capacity from 200 to 2,000 codes while processing 100K+ claims weekly in production.
tags:
  - Clinical NLP
  - Production ML
  - Transformers
  - Healthcare
---

## Overview

At XpertDox, I own the full ML lifecycle for automated medical coding — one of the highest-stakes applications of NLP, where a misclassification carries direct financial and clinical consequences. The system covers CPT, ICD, and billing classification across 2,000 codes, processing over 100,000 claims weekly across 80 production machines.

## What I Built

The core model is a domain-adaptive transformer pretrained specifically on clinical documentation — scoped precisely to the operational task rather than general-purpose pretraining. This required careful curation of training data, custom tokenization aligned to medical terminology, and an architecture tuned for the label distribution of real coding workflows.

I also redesigned the full data pipeline and infrastructure, cutting pipeline processing time by 83% through architectural changes that removed bottlenecks in ingestion, transformation, and batch inference.

## Production Role of the Model

The system operates in two deliberate modes suited to high-stakes clinical environments:

- **Confidence signal**: When the model and an independent coding procedure agree, mandatory human review is eliminated — reducing review load by 64%.
- **Auditor**: The model generates approximately 600 weekly suggestions where its learned patterns diverge from established coding rules, flagging edge cases for expert review.

## Ongoing Ownership

Production ownership means more than deploying and monitoring dashboards. I review outputs weekly, personally interrogate production data to surface patterns that automated monitoring alone wouldn't catch, and translate findings into model changes within days. The system runs on a continuous monitoring and monthly retraining cycle to handle coding guideline updates and distribution shift.
