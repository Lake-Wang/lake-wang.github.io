---
title: NBA Game Attendance Prediction — MLOps Pipeline
publishDate: 2025-04-01 00:00:00
img: /assets/stock-1.jpg
img_alt: Dashboard showing model performance metrics and data drift monitoring
description: |
  Two-stage PyTorch pipeline predicting NBA game attendance from game intensity and weather signals — with FastAPI serving, ONNX optimization, MLflow experiment tracking, and Alibi drift detection.
tags:
  - MLOps
  - PyTorch
  - FastAPI
  - MLflow
---

## Motivation

NBA schedules and resource allocation are rarely optimized for fan interest. This project builds an ML tool that forecasts game attendance using game intensity signals and contextual factors, giving the league a data-driven basis for scheduling decisions, targeted promotions, and dynamic ticket pricing.

## Two-Stage Pipeline

The core modeling approach is a chained two-stage architecture:

**Stage 1 — Game intensity modeling:** A PyTorch MLP predicts point differential from rolling 5-game team statistics. Point differential serves as a proxy for expected game excitement — a close, high-stakes matchup drives different attendance patterns than a blowout.

**Stage 2 — Attendance prediction:** A second PyTorch MLP takes the predicted score margin alongside weather data (temperature, wind, precipitation) to forecast game attendance. Both models are exported to ONNX with graph and quantization optimizations for efficient inference.

## Data Pipeline

Three seasons of data (2022–25) are pulled from the NBA API for box scores and attendance, and from WeatherAPI/Open-Meteo for game-day conditions. Rolling averages are computed season-wise with strict splits to prevent leakage, and weather is joined by game date and arena location.

## Serving and Monitoring

A FastAPI endpoint accepts a game date, home team, and away team — then runs both model stages in sequence to return a predicted attendance figure. The system supports both `.pth` and ONNX backends with staging and fallback logic.

Online evaluation is handled with Alibi Detect, which monitors incoming feature distributions against training baselines and surfaces drift alerts. MLflow tracks offline experiments — parameters, metrics, and model artifacts — across training runs.

## Infrastructure and Role

Training ran on A100 GPUs via Chameleon Cloud (KVM@TACC) with distributed data parallel across two VMs. My focus within the three-person team was model serving and monitoring — the FastAPI backend, ONNX export, and Alibi integration.

The NBA is an accessible domain. The point of the project is the infrastructure: what it takes to move beyond a notebook and into a system that can be served, monitored, and trusted.
