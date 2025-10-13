# 🔋 Battery SOH Estimation Using GCN-LSTM

This repository provides the official implementation of the paper:

> **State-of-health estimation for fast-charging lithium-ion batteries based on a short charge curve using graph convolutional and long short-term memory networks**  
> *Yuxin He, Zhongwei Deng, Jue Chen, Weihan Li, Jingjing Zhou, Fei Xiang, Xiaosong Hu*  
> [📄 Paper PDF (ScienceDirect)]([[https://doi.org/10.1016/j.jechem.2024.06.024]]
---

## 📖 Abstract

An efficient health estimation method based on **short-term charging data**, integrating **Graph Convolutional Networks (GCN)** and **Long Short-Term Memory (LSTM)** networks, is proposed to accurately estimate the health of batteries during fast charging.  
The method extracts short charging segments around current switch points, transforms them into graphical representations, and employs a hybrid GCN–LSTM architecture to capture both **local** and **temporal** degradation features.  
Extensive experiments on **185 cells and 81 fast-charging policies** validate the high accuracy and generalization capability of the proposed method (MAE = 0.34%, RMSE = 0.66%).

---

## ⚙️ Method Overview

### 🔹 Technical Roadmap
![Method Overview](figs/Fig4_Methodology.png)
> **Fig. 4.** Schematic of the proposed method:  
> (a) charging segment extraction, (b) structure of the GCN-LSTM model, and (c) complete workflow for SOH estimation.

---

## 📊 Dataset and Preprocessing

### 🔹 MIT–Stanford Battery Dataset
![Dataset Overview](figs/Fig1_MIT_Stanford.png)
> **Fig. 1.** (a) Examples of fast-charging policies; (b) aging trajectories under 81 distinct policies.

### 🔹 Feature Extraction and Correlation
![Feature Extraction](figs/Fig2_FeatureExtraction.png)
![Correlation Analysis](figs/Fig3_Correlation.png)
> **Figs. 2–3.** Voltage sequence extraction near current switching points and correlation distributions of extracted features across different durations.

---

## 🧠 Model Architecture

### 🔹 GCN-LSTM Structure
![GCN-LSTM Model](figs/Fig5_ModelStructure.png)
> **Fig. 5.** Architecture of the proposed GCN–LSTM model, combining spatial and temporal feature extraction.

### 🔹 Network Configuration
| Layer | Type | Output | Activation |
|:------|:-----|:--------|:-----------|
| 1 | GCNConv | 80 | ReLU |
| 2 | GCNConv | 40 | ReLU |
| 3 | LSTM | 10 | — |
| 4 | FC | 1 | — |

---

## 🧪 Experimental Results

### 🔹 SOH Estimation under Different Fast-Charging Policies
![SOH Results](figs/Fig6_Results.png)
> **Fig. 6.** Comparison between predicted and actual SOH values across six representative charging policies.

### 🔹 Estimation Errors
![Error Distribution](figs/Fig7_Errors.png)
> **Fig. 7.** Distribution of MAE and RMSE for 185 cells.

### 🔹 Comparative Performance
![Comparison with Other Methods](figs/Fig9_Comparison.png)
> **Fig. 9.** Comparison between traditional ML (SVR, RFR, GPR) and deep learning (GCN, LSTM, GCN-LSTM) models.

---

## 📈 Sensitivity Analysis

![Duration Influence](figs/Fig12_DurationEffect.png)
> **Fig. 12.** Influence of charging segment duration (2, 4, 6 min) on estimation accuracy.

![Results by Duration](figs/Fig13_DurationResults.png)
> **Fig. 13.** SOH estimation results at different segment durations.

---

## 📦 Repository Structure
