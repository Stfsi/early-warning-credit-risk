# Early Warning Credit Risk

## TL;DR
This project explores **early-warning credit risk modeling** using the German Credit dataset.  
The focus is not on automating credit decisions, but on understanding **risk signals, trade-offs, and limitations** through interpretable models, appropriate evaluation metrics, and a governance-aware analytical workflow.

---

## Overview

This repository contains an **early-warning credit risk modeling project** designed as a structured, reproducible analysis.  
The work examines how statistical and machine-learning models can support **early identification of elevated credit risk**, while maintaining interpretability, validation discipline, and explicit acknowledgment of uncertainty.

The project is exploratory and educational in nature and does **not** claim production readiness.

---

## Project objectives

- Identify structural drivers associated with credit default risk  
- Compare baseline and benchmark models from an early-warning perspective  
- Evaluate models using metrics suited to **imbalanced classification**  
- Emphasize interpretability, validation, and responsible use  

The intent is to **support human judgment**, not replace it.

---

## Repository structure

early-warning-credit-risk/
├─ 01_dataset/
│ └─ german.data
├─ 02_notebooks/
│ ├─ 01_EDA.ipynb
│ ├─ 02_data_preprocessing.ipynb
│ └─ 03_modeling_and_validation.ipynb
├─ 04_figures/
│ ├─ eda_class_balance.png
│ ├─ eda_credit_amount_age_distribution.png
│ ├─ eda_bad_rate_credit_history_purpose_housing.png
│ ├─ modeling_and_validation_ROC_curves_test.png
│ ├─ modeling_and_validation_precision_recall_curves_test.png
│ └─ modeling_and_validation_precision_recall_curves_test_baseline_vs_benchmark.png
├─ .gitignore
└─ README.md


---

## Notebooks

### 1. Exploratory Data Analysis (`01_EDA.ipynb`)
- Class balance and baseline risk assessment  
- Distributional analysis (e.g., age, credit amount)  
- Relationships between credit history, purpose, housing, and default risk  

### 2. Data preprocessing (`02_data_preprocessing.ipynb`)
- Feature encoding and transformation  
- Train/test split  
- Preprocessing designed to avoid data leakage  

### 3. Modeling and validation (`03_modeling_and_validation.ipynb`)
- Baseline vs benchmark models  
- ROC and Precision–Recall evaluation on test data  
- Comparison of performance trade-offs relevant to early warning systems  

---

## Modeling perspective

The modeling approach prioritizes:

- Early detection of elevated risk rather than final decisioning  
- Metrics that reflect asymmetric error costs  
- Transparency and traceability over maximal predictive power  

Precision–recall analysis is emphasized, as it better reflects performance under class imbalance.

---

## Results

### Classification performance

- Benchmark models demonstrate improved discriminatory power relative to the baseline.  
- ROC curves show moderate gains, while Precision–Recall curves reveal clearer differences in early-warning–relevant regions.  
- Improved recall is achieved at the cost of reduced precision, highlighting the trade-off between sensitivity and false positives.  

All performance visualizations are available in `04_figures/`.

---

## Analysis

### Early-warning interpretation

From an early-warning perspective:

- Model value lies in its ability to **surface elevated risk earlier**, even if conservative.  
- Performance should be interpreted in terms of **screening utility**, not final approval accuracy.  
- Threshold selection remains application-specific and intentionally unconstrained here.

---

### Interpretability and robustness

- Feature effects align with established credit risk drivers (credit history, financial burden, purpose).  
- No opaque feature engineering was introduced.  
- Model behavior is stable across training and test sets, supporting internal consistency.

---

### Limitations

- The dataset is small and static, limiting external validity.  
- Historical patterns may encode socio-economic bias.  
- No calibration, fairness metrics, or monitoring framework is implemented.  
- Results are context-dependent and not generalizable without further validation.

---

### Governance considerations

The results illustrate key governance tensions in credit modeling:

- Increased sensitivity improves early detection but raises operational and ethical questions.  
- Model outputs should be treated as **signals**, not prescriptions.  
- Any deployment would require additional validation, documentation, and oversight layers.

---

## Summary

This project demonstrates that:

- Early-warning credit risk modeling can be informative even with modest data.  
- Evaluation must go beyond accuracy and ROC-AUC.  
- Responsible use requires explicit acknowledgment of uncertainty and limits.

The primary contribution is not prediction alone, but a **structured, governance-aware analytical process**.

---

## Next steps (out of scope)

- Fairness and bias diagnostics  
- Model calibration and threshold optimization  
- Stress testing under distribution shift  
- Formal validation and governance documentation  

---

*This repository is intended for analytical demonstration and learning purposes only.*

**Author**: Stéphanie Simon  
**Focus**: Credit risk analysis, model governance, responsible analytics  
