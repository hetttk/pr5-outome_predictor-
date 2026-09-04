<div align="center">

# 🎓 Smart Outcome Predictor

### An Ensemble Machine Learning Project for Student Outcome Prediction

**Classification + Regression • Bagging • Boosting • Voting • Stacking**

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Used-189?logo=xgboost&logoColor=white)](https://xgboost.readthedocs.io/)
[![LightGBM](https://img.shields.io/badge/LightGBM-Used-9ACD32)](https://lightgbm.readthedocs.io/)

</div>

---

## 🚀 Project Snapshot

**Smart Outcome Predictor** is an ensemble-based machine learning system built around an EdTech-style student dataset. The project studies whether combining multiple learners can produce more stable and useful predictions than relying on a single Decision Tree.

The notebook solves **two related prediction problems**:

| Task | Target | What it predicts |
|---|---|---|
| 🟢 Classification | `completion_status` | Whether a student completes the course |
| 🔵 Regression | `final_score` | The student's final performance score |

The project follows the supplied **PR. 5** brief and covers bagging, boosting, voting, stacking, evaluation, interpretation, and a final deployment recommendation.

---

## 🎯 Why This Project Matters

Student performance is influenced by several connected factors such as engagement, assessment performance and attendance. A single model may miss part of that pattern.

This project compares different ensemble strategies to answer a practical question:

> **Can combining models give a better and more reliable view of student outcomes?**

The answer is studied experimentally rather than assumed in advance.

---

## 📊 Dataset at a Glance

- **5,200 student records**
- **19 original columns**
- Student engagement, assessment and course-related information
- Small missing-value groups in:
  - `time_spent_hours`
  - `avg_quiz_score`
  - `attendance_rate`

### Data preparation

```text
Raw Student Data
       │
       ├── Remove identifier: student_id
       │
       ├── Handle missing values
       │      ├── Numeric → median
       │      └── Categorical → most frequent value
       │
       ├── Convert course_start_date
       │      ├── start_month
       │      └── start_day
       │
       ├── One-hot encode categorical features
       │
       └── Train / Test Split
```

### Leakage control

The two targets are kept separate:

- **Classification:** `final_score` is excluded.
- **Regression:** `completion_status` is excluded.

This prevents one target from leaking into the prediction of the other.

---

## 🧠 Model Playground

### Classification models

| Model | Purpose |
|---|---|
| Decision Tree | Single-model baseline |
| Bagging Classifier | Reduce variance using multiple trees |
| AdaBoost Classifier | Sequentially focus on difficult observations |
| Gradient Boosting Classifier | Stage-wise boosted trees |
| LightGBM Classifier | Fast gradient boosting implementation |
| XGBoost Classifier | Strong boosted-tree comparison |
| Hard Voting | Majority vote from multiple classifiers |
| Soft Voting | Average model probabilities |
| Stacking Classifier | Base learners + meta-learner |

### Regression models

| Model | Purpose |
|---|---|
| Decision Tree | Single-model baseline |
| Bagging Regressor | Variance reduction through aggregation |
| AdaBoost Regressor | Sequential boosting for regression |
| Gradient Boosting Regressor | Stage-wise regression boosting |
| LightGBM Regressor | Fast boosted-tree regression |
| XGBoost Regressor | High-performance boosted-tree comparison |
| Stacking Regressor | Base regressors + meta-learner |

---

## 🏗️ Ensemble Flow

```text
                    SMART OUTCOME PREDICTOR
                              │
             ┌────────────────┴────────────────┐
             │                                 │
       CLASSIFICATION                     REGRESSION
             │                                 │
     Predict completion status          Predict final score
             │                                 │
     ┌───────┼────────┐                ┌───────┼────────┐
     │       │        │                │       │        │
   Bagging Boosting Voting          Bagging Boosting Stacking
     │       │        │                │       │        │
     └───────┴────────┘                └───────┴────────┘
             │                                 │
          Compare                           Compare
             │                                 │
       Best practical model              Best practical model
```

---

## 📈 Evaluation Metrics

### Classification

- **Accuracy** — overall correctness
- **Precision** — how many predicted completions were actually completions
- **Recall** — how many actual completions were identified
- **F1-score** — balance between precision and recall
- **ROC-AUC** — ranking quality across probability thresholds

### Regression

- **MAE** — average absolute prediction error
- **RMSE** — penalizes larger errors more strongly
- **R²** — proportion of variance explained by the model

---

## 🏆 Results Dashboard

### Classification — best scores from the supplied dataset

| Metric | Best Model | Score |
|---|---|---:|
| 🥇 Accuracy | Hard Voting | **0.7442** |
| 🥇 F1 | XGBoost | **0.6226** |
| 🥇 ROC-AUC | Soft Voting | **0.7929** |

### Full classification comparison

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Hard Voting | **0.7442** | **0.7081** | 0.5410 | 0.6134 | — |
| Gradient Boosting | 0.7385 | 0.6855 | 0.5590 | 0.6158 | **0.7920** |
| Soft Voting | 0.7385 | 0.6967 | 0.5359 | 0.6058 | **0.7929** |
| XGBoost | 0.7365 | 0.6726 | **0.5795** | **0.6226** | 0.7898 |
| Stacking Classifier | 0.7356 | 0.6803 | 0.5564 | 0.6121 | 0.7890 |
| Bagging Classifier | 0.7298 | 0.6698 | 0.5513 | 0.6048 | 0.7794 |
| LightGBM | 0.7288 | 0.6688 | 0.5487 | 0.6028 | 0.7809 |
| AdaBoost Classifier | 0.7279 | 0.6667 | 0.5487 | 0.6020 | 0.7852 |
| Single Decision Tree | 0.7029 | 0.6588 | 0.4308 | 0.5209 | 0.7547 |

### Regression — best scores from the supplied dataset

| Metric | Best Model | Score |
|---|---|---:|
| 🥇 MAE | Stacking Regressor | **7.8957** |
| 🥇 RMSE | XGBoost | **9.8544** |
| 🥇 R² | XGBoost | **0.4803** |

### Full regression comparison

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| XGBoost | 7.9004 | **9.8544** | **0.4803** |
| Stacking Regressor | **7.8957** | 9.8692 | 0.4787 |
| LightGBM | 7.9151 | 9.8877 | 0.4767 |
| Gradient Boosting | 8.0729 | 10.0448 | 0.4600 |
| Bagging Regressor | 8.1022 | 10.0696 | 0.4573 |
| AdaBoost Regressor | 8.5207 | 10.4697 | 0.4133 |
| Single Decision Tree | 8.7143 | 10.8031 | 0.3754 |

---

## 🔍 Mini Experiments

### AdaBoost estimator study

The project also checks how changing the number of estimators affects classification performance.

| Estimators | Accuracy | F1 | ROC-AUC |
|---:|---:|---:|---:|
| 20 | 0.7250 | 0.5843 | 0.7811 |
| 40 | 0.7298 | 0.5991 | 0.7843 |
| 80 | 0.7279 | 0.6020 | 0.7852 |
| 120 | 0.7298 | **0.6037** | **0.7867** |

### Gradient Boosting learning-rate study

| Learning Rate | Accuracy | F1 | ROC-AUC |
|---:|---:|---:|---:|
| 0.03 | 0.7231 | 0.5727 | 0.7853 |
| 0.06 | 0.7346 | 0.6057 | 0.7907 |
| 0.10 | **0.7385** | **0.6222** | **0.7929** |
| 0.15 | **0.7385** | **0.6222** | 0.7927 |

**Takeaway:** On this fixed experiment, moderate learning rates performed better than the smallest tested value.

---

## 💡 Final Recommendation

### 🟢 Course completion

**Soft Voting Classifier** is the recommended option when the objective is to use predicted probabilities for ranking students by completion risk or likelihood.

Hard Voting gives the highest raw accuracy in the tested split, while Soft Voting gives the highest ROC-AUC. That makes the choice depend on the actual use case rather than accuracy alone.

### 🔵 Final score prediction

**XGBoost Regressor** is the recommended model because it gives the **lowest RMSE** and **highest R²** in the comparison.

The Stacking Regressor has a very slightly lower MAE, so it remains a reasonable alternative when average absolute error is the priority.

> **Important:** A real deployment should choose a classification threshold using validation data and the cost of missing students who may need support.

---

## 📁 Project Contents

```text
Smart_Outcome_Predictor/
│
├── 📓 Smart_Outcome_Predictor_COMPLETE.ipynb   # Main submission notebook
├── 📘 Smart_Outcome_Predictor.ipynb            # Editable notebook
├── 🧪 Smart_Outcome_Predictor_Executed.ipynb   # Executed notebook
├── 🐍 smart_outcome_predictor.py               # Source code
├── 📄 dataset.csv                              # Supplied dataset
│
├── 📊 classification_results.csv
├── 📊 regression_results.csv
├── 📊 adaboost_analysis.csv
├── 📊 gradient_boosting_learning_rate_analysis.csv
├── 📊 attendance_summary.csv
├── 📊 course_level_summary.csv
│
├── 📈 plots/                                   # Charts used in the project
├── 🖼️ notebook_screenshots/                    # Evidence screenshots
├── 📚 Smart_Outcome_Predictor_Theory_and_Report.pdf
├── ✅ DELIVERABLES_MAP.md
└── 📖 README_HD.md
```

---

## ▶️ Run the Project

### 1. Install the packages

```bash
pip install -r requirements.txt
```

### 2. Keep the dataset beside the notebook

```text
dataset.csv
Smart_Outcome_Predictor_COMPLETE.ipynb
```

### 3. Open the notebook

Use **Jupyter Notebook, JupyterLab, or Google Colab**.

### 4. Run from top to bottom

The notebook contains the complete workflow, including preparation, model training, evaluation, comparison, plots, analysis and conclusion.

---

## 📝 Project Deliverables Covered

The notebook is organized to cover the major requirements of the supplied brief:

- ✅ Conceptual foundation / theory
- ✅ Dataset understanding and preparation
- ✅ Bagging classifier and regressor
- ✅ AdaBoost classifier and regressor
- ✅ Gradient Boosting classifier and regressor
- ✅ LightGBM classifier and regressor
- ✅ XGBoost classifier and regressor
- ✅ Hard Voting and Soft Voting
- ✅ Stacking Classifier
- ✅ Stacking Regressor
- ✅ Classification metrics
- ✅ Regression metrics
- ✅ Hyperparameter mini-experiments
- ✅ Model comparison tables
- ✅ Visual analysis
- ✅ Final interpretation and recommendation
- ✅ README and supporting submission files

---

## 🎓 Academic Note

This project is intentionally written in a **simple, explainable student-project style**. The focus is on understanding ensemble learning, comparing models fairly, reading metrics, and explaining why a particular model is selected.

The main submission file is:

### ⭐ `Smart_Outcome_Predictor_COMPLETE.ipynb`

It is designed to be the **single notebook to submit** for the project.

---

<div align="center">

### Built for learning • experimentation • comparison • practical ML thinking

**Smart Outcome Predictor — Ensemble Learning for Student Outcomes** 🎓📊

</div>
