---
title: NBA Game Attendance Prediction — MLOps Pipeline
publishDate: 2025-04-01 00:00:00
img: /assets/nba-mlops-diagram.png
img_alt: System architecture diagram showing data pipeline, model training, and serving infrastructure on Chameleon Cloud
description: |
  Two-stage PyTorch pipeline predicting NBA game attendance from game intensity and weather signals — with Airflow orchestration, MLflow tracking, and FastAPI/Triton serving on Chameleon Cloud.
tags:
  - MLOps
  - PyTorch
  - FastAPI
  - MLflow
type: project
---

## Motivation

NBA schedules and resource allocation are rarely optimized for fan interest. This project builds an ML tool that forecasts game attendance using game intensity signals and contextual factors, giving the league a data-driven basis for scheduling decisions, targeted promotions, and dynamic ticket pricing.

## Two-Stage Pipeline

The core modeling approach is a chained two-stage architecture:

**Stage 1 — Game intensity modeling:** A PyTorch MLP predicts point differential from rolling 5-game team statistics. Point differential serves as a proxy for expected game excitement — a close, high-stakes matchup drives different attendance patterns than a blowout.

**Stage 2 — Attendance prediction:** A second PyTorch MLP takes the predicted score margin alongside weather data (temperature, wind, precipitation) to forecast game attendance. Both models are optimized with ONNX graph and quantization passes for efficient inference.

## Infrastructure

![NBA MLOps System Architecture](/assets/nba-mlops-diagram.png)

The system runs across three nodes on Chameleon Cloud (KVM@TACC), connected via a shared network:

- **Data pipeline:** Airflow orchestrates ingestion from the NBA API and weather sources into Postgres, with artifacts stored in a persistent object store
- **Training:** A two-GPU server runs distributed PyTorch training with MLflow and MinIO for experiment tracking and artifact management
- **Serving:** A separate GPU server hosts Flask + FastAPI/Triton endpoints, supporting both `.pth` and ONNX backends with staging and fallback logic

## Online Evaluation

Rather than static holdout metrics alone, the system uses Alibi Detect to monitor incoming feature distributions against training baselines and surface drift alerts in real time. Synthetic data generated with Gaussian noise and date shifts was used to validate the detection pipeline.

## Team and Role

Three-person project (NYU MS capstone). My focus was model serving and monitoring — the FastAPI/Triton backend, ONNX export pipeline, and Alibi integration. The NBA domain is intentionally approachable; the point is the infrastructure: what it takes to move a model from a notebook into a system that can be served, monitored, and maintained.
