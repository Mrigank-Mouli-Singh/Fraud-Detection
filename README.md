# Fraud Detection with Machine Learning

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/18PbvB_Cyeo6qE-MrDtuY6S8DrMt1NL3l?usp=sharing)
[![Python](https://img.shields.io/badge/Python–3.12-blue)](https://www.python.org/)
[![LightGBM](https://img.shields.io/badge/LightGBM-GradientBoosting-green)](https://lightgbm.readthedocs.io/)

## Overview
This project implements a **fraud detection system** using machine learning on a dataset of **6.3M+ transactions**, where only ~0.13% are fraudulent.  
The goal is to build a highly accurate and interpretable model that can detect fraud in real time while providing insights into key risk factors.

---

## Links
- ** Colab Notebook:** [Open in Colab](https://colab.research.google.com/drive/18PbvB_Cyeo6qE-MrDtuY6S8DrMt1NL3l?usp=sharing)  
- ** GitHub Repo:** [Fraud-Detection](https://github.com/Mrigank-Mouli-Singh/Fraud-Detection)

---

## Dataset
- **Records:** ~6.36 million  
- **Features:** Transaction amount, balances, transaction type, merchant flags, timestamps, fraud label  
- **Challenge:** High class imbalance (fraud cases are only ~0.13%)

---

## Methodology

### 🔹 Data Processing & Feature Engineering
- Engineered features like `deltaOrig`, `amt_to_org_bal`, log transforms, and time-based (`hour`, `day`).  
- Encoded categorical transaction types into `type_code`.  
- Created merchant and cash-out flags for better fraud detection.  

### 🔹 Handling Imbalance
- Used LightGBM’s `scale_pos_weight` to balance fraud vs. non-fraud classes.  
- Optimized evaluation on **PR-AUC**, more suitable for rare-event detection.  

### 🔹 Model Training
- Algorithm: **LightGBM Gradient Boosting**  
- Hyperparameter Tuning: **Optuna (20 trials)**  
- Early stopping and regularization for robustness.  

### 🔹 Evaluation
- **ROC-AUC:** 0.9998  
- **PR-AUC:** 0.90  
- Achieved **99% recall** at threshold optimization with acceptable precision.  

### 🔹 Model Interpretability (SHAP)
- **Top features:**  
  - `amt_to_org_bal` → Large proportion of transaction relative to account balance.  
  - `deltaOrig`, `oldbalanceDest` → Unusual balance changes.  
  - `type_code` → Transfers & Cash-outs most fraud-prone.  
- Local SHAP analysis explains individual flagged transactions.  

---

## Business Insights

- Fraudsters often:  
  - Transfer unusually large amounts compared to available balance.  
  - Use cash-out and transfer transactions.  
  - Exploit suspicious/new merchant accounts.  

- **Recommendations:**  
  - Flag transactions where `amt_to_org_bal > 80%`.  
  - Apply stricter review for transfers & cash-outs.  
  - Profile new merchants with sudden inflows.  
  - Deploy real-time fraud scoring with human-in-the-loop review.  

---

## Deliverables

- `FraudDetection.ipynb` – End-to-end notebook  
- `final_fraud_lgb.txt` – Trained LightGBM model  
- CSV outputs:  
  - `feature_importance.csv`  
  - `shap_feature_importance.csv`  
  - `shap_fraud_only.csv`  
  - `shap_type_influence.csv`  
- `final_metrics.json` – Model performance metrics  
- `validation_predictions.csv` – Predictions with optimized thresholds  

---

## Author
**Mrigank Mouli Singh**  
B.Tech CSE, IIIT Sonepat (2022–2026)  
[LinkedIn](https://www.linkedin.com/in/mrigank-mouli-singh/) | [GitHub](https://github.com/Mrigank-Mouli-Singh)  


---
