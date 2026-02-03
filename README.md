# Early Warning Credit Risk Modeling  
**Interpretable, governance-oriented risk analytics**

## TL;DR
This project builds an **early warning credit risk model** using the German Credit dataset, prioritizing **interpretability, auditability, and governance** over automated decision-making.

Interpretable logistic models are evaluated against a Random Forest benchmark to illustrate **performance–transparency trade-offs** typical of regulated environments such as **banking, insurance, and audit**.

---

## Overview
This repository develops a **governance-ready early warning credit risk pipeline** designed to support **risk identification and human review**, not automated approval or rejection decisions.

The project emphasizes:
- Interpretability over raw predictive performance  
- Explicit target definition and documentation  
- Strict separation between EDA, preprocessing, modeling, and evaluation  
- Reproducible, reviewable artifacts suitable for audit and validation  

The structure mirrors how models are typically developed and assessed in **regulated financial institutions**.

---

## Why early warning credit risk?
Early warning systems aim to detect **elevated risk before default**, enabling organizations to:
- Prioritize accounts for human review  
- Allocate monitoring and oversight resources  
- Manage trade-offs between false positives and missed risk events  

In regulated contexts, models must be **explainable, reviewable, and defensible**—not merely accurate.

---

## Dataset
**Source:** German Credit Dataset (UCI Machine Learning Repository)  
**Observations:** 1,000  

**Target variable**
- Original encoding:  
  - `1` = good credit  
  - `2` = bad credit  

**Early warning event definition**
- `y_bad = 1` → bad credit (risk event)  
- `y_bad = 0` → good credit  

**Event rate:** ~30%

The target definition is **explicitly defined, validated, and frozen during EDA** to prevent downstream analytical drift.

---

## Repository structure

early-warning-credit-risk/
│
├── 01_dataset/
│   └── german.data
│
├── 02_notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_data_preprocessing.ipynb
│   └── 03_modeling_and_validation.ipynb
│
├── 03_artifacts/
│   ├── notebook01/
│   ├── notebook02/
│   └── notebook03/
│
├── 04_figures/
│   ├── eda_*.png
│   └── modeling_evaluation_*.png
│
└── README.md
Artifacts are generated under `03_artifacts/` and **selectively versioned** to support interpretation, validation, and auditability.

---

## Methodology

### 1. Exploratory Data Analysis & Target Definition (Notebook 01)

**Objectives**
- Validate data integrity and structure  
- Define and freeze the early warning target  
- Analyze class imbalance and event prevalence  
- Verify plausible credit risk signals  

**Key outputs**
- `data_dictionary.csv`  
- `missingness_report.csv`  
- `german_credit_with_y_bad.csv`  
- `run_metadata.json`  
- EDA figures (class balance, distributions, bad rates by variable)  

**Governance principle**  
No preprocessing or modeling decisions are made **before the target definition is finalized and documented**.

---

### 2. Preprocessing & Interpretable Models (Notebook 02)

**Design choices**
- Stratified train/test split  
- Preprocessing pipelines fit **only on training data**  
- Numeric features: median imputation + standardization  
- Categorical features: most-frequent imputation + one-hot encoding  
- Explicit leakage prevention (raw target columns excluded)  

**Models**
- Logistic Regression (interpretable baseline)  
- L1-regularized Logistic Regression (feature sparsity and stability)  

**Key governed outputs**
- Fitted pipelines  
  - `pipeline_logistic.joblib`  
  - `pipeline_l1_logistic.joblib`  
- Train/test splits  
  - `X_train.csv`, `X_test.csv`, `y_train.csv`, `y_test.csv`  
- Probability outputs  
  - `train_predictions.csv`, `test_predictions.csv`  
- Execution metadata  
  - `run_metadata.json`

---

### 3. Evaluation & Benchmarking (Notebook 03)

Evaluation focuses on **early warning performance**, not accuracy alone.

**Metrics**
- ROC-AUC (ranking performance)  
- PR-AUC (more informative under class imbalance)  
- Threshold-based precision, recall, and false positive rate  

Threshold selection is treated as a **governance decision**, reflecting operational capacity and risk tolerance.

**Benchmark model**
- Random Forest trained on the **same governed train/test split**  
- Uses the **same fitted preprocessing transformer** learned by the logistic baseline  
- Included strictly as a **performance reference**, not as a default deployment model  

---

## Results (test set)

| Model                     | ROC-AUC | PR-AUC |
|---------------------------|--------:|-------:|
| Logistic Regression       | ~0.78   | ~0.61  |
| L1 Logistic Regression    | ~0.78   | ~0.62  |
| Random Forest (benchmark) | ~0.82   | ~0.70  |

**Key takeaway**
- Interpretable models provide strong early warning signals  
- Performance gains from more complex models come with **reduced transparency and governance challenges**

---

## Figures
The `04_figures/` directory contains:
- EDA figures (class balance, distributions, bad rates by variable)  
- ROC and Precision–Recall curves for baseline and benchmark models  

These figures support **model interpretation and review**, not presentation-only reporting.

---

## Governance & reproducibility
This project explicitly demonstrates:
- Separation of analytical responsibilities across stages  
- Frozen targets and documented assumptions  
- Selective artifact versioning  
- Reproducible pipelines without requiring reviewers to re-run notebooks  

Key evaluation outputs include:
- `baseline_metrics.csv`  
- `all_model_metrics.csv`  
- `threshold_table.csv`  

These files support **auditability, validation, and independent review**.

---

## What this project is (and is not)

**This project is**
- A decision-support modeling exercise  
- Designed for regulated environments  
- Focused on transparency, traceability, and governance  

**This project is not**
- An automated credit approval system  
- A production deployment  
- An optimization exercise that sacrifices interpretability  

---

## Author
**Stéphanie Simon**  
Statistics student (B.Sc. Mathematics – Statistics)  
Interests: risk analytics, audit analytics, model governance  
