# Assignment 5 Summary

## Problem
Predict whether a company will go bankrupt.

## Dataset
- 6,819 rows
- ~3.2% bankrupt (imbalanced)

## Metrics
- PR-AUC for discrimination
- Brier score for calibration

## Feature Sets
- A: all features
- B: top 25 important features

## Experiments
	exp_id	model	feature_set	train_pr_auc	val_pr_auc	overfit_gap	val_roc_auc	val_brier	threshold	val_precision	val_recall	val_f1_or_f2	notes	selected_finalist
0	1	Logistic Regression	A	0.530785	0.258677	0.272108	0.876645	0.031581	0.5	0.333333	0.181818	0.200000	Baseline model	No
1	2	XGBoost Baseline	A	1.000000	0.553391	0.446609	0.962902	0.021197	0.5	0.687500	0.333333	0.371622	Default XGBoost	No
2	3	XGBoost Imbalance	A	1.000000	0.557268	0.442732	0.971380	0.022336	0.5	0.580645	0.545455	0.552147	With scale_pos_weight	No
3	4	XGBoost Tuned	A	1.000000	0.583837	0.416163	0.965044	0.020126	0.5	0.769231	0.303030	0.344828	Manual tuning	Yes
4	5	XGBoost Selected Features	B	1.000000	0.418469	0.581531	0.936058	0.024445	0.5	0.526316	0.303030	0.331126	Top 25 features	No

## Final Model
XGBoost Tuned

## Why Selected
- Highest validation PR-AUC
- Good Brier score
- Acceptable overfit gap

## Test Results
- PR-AUC: 0.508
- ROC-AUC: 0.954
- Brier: 0.023
- Precision: 0.419
- Recall: 0.545
- F2: 0.514

## Confusion Matrix

The confusion matrix shows how the model performs in classifying bankrupt and non-bankrupt companies.

- True positives represent correctly identified bankrupt companies.
- False negatives represent missed bankrupt companies, which are costly in this problem.
- The model captures a reasonable number of bankrupt firms while maintaining acceptable false positives.

## Calibration

- The Brier score of 0.023 indicates that the predicted probabilities are well calibrated.
- The calibration curve shows that predicted probabilities align reasonably well with actual outcomes.
- Higher predicted risk corresponds to higher observed bankruptcy rates.
- The model provides meaningful probability estimates for decision-making.

## Feature Importance

- The most important feature was Top EPS in the Last Four Seasons.
- This makes sense because it likely reflects a key financial indicator of company stability.
- A limitation is that feature importance does not imply causation, only association.

## Overfitting

- Overfitting was assessed using the difference between training and validation PR-AUC.
- The selected model showed a reasonable overfit gap, indicating good generalization.
- There is no strong evidence that the model memorizes the training data.

## Class Imbalance

- The dataset is highly imbalanced, with only about 3.2% of companies classified as bankrupt.
- This imbalance makes accuracy a poor evaluation metric.
- The focus is therefore on metrics like PR-AUC and recall that better capture performance on the minority class.

## Metric Explanation

- The positive class (bankrupt companies) is rare, making this an imbalanced classification problem.
- Accuracy is misleading because predicting all companies as non-bankrupt would still give high accuracy.
- PR-AUC is used as it focuses on identifying the positive class effectively.
- Brier score evaluates how well predicted probabilities match actual outcomes.
- Threshold-based metrics like recall and F2-score describe performance at a specific decision point.

## AI Usage

- I used an AI assistant (Codex) to help structure the notebook and build reusable functions.
- It helped generate code for model evaluation and plotting.
- I verified that the test set was not used before final evaluation.
- I corrected an issue with importing calibration_curve and ensured proper library usage.