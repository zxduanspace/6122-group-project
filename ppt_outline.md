# SC6122 Group Project — PPT Outline
*15 minutes total (12 min presentation + 3 min Q&A)*

---

## Slide 1: Title Slide
- SC6122 Emerging Topics in FinTech — Group Project
- Title: Predicting Credit Delinquency with Machine Learning
- Group members + emails
- Date

---

## Slide 2: Problem & Motivation (~1 min)
- Credit card defaults cost financial institutions billions annually
- Goal: predict whether a borrower will default within 2 years
- Challenge: severe class imbalance (only 6.68% default)
- Why this matters: early detection enables better risk management

---

## Slide 3: Dataset Overview (~1 min)
- "Give Me Some Credit" dataset (Kaggle)
- 150,000 records, 10 features, 1 binary target
- Key features: credit utilization, age, past-due history, debt ratio, income
- Class distribution: 93.32% non-default vs. 6.68% default
- [放一张类别分布饼图]

---

## Slide 4: Data Preprocessing (~1.5 min, DUAN ZHIXUAN讲)
- Outlier handling: age=0, past-due sentinel values (96/98)
- Missing values: MonthlyIncome (19.7%), NumberOfDependents (2.6%) → median imputation
- Standardization: StandardScaler
- Train/test split: 80/20 stratified
- Class imbalance: SMOTE (applied within CV pipeline)
- [放特征相关性热力图]

---

## Slide 5: Models Overview (~0.5 min)
- 6 models across 4 families:
  - Linear: Logistic Regression (L2), Lasso (L1)
  - Instance-based: KNN
  - Ensemble: Random Forest, XGBoost
  - Deep Learning: Neural Network (MLP)
- All tuned via cross-validation, evaluated on ROC AUC

---

## Slide 6: Logistic Regression & Lasso (~1.5 min, DUAN ZHIXUAN讲)
- L2 regularization, C tuned via 5-fold CV → best C=0.01
- Lasso (L1): same setup, best C=0.01, dropped 1 feature
- Test ROC AUC: LR 0.819, Lasso 0.819
- Interpretable: coefficient analysis shows key risk factors
- [放系数重要性条形图]

---

## Slide 7: Random Forest & XGBoost (~1.5 min, XIANG JIAYI讲)
- RF: Bagging ensemble, 300 trees, max_depth=8 → Test ROC AUC 0.856, Accuracy 79.5%
- XGBoost: Boosting ensemble, 300 rounds, max_depth=3, lr=0.05 → Test ROC AUC 0.851, Accuracy 85.4%
- [放RF/XGBoost特征重要性图]

---

## Slide 8: KNN (~1 min, HE PEIYU讲)
- Non-parametric, distance-based classifier
- Tuned: K ∈ {3,5,7,11}, uniform/distance weighting, Euclidean/Manhattan
- Best: K=11, Manhattan, uniform → CV AUC 0.757
- Test: Accuracy 80.2%, ROC AUC 0.765, Recall(default) 60.9%
- Limitation: curse of dimensionality with 10 features

---

## Slide 9: Neural Network (MLP) (~1 min, HE PEIYU讲)
- Feedforward neural network, captures non-linear interactions
- Tuned: hidden layers, regularization α, early stopping
- Best: single layer (100 neurons), α=0.001 → CV AUC 0.836
- Test: Accuracy 82.1%, ROC AUC 0.852, Recall(default) 71.3%
- Strong recall — catches majority of defaulters

---

## Slide 10: Results Comparison (~1.5 min)
- [放模型对比总表 — Table 1 from report]
- [放所有模型ROC曲线对比图]
- Key findings:
  - RF achieves best ROC AUC (0.856), followed by MLP (0.852) and XGBoost (0.851)
  - XGBoost best accuracy (85.4%), LR/Lasso best interpretability
  - RF highest default recall (76.6%)
  - KNN weakest due to curse of dimensionality
  - Accuracy misleading for imbalanced data — ROC AUC is the right metric

---

## Slide 11: Conclusion & Future Work (~1 min)
- Best model: Random Forest (ROC AUC 0.856), risk mgmt → RF, revenue → XGBoost, compliance → LR
- Trade-off: accuracy vs. interpretability vs. recall
- Limitations: class imbalance, missing data, black-box models
- Future: feature engineering, threshold optimization, ensemble tuning, SHAP for interpretability

---

## Slide 12: Q&A
- Thank you
- [分工表]

---

## 分工建议
| 谁 | 讲什么 | 大约时间 |
|---|--------|---------|
| DUAN ZHIXUAN | Slide 2-4, 6 (问题背景 + 预处理 + 线性模型) | ~4 min |
| XIANG JIAYI | Slide 5, 7 (模型总览 + RF/XGBoost) | ~3 min |
| HE PEIYU | Slide 8-11 (KNN + MLP + 结果对比 + 结论) | ~4.5 min |
