---
title: Automated Medical Coding at XpertDox
publishDate: 2025-10-01 00:00:00
img: /assets/xpertdox-thumbnail.png
img_alt: Medical coder reviewing ICD-10, CPT, and HCPCS codes on dual monitors
description: |
  Full-stack ML ownership for automated medical coding — production models serving a large distributed clinical fleet, with direct accountability for accuracy, reliability, and business impact.
tags:
  - Clinical NLP
  - Production ML
  - Healthcare
  - MLOps
type: experience
---

## What the System Does

XpertDox automates medical coding for healthcare clients. Clinical documentation — notes, diagnoses, procedures — needs to be translated into standardized codes for reimbursement, a process traditionally done by human coders. The ML system augments and partially automates this at scale across a large production fleet.

## My Role

I own the full ML lifecycle: architecture, training, deployment, monitoring, and iteration. This includes building domain-adaptive models pretrained on clinical text, redesigning data infrastructure end-to-end, and maintaining direct production accountability — reviewing outputs regularly, personally interrogating production data to surface issues automated monitoring misses, and shipping changes quickly based on findings.

## How the Models Create Business Value

The production system is designed around two deliberate roles in clinical workflows.

The first serves as a **confidence signal** — enabling cases where model output aligns with established coding logic to clear without mandatory human review, substantially reducing downstream review burden.

The second serves as an **auditor** — surfacing cases where model predictions diverge from established coding rules as actionable suggestions for potential refinement. Divergences are treated as signal rather than noise.

Both roles reflect the same principle: in high-stakes clinical settings, a model earns its place not by replacing human judgment, but by being useful precisely where its perspective adds something distinct from established practice.

## Engineering and Ownership

Production ownership extends well beyond training and deploying models:

- Redesigning data infrastructure to substantially reduce pipeline processing time end-to-end
- Regular review of model outputs alongside human coding experts
- Direct interrogation of production data to surface patterns automated monitoring misses
- Continuous performance monitoring and retraining to handle coding guideline updates and distribution shift
