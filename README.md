# Residual Load Forecasting using LSTM and CNN-LSTM: A Deep Learning Approach

## Overview
This project focuses on **short-term residual load forecasting** for the Swiss electricity system using deep learning techniques.

Residual load is defined as:
> **Total electricity demand – (solar generation + wind generation)**

Accurate forecasting of residual load is critical for:
- Grid stability
- Energy planning
- Renewable integration

This project compares multiple deep learning architectures and demonstrates that **feature engineering plays a more important role than model complexity**.

---

## Problem Statement
Predict **residual load one hour ahead (t+1)** using only information available up to time **t**, ensuring a realistic and leakage-free forecasting setup.

---

## Dataset
### Sources
- **Swissgrid**
  - Electricity demand
  - Wind generation
  - Solar generation

- **ERA5 (Weather Data)**
  - Temperature
  - Wind speed
  - Solar radiation
  - Pressure

### Characteristics
- Hourly time-series data
- Time period: 2022 – 2025
- Spatial weather grids: **21 × 48 resolution**

---

## Key Features & Engineering

### Temporal Features
- Lagged values: (t-1, t-2, t-24)
- Rolling statistics (moving averages)
- Calendar features:
  - Hour of day
  - Day of week
  - Month

### Spatial Features
- Weather data represented as **2D grids**
- Used in CNN-based models

---

## Models Implemented

### 1. Lagged LSTM (Best Performer)
- Uses engineered temporal features
- Short input sequences
- Stable and efficient

### 2. CNN-LSTM (CNN3LSTM)
- CNN extracts spatial features from weather grids
- LSTM models temporal evolution

### 3. GCN-LSTM (Experimental)
- Graph-based spatial modeling
- Did not outperform simpler models

---

## Model Architecture

### CNN-LSTM Pipeline
1. CNN extracts spatial patterns from weather grids  
2. Feature maps passed to LSTM  
3. LSTM predicts future residual load  

---

## Training Strategy
- Strict chronological data split:
  - Train: 2022 – early 2024
  - Validation: mid 2024 – mid 2025
  - Test: late 2025

- Prevented **data leakage**
- Real-world forecasting setup

---

## Hyperparameter Optimization
- Framework: **Optuna**
- Tuned:
  - Learning rate
  - Hidden sizes
  - Dropout
  - Optimizers (Adam, RMSprop, SGD)

---

## Results

### Key Findings
- **Lagged LSTM outperformed all complex models**
- ~60% improvement after tuning
- CNN-LSTM and GCN-LSTM did not provide gains

### Insight
> Strong feature engineering + proper tuning > complex architectures

---
