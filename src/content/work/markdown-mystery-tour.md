---
title: End-to-End MLOps Pipeline — NBA Attendance Prediction
publishDate: 2025-04-01 00:00:00
img: /assets/stock-1.jpg
img_alt: Dashboard showing model performance metrics and monitoring charts
description: |
  Full MLOps pipeline predicting NBA game attendance using PyTorch and team/weather features — with FastAPI serving, ONNX optimization, MLflow tracking, and Prometheus drift monitoring.
tags:
  - MLOps
  - PyTorch
  - FastAPI
  - MLflow
---

## Overview

An end-to-end MLOps pipeline built to predict NBA game attendance, covering the full lifecycle from raw data to a monitored production deployment. The project was designed to demonstrate real MLOps discipline — not just model training, but the infrastructure that makes a model usable and trustworthy over time.

## Pipeline Architecture

**Data layer:** Ingestion, transformation, and storage pipeline pulling team statistics, opponent data, and weather features. Feature engineering handles missing values, categorical encoding, and temporal alignment across seasons.

**Modeling:** PyTorch models trained with MLflow experiment tracking — logging parameters, metrics, and artifacts across runs for reproducibility and comparison. Models are exported to ONNX format for optimized inference.

**Serving:** FastAPI backend exposing prediction endpoints with a user-facing frontend for interactive inference. ONNX runtime reduces latency compared to full PyTorch serving.

**Monitoring:** Prometheus integration tracks real-time data drift and model performance degradation — alerting when incoming feature distributions shift significantly from training data.

## What This Demonstrates

The NBA domain is intentionally approachable — the interesting work is the infrastructure. This project shows what it takes to move a model from notebook to a system that can be monitored, updated, and trusted: versioned experiments, optimized serving, and observability baked in from the start.
