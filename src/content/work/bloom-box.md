---
title: Automated Medical Coding at XpertDox
publishDate: 2025-10-01 00:00:00
img: /assets/xpertdox-thumbnail.png
img_alt: Medical coder reviewing ICD-10, CPT, and HCPCS codes on dual monitors
description: |
  Full-stack ML ownership for automated ICD, CPT, and billing classification — production models operating at scale across a distributed fleet, substantially reducing mandatory human review.
tags:
  - Clinical NLP
  - Production ML
  - Healthcare
  - MLOps
type: experience
---

## What the System Does

XpertDox automates medical coding for healthcare clients. When a patient visit ends, clinical documentation — notes, diagnoses, procedures — needs to be translated into standardized codes for reimbursement. This is traditionally done by human coders. The ML system augments and partially automates that process at scale, processing 100K+ claims weekly across a distributed production fleet.

## My Role

I own the full ML lifecycle: architecture, training, deployment, monitoring, and iteration. The platform has expanded from a narrow ICD classifier to a system covering CPT, ICD, and billing classification across 2,000 codes — with pipeline infrastructure redesigned end-to-end, cutting processing time by 83%.

The core work involves building a domain-adaptive transformer pretrained specifically on clinical text, scoped to fit the task within real operational constraints. Production ownership spans ~80 machines: reviewing outputs weekly, personally interrogating production data to surface patterns automated monitoring misses, and shipping model changes within days of a meaningful finding.

## How the Models Create Business Value

The production system is designed around two deliberate roles suited to high-stakes clinical workflows.

**Confidence signal** — when model output and established coding procedure converge, the case clears without mandatory human review. This reduces downstream review load by 64% across the pipeline.

**Auditor** — when model predictions diverge from established coding rules, those cases surface as ~600 weekly suggestions that flag potential refinements to deterministic coding logic. Rather than treating divergences as noise, the system treats them as signal worth examining.

Both roles are deliberate: in clinical settings, a model earns its place not by replacing human judgment, but by being useful precisely where its perspective differs from established practice.

## Engineering and Ownership

Production ownership at this scale extends well beyond training and deploying models:

- Redesigning data infrastructure to cut pipeline processing time by 83% end-to-end
- Weekly review of model outputs alongside human coding experts
- Direct interrogation of production data to surface patterns automated monitoring misses
- Continuous performance monitoring and regular retraining to handle coding guideline updates and distribution shift
