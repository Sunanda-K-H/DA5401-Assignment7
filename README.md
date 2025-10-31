# DA5401 Assignment 7: Multi-Class Model Selection using ROC and Precision-Recall Curves

**Name**: Kaki Hephzi Sunanda  
**Roll Number**: DA25M015  
**Date**: 31.10.2025

---

# Repository Information
This repository contains the implementation and evaluation of multiple classification models using **ROC-AUC** and **Precision-Recall AP metrics** on a multi-class dataset.  
The study explores how model performance changes when evaluated across different metrics and decision thresholds.

---

# Repository Structure

```
.
└── DA5401-Assignment7/
    ├── README.md
    └── DA5401_A7_DA25M015.ipynb
```

---

# Dataset Information
- Multi-class dataset with **7 output classes**
- All features scaled prior to training (StandardScaler)
- Train–test split applied before model fitting
- Class distribution moderately imbalanced → important for PRC evaluation

---

# Work Done

## Models Trained
| Model Category | Models Used |
|---|---|
| Baseline | Dummy Classifier |
| Classical ML | Logistic Regression, Decision Tree, Naive Bayes |
| Distance-based | K-Nearest Neighbors (KNN) |
| Margin-based | Support Vector Machine (SVC) |
| Ensemble | Random Forest, XGBoost |
| Weak / Poor Model (for AUC < 0.5 requirement) | Bernoulli Naive Bayes |

All models were trained **without hyperparameter tuning** as per assignment constraints.

---

## Metrics Used

- **Weighted F1-Score** (threshold-based metric)
- **Macro-Averaged ROC-AUC**  
- **Macro-Averaged PRC-AP** (important for class imbalance)

---

## Macro-Averaged ROC Curves

Observations:
- **KNN and SVC achieved the highest ROC-AUC (≈ 0.98)**
- Logistic Regression and Naive Bayes followed closely (0.94–0.97)
- Dummy classifier sits around **0.50** = random guessing

---

## Macro-Averaged Precision-Recall Curves

Observations:
- **PRC reveals clearer ranking differences than ROC**
- KNN performs best with **AP ≈ 0.922**
- SVC also strong (**AP ≈ 0.900**)
- Decision Tree & Naive Bayes decline when recall increases
- Dummy classifier extremely poor → AP ≈ 0.167

---

## Ranking Table (Final Comparison)

| Rank | Based on Weighted F1 | Based on ROC-AUC | Based on PRC-AP |
|---|---|---|---|
| 1 | KNN (0.910) | KNN (0.980) | KNN (0.922) |
| 2 | SVC (0.891) | SVC (0.980) | SVC (0.900) |
| 3 | Decision Tree (0.847) | Logistic Regression (0.972) | Logistic Regression (0.864) |
| 4 | Logistic Regression (0.843) | Naive Bayes (0.947) | Naive Bayes (0.786) |
| 5 | Naive Bayes (0.790) | Decision Tree (0.894) | Decision Tree (0.722) |
| 6 | Dummy (0.092) | Dummy (0.500) | Dummy (0.167) |

---

# Analysis & Insights

- Rankings differ across metrics →  
  **ROC-AUC hides false positives**, leading weak models to appear strong.
- **PRC-AP is more reliable in class-imbalance settings**.
- Decision Tree performs inconsistently due to overfitting.
- KNN and SVC show **best generalization** across all metrics.

---

## Additional Model Evaluation – Bernoulli Naive Bayes (AUC < 0.5)

As required, we experimented with another model whose ROC-AUC score is poor compared to other classifiers.

### Model Used:
- **Bernoulli Naive Bayes**

### Why Bernoulli NB?
- It assumes binary features and strong independence between them.
- Such assumptions are unrealistic for a **7-class ordinal food rating** dataset.
- We expect poor performance → Good candidate for comparison.

---

### ROC Curve and AUC Score

The macro-averaged ROC curve is plotted below:

**Macro-Averaged AUC = 0.500**

This means the model performs **similar to random guessing**.

---

### Precision-Recall Curve and AP Score

**Macro-Averaged AP = ~0.17**

This shows very low precision when recall increases — meaning the model makes many incorrect predictions for minority classes.

---

### Key Observations

- The ROC curve lies very close to the diagonal baseline → **no discriminative power**.
- Precision drops sharply as recall increases → **many false positives**.
- Model assumptions conflict with real data structure (multiclass, correlated features).
- This confirms why BernoulliNB performs significantly worse than:
  - KNN  
  - Logistic Regression  
  - Random Forest  
  - XGBoost  

Thus, BernoulliNB stands as the required poor-performing model for comparison in this assignment.

---

### Conclusion

Bernoulli Naive Bayes is **not suitable for this dataset** due to:
- Strong independence assumptions
- Inability to handle multiclass ordinal structure
- Very poor ROC-AUC and PRC-AP metrics

Compared to high-performing models (KNN, LR, SVM, RF, XGB), the contrast clearly justifies model selection decisions.
