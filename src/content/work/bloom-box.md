---
title: Automated Medical Coding at XpertDox
publishDate: 2025-10-01 00:00:00
img: /assets/stock-1.jpg
img_alt: Abstract visualization of a machine learning system processing clinical documents
description: |
  Full-stack ML ownership for automated ICD, CPT, and billing classification — two complementary model architectures operating in production across 100K+ weekly claims, cutting mandatory human review by 64%.
tags:
  - Clinical NLP
  - Production ML
  - Healthcare
  - MLOps
---

## What the System Does

XpertDox automates medical coding for healthcare clients. When a patient visit ends, clinical documentation — notes, diagnoses, procedures — needs to be translated into standardized codes for reimbursement. This is traditionally done by human coders. The ML system augments and partially automates that process at scale, processing 100K+ claims weekly across ~80 production machines.

## Two Complementary Models

The system runs two architecturally distinct models designed for different tradeoffs:

One is a fast, interpretable ensemble optimized for throughput — covering ~2,000 codes across CPT and ICD, with per-code thresholds tuned to each code's clinical importance. It's the production workhorse: changes ship within 2–3 days of identifying an issue, making it the primary vehicle for rapid iteration.

The other is a domain-adaptive transformer encoder pretrained specifically on clinical text. Where the ensemble learns sparse patterns, the transformer learns dense contextual representations of entire clinical documents — capturing the meaning of a note rather than just its surface features. It's built to generalize across unseen clients and coding environments without requiring client-specific retraining.

The two models are complementary: the ensemble handles speed and scale, the transformer handles generalization and depth.

## How the Models Create Business Value

The models serve two distinct roles in production, both designed around the realities of high-stakes clinical workflows:

**Confidence gate** — when the model and an established coding procedure independently agree, mandatory human review is skipped. The probability of both being simultaneously wrong is low enough to justify this. This reduces downstream review load by 64%.

**Auditor** — the model occasionally predicts differently from the procedure-derived labels it was trained on. Rather than treating this as noise, those divergences surface as ~600 weekly suggestions that flag potential refinements in deterministic coding rules. The model stress-tests its own training signal.

## Engineering and Ownership

Owning production ML at this scale means more than training and deploying models. The scope includes:

- Redesigning data infrastructure to cut pipeline processing time by 83%
- Weekly review of model outputs alongside human coding experts
- Direct interrogation of production data to surface patterns automated monitoring misses
- Continuous performance monitoring with monthly retraining to handle coding guideline updates and distribution shift

The development cycle for the transformer runs on a ~2-month cadence; the ensemble ships changes within days. Both are designed to be maintained and improved independently without destabilizing the other.
